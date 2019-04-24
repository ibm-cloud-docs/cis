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

# Cas d'utilisation des fonctions Edge (bêta) 
{:#edge-functions-use-cases-beta-}

CE LOGICIEL EST FOURNI PAR IBM "TEL QUEL" ET TOUTE GARANTIE EXPLICITE OU IMPLICITE, Y COMPRIS, ET DE FAÇON NON LIMITATIVE, TOUTE GARANTIE IMPLICITE D'APTITUDE A L'EXECUTION D'UN TRAVAIL DONNE EST DÉCLINÉE. EN AUCUN CAS, IBM NE POURRA ÊTRE TENU RESPONSABLE DE TOUT DOMMAGE DIRECT, INDIRECT, ACCESSOIRE, SPÉCIAL, EXEMPLAIRE OU CONSÉCUTIF (Y COMPRIS, ET DE FAÇON NON LIMITATIVE, L'ACHAT DE MARCHANDISES OU DE SERVICES SUBSTITUTIFS ; LA PERTE D'UTILISATION, DE DONNÉES OU DE BESOINS ; OU L'INTERRUPTION D'ACTIVITE) CAUSÉ ET DE TOUTE THÉORIE DE LA RESPONSABILITÉ, QU'IL S'AGISSE DE RESPONSABILITE CONTRACTUELLE, RESPONSABILITÉ STRICTE OU RESPONSABILITÉ POUR INFRACTION (INCLUANT LA NÉGLIGENCE OU AUTRE) DÉCOULANT DE L'UTILISATION DE CE LOGICIEL, MÊME SI AVISÉ DE LA POSSIBILITE DE CE DOMMAGE. 

## Tests A/B
{: #ab-testing}
Vous pouvez créer une fonction Edge CIS pour contrôler les tests A/B. 
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

## Ajout d'un en-tête de réponse  
{: #add-response-header}
Pour modifier les en-têtes de réponse, vous devez d’abord faire une copie de la réponse afin de la rendre modifiable. Vous pouvez ensuite utiliser l'interface En-têtes pour ajouter, modifier ou supprimer des en-têtes. 
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

## Agrégation de plusieurs demandes 
{: #aggregate-multiple-requests}
Ici, nous adressons plusieurs demandes à différents noeuds finaux d'API, agrégeons les réponses et les renvoyons dans une réponse unique. 
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

## Routage conditionnel
{: #conditional-routing}
Le moyen le plus simple de fournir différents contenus en fonction du périphérique utilisé est de réécrire l'URL de la demande en fonction de la condition qui est importante pour vous. Exemple :

### Type de terminal
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
### En-têtes personnalisés
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

## Protection des liens dynamiques
{: #hot-link-protection}
Vous pouvez utiliser des fonctions Edge CIS pour protéger vos liens dynamiques sur vos propriétés Web. 
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

## Réponses sans origine 
{: #originless-responses}
Vous pouvez renvoyer les réponses directement à partir du bord (Edge). Il est inutile de trouver votre origine.

### Ignorer les demandes HTTP POST et PUT 
{: #originless-responses-ignore-post-put-http-requests}

Ignorez les demandes HTTP POST et PUT. Ce fragment de code permet à toutes les autres demandes de traverser à l'origine. 
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
### Refuser un moteur de balayage ou un moteur d'exploration
{: #originless-responses-deny-spider-crawler}

Protégez votre origine des moteurs de balayage ou d'exploration indésirables. Dans ce cas, si l'agent utilisateur est un "annoying_robot", la fonction Edge renvoie la réponse au lieu d'envoyer la demande à l'origine. 
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
### Empêcher une adresse IP spécifique de se connecter 
{: #originless-responses-prevent-specific-ip-connection}

Liste noire des adresses IP. Ce fragment de code empêche une adresse IP spécifique, dans le cas présent "225.0.0.1" de se connecter à l'origine. 
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

## Demandes POST
{: #post-requests}
Lecture du contenu d'une demande POST HTTP 
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
Création d'une requête POST HTTP à partir d'une fonction Edge
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

## Définition d'un cookie 
{: #setting-cookies}
Vous pouvez définir des cookies à l'aide des fonctions Edge CIS. 
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

## Demandes signées
{: #signed-requests}
Une méthode d'authentification d'URL commune appelée signature de requête peut être implémentée dans une fonction Edge à l'aide de l'API Crypto Web. 

Dans l’exemple présenté ici, nous authentifierons le chemin d’une URL, ainsi que l’horodatage d’expiration correspondant, à l’aide d’un code HMAC (Hash-based Message Authentication Code) avec un algorithme de synthèse SHA-256. Pour qu'un agent utilisateur puisse extraire une ressource authentifiée, il doit fournir le chemin correct, l'horodatage d'expiration et le code HMAC via des paramètres de requête. Si l'un des trois est altéré, la demande échouera. 

Notez que l'authenticité de l'horodatage d'expiration est couverte par le code HMAC. Par conséquent, nous pouvons penser que l'horodatage fourni par l'utilisateur est correct si le code HMAC est correct et ainsi connaître le délai d'expiration de l'URL. De plus, l'utilisateur peut également déterminer si une URL en sa possession a expiré ou non. 

### Vérification des demandes signées 
{: #signed-requests-verify}
Cet exemple vérifie le code HMAC pour toute URL de demande dont le nom de chemin commence par `/verify/`.

Pour faciliter le débogage, cette fonction Edge renvoie 403 si l'URL ou le code HMAC n'est pas valide ou si l'URL est arrivée à expiration. Vous souhaiterez peut-être renvoyer le 404 dans une implémentation réelle. 
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
### Génération de demandes signées 
{: #signed-requests-generate}

En règle générale, la demande signée est transmise à l'utilisateur en externe, par exemple par courrier électronique, ou est générée par l'utilisateur lui-même s'il possède également la clé symétrique. Bien entendu, nous pouvons également générer les requêtes signées dans une fonction Edge. 

Pour toute URL de requête commençant par `/generate/`, nous allons remplacer `/generate/` par `/verify/`, signer le chemin obtenu avec son horodatage et renvoyer l'URL complète signée dans le corps de la réponse.
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

## Réponses en continu  
{: #streaming-responses}
Un script de fonction Edge n’a pas besoin de préparer tout le corps de la réponse avant d’envoyer une réponse à `event.respondWith()`. En utilisant TransformStream, il est possible de diffuser un corps de réponse après l’envoi de son sujet principal (à savoir, la ligne d’état HTTP et les en-têtes). Cela nous permet de minimiser : 

* Temps du visiteur jusqu'au premier octet 

* Quantité de mise en mémoire tampon qui doit être effectuée dans le script de la fonction Edge. 

Réduire la mise en mémoire tampon est particulièrement important si vous devez traiter ou transformer des corps de réponse supérieurs à la limite de mémoire de la fonction Edge. Dans ces cas, la diffusion en continu est la seule stratégie de mise en oeuvre réalisable. 

Le service CIS Edge Function est déjà diffusé par défaut dans la mesure du possible. Vous ne devez utiliser ces API que si vous souhaitez modifier le corps de la réponse d'une manière ou d'une autre, tout en conservant le comportement de diffusion. Si votre script de fonction Edge transmet uniquement les réponses des sous-demandes au verbatim client, sans lire le corps des réponses, la manipulation est déjà optimale et les techniques décrites ici ne sont plus nécessaires.
 {:note}

### Passe-système en continu
{: #streaming-responses-pass-through}

Voici un exemple de passe-système minimal pour commencer :
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
D'importants détails doivent être pris en compte : 

* Si `streamBody()` est une fonction asynchrone, nous ne `l'attendons` pas, afin qu'elle ne bloque pas la progression de la fonction appelante `fetchAndStream()`. Elle continuera à s'exécuter de manière asynchrone tant qu'elle comportera une opération `reader.read()` ou `writer.write()` en suspens.

* Contre-pression : nous `attendons` l’opération de lecture avant d’appeler l’opération d’écriture. De même, nous `attendons` l’opération d’écriture avant d'appeler la prochaine opération de lecture. Ce masque propage la contre-pression à l'origine.

* Achèvement : nous appelons `writer.close()` à la fin, ce qui indique au moteur d’exécution de la fonction Edge que nous avons complètement terminé l’écriture de ce corps de réponse. Une fois appelé, `streamBody()` s'arrête - si cela n'est pas souhaitable, transmettez sa promesse renvoyée à `FetchEvent.waitUntil()`. Si votre script n'appelle jamais `writer.close()`, le corps apparaît tronqué au moment de l'exécution, mais il peut continuer à fonctionner comme prévu.

### Agrégation et diffusion de plusieurs demandes 
{: #streaming-responses-aggregate-and-stream-multiple-requests}

Cette méthode est similaire à notre recette Agrégation de plusieurs demandes, mais cette fois, nous commencerons à écrire notre réponse dès que nous aurons vérifié que chaque sous-demande a abouti - inutile d’attendre le corps de la réponse. 
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
Là encore, d'importants détails doivent être pris en compte : 

* Le moteur d'exécution s'attend à recevoir TypedArrays du côté lisible du TransformStream. Par conséquent, nous ne transmettons jamais de chaîne à `writer.write()`, uniquement Uint8Arrays. Si vous devez écrire une chaîne, utilisez un TextEncoder. 

* La fonction `manualPipeTo()` est nommée ainsi parce que `ReadableStream.pipeTo()` n’est pas encore implémentée dans les Fonctions Edge CIS, à ce jour. Lorsque cette fonction sera disponible, elle sera le moyen le plus idiomatique et optimal de transmettre des octets d'un ReadableStream vers un WritableStream. 
