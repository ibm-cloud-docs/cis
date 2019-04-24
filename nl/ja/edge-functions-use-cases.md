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

# エッジ機能のユース・ケース (ベータ版)
{:#edge-functions-use-cases-beta-}

IBM は、このソフトウェアを特定物として現存するままの状態で提供し、法律上の瑕疵担保責任、商品性の保証および特定目的適合性の保証を含むすべての明示もしくは黙示の保証責任を負いません。起こりうる損害について予見の有無を問わず、「ソフトウェア」を使用したために生じる、直接的、間接的、付帯的、特別、懲罰的、または結果的損害 (代替の製品またはサービスの調達、データまたは利益の喪失、事業の中断などを含み、他のいかなる場合も含む) については、それが契約、厳格な責任、不法行為 (過失の場合もそうでない場合も含む) など、いかなる責任の理論においても、IBM はその責任を負いません。

## A/B テスト
{: #ab-testing}
CIS エッジ機能を作成して、A/B テストを制御できます。
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

## 応答ヘッダーの追加
{: #add-response-header}
応答ヘッダーを変更するには、まず変更可能にするために応答のコピーを作成する必要があります。次に「ヘッダー」インターフェースを使用してヘッダーの追加、変更、または削除を実行できます。
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

## 複数の要求の集約
{: #aggregate-multiple-requests}
以下では、さまざまな API エンドポイントに対して複数の要求を行い、応答を集約して単一の応答として送り返します。
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

## 条件付きルーティング
{: #conditional-routing}
使用されるデバイスに基づいてさまざまなコンテンツを送達するには、関心のある条件に基づいて要求の URL を書き直すのが最も簡単な方法です。例えば次のようにします。

### デバイス・タイプ
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
### カスタム・ヘッダー
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

## ホット・リンクの保護
{: #hot-link-protection}
CIS エッジ機能を使用して、Web プロパティー上でホット・リンクを保護できます。
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

## 起点のない応答
{: #originless-responses}
直接エッジから応答を戻すことができます。起点に達する必要はありません。

### POST と PUT の HTTP 要求の無視
{: #originless-responses-ignore-post-put-http-requests}

POST と PUT の HTTP 要求を無視します。以下のスニペットを使用すると、その他の要求をすべて起点にパススルーできます。
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
### スパイダーまたはクローラーの拒否
{: #originless-responses-deny-spider-crawler}

望ましくないスパイダーまたはクローラーから起点を保護します。以下のケースでは、ユーザー・エージェントが「うるさいロボット」の場合、エッジ機能は要求を起点に送信する代わりに応答を戻します。
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
### 特定の IP の接続の防止
{: #originless-responses-prevent-specific-ip-connection}

IP アドレスをブラックリストに登録します。以下のコード・スニペットは、特定の IP (このケースでは「225.0.0.1」) が起点に接続できないようにします。
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

## Post 要求
{: #post-requests}
HTTP POST 要求からのコンテンツの読み取り
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
エッジ機能からの HTTP POST 要求の作成
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

## Cookie の設定
{: #setting-cookies}
CIS エッジ機能を使用して Cookie を設定できます。
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

## 署名済み要求
{: #signed-requests}
Web 暗号 API の助けを借りて、要求の署名という一般的な URL 認証方式をエッジ機能に実装できます。

ここで示されている例では、Hash-based Message Authentication Code (HMAC) と SHA-256 ダイジェスト・アルゴリズムを併用して、URL のパスと、付随する有効期限のタイム・スタンプを認証します。ユーザー・エージェントが認証済みのリソースを正常に取り出すには、照会パラメーターを使用して、正しいパス、有効期限タイム・スタンプ、HMAC を提供する必要があります。これらの 3 つのいずれかが改ざんされていると、要求は失敗します。

有効期限タイム・スタンプの真正性は HMAC に包含されているので、HMAC が正しい場合はユーザー提供のタイム・スタンプが正しいことを信頼でき、URL の期限が切れる時点を特定できることに注意してください。さらに、ユーザーは保有している URL の有効期限が切れているかどうか判別することもできます。

### 署名済み要求の検証
{: #signed-requests-verify}
以下の例では、パス名の先頭が `/verify/` の要求 URL について HMAC を検証します。

デバッグの便宜上、URL または HMAC が無効な場合や URL が期限切れの場合には、このエッジ機能は 403 を戻します。実際の実装では 404 を戻すこともできます。
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
### 署名済み要求の生成
{: #signed-requests-generate}

通常、署名済み要求は、E メールなどのアウト・オブ・バンド経由でユーザーに送達されるか、ユーザーが対称鍵も所有している場合はユーザー自身により実際に生成されます。もちろん、弊社がエッジ機能で署名済み要求を生成することもできます。

先頭が `/generate/` の要求 URL の場合、`/generate/` を `/verify/` に置き換え、タイム・スタンプを使用して置換結果のパスに署名して、応答本体で完全な署名済み URL を戻します。
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

## 応答のストリーミング
{: #streaming-responses}
応答を `event.respondWith()` に送達する前に、エッジ機能のスクリプトで応答本体全体を準備する必要はありません。TransformStream を使用して、応答の前付け (つまり HTTP 状況表示行とヘッダー) の送信後に応答本体をストリーミングできます。この方法の場合、以下を最小限にすることができます。

* 訪問者の最初のバイトまでの時間。

* エッジ機能のスクリプト内で行う必要があるバッファリングの量。

バッファリングを最小にすることは、エッジ機能のメモリー制限より大きい応答本体を処理したり変換したりしなければならない場合に特に重要です。このようなケースでは、ストリーミングが唯一の実現可能な実装戦略になります。

デフォルトでは、CIS エッジ機能サービスは可能な場合には必ずストリーミングしています。これらの API を使用する必要があるのは、ストリーミングの動作を維持しながら何らかの方法で応答本体を変更しようとしている場合に限られます。エッジ機能のスクリプトが二次要求の応答本体を読み取らずに逐語的にクライアントに渡し戻すだけの場合は、その本体の処理は既に最適なので、ここで説明されている手法は不要です。
{:note}

### パススルーのストリーミング
{: #streaming-responses-pass-through}

初めて使用するための最小のパススルーの例を以下に示します。
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
以下の重要な詳細情報に注意してください。

* 非同期関数の `streamBody()` を`待機`することはないので、この関数により呼び出し側の `fetchAndStream()` 関数が先に進むのをブロックされることはありません。未処理の `reader.read()` または `writer.write()` 操作がある限り、引き続き非同期的に実行されます。

* バック・プレッシャー: 書き込み操作を呼び出す前に、読み取り操作を`待機`します。同様に、次の読み取り操作を呼び出す前に、書き込み操作を`待機`します。このパターンに従って、バック・プレッシャーを起点に伝搬します。

* 完了: 最後に `writer.close()` を呼び出します。これは、この応答本体の書き込みが完了したことをエッジ機能ランタイムに通知します。呼び出しが行われると、`streamBody()` は終了します。これが望ましくない場合は、戻されるプロミスを `FetchEvent.waitUntil()` に渡します。ご使用のスクリプトで `writer.close()` が呼び出されることがない場合は、本体はランタイムに切り捨てられるように見えますが、引き続き想定どおりに機能している可能性があります。

### 複数の要求の集約とストリーミング
{: #streaming-responses-aggregate-and-stream-multiple-requests}

これは「複数の要求の集約」の方策に似ていますが、二次要求がすべて正常に実行されたことが検証されると即時に応答の書き込みが開始されます。実際の応答本体を待機する必要はありません。
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
再び以下の 2 つの重要な詳細情報に注意してください。

* ランタイムは TransformStream の読み取り可能な側で TypedArrays を受け取ることを予期しています。したがって、`writer.write()` にストリングを渡すことはなく、Uint8Arrays のみです。ストリングを書き込む必要がある場合は、TextEncoder を使用します。

* この資料の作成時点で `ReadableStream.pipeTo()` がまだ CIS エッジ機能で実装されていないので、上記のように `manualPipeTo()` という名前が指定されています。使用可能になると、前者の方が ReadableStream から WritableStream にバイトをポンプする慣用的で最適な方法になります。
