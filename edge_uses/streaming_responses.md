# Streaming Responses
An edge function script doesn’t need to prepare its entire response body before delivering a Response to `event.respondWith()`. Using a TransformStream, it is possible to stream a response body after sending the response’s front matter (i.e., HTTP status line and headers). This allows us to minimize:

* The visitor’s time-to-first-byte.

* The amount of buffering that must be done in the edge function script.

Minimizing buffering is especially important if you must process or transform response bodies that are larger than the edge function’s memory limit. In these cases, streaming is the only feasible implementation strategy.

**Note**: The CIS Edge Function service already streams by default wherever possible. You only need to use these APIs if you wish to modify the response body in some way, while maintaining streaming behavior. If your edge function script only passes subrequest responses back to the client verbatim, without reading their bodies, then its body handling is already optimal, and there is no need for the techniques described here.

## Streaming Pass-Through
Here’s a minimal pass-through example to get started:
```
addEventListener("fetch", event => {
  event.respondWith(fetchAndStream(event.request))
})

async function fetchAndStream(request) {
  // Fetch from origin server.
  let response = await fetch(request)

  // Create an identity TransformStream (a.k.a. a pipe).
  // The readable side will become our new response body.
  let { readable, writable } = new TransformStream()

  // Start pumping the body. NOTE: No await!
  streamBody(response.body, writable)

  // ... and deliver our Response while that's running.
  return new Response(readable, response)
}

async function streamBody(readable, writable) {
  let reader = readable.getReader()
  let writer = writable.getWriter()

  while (true) {
    const { done, value } = await reader.read()
    if (done) break
    // Optionally transform value's bytes here.
    await writer.write(value)
  }

  await writer.close()
}
```
There are some important details to note:

* Although `streamBody()` is an asynchronous function, we do not `await` it, so that it does not block forward progress of the calling `fetchAndStream()` function. It will continue to run asynchronously for as long as it has an outstanding `reader.read()` or `writer.write()` operation.

* Backpressure: We `await` the read operation before calling the write operation. Likewise, we `await` the write operation before calling the next read operation. Following this pattern propagates backpressure to the origin.

* Completion: We call `writer.close()` at the end, which signals to the Edge Function runtime that we’re completely done writing this response body. Once called, `streamBody()` will terminate — if this is undesirable, pass its returned promise to `FetchEvent.waitUntil()`. If your script never calls `writer.close()`, the body will appear truncated to the runtime, though it may continue to function as intended.

## Aggregate And Stream Multiple Requests
This is similar to our Aggregating Multiple Requests recipe, but this time we’ll start writing our response as soon as we’ve verified that every subrequest succeeded — no need to wait for the actual response bodies.
```
addEventListener('fetch', event => {
    event.respondWith(fetchAndApply(event.request))
})

/**
 * Make multiple requests,
 * aggregate the responses and
 * stream it back as a single response.
 */
async function fetchAndApply(request) {
  const requestInit = {
    headers: { "Authorization": "XXXXXX" }
  }
  const fetches = [
    "https://api.coinbase.com/v2/prices/BTC-USD/spot",
    "https://api.coinbase.com/v2/prices/ETH-USD/spot",
    "https://api.coinbase.com/v2/prices/LTC-USD/spot"
  ].map(url => fetch(url, requestInit))

  // Wait for each fetch() to complete.
  let responses = await Promise.all(fetches)

  // Make sure every subrequest succeeded.
  if (!responses.every(r => r.ok)) {
    return new Response(null, { status: 502 })
  }

  // Create a pipe and stream the response bodies out
  // as a JSON array.
  let { readable, writable } = new TransformStream()
  streamJsonBodies(responses.map(r => r.body), writable)

  return new Response(readable)
}

async function streamJsonBodies(bodies, writable) {
  // We're presuming these bodies are JSON, so we
  // concatenate them into a JSON array. Since we're
  // streaming, we can't use JSON.stringify(), but must
  // instead manually write an initial '[' before the
  // bodies, interpolate ',' between them, and write a
  // terminal ']' after them.

  let writer = writable.getWriter()
  let encoder = new TextEncoder()

  await writer.write(encoder.encode("[\n"))

  for (let i = 0; i < bodies.length; ++i) {
    if (i > 0) await writer.write(encoder.encode(",\n"))
    await manualPipeTo(bodies[i].getReader(), writer)
  }

  await writer.write(encoder.encode("]"))

  await writer.close()
}

async function manualPipeTo(reader, writer) {
  while (true) {
    const { done, value } = await reader.read()
    if (done) break
    await writer.write(value)
  }
}
```
Again, there are couple important details to note:

* The runtime expects to receive TypedArrays on the readable side of the TransformStream. Therefore, we never pass a string to `writer.write()`, only Uint8Arrays. If you need to write a string, use a TextEncoder.

* `manualPipeTo()` is so-named because `ReadableStream.pipeTo()` is not yet implemented in CIS Edge Functions, as of this writing. When it becomes available, it will be the more idiomatic and optimal way to pump bytes from a ReadableStream to a WritableStream.
