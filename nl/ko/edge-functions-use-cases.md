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

# Edge Functions 유스 케이스(베타)
{:#edge-functions-use-cases-beta-}

IBM은 상품성 및 특정 목적에의 적합성에 대한 묵시적 보증을 포함하여(단, 이에 한하지 않음) 묵시적이든 명시적이든 어떠한 종류의 보증 없이 이 소프트웨어를 "현상태대로" 제공합니다. 어떠한 경우에도 IBM은 책임 이론에 의한 모든 손해에 대해 그러한 손해의 발생 가능성을 통지받은 경우에도 계약상, 무과실 책임 또는 불법 행위(과실 및 기타 경우 포함)에 관계 없이, 본 소프트웨어를 사용하여 발생한 직접 손해, 간접 손해, 부수적 손해, 특별 손해, 징벌적 손해 또는 결과적 손해(대체품 또는 대체 서비스 조달, 용익권 손실 또는 데이터 분실 또는 이익 손실, 사업 중단 포함. 단, 이에 한하지 않음)에 대해 일체의 책임을 지지 않습니다. 

## A/B 테스트
{: #ab-testing}
CIS Edge Function을 작성하여 A/B 테스트를 제어할 수 있습니다.
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

## 응답 헤더 추가
{: #add-response-header}
응답 헤더를 수정하려면 먼저 변경 가능하도록 응답 사본을 작성해야 합니다. 그런 다음 헤더 인터페이스를 사용하여 헤더를 추가하거나 변경하거나 제거할 수 있습니다.
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

## 다중 요청 집계
{: #aggregate-multiple-requests}
여기서 서로 다른 API 엔드포인트에 대한 여러 요청을 작성하고 응답을 집계한 다음 단일 응답으로 돌려보냅니다.
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

## 조건부 라우팅
{: #conditional-routing}
사용 중인 디바이스에 따라 여러 컨텐츠를 제공하는 가장 쉬운 방법은 관심 있는 조건을 기반으로 요청 URL을 다시 작성하는 것입니다. 예를 들어 다음과 같습니다.

### 디바이스 유형
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
### 사용자 정의 헤더
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

## 핫링크(hot-link) 보호
{: #hot-link-protection}
CIS Edge Functions를 사용하여 웹 특성에서 핫링크를 보호할 수 있습니다.
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

## 오리진 없는 응답
{: #originless-responses}
에지에서 직접 응답을 리턴할 수 있습니다. 오리진에 도달하지 않아도 됩니다.

### POST 및 PUT HTTP 요청 무시
{: #originless-responses-ignore-post-put-http-requests}

POST 및 PUT HTTP 요청을 무시합니다. 이 스니펫에서는 다른 모든 요청이 오리진을 거칠 수 있습니다.
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
### 스파이더 또는 크롤러 거부
{: #originless-responses-deny-spider-crawler}

원하지 않는 스파이더나 크롤러로부터 오리진을 보호합니다. 이 경우 사용자 에이전트가 “성가신 로봇”이면 에지 함수가 요청을 오리진으로 보내는 대신 응답을 리턴합니다.
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
### 연결에서 특정 IP 방지
{: #originless-responses-prevent-specific-ip-connection}

IP 주소를 블랙리스트에 추가합니다. 이 코드 스니펫은 특정 IP(이 경우 ‘225.0.0.1’)가 오리진에 연결되지 않도록 합니다.
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

## Post 요청
{: #post-requests}
HTTP POST 요청에서 컨텐츠 읽기
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
에지 함수에서 HTTP POST 요청 작성
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

## 쿠키 설정
{: #setting-cookies}
CIS Edge Functions를 사용하여 쿠키를 설정할 수 있습니다.
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

## 서명된 요청
{: #signed-requests}
Web Crypto API를 사용하여 에지 함수에서 요청 서명으로 알려진 일반 URL 인증 메소드를 구현할 수 있습니다.

여기에 제공된 예제에서는 SHA-256 요약 알고리즘이 있는 HMAC(Hash-based Message Authentication Code)를 사용하여 만기 시간소인과 함께 URL 경로를 인증합니다. 사용자 에이전트가 인증된 리소스를 페치하려면 조회 매개변수를 통해 올바른 경로, 만기 시간소인 및 HMAC를 제공해야 합니다. 이 세 가지 중 하나 이상이 변경되면 요청이 실패합니다.

만기 시간소인의 인증은 HMAC에 의해 처리되므로, HMAC가 올바른 경우 올바른 사용자 제공 시간소인에 의존하게 되어 URL 만기를 알 수 있습니다. 또한 사용자는 소유한 URL이 만료되었는지 여부를 판별할 수 있습니다.

### 서명된 요청 확인
{: #signed-requests-verify}
이 예제에서는 경로 이름이 `/verify/`로 시작되는 요청 URL의 HMAC를 확인합니다.

URL 또는 HMAC가 올바르지 않거나 URL이 만료된 경우 디버깅 편의를 위해 이 에지 함수는 403을 리턴합니다. 실제 구현에서는 404를 리턴할 수 있습니다.
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
### 서명된 요청 생성
{: #signed-requests-generate}

일반적으로 서명된 요청은 이메일과 같은 대역 외 방식으로 사용자에게 제공되거나, 대칭 키를 소유한 사용자에 의해 실제로 생성됩니다. 물론 에지 함수에서 서명된 요청을 생성할 수도 있습니다.

`/generate/`로 시작되는 요청 URL의 경우 `/generate/`를 `/verify/`로 바꾸고 결과 경로를 해당 시간소인으로 서명한 다음 응답 본문을 통해 서명된 전체 URL을 리턴합니다.
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

## 응답 스트리밍
{: #streaming-responses}
에지 함수 스크립트는 `event.respondWith()`에 대한 응답을 제공하기 전에 전체 응답 본문을 준비하지 않아도 됩니다. TransformStream을 사용하면 응답의 앞부분(예: HTTP 상태 행과 헤더)을 보낸 후 응답 본문을 스트리밍할 수 있습니다. 이렇게 하면 다음을 최소화할 수 있습니다.

* 방문자의 TTFB(Time-to-first-byte).

* 에지 함수 스크립트에서 수행해야 하는 버퍼링의 양.

에지 함수의 메모리 한계보다 큰 응답 본문을 처리하거나 변환해야 하는 경우 버퍼링을 최소화하는 것이 특히 중요합니다. 이러한 경우 스트리밍은 실현 가능한 유일한 구현 전략입니다.

CIS Edge Function 서비스는 가능한 경우 기본적으로 스트리밍합니다. 스트리밍 동작을 유지하면서 어떤 방식으로든 응답 본문을 수정하려는 경우 이러한 API를 사용해야 합니다. 에지 함수 스크립트가 하위 요청의 응답만 다시 클라이언트로 전달하는 경우, 본문을 읽지 않는 상태에서 본문 처리가 이미 최적의 상태이며 여기에 설명된 기술이 필요하지 않습니다.
{:note}

### 패스 스루 스트리밍
{: #streaming-responses-pass-through}

다음은 시작하는 데 필요한 최소 패스 스루 예제입니다.
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
다음과 같은 몇 가지 중요한 세부사항이 있습니다.

* `streamBody()`는 비동기 함수이지만, `fetchAndStream()` 함수 호출의 진행을 막지 않도록 `기다리지` 않습니다. 이 함수는 중요한 `reader.read()` 또는 `writer.write()` 오퍼레이션을 포함하는 한 계속해서 비동기식으로 실행됩니다.

* 역압: 쓰기 오퍼레이션을 호출하기 전에 읽기 오퍼레이션을 `기다립니다`. 마찬가지로 다음 읽기 오퍼레이션을 호출하기 전에 쓰기 오퍼레이션을 `기다립니다`. 이 패턴을 따르면 오리진으로 역압(backpressure)이 전파됩니다.

* 완료: 마지막에 이 응답 본문 쓰기를 완료했다는 신호를 Edge Function 런타임으로 보내는 `writer.close()`를 호출합니다. 호출되면 `streamBody()`가 종료됩니다. 이를 원하지 않으면 리턴된 프라미스를 `FetchEvent.waitUntil()`로 전달하십시오. 스크립트가 `writer.close()`를 호출하지 않으면 계속 의도대로 작동할 수는 있지만 본문이 런타임에 잘린 것처럼 보입니다.

### 다중 요청 집계 및 스트리밍
{: #streaming-responses-aggregate-and-stream-multiple-requests}

이는 다중 요청 집계 방법과 유사하지만, 이 경우 모든 하위 요청이 성공하자마자 응답을 작성하기 시작하며 실제 응답 본문을 기다리지 않아도 됩니다.
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
다시 말하지만, 주목해야 할 몇 가지 중요한 세부사항이 있습니다.

* 런타임은 읽기 가능한 TransformStream에서 TypedArrays를 수신해야 합니다. 따라서 문자열을 `writer.write()`로 전달하지 않으며 Uint8Arrays만 전달합니다. 문자열을 작성해야 하는 경우에는 TextEncoder를 사용하십시오.

* 현재 이 문서에서는 `ReadableStream.pipeTo()`가 CIS Edge Functions에서 아직 구현되지 않았으므로 `manualPipeTo()`라고 합니다. 사용 가능하게 되면 ReadableStream에서 WritableStream으로 바이트를 펌프하는 것이 자연스러우며 최선의 방법입니다.
