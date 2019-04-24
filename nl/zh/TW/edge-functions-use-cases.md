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

# Edge Functions 使用案例（測試版）
{:#edge-functions-use-cases-beta-}

IBM 僅以「現狀」交付本軟體，而不提供任何明示或默示之保證，包括但不限於可售性及符合特定效用之默示保證。對於任何直接、間接、附帶、特殊、懲罰性或衍生損害（包括，惟不限於代用品或服務的購買；使用、資料或利潤的損失；或業務中斷）；任何責任條款（無論是否記錄於合約中）均無過失責任；或因使用本軟體所造成的任何侵權行為（包括疏失或其他原因），IBM 將不負任何責任，即使已被告知該情事可能發生時，亦同。

## A/B 測試
{: #ab-testing}
您可以建立「CIS 邊緣功能」來控制 A/B 測試。
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

## 新增回應標頭
{: #add-response-header}
若要修改回應標頭，您需要先建立該回應的副本，使其成為可變動的。然後，您可以使用「標頭」介面來新增、變更或移除標頭。
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

## 聚集多個要求
{: #aggregate-multiple-requests}
此時，我們對不同的 API 端點提出多個要求，聚集回應，並以單一回應傳回它。
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

## 條件式遞送
{: #conditional-routing}
根據所使用的裝置遞送不同內容的最簡單方法，是根據您關注的條件來重寫該要求的 URL。例如：

### 裝置類型
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
### 自訂標頭
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

## 快速鏈結保護
{: #hot-link-protection}
您可以使用 CIS Edge Functions 來保護 Web 內容的快速鏈結。
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

## 無原點回應
{: #originless-responses}
您可以直接從邊緣傳回回應。不需要命中原點。

### 忽略 POST 及 PUT HTTP 要求
{: #originless-responses-ignore-post-put-http-requests}

忽略 POST 及 PUT HTTP 要求。此 Snippet 容許所有其他要求通過原點。
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
### 拒絕網路蜘蛛或搜索器
{: #originless-responses-deny-spider-crawler}

保護原點不讓惡意網路蜘蛛或搜索器進入。在此情況下，如果使用者代理程式是 "annoycing-robot"，則邊緣功能會傳回回應，而不是將要求傳送至原點。
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
### 防止特定 IP 連接
{: #originless-responses-prevent-specific-ip-connection}

將 IP 位址列入黑名單。這個程式碼 Snippet 會防止特定 IP（在此案例中為 '225.0.0.1'）連接至原點。
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

## POST 要求
{: #post-requests}
從 HTTP POST 要求中讀取內容
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
從邊緣功能建立 HTTP POST 要求
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

## 設定 Cookie
{: #setting-cookies}
您可以使用 CIS Edge Functions 來設定 Cookie。
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

## 已簽署的要求
{: #signed-requests}
在 Web 加密 API 的協助下，您可以在邊緣功能中實作一般 URL 鑑別方法，即所謂的要求簽署。

在這裡呈現的範例中，我們會使用具有 SHA-256 摘要演算法的「雜湊式訊息鑑別碼 (HMAC)」，來鑑別 URL 的路徑以及隨附的有效期限時間戳記。為了讓使用者代理程式順利提取已鑑別的資源，他們需要透過查詢參數提供正確的路徑、有效期限時間戳記及 HMAC（如果這三者有任何一個遭到竄改），否則要求會失敗。

請注意，HMAC 包含有效期限時間戳記的確實性，因此，如果 HMAC 是正確的，我們可以信賴使用者提供的時間戳記是正確的，因而知道 URL 何時到期。此外，使用者還可以判斷其佔有的 URL 是否過期。

### 驗證已簽署的要求
{: #signed-requests-verify}
這個範例會針對其路徑名稱開頭為 `/verify/` 的任何要求 URL 來驗證 HMAC。

為了方便進行除錯，如果 URL 或 HMAC 無效，或是 URL 過期，這個邊緣功能會傳回 403。在實際的實作中，您可能想要傳回 404。
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
### 產生已簽署的要求
{: #signed-requests-generate}

通常，已簽署的要求會以某種頻外方式（例如電子郵件）遞送給使用者，如果使用者也擁有對稱金鑰，則實際上會由使用者自己產生已簽署的要求。當然，我們也可以在邊緣功能中產生已簽署的要求。

對於開頭為 `/generate/` 的任何要求 URL，我們會將 `/generate/` 取代為 `/verify/`，並以其時間戳記來簽署產生的路徑，然後透過回應內文傳回完整且已簽署的 URL。
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

## 串流回應
{: #streaming-responses}
在將「回應」遞送至 `event.respondWith()` 之前，邊緣功能 Script 並不需要準備它的整個回應內文。使用 TransformStream，在傳送回應的前頁（亦即 HTTP 狀態行和標頭）之後，可以串流處理回應內文。這樣可以將下列項目最小化：

* 訪客的第一個位元組時間。

* 邊緣功能 Script 中必須完成的緩衝數量。

如果您必須處理或轉換大於邊緣功能記憶體限制的回應內文，則將緩衝最小化特別重要。在這些情況下，串流是唯一可行的實作策略。

如有可能，「CIS 邊緣功能」服務預設已串流處理。只有當您想要以某種方式修改回應內文，但又想要維護串流行為時，才需要使用這些 API。如果邊緣功能 Script 僅將子要求回應逐項傳回至用戶端，而未讀取其內文，則其內文處理已經最佳化，因此不需要這裡所描述的技術。
{:note}

### 串流透通
{: #streaming-responses-pass-through}

以下是開始使用的最小透通範例：
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
有一些重要的詳細資料要注意：

* 雖然 `streamBody()` 為非同步函數，但我們不會`等待`，以免它封鎖 `fetchAndStream()` 函數呼叫的轉遞進度。只要它還有未完成的 `reader.sread()` 或 `writer.write()` 作業，它就會繼續以非同步方式執行。

* 反壓：在呼叫寫入作業之前，我們會`等待`讀取作業。同樣地，在呼叫下一個讀取作業之前，我們會先`等待`寫入作業。遵循此一型樣可將反壓延伸至原點。

* 完成：結束時我們會呼叫 `writer.close()`，它向邊緣功能運行環境指出我們已徹底完成撰寫此回應內文。呼叫它之後，`streamBody()` 就會終止 - 如果不希望這樣，請將其傳回的承諾傳遞給 `FetchEvent.waitUntil()`。如果您的 Script 從未呼叫 `writer.close()`，則內文看起來將截斷至運行環境，但它仍可如預期一般繼續運作。

### 聚集及串流處理多個要求
{: #streaming-responses-aggregate-and-stream-multiple-requests}

這類似「聚集多個要求」秘訣，但這次我們一驗證每個子要求成功，就會開始撰寫回應 - 而不需要等待實際的回應內文。
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
同樣地，有一些重要的詳細資料要注意：

* 運行環境預期會在 TransformStream 的可讀取端接收 TypedArrays。因此，我們絕不能將字串傳遞至 `writer.write()`，只能傳遞 Uint8Arrays。如果您需要撰寫字串，請使用 TextEncoder。

* `manualPipeTo()` 會如此命名，是因為在撰寫本書時，尚未在 CIS Edge Functions 中實作 `ReadableStream.pipeTo()`。當它變成可用時，它將是更慣用且更理想的方法，可將 ReadableStream 的位元組灌注到 WritableStream。
