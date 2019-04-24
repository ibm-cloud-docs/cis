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

# Casos de uso de Edge Functions (Beta)
{:#edge-functions-use-cases-beta-}

ESTE SOFTWARE LO PROPORCIONA IBM “TAL CUAL” Y SE RECHAZA CUALQUIER GARANTÍA EXPLÍCITA O IMPLÍCITA, INCLUYENDO (PERO SIN LIMITACIÓN A), LAS GARANTÍAS DE COMERCIABILIDAD E IDONEIDAD PARA UN FIN CONCRETO. BAJO NINGUNA CIRCUNSTANCIA IBM SERÁ RESPONSABLE DE NINGÚN DAÑO DIRECTO, INDIRECTO, INCIDENTAL, ESPECIAL, EJEMPLAR O CONSECUENTE (INCLUYENDO, PERO SIN LIMITACIÓN A LA ADQUISICIÓN DE PRODUCTOS O SERVICIOS DE SUSTITUCIÓN, LA PÉRDIDA DE USO, DATOS O BENEFICIOS O LA INTERRUPCIÓN DEL NEGOCIO), PROVOCADOS DE CUALQUIER MODO Y DE ACUERDO CON CUALQUIER TEORÍA JURÍDICA, TANTO POR CONTRATO, COMO POR RESPONSABILIDAD EXCLUSIVA O AGRAVIO, (INCLUYENDO LA NEGLIGENCIA Y SIMILARES) QUE SE PUDIERAN DERIVAR DEL USO DE ESTE SOFTWARE, INCLUSO SI SE AVISASE DE ANTEMANO DE LA POSIBILIDAD DE DICHO DAÑO.

## Pruebas A/B
{: #ab-testing}
Puede crear una función Edge de CIS para controlar las pruebas A/B.
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

## Añadir una cabecera de respuesta
{: #add-response-header}
Para modificar las cabeceras de respuesta, primero tiene que hacer una copia de la respuesta para hacerla mutable. A continuación, puede utilizar la interfaz Cabeceras para añadir, cambiar o eliminar cabeceras.
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

## Agregar varias solicitudes
{: #aggregate-multiple-requests}
En esta sección, se realizan diversas solicitudes de distintos puntos finales de API, se agregan las respuestas y se devuelven como una única respuesta.
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

## Direccionamiento condicional
{: #conditional-routing}
La forma más fácil de entregar un contenido diferente basado en el dispositivo que se utiliza es volver a escribir el URL de la solicitud basándose en la condición que le interesa. Por ejemplo:

### Tipo de dispositivo
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
### Cabeceras personalizadas
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

## Protección de enlaces dinámicos
{: #hot-link-protection}
Puede utilizar CIS Edge Functions para proteger los enlaces dinámicos de las propiedades de la web.
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

## Respuestas sin origen
{: #originless-responses}
Puede devolver respuestas directamente desde el servidor edge. No es necesario acceder a su origen.

### Ignorar las solicitudes HTTP POST y PUT
{: #originless-responses-ignore-post-put-http-requests}

Ignorar las solicitudes HTTP POST y PUT. Este fragmento de código permite que todas las demás solicitudes pasen a través del origen.
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
### Denegar una araña o un rastreador web
{: #originless-responses-deny-spider-crawler}

Proteja su origen de las arañas o rastreadores no deseados. En este caso, si el agente de usuario es “annoying-robot”, la función edge devuelve la respuesta en lugar de enviar la solicitud a su origen.
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
### Impedir la conexión a una IP específica
{: #originless-responses-prevent-specific-ip-connection}

Direcciones IP de lista negra. Este fragmento de código impide que una IP específica, en este caso ‘225.0.0.1’, se conecte al origen.
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

## Solicitudes POST
{: #post-requests}
Leer el contenido de una solicitud HTTP POST
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
Crear una solicitud HTTP POST a partir de una función edge
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

## Establecer una cookie
{: #setting-cookies}
Puede establecer cookies utilizando CIS Edge Functions.
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

## Solicitudes firmadas
{: #signed-requests}
Se puede implementar un método frecuente de autenticación de URL conocido como firma de solicitud en una función edge con la Web Crypto API.

En el ejemplo que se presenta aquí, autenticaremos la vía de acceso de un URL, junto con una indicación de fecha y hora de caducidad, utilizando un código de autenticación de mensajes basado en hash (HMAC) con un algoritmo de resumen SHA-256. Para que un agente de usuario pueda captar correctamente un recurso autenticado, tendrá que proporcionar la vía de acceso correcta, la indicación de fecha y hora de caducidad y el HMAC a través de los parámetros de consulta — si alguno de estos tres se ha manipulado indebidamente, la solicitud fallará.

Tenga en cuenta que la autenticidad de la indicación de fecha y hora de caducidad la cubre el HMAC, por lo que podemos confiar en que la indicación de fecha y hora proporcionada por el usuario será correcta si el HMAC es correcto y, por lo tanto, saber cuándo vence el URL. Ademas, el usuario también puede determinar si un URL de su posesión ha expirado o no.

### Verificación de las solicitudes firmadas
{: #signed-requests-verify}
En este ejemplo se verifica el HMAC de cualquier URL de solicitud cuyo nombre de vía de acceso empiece por `/verify/`.

Para fines de depuración, esta función edge devuelve 403 si el URL o el HMAC no es válido, o si el URL ha caducado. Puede que desee devolver 404 en una implementación real.
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
### Generación de solicitudes firmadas
{: #signed-requests-generate}

Generalmente, la solicitud firmada se entregaría al usuario en alguna forma fuera de banda, como por ejemplo por correo electrónico, o la generaría el propio usuario si también posee la clave simétrica. Por supuesto, también podemos generar las solicitudes firmadas en una función edge.

Por cada URL de solicitud que empiece por `/generate/`, sustituiremos `/generate/` por `/verify/`, firmaremos la vía de acceso resultante con su indicación de fecha y hora y devolveremos el URL firmado a través del cuerpo de respuesta.
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

## Respuestas en streaming
{: #streaming-responses}
Un script de función edge no necesita preparar todo el cuerpo de la respuesta antes de entregar una respuesta a `event.respondWith()`. Utilizando una TransformStream, es posible transmitir un cuerpo de respuesta después de enviar el tema inicial de la respuesta (es decir, la línea de estado HTTP y las cabeceras). Esto nos permite minimizar:

* El time-to-first-byte del visitante.

* La cantidad de almacenamiento intermedio que se debe realizar en el script de función edge.

Es especialmente importante minimizar el almacenamiento intermedio si procesa o transforma cuerpos de respuesta más grandes que el límite de memoria de la función edge. En estos casos, el streaming es la única estrategia de aplicación viable.

El servicio CIS Edge Function ya envía por streaming de forma predeterminada siempre que es posible. Sólo tiene que utilizar estas API si desea modificar el cuerpo de la respuesta de alguna forma, al tiempo que mantiene el comportamiento de streaming. Si el script de función edge sólo pasa respuestas de subsolicitud al verbatim del cliente, sin leer sus cuerpos, entonces su manejo de cuerpo ya es óptimo, y no hay necesidad de las técnicas descritas aquí.
{:note}

### Paso a través de streaming
{: #streaming-responses-pass-through}

A continuación se muestra un ejemplo de paso a través mínimo para empezar:
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
Hay algunos detalles importantes a tener en cuenta:

* Aunque `streamBody()` es una función asíncrona, no la esperamos (`await`), por lo que no bloquea el avance de la función de llamada `fetchAndStream()`. Seguirá ejecutándose de forma asíncrona siempre y cuando tenga una operación pendiente `reader.read()` o `writer.write()`.

* Resistencia: Sí que esperamos (`await`) a la operación de lectura antes de llamar a la operación de escritura. Del mismo modo, esperamos (`await`)a la operación de escritura antes de llamar a la siguiente operación de lectura. Al seguir este patrón, se propaga la resistencia hacia el origen.

* Finalización: al final, llamamos a `writer.close()`, lo que indica al tiempo de ejecución de la función edge que ya hemos terminado completamente de escribir este cuerpo de respuesta. Una vez llamado, `streamBody()` finalizará — si esto no es lo que desea, pase la promesa que ha devuelto a `FetchEvent.waitUntil()`. Si el script nunca llama a `writer.close()`, el cuerpo aparecerá truncado en base al tiempo de ejecución, aunque puede seguir funcionando normalmente.

### Agregar y enviar por streaming varias solicitudes
{: #streaming-responses-aggregate-and-stream-multiple-requests}

Esto es similar a nuestra receta para Agregar varias solicitudes, pero esta vez comenzaremos a escribir nuestra respuesta tan pronto como hayamos verificado que cada subsolicitud ha tenido éxito — no es necesario esperar los cuerpos de respuesta.
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
De nuevo, hay un par de detalles importantes que señalar:

* El tiempo de ejecución espera recibir TypedArrays en el lado legible de TransformStream. Por lo tanto, nunca pasamos una serie a `writer.write()`, sólo Uint8Arrays. Si tiene que escribir una serie, utilice un TextEncoder.

* `manualPipeTo()` se llama así porque `ReadableStream.pipeTo()` aún no está implementado en CIS Edge Functions, en el momento que se está redactando este texto. Cuando esté disponible, será la forma más idiomática y óptima de bombear bytes de una ReadableStream a una WritableStream.
