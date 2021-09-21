---

copyright:
  years: 2018, 2020
lastupdated: "2020-05-06"

keywords:

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:term: .term}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Edge functions use cases
{: #edge-functions-use-cases}

THIS SOFTWARE IS PROVIDED BY IBM “AS IS” AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL IBM BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

## A/B testing
{: #ab-testing}

You can create a CIS Edge function to control A/B tests.

```sh
addEventListener('fetch', event => {
  event.respondWith(fetchAndApply(event.request))
})

async function fetchAndApply(request) {
  const name = 'experiment-0'
  let group          // 'control' or 'test', set below
  let isNew = false  // is the group newly-assigned?

  // Determine which group this request is in.
  const cookie = request.headers.get('Cookie')
  if (cookie && cookie.includes(`${name}=control`)) {
    group = 'control'
  } else if (cookie && cookie.includes(`${name}=test`)) {
    group = 'test'
  } else {
    // 50/50 Split
    group = Math.random() < 0.5 ? 'control' : 'test'
    isNew = true
  }

  // We'll prefix the request path with the experiment name. This way,
  // the origin server merely has to have two copies of the site under
  // top-level directories named "control" and "test".
  let url = new URL(request.url)
  // Note that `url.pathname` always begins with a `/`, so we don't
  // need to explicitly add one after `${group}`.
  url.pathname = `/${group}${url.pathname}`

  const modifiedRequest = new Request(url, {
    method: request.method,
    headers: request.headers
  })

  const response = await fetch(modifiedRequest)

  if (isNew) {
    // The experiment was newly-assigned, so add a Set-Cookie header
    // to the response.
    const newHeaders = new Headers(response.headers)
    newHeaders.append('Set-Cookie', `${name}=${group}; path=/`)
    return new Response(response.body, {
      status: response.status,
      statusText: response.statusText,
      headers: newHeaders
    })
  } else {
    // Return response unmodified.
    return response
  }
}

```
{: codeblock}

## Adding a response header
{: #add-response-header}

To modify the response headers, you’ll first need to make a copy of the response in order to make it mutable. Then you can use the Headers interface to add, change, or remove headers.

```sh
addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request))
})

/**
 * Set the `x-my-header` header
 * @param {Request} request
 */
async function handleRequest(request) {
  let response = await fetch(request);

  // Make the headers mutable by re-constructing the Response.
  response = new Response(response.body, response);
  response.headers.set('x-my-header', 'custom value');
  return response;
}
```
{: codeblock}

## Aggregating multiple requests
{: #aggregate-multiple-requests}

Here, we make multiple requests to different API endpoints, aggregate the responses and send it back as a single response.

```sh
addEventListener('fetch', event => {
    event.respondWith(fetchAndApply(event.request))
})

/**
 * Make multiple requests,
 * aggregate the responses and
 * send it back as a single response
 */
async function fetchAndApply(request) {
    const init = {
      method: 'GET',
      headers: {'Authorization': 'XXXXXX'}
    }
    const [btcResp, ethResp, ltcResp] = await Promise.all([
      fetch('https://api.coinbase.com/v2/prices/BTC-USD/spot', init),
      fetch('https://api.coinbase.com/v2/prices/ETH-USD/spot', init),
      fetch('https://api.coinbase.com/v2/prices/LTC-USD/spot', init)
    ])

    const btc = await btcResp.json()
    const eth = await ethResp.json()
    const ltc = await ltcResp.json()

    let combined = {}
    combined['btc'] = btc['data'].amount
    combined['ltc'] = ltc['data'].amount
    combined['eth'] = eth['data'].amount

    const responseInit = {
      headers: {'Content-Type': 'application/json'}
    }
    return new Response(JSON.stringify(combined), responseInit)
}
```
{: codeblock}

## Conditional routing
{: #conditional-routing}

The easiest way to deliver different content based on the device being used is to rewrite the URL of the request based on the condition you care about. For example:

### Device type
{: #conditional-routing-device-type}

```sh
addEventListener('fetch', event => {
  event.respondWith(fetchAndApply(event.request))
})

async function fetchAndApply(request) {
  let uaSuffix = ''

  const ua = request.headers.get('user-agent')
  if (ua.match(/iphone/i) || ua.match(/ipod/i)) {
    uaSuffix = '/mobile'
  } else if (ua.match(/ipad/i)) {
    uaSuffix = '/tablet'
  }

  return fetch(request.url + uaSuffix, request)
}
```
{: codeblock}

### Custom headers
{: #conditional-routing-custom-headers}

```sh
addEventListener('fetch', event => {
  event.respondWith(fetchAndApply(event.request))
})

async function fetchAndApply(request) {
  let suffix = ''
  //Assuming that the client is sending a custom header
  const cryptoCurrency = request.headers.get('X-Crypto-Currency')
  if (cryptoCurrency === 'BTC') {
    suffix = '/btc'
  } else if (cryptoCurrency === 'XRP') {
    suffix = '/xrp'
  } else if (cryptoCurrency === 'ETH') {
    suffix = '/eth'
  }

  return fetch(request.url + suffix, request)
}
```
{: codeblock}

## Hot-link protection
{: #hot-link-protection}

You can use CIS Edge functions to protect your hot-links on your web properties.

```sh
addEventListener('fetch', event => {
  event.respondWith(fetchAndApply(event.request))
})

/**
 * If the browser is requesting an image and
 * the referer does not match your host
 * we redirect the request to your page
 */
async function fetchAndApply(request) {
  // Fetch the response.
  let response = await fetch(request)

  // If it's an image, engage hotlink protection based on the
  // Referer header.
  let referer = request.headers.get('Referer')
  let contentType = response.headers.get('Content-Type') || ''
  if (referer && contentType.startsWith('image/')) {
    // It's an image and there's a Referer. Verify that the
    // hostnames match.
    if (new URL(referer).hostname !==
        new URL(request.url).hostname) {
      // Hosts don't match. This is a hotlink. Redirect the
      // user to our homepage.
      return new Response('', {
        status: 302,
        headers: {
          'Location': '/'
        }
      })
    }
  }

  // Everything is fine, return the response normally.
  return response
}
```
{: codeblock}

## Originless responses
{: #originless-responses}

You can return responses directly from the edge. No need to hit your origin.

### Ignore POST and PUT HTTP requests
{: #originless-responses-ignore-post-put-http-requests}

Ignore POST and PUT HTTP requests. This snippet allows all other requests to pass through to the origin.

```sh
addEventListener('fetch', event => {
  event.respondWith(fetchAndApply(event.request))
})

async function fetchAndApply(request) {
  if (request.method === 'POST' || request.method === 'PUT') {
    return new Response('Sorry, this page is not available.',
        { status: 403, statusText: 'Forbidden' })
  }

  return fetch(request)
}
```
{: codeblock}

### Deny a spider or crawler
{: #originless-responses-deny-spider-crawler}

Protect your origin from unwanted spiders or crawlers. In this case, if the user-agent is “annoying-robot”, the Edge function returns the response instead of sending the request to the origin.

```sh
addEventListener('fetch', event => {
  event.respondWith(fetchAndApply(event.request))
})

async function fetchAndApply(request) {
  if (request.headers.get('user-agent').includes('annoying_robot')) {
    return new Response('Sorry, this page is not available.',
        { status: 403, statusText: 'Forbidden' })
  }

  return fetch(request)
}
```
{: codeblock}

### Prevent a specific IP from connecting
{: #originless-responses-prevent-specific-ip-connection}

Blocklist IP addresses. This snippet of code prevents a specific IP, in this case ‘225.0.0.1’ from connecting to the origin.

```sh
addEventListener('fetch', event => {
  event.respondWith(fetchAndApply(event.request))
})

async function fetchAndApply(request) {
  if (request.headers.get('cf-connecting-ip') === '225.0.0.1') {
    return new Response('Sorry, this page is not available.',
        { status: 403, statusText: 'Forbidden' })
  }

  return fetch(request)
}
```
{: codeblock}

## Post requests
{: #post-requests}

Reading content from an HTTP POST request:

```sh
addEventListener('fetch', event => {
  event.respondWith(fetchAndApply(event.request))
})

/**
 * Making a curl request that looks like
 * curl -X POST --data 'key=world' example.com
 * or
 * curl -X POST --form 'key=world' example.com
 */
async function fetchAndApply(request) {
  try {
    const postData = await request.formData();
    return new Response(`hello ${postData.get('key')}`)
  } catch (err) {
    return new Response('could not unbundle post data')
  }
}
```
{: codeblock}

Creating an HTTP POST request from an Edge function:

```sh
addEventListener('fetch', event => {
  event.respondWith(fetchAndApply(event.request))
})

/**
 * Create a POST request with body 'key=world'
 * Here, we are assuming that example.com acknowledges the POST request with body key=world
 */
async function fetchAndApply(request) {
  let content = 'key=world'
  let headers = {
    'Content-Type': 'application/x-www-form-urlencoded'
  }
  const init = {
    method: 'POST',
    headers: headers,
    body: content
  }
  const response = await fetch('https://example.com', init)
  console.log('Got response', response)
  return response
}
```
{: codeblock}

## Setting a cookie
{: #setting-cookies}

You can set cookies using CIS Edge functions.

```sh
addEventListener('fetch', event => {
  event.respondWith(fetchAndApply(event.request))
})

async function fetchAndApply(request) {
  let response = await fetch(request)

  const randomStuff = `randomcookie=${Math.random()}; Expires=Wed, 21 Oct 2018 07:28:00 GMT; Path='/';`

  // Make the headers mutable by re-constructing the Response.
  response = new Response(response.body, response)
  response.headers.set('Set-Cookie', randomStuff)

  return response
}
```
{: codeblock}

## Signed requests
{: #signed-requests}

A common URL authentication method known as request signing can be implemented in an Edge function with the help of the Web Crypto API.

In the example presented here, we’ll authenticate the path of a URL along with an accompanying expiration timestamp, using a Hash-based Message Authentication Code (HMAC) with a SHA-256 digest algorithm. For a user agent to successfully fetch an authenticated resource, they’ll need to provide the correct path, expiration timestamp, and HMAC using query parameters — if any of those three are tampered with, the request fails.

Note that the authenticity of the expiration timestamp is covered by the HMAC, so we can rely on the user-provided timestamp being correct if the HMAC is correct, and thus know when the URL expires. Moreover, you can also determine whether a URL in their possession has expired or not.

### Verifying signed requests
{: #signed-requests-verify}

This example verifies the HMAC for any request URL whose pathname starts with `/verify/`.

For debugging convenience, this Edge function returns 403 if the URL or HMAC is invalid, or if the URL has expired. You might want to return 404 in an actual implementation.

```sh
addEventListener('fetch', event => {
  event.respondWith(verifyAndFetch(event.request))
})

async function verifyAndFetch(request) {
  const url = new URL(request.url)

  // If the path doesn't begin with our protected prefix, just pass the request
  // through.
  if (!url.pathname.startsWith("/verify/")) {
    return fetch(request)
  }

  // Make sure we have the minimum necessary query parameters.
  if (!url.searchParams.has("mac") || !url.searchParams.has("expiry")) {
    return new Response("Missing query parameter", { status: 403 })
  }

  // We'll need some super-secret data to use as a symmetric key.
  const encoder = new TextEncoder()
  const secretKeyData = encoder.encode("my secret symmetric key")
  const key = await crypto.subtle.importKey(
    "raw", secretKeyData,
    { name: "HMAC", hash: "SHA-256" },
    false, [ "verify" ]
  )

  // Extract the query parameters we need and run the HMAC algorithm on the
  // parts of the request we're authenticating: the path and the expiration
  // timestamp.
  const expiry = Number(url.searchParams.get("expiry"))
  const dataToAuthenticate = url.pathname + expiry

  // The received MAC is Base64-encoded, so we have to go to some trouble to
  // get it into a buffer type that crypto.subtle.verify() can read.
  const receivedMacBase64 = url.searchParams.get("mac")
  const receivedMac = byteStringToUint8Array(atob(receivedMacBase64))

  // Use crypto.subtle.verify() to guard against timing attacks. Since HMACs use
  // symmetric keys, we could implement this by calling crypto.subtle.sign() and
  // then doing a string comparison -- this is insecure, as string comparisons
  // bail out on the first mismatch, which leaks information to potential
  // attackers.
  const verified = await crypto.subtle.verify(
    "HMAC", key,
    receivedMac,
    encoder.encode(dataToAuthenticate)
  )

  if (!verified) {
    const body = "Invalid MAC"
    return new Response(body, { status: 403 })
  }

  if (Date.now() > expiry) {
    const body = `URL expired at ${new Date(expiry)}`
    return new Response(body, { status: 403 })
  }

  // We've verified the MAC and expiration time; we're good to pass the request
  // through.
  return fetch(request)
}

// Convert a ByteString (a string whose code units are all in the range
// [0, 255]), to a Uint8Array. If you pass in a string with code units larger
// than 255, their values overflow!
function byteStringToUint8Array(byteString) {
  const ui = new Uint8Array(byteString.length)
  for (let i = 0; i < byteString.length; ++i) {
    ui[i] = byteString.charCodeAt(i)
  }
  return ui
}
```
{: codeblock}

### Generating signed requests
{: #signed-requests-generate}

Typically, signed requests are delivered to you in some out-of-band way, such as email, or actually generated by you yourself if you have the symmetric key. We can, of course, also generate the signed requests in an Edge function.

For any request URL beginning with `/generate/`, we’ll replace `/generate/` with `/verify/`, sign the resulting path with its timestamp, and return the full, signed URL using the response body.

```sh
addEventListener('fetch', event => {
  const url = new URL(event.request.url)
  const prefix = "/generate/"
  if (url.pathname.startsWith(prefix)) {
    // Replace the "/generate/" path prefix with "/verify/", which we
    // use in the first example to recognize authenticated paths.
    url.pathname = `/verify/${url.pathname.slice(prefix.length)}`
    event.respondWith(generateSignedUrl(url))
  } else {
    event.respondWith(fetch(event.request))
  }
})

async function generateSignedUrl(url) {
  // We'll need some super-secret data to use as a symmetric key.
  const encoder = new TextEncoder()
  const secretKeyData = encoder.encode("my secret symmetric key")
  const key = await crypto.subtle.importKey(
    "raw", secretKeyData,
    { name: "HMAC", hash: "SHA-256" },
    false, [ "sign" ]
  )

  // Signed requests expire after one minute. Note that you could choose
  // expiration durations dynamically, depending on, e.g. the path or a query
  // parameter.
  const expirationMs = 60000
  const expiry = Date.now() + expirationMs
  const dataToAuthenticate = url.pathname + expiry

  const mac = await crypto.subtle.sign(
    "HMAC", key,
    encoder.encode(dataToAuthenticate)
  )

  // `mac` is an ArrayBuffer, so we need to jump through a couple hoops to get
  // it into a ByteString, then a Base64-encoded string.
  const base64Mac = btoa(String.fromCharCode(...new Uint8Array(mac)))

  url.searchParams.set("mac", base64Mac)
  url.searchParams.set("expiry", expiry)

  return new Response(url)
}
```
{: codeblock}

## Streaming responses
{: #streaming-responses}

An Edge function script doesn’t need to prepare its entire response body before delivering a Response to `event.respondWith()`. Using a TransformStream, it is possible to stream a response body after sending the response’s front matter (for example, HTTP status line and headers). This allows us to minimize:

* The visitor’s time-to-first-byte.
* The amount of buffering that must be done in the Edge function script.

Minimizing buffering is especially important if you must process or transform response bodies that are larger than the Edge function’s memory limit. In these cases, streaming is the only feasible implementation strategy.

The CIS Edge Function service already streams by default wherever possible. You only need to use these APIs if you wish to modify the response body in some way, while maintaining streaming behavior. If your Edge function script only passes subrequest responses back to the client verbatim, without reading their bodies, then its body handling is already optimal, and there is no need for the techniques described here.
{: note}

### Streaming pass-through
{: #streaming-responses-pass-through}

Here’s a minimal pass-through example to get started.

```sh
addEventListener("fetch", event => {
  event.respondWith(fetchAndStream(event.request))
})

async function fetchAndStream(request) {
  // Fetch from origin server.
  let response = await fetch(request)

  // Create an identity TransformStream (a.k.a. a pipe).
  // The readable side becomes our new response body.
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
{: codeblock}

Some important details to note:

* Although `streamBody()` is an asynchronous function, we do not want to call `await` on it, so that it does not block forward progress of the calling `fetchAndStream()` function. It continues to run asynchronously for as long as it has an outstanding `reader.read()` or `writer.write()` operation.
* Backpressure: We `await` the read operation before calling the write operation. Likewise, we `await` the write operation before calling the next read operation. Following this pattern propagates backpressure to the origin.
* Completion: We call `writer.close()` at the end, which signals to the Edge function runtime that we’re done writing this response body. After being called, `streamBody()` terminates — if this is undesirable, pass its returned promise to `FetchEvent.waitUntil()`. If your script never calls `writer.close()`, the body appears truncated to the runtime, though it might continue to function as intended.

### Aggregate and stream multiple requests
{: #streaming-responses-aggregate-and-stream-multiple-requests}

This is similar to our aggregating multiple requests recipe, but this time we’ll start writing our response as soon as we’ve verified that every subrequest succeeded — no need to wait for the actual response bodies.

```sh
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
    if (i > 0) {
      await writer.write(encoder.encode(",\n"))
    }
    writer.releaseLock()
    await bodies[i].pipeTo(writable, { preventClose: true })
    writer = writable.getWriter()
  }

  await writer.write(encoder.encode("]"))

  await writer.close()
}
```
{: codeblock}

Again, there are a couple of important details to note:

* The runtime expects to receive TypedArrays on the readable side of the TransformStream. Therefore, we never pass a string to `writer.write()`, only Uint8Arrays. If you need to write a string, use a TextEncoder.

## Custom load balancer with Edge functions
{: #custom-load-balancer-edge-functions}

Load balancing helps you maintain the scalability and reliability of websites you host. You can use Edge functions to create custom load balancers designed to address your specific needs.

```sh
const US_HOSTS = [
  "0.us.example.com",
  "1.us.example.com",
  "2.us.example.com"
];

const IN_HOSTS = [
  "0.in.example.com",
  "1.in.example.com",
  "2.in.example.com"
];

var COUNTRIES_MAP = {
  IN: IN_HOSTS,
  PK: IN_HOSTS,
  BD: IN_HOSTS,
  SL: IN_HOSTS,
  NL: IN_HOSTS
}
addEventListener('fetch', event => {
  var url = new URL(event.request.url);

  var countryCode = event.request.headers.get('CF-IPCountry');
  var hostnames = US_HOSTS;
  if (COUNTRIES_MAP[countryCode]) {
    hostnames = COUNTRIES_MAP[countryCode];
  }
  // Randomly pick the next host
  var primary = hostnames[getRandomInt(hostnames.length)];

  var primaryUrl = new URL(event.request.url);
  primaryUrl.hostname = hostnames[primary];

  // Fallback if there is no response within timeout
  var timeoutId = setTimeout(function() {
    var backup;
    do {
        // Naive solution to pick a backup host
        backup = getRandomInt(hostnames.length);
    } while(backup === primary);

    var backupUrl = new URL(event.request.url);
    backupUrl.hostname = hostnames[backup];

    event.respondWith(fetch(backupUrl));
  }, 2000 /* 2 seconds */);

  fetch(primaryUrl)
    .then(function(response) {
        clearTimeout(timeoutId);
        event.respondWith(response);
    });  
});

function getRandomInt(max) {
  return Math.floor(Math.random() * max);
}
```
{: codeblock}

## Caching using fetch
{: #caching-using-fetch}

Determine how to cache a resource by setting TTLs, custom cache keys, and cache headers in a fetch request.

```sh
async function handleRequest(request) {  
  const url = new URL(request.url)
  
  // Only use the path for the cache key, removing query strings  
  // and always store using HTTPS, for example, https://www.example.com/file-uri-here  
  const someCustomKey = `https://${url.hostname}${url.pathname}`
  
  let response = await fetch(request, {    
    cf: {      
      // Always cache this fetch regardless of content type      
      // for a max of 5 seconds before revalidating the resource      
      cacheTtl: 5,      
      cacheEverything: true,      
      //Enterprise only feature, see Cache API for other plans      
      cacheKey: someCustomKey,    
      },  
    })  
    // Reconstruct the Response object to make its headers mutable.  
    response = new Response(response.body, response)
    
    //Set cache control headers to cache on browser for 25 minutes  
    response.headers.set("Cache-Control", "max-age=1500")  
    return response
}

addEventListener("fetch", event => {
  return event.respondWith(handleRequest(event.request))
})
```
{: codeblock}

### Caching HTML resources
{: #caching-html-resources}

```sh
// Force CIS to cache an asset
fetch(event.request, { cf: { cacheEverything: true } })
```
{: codeblock}

Setting the cache level to Cache Everything overrides the default "cacheability" of the asset. For TTL, {{site.data.keyword.cis_short_notm}} still relies on headers set by the origin.

### Custom cache keys
{: #custom-cache-keys}

This feature is available only to enterprise customers.
{: note}

A request's cache key is what determines if two requests are "the same" for caching purposes. If a request has the same cache key as some previous request, then we can serve the same cached response for both.

```sh
// Set cache key for this request to "some-string".
fetch(event.request, { cf: { cacheKey: "some-string" } })
```
{: codeblock}

Normally, {{site.data.keyword.cis_short_notm}} computes the cache key for a request based on the request's URL, but you might want different URLs to be treated as if they were the same for caching purposes. For example, if your web site content is hosted from both Amazon S3 and Google Cloud Storage - you have the same content in both places, and you use a Worker to randomly balance between the two. However, you don't want to end up caching two copies of your content. You could utilize custom cache keys to cache based on the original request URL rather than the subrequest URL:

```sh
addEventListener("fetch", (event) => {
  let url = new URL(event.request.url)  
  if (Math.random() < 0.5) {    
    url.hostname = "example.s3.amazonaws.com"  
  }  
  else {    
    url.hostname = "example.storage.googleapis.com"  
  }

  let request = new Request(url, event.request)  
  event.respondWith(    
    fetch(request, {      
      cf: { cacheKey: event.request.url },    
    })  
  )
})
```
{: codeblock}

Remember, edge functions operating on behalf of different zones cannot affect each other's cache. You can only override cache keys when making requests within your own zone (in the previous example `event.request.url` was the key stored), or requests to hosts that are not on {{site.data.keyword.cis_short_notm}}. When making a request to another {{site.data.keyword.cis_short_notm}} zone (for example, belonging to a different {{site.data.keyword.cis_short_notm}} customer), that zone fully controls how its own content is cached within {{site.data.keyword.cis_short_notm}}; you cannot override it.

### Override based on origin response code
{: #override-origin-response-code}

This feature is available only to enterprise customers.
{: note}

```sh
// Force response to be cached for 86400 seconds for 200 status
// codes, 1 second for 404, and do not cache 500 errors.
fetch(request, {  
  cf: { cacheTtlByStatus: { "200-299": 86400, 404: 1, "500-599": 0 } },
})
```
{: codeblock}

This option is a version of the `cacheTtl` feature which chooses a TTL based on the response's status code and does not automatically set `cacheEverything: true`. If the response to this request has a status code that matches, {{site.data.keyword.cis_short_notm}} caches for the instructed time, and override cache directives sent by the origin.

#### TTL interpretation
{: #ttl-interpretation}

The following TTL values are interpreted by {{site.data.keyword.cis_short_notm}}:
- Positive values: Indicate in seconds how long {{site.data.keyword.cis_short_notm}} should cache the asset for.
- `0`: The asset is cached but expires immediately (revalidate from origin every time).
- `-1` or any negative value: Instructs {{site.data.keyword.cis_short_notm}} not to cache at all.

## Cache API
{: #cache-api}

Cache using the {{site.data.keyword.cis_short_notm}} Cache API. This example can also cache POST requests.

```js
const someOtherHostname = "my.herokuapp.com"

async function handleRequest(event) {
  const request = event.request
  const cacheUrl = new URL(request.url)

  // Hostname for a different zone
  cacheUrl.hostname = someOtherHostname

  const cacheKey = new Request(cacheUrl.toString(), request)
  const cache = caches.default

  // Get this request from this zone's cache
  let response = await cache.match(cacheKey)

  if (!response) {
    //If not in cache, get it from origin
    response = await fetch(request)

    // Must use Response constructor to inherit all of response's fields
    response = new Response(response.body, response)

    // Cache API respects Cache-Control headers. Setting max-age to 10
    // will limit the response to be in cache for 10 seconds max
    response.headers.append("Cache-Control", "max-age=10")

    // Store the fetched response as cacheKey
    // Use waitUntil so computational expensive tasks don"t delay the response
    event.waitUntil(cache.put(cacheKey, response.clone()))
  }
  return response
}

async function sha256(message) {
  // encode as UTF-8
  const msgBuffer = new TextEncoder().encode(message)

  // hash the message
  const hashBuffer = await crypto.subtle.digest("SHA-256", msgBuffer)

  // convert ArrayBuffer to Array
  const hashArray = Array.from(new Uint8Array(hashBuffer))

  // convert bytes to hex string
  const hashHex = hashArray.map(b => ("00" + b.toString(16)).slice(-2)).join("")
  return hashHex
}

async function handlePostRequest(event) {
  const request = event.request
  const body = await request.clone().text()
  const hash = await sha256(body)
  const cacheUrl = new URL(request.url)

  // Store the URL in cache by prepending the body's hash
  cacheUrl.pathname = "/posts" + cacheUrl.pathname + hash

  // Convert to a GET to be able to cache
  const cacheKey = new Request(cacheUrl.toString(), {
    headers: request.headers,
    method: "GET",
  })

  const cache = caches.default

  //Find the cache key in the cache
  let response = await cache.match(cacheKey)

  // Otherwise, fetch response to POST request from origin
  if (!response) {
    response = await fetch(request)
    event.waitUntil(cache.put(cacheKey, response.clone()))
  }
  return response
}

addEventListener("fetch", event => {
  try {
    const request = event.request
    if (request.method.toUpperCase() === "POST")
      return event.respondWith(handlePostRequest(event))
    return event.respondWith(handleRequest(event))
  } catch (e) {
    return event.respondWith(new Response("Error thrown " + e.message))
  }
})
```
{: codeblock}
