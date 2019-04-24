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

# Casos de uso do Edge Functions (Beta)
{:#edge-functions-use-cases-beta-}

ESSE SOFTWARE É FORNECIDO PELA IBM “NO ESTADO EM QUE SE ENCONTRA”, QUE RENUNCIA SUA RESPONSABILIDADE POR QUAISQUER GARANTIAS EXPRESSAS OU IMPLÍCITAS, INCLUINDO, MAS A ELAS NÃO SE LIMITANDO, GARANTIAS IMPLÍCITAS DE COMERCIALIZAÇÃO E ADEQUAÇÃO A UMA FINALIDADE ESPECÍFICA. EM NENHUM CASO A IBM SERÁ RESPONSÁVEL POR QUAISQUER DANOS DIRETOS, INDIRETOS, INCIDENTAIS, ESPECIAIS, EXEMPLARES OU CONSEQUENCIAIS (INCLUINDO, MAS NÃO SE LIMITANDO A, AQUISIÇÃO DE BENS OU SERVIÇOS SUBSTITUTOS, PERDA DE USO, DADOS OU LUCROS OU INTERRUPÇÃO DE NEGÓCIOS) INDEPENDENTEMENTE DE CAUSA E DE QUALQUER TEORIA DE RESPONSABILIDADE, SEJA EM CONTRATO, RESPONSABILIDADE ESTRITA OU ATO ILÍCITO (INCLUINDO NEGLIGÊNCIA OU OUTRO) DECORRENTE DE QUALQUER FORMA DO USO DESSE SOFTWARE, MESMO SE AVISADA DA POSSIBILIDADE DE TAIS DANOS.

## Teste A/B
{: #ab-testing}
É possível criar um CIS Edge Function para controlar testes A/B.
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

  // We'll prefix the request path with the experiment name. Desta forma,
  // o servidor de origem simplesmente tem de ter duas cópias do site sob
  // diretórios de nível superior denominados "control" e "test".
  let url = new URL(request.url)
  // Note that `url.pathname` always begins with a `/`, so we don't
  // need to explicitly add one after `${group}`.
  url.pathname = `/${group}${url.pathname}`

  const modifiedRequest = new Request (url, {
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
    // Retornar resposta não modificada.
    return response
  }
}

```

## Incluindo um cabeçalho de resposta
{: #add-response-header}
Para modificar os cabeçalhos de resposta, primeiro será necessário fazer uma cópia da resposta para torná-la mutável. Em seguida, será possível usar a interface Cabeçalhos para incluir, mudar ou remover cabeçalhos.
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

## Agregando diversas solicitações
{: #aggregate-multiple-requests}
Aqui, fazemos diversas solicitações para diferentes terminais de API, agregamos as respostas e as enviamos de volta como uma resposta única.
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

    const btc = aguardar btcResp.json ()
    const eth = aguardar ethResp.json ()
    const ltc = aguardar ltcResp.json ()

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

## Roteamento condicional
{: #conditional-routing}
A maneira mais fácil de entregar conteúdos diferentes com base no dispositivo sendo usado é regravar a URL da solicitação com base na condição desejada. Por exemplo:

### Tipo de Dispositivo
{: #conditional-routing-device-type}

```
addEventListener('fetch', event => {
  event.respondWith(fetchAndApply(event.request))
})

async function fetchAndApply(request) {
  let uaSuffix = ''

  const ua = request.headers.get ('user-agent')
  if (ua.match (/iphone/i) | | ua.match (/ipod/i)) {
    uaSuffix = '/mobile'
  } else if (ua.match(/ipad/i)) {
    uaSuffix = '/tablet'
  }

  return fetch(request.url + uaSuffix, request)
}
```
### Cabeçalhos customizados
{: #conditional-routing-custom-headers}

```
addEventListener('fetch', event => {
  event.respondWith(fetchAndApply(event.request))
})

async function fetchAndApply(request) {
  sufixo let = ''
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

## Proteção de hot-link
{: #hot-link-protection}
É possível usar o CIS Edge Functions para proteger seus hot-links em suas propriedades da web.
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
  let referer = request.headers.get ('Referer ')
  let contentType = response.headers.get ('Content-Type ') | | ''
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

## Respostas sem origem
{: #originless-responses}
É possível retornar respostas diretamente da borda. Não há necessidade de atingir sua origem.

### Ignorar solicitações de POST e PUT de HTTP
{: #originless-responses-ignore-post-put-http-requests}

Ignorar solicitações de POST e PUT de HTTP. Esse fragmento permite que todas as outras solicitações sejam transmitidas à origem.
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
### Negar uma aranha ou crawler
{: #originless-responses-deny-spider-crawler}

Proteja sua origem contra aranhas ou crawlers indesejados. Nesse caso, se o agente do usuário for "annoying-robot", a função de borda retornará a resposta em vez de enviar a solicitação à origem.
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
### Evitar a conexão de um IP específico
{: #originless-responses-prevent-specific-ip-connection}

Insira endereços IP na lista de bloqueio. Esse fragmento de código evita que um IP específico, nesse caso, '225.0.0.1', se conecte à origem.
```
addEventListener('fetch', event => {
  event.respondWith(fetchAndApply(event.request))
})

async function fetchAndApply(request) {
  if (request.headers.get ('cf-conectando-ip') == = '225.0.0.1') {
    return new Response('Sorry, this page is not available.',
        { status: 403, statusText: 'Forbidden' })
  }

  return fetch(request)
}
```

## Solicitações de Post
{: #post-requests}
Lendo conteúdos de uma solicitação de POST de HTTP
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
Criando uma solicitação de POST de HTTP por meio de uma função de borda
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
    método: 'POST',
    Cabeçalhos: cabeçalhos,
    corpo: conteúdo
  } resposta const = aguardar busca ('https: //example.com', init)
  console.log ('Obtido resposta', resposta)
  resposta de retorno
}
```

## Configurando um cookie
{: #setting-cookies}
É possível configurar cookies usando o CIS Edge Functions.
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

## Solicitações assinadas
{: #signed-requests}
Um método de autenticação de URL comum, conhecido como assinatura de solicitação, pode ser implementado em uma função de borda com a ajuda da API do Web Crypto.

No exemplo apresentado aqui, vamos autenticar o caminho de uma URL com um registro de data e hora de expiração que o acompanhará, usando um Código de Autenticação de Mensagem Baseado em Hash (HMAC) com um algoritmo digest SHA-256. Para que um agente do usuário busque com sucesso um recurso autenticado, ele precisará fornecer o caminho correto, o registro de data e hora de expiração e o HMAC por meio de parâmetros de consulta e, se algum desses três estiver corrompido, a solicitação falhará.

Observe que a autenticidade do registro de data e hora de expiração é coberta pelo HMAC, portanto, podemos confiar que o registro de data e hora fornecido pelo usuário estará correto se o HMAC estiver correto e, assim, saberemos quando a URL expirará. Além disso, o usuário também pode determinar se uma URL em sua posse expirou ou não.

### Verificando solicitações assinadas
{: #signed-requests-verify}
Este exemplo verifica o HMAC para qualquer URL de solicitação cujo nome do caminho começa com `/verify/`.

Para fins de conveniência de depuração, essa função de borda retornará 403 se a URL ou o HMAC for inválido ou se a URL expirou. É possível que você deseje retornar 404 em uma implementação real.
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

  // O MAC recebido é codificado em Base64-encoded, portanto, temos de ir a algum problema para
  // obtenha-o em um tipo de buffer que crypto.subtle.verify () possa ler.
  const receivedMacBase64 = url.searchParams.get("mac")
  const receivedMac = byteStringToUint8Array(atob(receivedMacBase64))

  // Use crypto.subtle.verify () para proteger contra ataques de sincronização. Since HMACs use
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
função byteStringToUint8Array (byteString) {
  const ui = new Uint8Array(byteString.length)
  for (let i = 0; i < byteString.length; ++i) {
    ui[i] = byteString.charCodeAt(i)
  }
  return ui
}
```
### Gerando solicitações assinadas
{: #signed-requests-generate}

Geralmente, a solicitação assinada seria entregue ao usuário de alguma forma fora da banda, como por e-mail, ou realmente gerada pelo próprio usuário se ele também possuísse a chave simétrica. É possível, naturalmente, também gerar as solicitações assinadas em uma função de borda.

Para qualquer URL de solicitação que comece com `/generate/`, substituiremos `/generate/` por `/verify/`, assinaremos o caminho resultante com seu registro de data e hora e retornaremos a URL completa e assinada por meio do corpo de resposta.
```
addEventListener('fetch', event => {
  url const = new URL(event.request.url)
  prefixo const = "/generate/"
  if (url.pathname.startsWith (prefix)) {
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

## Transmitindo respostas
{: #streaming-responses}
Um script de função de borda não precisa preparar seu corpo de resposta inteiro antes de entregar uma resposta a `event.respondWith()`. Usando um TransformStream, é possível transmitir um corpo de resposta depois de enviar a matéria frontal da resposta (ou seja, a linha de status HTTP e os cabeçalhos). Isto permite-nos minimizar:

* O time-to-first-byte do visitante.

* A quantidade de armazenamento em buffer que deve ser realizada no script de função de borda.

Minimizar o armazenamento em buffer é especialmente importante caso seja necessário processar ou transformar corpos de resposta maiores que o limite de memória da função de borda. Nesses casos, a transmissão é a única estratégia de implementação viável.

O serviço CIS Edge Function já realiza transmissões por padrão sempre que possível. Você só precisa usar essas APIs se desejar modificar o corpo de resposta de alguma maneira, enquanto mantém o comportamento de fluxo. Se seu script de função de borda apenas transmite respostas de subsolicitação de volta para o cliente textualmente sem ler seus corpos, sua manipulação de corpo já é ideal e não há necessidade das técnicas descritas aqui.
{:note}

### Passagem da transmissão
{: #streaming-responses-pass-through}

Para começar, consulte um exemplo de passagem mínima a seguir:
```
addEventListener ("fetch", evento = >{
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

  // ... e entregar nossa resposta enquanto isso estiver em execução.
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
Há alguns detalhes importantes para observar:

* Embora `streamBody()` seja uma função assíncrona, não `aguardamos` por ela para que ela não bloqueie o progresso do encaminhamento da função de chamada `fetchAndStream()`. Ela continuará a ser executada de forma assíncrona, desde que tenha uma operação `reader.read()` ou `writer.write()` pendente.

* Contrapressão: `aguardamos` a operação de leitura antes de chamar a operação de gravação. Da mesma forma, `aguardamos` a operação de gravação antes de chamar a próxima operação de leitura. Seguir esse padrão propaga a contrapressão para a origem.

* Conclusão: chamamos `writer.close()` ao final, que sinaliza para o tempo de execução do Edge Function que concluímos completamente a gravação desse corpo de resposta. Uma vez chamado, `streamBody()` será finalizado e, caso isso não seja desejável, passe sua promessa retornada para `FetchEvent.waitUntil()`. Se seu script nunca chamar `writer.close()`, o corpo aparecerá truncado para o tempo de execução, embora possa continuar a funcionar conforme desejado.

### Agregar e transmitir diversas solicitações
{: #streaming-responses-aggregate-and-stream-multiple-requests}

É semelhante à nossa receita de Agregar diversas solicitações, mas, nesse caso, começaremos a gravar nossa resposta assim que verificarmos que cada subsolicitação foi bem-sucedida, não sendo necessário esperar pelos corpos de resposta reais.
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
    cabeçalhos: { "Authorization": "XXXXXX" }
  }
  fetches const = [
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

  // Crie um canal e fluxo os corpos de resposta para fora
  // como uma matriz JSON.
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

  para (let i = 0; i < bodies.length; + + i) {
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
Novamente, há dois detalhes importantes a serem observados:

* O tempo de execução espera receber TypedArrays no lado legível de TransformStream. Portanto, nunca transmitimos uma sequência para `writer.write()`, somente para Uint8Arrays. Se precisar gravar uma sequência, use um TextEncoder.

* `manualPipeTo()` tem esse nome porque `ReadableStream.pipeTo()` ainda não foi implementado no CIS Edge Functions, desde essa gravação. Quando se tornar disponível, será a maneira mais idiomática e ideal de extrair bytes de um ReadableStream para um WritableStream.
