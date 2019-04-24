---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: edge function use cases, beta

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Edge Functions 用例 (Beta)
{:#edge-functions-use-cases-beta-}

本软件“按现状”提供，特此声明免除任何明示的或暗含的保证，包括但不限于暗含的有关适销性和适用于某种特定用途的保证。在任何情况下，IBM 对由于使用本软件而造成的任何直接的、间接的、附带的、特别的、惩罚性或后果性的损害赔偿（包括但不限于购买替代商品或服务、无法使用、丢失数据、利润的损失或业务中断）不承担任何责任，无论由于什么原因、根据何种责任条款；无论是合同责任、严格责任还是侵权责任（包括过失或其他原因），即使事先已被告知可能会造成此类损害赔偿，也是如此。

## A/B 测试
{: #ab-testing}
您可以创建 CIS Edge Function 以控制 A/B 测试。
```
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

## 添加响应头
{: #add-response-header}
要修改响应头，首先需要生成响应的副本以使其可变。然后，您可以使用 Headers 接口来添加、更改或除去头。
```
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

## 聚集多个请求
{: #aggregate-multiple-requests}
此处，我们针对不同的 API 端点生成多个请求，聚集响应并将其作为单个响应发回。
```
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

## 条件路由
{: #conditional-routing}
基于使用的设备交付不同内容的最简单方式是基于关注的条件重新编写请求的 URL。例如：


### 设备类型
{: #conditional-routing-device-type}

```
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
### 定制头
{: #conditional-routing-custom-headers}

```
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

## 热链接保护
{: #hot-link-protection}
您可以使用 CIS Edge Functions 来保护 Web 属性上的热链接。
```
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

## 无源响应
{: #originless-responses}
您可以直接从 Edge 返回响应。无需点击源。

### 忽略 POST 和 PUT HTTP 请求
{: #originless-responses-ignore-post-put-http-requests}

忽略 POST 和 PUT HTTP 请求。此片段允许将所有其他请求传递到源。
```
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
### 拒绝 Spider 或搜寻器
{: #originless-responses-deny-spider-crawler}

保护源避免不想要的 spider 或搜寻器。在此情况下，如果用户代理程序为“annoying-robot”，那么 Edge 函数会返回响应，而不是将请求发送到源。
```
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
### 阻止特定 IP 的连接
{: #originless-responses-prevent-specific-ip-connection}

将 IP 地址列入黑名单。此代码片段阻止特定 IP（在此情况下为“225.0.0.1”）连接到源。
```
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

## Post 请求
{: #post-requests}
读取 HTTP POST 请求的内容
```
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
从 Edge 函数创建 HTTP POST 请求
```
addEventListener('fetch', event => {
  event.respondWith(fetchAndApply(event.request))
})

/**
 * Create a POST request with body 'key=world'
 * Here, we are assuming that example.com will acknowledge the POST request with body key=world
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

## 设置 cookie
{: #setting-cookies}
您可以使用 CIS Edge Functions 设置 cookie。
```
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

## 已签名请求
{: #signed-requests}
借助于 Web Crypto API，可以在 Edge 函数中实现被称为请求签名的常用 URL 认证方法。

在此处显示的示例中，我们将使用基于散列的消息认证代码 (HMAC) 以及 SHA-256 摘要算法，认证 URL 的路径以及附带的到期时间戳记。要使用户代理程序成功访存已认证的资源，它们将需要通过查询参数提供正确的路径、到期时间戳记和 HMAC - 如果这三者中有任何一个被篡改，那么请求将失败。

请注意，到期时间戳记的真实性由 HMAC 涵盖，因此如果 HMAC 正确，那么我们可确信用户提供的时间戳记正确，并因此知道 URL 何时到期。此外，用户还可以确定其拥有的 URL 是否已到期。

### 验证已签名请求
{: #signed-requests-verify}
此示例针对路径名以 `/verify/` 开头的任何请求 URL 验证 HMAC。

为方便调试起见，如果 URL 或 HMAC 无效，或者 URL 已到期，那么此 Edge 函数会返回 403。您可能希望在实际实现中返回 404。
```
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
// than 255, their values will overflow!
function byteStringToUint8Array(byteString) {
  const ui = new Uint8Array(byteString.length)
  for (let i = 0; i < byteString.length; ++i) {
    ui[i] = byteString.charCodeAt(i)
  }
  return ui
}
```
### 生成已签名请求
{: #signed-requests-generate}

通常，已签名请求将以某种频带外方式（例如，电子邮件）交付给用户，或者由用户自己实际生成（如果用户还拥有对称密钥）。当然，我们还可以在 Edge 函数中生成已签名请求。

对于以 `/generate/` 开头的任何请求 URL，我们将 `/generate/` 替换为 `/verify/`，使用其时间戳记对生成的路径签名，然后通过响应主体返回完整的已签名 URL。
```
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

## 以流式方法传递响应
{: #streaming-responses}
在向 `event.respondWith()` 交付响应之前，Edge 函数脚本不需要准备其整个响应主体。使用 TransformStream，可以在发送响应的前文（即，HTTP 状态行和头）后以流式方法传递响应主体。这样一来，我们可以最大程度地减少：

* 访问者获得第一个字节所需的时间。

* 必须在 Edge 函数脚本中完成的缓冲量。

如果必须处理或变换大于 Edge 函数内存限制的响应主体，那么最大程度地减少缓冲尤为重要。在这些情况下，流式方法是唯一可行的实现策略。

缺省情况下，CIS Edge Function 服务已尽可能以流式方式进行传递。如果希望以某种方式修改响应主体，同时保持流式方法行为，那么只需使用这些 API。如果 Edge 函数脚本仅照字面将后续响应传递回客户机，而不读取其主体，那么其主体处理已处于最佳状态，并且无需使用此处描述的方法。
{:note}

### 流式传递
{: #streaming-responses-pass-through}

以下是用于入门的极简传递示例：
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
以下是需要注意的一些重要详细信息：

* 虽然 `streamBody()` 是异步函数，但是我们不会`等待`它，因此它不会阻止调用 `fetchAndStream()` 函数继续向前执行。只要它有未完成的 `reader.read()` 或 `writer.write()` 操作，就会继续异步运行。

* 反压：我们在调用写操作之前`等待`读操作。类似地，我们在调用下一读操作之前`等待`写操作。遵循此模式会将反压传播到源。

* 完成：我们在结束时调用 `writer.close()`，这会向 Edge Function 运行时发信号称我们已完全完成编写此响应主体的操作。调用时，`streamBody()` 将终止 - 如果不希望发生此情况，请将其返回的 Promise 传递到 `FetchEvent.waitUntil()`。如果脚本从未调用 `writer.close()`，那么主体将对运行时显示为截断，但它仍可继续按预期运行。

### 聚集和以流式方法传递多个请求
{: #streaming-responses-aggregate-and-stream-multiple-requests}

这类似于“聚集多个请求”诀窍，但这次我们将在验证每个子请求已成功后立即开始编写响应 - 无需等待实际响应主体。
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
同样，还要注意以下几个重要详细信息：

* 运行时期望在 TransformStream 的可读端接收 TypedArray。因此，我们从不将字符串传递到 `writer.write()`，仅传递 Uint8Array。如果需要编写字符串，请使用 TextEncoder。

* `manualPipeTo()` 如此命名，是因为截至本文发布时，`ReadableStream.pipeTo()` 尚未在 CIS Edge Functions 中实现。在后者变为可用时，更符合习惯且更理想的方式是将字节从 ReadableStream 抽取到 WritableStream。
