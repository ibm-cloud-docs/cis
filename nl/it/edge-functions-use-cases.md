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

# Casi di utilizzo delle funzioni edge (Beta)
{:#edge-functions-use-cases-beta-}

QUESTO SOFTWARE VIENE FORNITO DA IBM NELLO STATO IN CUI SI TROVA E NON VIENE FORNITA ALCUNA GARANZIA, ESPRESSA O IMPLICITA, INCLUSE A TITOLO ESEMPLIFICATIVO, GARANZIE IMPLICITE DI COMMERCIABILITÀ E IDONEITÀ PER UNO SCOPO SPECIFICO. IN NESSUN CASO IBM SARÀ RESPONSABILE PER EVENTUALI DANNI DIRETTI, INDIRETTI, INCIDENTALI, SPECIALI, ESEMPLARI O CONSEQUENZIALI (INCLUSI, A TITOLO ESEMPLIFICATIVO MA NON ESAUSTIVO, L'ACQUISTO DI BENI O SERVIZI SOSTITUTIVI; PERDITA DI DATI, USO O PROFITTI; O INTERRUZIONE DELL'ATTIVITÀ) A PRESCINDERE DALLA CAUSA E IN BASE A QUALSIASI TEORIA DI RESPONSABILITÀ, PER CONTRATTO, RESPONSABILITÀ OGGETTIVA O TORTO (COMPRESA LA NEGLIGENZA O ALTRO) INSORGENTE IN QUALSIASI MODO DALL'USO DI QUESTO SOFTWARE, ANCHE NEL CASO IN CUI FOSSERO STATI PREVENTIVAMENTE INFORMATI DI TALE DANNO. 

## Test A/B
{: #ab-testing}
Puoi creare una funzione edge CIS per controllare i test A/B.
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

## Aggiunta di un'intestazione della risposta
{: #add-response-header}
Per modificare le intestazioni delle risposte, devi innanzitutto creare una copia della risposta per poterla rendere mutabile. Poi puoi utilizzare l'interfaccia Headers per aggiungere, modificare o rimuovere le intestazioni. 
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

## Aggregazione di più richieste
{: #aggregate-multiple-requests}
Di seguito, eseguiamo più richieste a endpoint API diversi, aggreghiamo le risposte e le rimandiamo indietro come una singola risposta. 
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

## Instradamento condizionale
{: #conditional-routing}
Il modo più semplice per fornire contenuto diverso in base al dispositivo utilizzato, è quello di riscrivere l'URL della richiesta in base alla condizione che ti interessa. Ad esempio:

### Tipo di dispositivo
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
### Intestazioni personalizzate
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

## Protezione hotlink
{: #hot-link-protection}
Puoi utilizzare le funzioni edge CIS per proteggere i tuoi hotlink nelle tue proprietà web. 
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

## Risposte senza origine
{: #originless-responses}
Puoi restituire le risposte direttamente dall'edge. Non ha bisogno di cercare riscontri nella tua origine. 

### Ignora le richieste HTTP POST e PUT
{: #originless-responses-ignore-post-put-http-requests}

Ignora le richieste HTTP POST e PUT. Questo frammento consente a tutte le altre richieste di passare attraverso l'origine. 
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
### Blocca uno spider o un crawler
{: #originless-responses-deny-spider-crawler}

Proteggi la tua origine da spider o crawler non desiderati. In questo caso, se l'agent utente (user-agent) è “annoying-robot”, la funzione edge restituisce la risposta invece di inviare la richiesta all'origine. 
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
### Impedisci il collegamento di uno specifico IP
{: #originless-responses-prevent-specific-ip-connection}

Inserisci nella blacklist gli indirizzi IP. Questo frammento di codice impedisce a uno specifico IP, in questo caso ‘225.0.0.1’ di collegarsi all'origine. 
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

## Richieste Post
{: #post-requests}
Lettura del contenuto da una richiesta HTTP POST
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
Creazione di una richiesta HTTP POST da una funzione edge
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

## Impostazione di un cookie
{: #setting-cookies}
Puoi impostare i cookie utilizzando le funzioni edge CIS.
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

## Richieste firmate
{: #signed-requests}
Un metodo di autenticazione URL comune noto come firma della richiesta può essere implementato in una funzione edge con il supporto dell'API Web Crypto.

Nell'esempio qui presentato, autenticheremo il percorso di un URL, insieme ad una data/ora di scadenza di accompagnamento, utilizzando un HMAC (Hash-based Message Authentication Code) con un algoritmo digest SHA-256. Affinché un agent utente richiami correttamente una risorsa autenticata, dovremo fornire il percorso corretto, la data/ora di scadenza e HMAC tramite i parametri di query — se uno qualsiasi di questi elementi è manomesso, la richiesta avrà esito negativo. 

Tieni presente che l'autenticità della data/ora di scadenza è coperta da HMAC, quindi possiamo contare sul fatto che la data/ora fornita dall'utente è corretta se HMAC è corretto e quindi sa quando scade l'URL. Inoltre, l'utente può anche determinare se un URL in suo possesso è scaduto o meno. 

### Verifica delle richieste firmate
{: #signed-requests-verify}
Questo esempio verifica l'HMAC per qualsiasi URL della richiesta il cui nome percorso inizia con `/verify/`.

Per comodità di debug, questa funzione edge restituisce 403 se l'URL o HMAC non è valido oppure se l'URL è scaduto. Potresti voler restituire 404 in un'implementazione reale. 
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
### Generazione delle richieste firmate
{: #signed-requests-generate}

Di norma, la richiesta firmata verrebbe consegnata all'utente in un modo fuori banda, ad esempio email, o generata realmente dall'utente stesso se possiede anche la chiave simmetrica. Possiamo, ovviamente, generare anche le richieste firmate in una funzione edge. 

Per qualsiasi URL della richiesta che inizia con `/generate/`, sostituiremo `/generate/` con `/verify/`, firmeremo il percorso risultante con la sua data/ora e restituiremo l'URL firmato completo tramite il corpo della risposta. 
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

## Risposte in streaming
{: #streaming-responses}
Un script della funzione edge non ha bisogno di preparare l'intero corpo della sua risposta prima di fornire una risposta a `event.respondWith()`. Utilizzando un TransformStream, è possibile inviare in streaming un corpo della risposta dopo aver inviato l'introduzione della risposta (ad esempio, Riga stato HTTP e intestazioni). Ciò ci consente di ridurre: 

* Il TTFB (Time to First Byte) del visitatore. 

* La quantità di buffer dei dati che deve essere eseguita nello script della funzione edge. 

La riduzione del buffer dei dati è particolarmente importante se devi elaborare o trasformare corpi di risposte che superano il limite di memoria della funzione edge. In questi casi, lo streaming è l'unica strategia di implementazione praticabile. 

Il servizio della funzione edge CIS utilizza già lo streaming ovunque possibile, per impostazione predefinita. Devi solo utilizzare queste API se desideri modificare in qualche modo il corpo della risposta mentre mantieni la funzionalità di streaming. Se il tuo script della funzione edge restituisce, parola per parola, le risposte della sottorichiesta al client senza leggerne i corpi, la sua gestione del corpo è già ottimale e non hai bisogno delle tecniche qui descritte.
{:note}

### Pass-Through in streaming
{: #streaming-responses-pass-through}

Di seguito troverai un breve esempio di pass-through per iniziare:
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
Devi tenere presente alcuni dettagli importanti:

* Sebbene `streamBody()` sia una funzione asincrona, noi non la aspettiamo (`await`), quindi non blocca l'avanzamento della funzione `fetchAndStream()` chiamante. Continuerà ad essere eseguita in modo asincrono fino a quando avrà un'operazione `reader.read()` o `writer.write()` in sospeso.

* Contropressione: attendiamo (`await`) l'operazione di lettura prima di richiamare quella di scrittura. Allo stesso modo, attendiamo (`await`) l'operazione di scrittura prima dell'operazione di lettura successiva. Seguendo questo modello, si propaga la contropressione all'origine. 

* Completamento: richiamiamo `writer.close()` alla fine, ciò indica al runtime della funzione edge che abbiamo terminato definitivamente la scrittura di questo corpo della risposta. Una volta richiamato, `streamBody()` terminerà — se non è questo ciò che desideri, passa la promessa restituita a `FetchEvent.waitUntil()`. Se il tuo script non richiama mai `writer.close()`, il corpo apparirà troncato nel runtime, anche se può continuare a funzionare come previsto. 

### Aggrega e invia in streaming più richieste
{: #streaming-responses-aggregate-and-stream-multiple-requests}

È simile alla strategia di Aggregazione di più richieste, ma questa volta inizieremo a scrivere la nostra risposta non appena avremo verificato che ogni sottorichiesta successiva ha avuto esito positivo — non avremo bisogno di attendere i corpi della risposta effettivi. 
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
Di nuovo, devi tenere presente un paio di dettagli importanti: 

* Il runtime prevede di ricevere TypedArrays sul lato leggibile di TransformStream. Quindi, non passiamo mai una stringa a `writer.write()`, solo Uint8Arrays. Se devi scrivere una stringa, utilizza un TextEncoder.

* `manualPipeTo()` è denominato in questo modo perché `ReadableStream.pipeTo()` non è ancora implementato nelle funzioni edge CIS in questo momento. Quando diventerà disponibile, sarà il modo più peculiare e ottimale per immettere i byte da ReadableStream a WritableStream.
