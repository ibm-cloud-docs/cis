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

# Anwendungsfälle für Edge-Funktionen (Beta)
{:#edge-functions-use-cases-beta-}

Diese Software wird von IBM ohne Wartung (auf "as-is"-Basis) und ohne jegliche Gewährleistung (ausdrücklich oder stillschweigend) zur Verfügung gestellt, insbesondere ohne Gewährleistung für die Handelsüblichkeit oder die Verwendungsfähigkeit für einen bestimmten Zweck.
Unter keinen Umständen ist IBM haftbar für unmittelbare und
mittelbare Schäden oder Folgeschäden (einschließlich, aber nicht beschränkt auf die Beschaffung von Ersatzprodukten
oder -leistungen, Nutzungsausfall, Datenverlust, entgangenen Gewinn oder Unterbrechung von Geschäftsabläufen),
die aufgrund der Nutzung dieser Software entstehen, selbst wenn sie auf die Möglichkeit solcher Schäden hingewiesen wurden.
Dies gilt unabhängig davon, wie die Schäden verursacht wurden und ungeachtet jeglicher Haftungstheorie,
gleich ob vertragliche Haftung, Gefährdungshaftung oder Haftung aufgrund unerlaubter Handlungen
(einschließlich Fahrlässigkeit oder anderweitiger Handlungen).


## A/B-Test
{: #ab-testing}
Sie können eine CIS Edge-Funktion erstellen, um A/B-Tests zu steuern.
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

## Antwortheader hinzufügen
{: #add-response-header}
Um die Antwortheader zu ändern, müssen Sie zuerst eine Kopie der Antwort erstellen, um sie veränderbar zu machen. Anschließend können sie die Headerschnittstelle verwenden, um Header hinzuzufügen, zu ändern oder zu entfernen. 
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

## Mehrere Anforderungen zusammenfassen
{: #aggregate-multiple-requests}
Hier werden mehrere Anforderungen an unterschiedliche API-Endpunkte gestellt, die Antworten werden zusammengefasst und als eine Antwort zurückgesendet. 
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

## Bedingtes Routing
{: #conditional-routing}
Die einfachste Möglichkeit, auf Basis der verwendeten Geräte unterschiedlichen Inhalte zu liefern, besteht darin, die URL der Anforderung auf Grundlage der entscheidenden Bedingung neu zu schreiben. Beispiel:

### Gerätetyp
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
### Header anpassen
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

## Hot Link-Schutz
{: #hot-link-protection}
Sie können CIS-Edge-Funktionen verwenden, um Ihre Hot-Links in Ihren Webeigenschaften zu schützen. 
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

## Ursprungslose Antworten
{: #originless-responses}
Sie können Antworten direkt vom Edge zurückgeben. Sie müssen Ihren Ursprung nicht antasten. 

### POST und PUT HTTP-Anforderungen ignorieren
{: #originless-responses-ignore-post-put-http-requests}

Ignorieren Sie POST und PUT HTTP-Anforderungen. Dieses Snippet ermöglicht allen anderen Anforderungen, den Weg bis zum Ursprung zu durchlaufen. 
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
### Spider oder Crawler zurückweisen
{: #originless-responses-deny-spider-crawler}

Schützen Sie Ihren Ursprung vor unerwünschten Spidern oder Crawlern. Wenn ein Benutzeragent ein störender Roboter (“annoying-robot”) ist, gibt die Edge-Funktion die Antwort zurück, anstatt die Anforderung an den Ursprung zu senden. 
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
### Verbindung einer bestimmten IP verhindern
{: #originless-responses-prevent-specific-ip-connection}

Schwarze Liste mit IP-Adressen. Dieses Code-Snippet bewirkt, dass bestimmte IP-Adressen, in diesem Fall ‘225.0.0.1’, keine Verbindung zum Ursprung herstellen können.
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

## Post-Anforderungen
{: #post-requests}
Lesen des Inhalts von einer HTTP POST-Anforderung
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
Erstellen einer HTTP POST-Anforderung von einer Edge-Funktion
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

## Cookie setzen
{: #setting-cookies}
Sie können Cookies mithilfe der CIS-Edge-Funktionen setzen. 
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

## Signierte Anforderungen
{: #signed-requests}
Eine allgemeine URL-Authentifizierungsmethode, die als Anforderung zum Signieren bekannt ist, kann mithilfe der Web Crypto API in einer Edge-Funktion implementiert werden. 

Im hier dargestellten Beispiel, wird der Pfad einer URL zusammen mit einer Zeitmarke für den Ablauf mithilfe eines HMAC (Hash-based Message Authentication Code) und einem SHA-256-Hashalgorithmus authentifiziert. Damit ein Benutzeragent eine authentifizierte Ressource erfolgreich abrufen kann, muss er den korrekten Pfad, die Ablaufzeitmarke und den HMAC über Abfrageparameter angeben. Wenn eines der drei Elemente verfälscht wurde, schlägt die Anforderung fehl. 

Beachten Sie, dass die Authentizität der Ablaufzeitmarke durch HMAC abgedeckt ist, sodass Sie sich auf die Richtigkeit der vom Benutzer bereitgestellten Zeitmarke verlassen können, wenn der HMAC korrekt ist, da diesem das Ablaufdatum der URL bekannt ist. Der Benutzer kann darüber hinaus bestimmen, ob eine URL in seinem Besitz abgelaufen ist oder nicht. 

### Signierte Anforderungen überprüfen
{: #signed-requests-verify}
Dieses Beispiel überprüft den HMAC für eine beliebige Anforderungs-URL, deren Pfadname mit `/verify/` beginnt.

Zur besseren Fehlerbehebung gibt diese Edge-Funktion 403 zurück, wenn die URL oder der HMAC ungültig ist oder wenn die URL abgelaufen ist. Sie möchten möglicherweise in einer tatsächlichen Implementierung 404 zurückgeben. 
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
### Signierte Anforderungen generieren
{: #signed-requests-generate}

Gewöhnlich werden signierte Anforderungen an den Benutzer in einer externen Weise wie beispielsweise per E-Mail übergeben oder sie werden tatsächlich vom Benutzer selbst generiert, wenn dieser über den symmetrischen Schlüssel verfügt. Natürlich können wir auch die signierten Anforderungen in einer Edge-Funktion generieren.

Bei jeder Anforderungs-URL, die mit `/generate/` beginnt, ersetzen wir `/generate/` durch `/verify/`, signieren den daraus resultierenden Pfad mit seiner Zeitmarke und geben die vollständig signierte URL über den Antworthauptteil zurück. 
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

## Streaming von Antworten
{: #streaming-responses}
Ein Edge-Funktionsscript muss seinen gesamten Antworthauptteil nicht vor der Lieferung einer Antwort an `event.respondWith()` erstellen. Mit einem TransformStream ist es möglich, einen Antworthauptteil zu streamen, nachdem der Frontteil der Antwort (z. B. HTTP-Statuszeile und Header) gesendet wurde. Dies ermöglicht die Minimierung von: 

* Der Zeit, die der Besucher wartet, bis der Browser die ersten Daten vom Server empfängt (TTFB Time-To-First-Byte).

* Der Menge an Pufferung, die in den Edge-Funktionsscripts erforderlich ist. 

Das Minimieren der Pufferung ist besonders wichtig, wenn Sie Antworthauptteile verarbeiten oder transformieren müssen, die größer als die Speicherbegrenzung der Edge-Funktion sind. In diesen Fällen ist das Streaming die einzig durchführbare Implementierungsstrategie. 

Der Service der Edge-Funktion von CIS streamt bereits standardmäßig so oft dies möglich ist. Sie müssen diese APIs nur verwenden, wenn Sie den Antworthauptteil auf irgendeine Weise ändern möchten, während das Streamingverhalten beibehalten wird. Wenn Ihr Edge-Funktionsscript nur untergeordnete Anforderungsantworten wortgetreu an den Client zurückgibt, ohne deren Hauptteile zu lesen, dann ist die zugehörige Handhabung von Hauptteilen bereits optimal. Sie müssen die hier beschriebenen Techniken dann nicht anwenden.
{:note}

### Durchgriff streamen 
{: #streaming-responses-pass-through}

Es folgt als Einstieg ein sehr einfaches Beispiel für einen Durchgriff: 
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
Bitte beachten Sie hierbei einige wichtige Details: 

* Obwohl `streamBody()` eine asynchrone Funktion ist, `erwarten` wir sie nicht, damit sie nicht den Verarbeitungsfortschritt der aufrufenden Funktion `fetchAndStream()` blockiert. Sie wird so lange weiter asynchron ausgeführt, solange eine Operation wie `reader.read()` oder `writer.write()` aussteht. 

* Rückstau: Wir `erwarten` die Leseoperation vor dem Aufrufen der Schreiboperation. Ebenso `erwarten` wir die Schreiboperation vor dem Aufruf der nächsten Leseoperation. Das Befolgen dieses Musters gibt den Rückstau an den Ursprung weiter. 

* Abschluss: Wir rufen am Ende `writer.close()` auf und signalisieren so der Laufzeit der Edge-Funktion, dass wir diesen Antworthauptteil vollständig geschrieben haben. Sofort nach dem Aufruf wird `streamBody()` beendet. Wenn dies nicht erwünscht ist, übergeben Sie das zugehörige zurückgegeben Promise an `FetchEvent.waitUntil()`. Wenn Ihr Script `writer.close()` niemals aufruft, erscheint der Hauptteil für die Laufzeit abgeschnitten, obwohl er möglicherweise wie beabsichtigt funktioniert. 

### Mehrere Anforderungen zusammenfassen und streamen
{: #streaming-responses-aggregate-and-stream-multiple-requests}

Dies ist mit der Anleitung für das Zusammenfassen mehrerer Anforderungen vergleichbar. Aber in diesem Fall beginnen wir mit dem Schreiben der Antwort, sobald wir überprüft haben, dass keine nachfolgende Unteranforderung auf die tatsächlichen Antworthauptteile warten muss. 
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
Auch hier sind einige wichtige Details zu beachten:

* Die Laufzeit erwartet den Empfang von TypedArrays auf der lesbaren Seite des TransformStreams. Daher übergeben wir niemals eine Zeichenfolge an `writer.write()`, sondern nur an Uint8Arrays. Wenn Sie eine Zeichenfolge schreiben müssen, verwenden Sie einen TextEncoder.

* `manualPipeTo()` wurde so benannt, weil `ReadableStream.pipeTo()` noch nicht in den CIS Edge-Funktionen implementiert ist, wie in diesem Schreiben dargestellt. Wenn die Verfügbarkeit gegeben ist, wird dies die idiomatischere und bessere Möglichkeit sein, um Bytes von einem ReadableStream in einen WritableStream weiterzuleiten.
