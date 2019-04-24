---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: log pull, logpull, time-based, rayID

subcollection: cis

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Logpull
{:#logpull}

Los clientes de IBM pueden acceder al servicio de Logpull en cuentas de empresa. Este servicio permite a los usuarios consumir registros de solicitud por HTTP utilizando una [CLI](/docs/cis-cli-plugin?topic=cis-cli-plugin-cis-cli-commands#log).

Estos registros contienen datos relacionados con el cliente que se conecta, la vía de acceso de solicitud a través de la red y la respuesta desde el servidor web de origen.


## Casos prácticos
{:#logpull-usecases}

### Basado en RayID
{:#logpull-usecases-rayid}

Si un usuario recibe un mensaje de error después de ejecutar un mandato, puede utilizar el RayID que se proporciona en la cabecera de respuesta para obtener los registros relacionados con el mandato.

Si tiene un RAY_ID con `-XXX` al final, asegúrese de eliminarlo. Por ejemplo, `12ab34cdef567gh8-XXX` pasa a `12ab34cdef567gh8`.
{.note}

**Solicitud**

```
ibmcloud cis logpull DNS_DOMAIN_ID --ray-id RAY_ID
```

**Respuesta**

```
{
    "ClientIP": "68.278.11.89",
    "ClientRequestHost": "testing.logpull.com",
    "ClientRequestMethod": "GET",
    "ClientRequestURI": "/var/www",
    "EdgeEndTimestamp": 1545155129703000000,
    "EdgeResponseBytes": 1935,
    "EdgeResponseStatus": 403,
    "EdgeStartTimestamp": 1545155129696000000,
    "RayID": "48b371889c489b2c"
}
```

### Basado en la duración de tiempo
{:#logpull-usecases-time-duration}

Si un usuario recibe un mensaje de error después de ejecutar un mandato pero no conoce el RayID de la respuesta, en su lugar, puede utilizar una duración de tiempo. Recibirá todos los registros de la zona determinada que se han producido durante la ventana de tiempo alrededor del momento en que se produjo el error, y puede buscar en los resultados.


**Parámetros necesarios**

Hora de inicio y de finalización en forma de indicación de fecha y hora de UNIX (en segundos o nanosegundos) o una indicación de fecha y hora absoluta conforme a RFC 3339, con una duración de tiempo de un minuto o una hora.

**Solicitud**
```
ibmcloud cis logpull DNS_DOMAIN_ID --start 2019-01-02T01:00:00+00:00 --end 2019-01-02T01:00:00+00:00
```
**Respuesta**
```
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/bootstrap-collapse.js","EdgeEndTimestamp":1545067628046000000,"EdgeResponseBytes":2205,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067628044000000,"RayID":"48ab19434891c7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/3d.gif","EdgeEndTimestamp":1545067627970000000,"EdgeResponseBytes":2538446,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067627951000000,"RayID":"48ab1942bf96c7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/logo.gif","EdgeEndTimestamp":1545067628051000000,"EdgeResponseBytes":82257,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067628048000000,"RayID":"48ab194348a0c7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/docs.css","EdgeEndTimestamp":1545067627952000000,"EdgeResponseBytes":540,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067627948000000,"RayID":"48ab1942af8ac7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/bootstrap.css","EdgeEndTimestamp":1545067627952000000,"EdgeResponseBytes":17311,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067627948000000,"RayID":"48ab1942af85c7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/jquery.js","EdgeEndTimestamp":1545067628045000000,"EdgeResponseBytes":33555,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067628042000000,"RayID":"48ab19434882c7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/watson.gif","EdgeEndTimestamp":1545067628052000000,"EdgeResponseBytes":893230,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067628046000000,"RayID":"48ab194348a3c7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/bootstrap-386.js","EdgeEndTimestamp":1545067628046000000,"EdgeResponseBytes":1663,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067628043000000,"RayID":"48ab19434884c7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/Fixedsys500c.woff","EdgeEndTimestamp":1545067630272000000,"EdgeResponseBytes":14055,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067629064000000,"RayID":"48ab1949aca2c7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/bios.gif","EdgeEndTimestamp":1545067628055000000,"EdgeResponseBytes":1121237,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067628046000000,"RayID":"48ab1943489ec7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/bootstrap-modal.js","EdgeEndTimestamp":1545067628046000000,"EdgeResponseBytes":2569,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067628043000000,"RayID":"48ab1943488ac7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/holder.js","EdgeEndTimestamp":1545067628053000000,"EdgeResponseBytes":4593,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067628046000000,"RayID":"48ab19434898c7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/old_school.png","EdgeEndTimestamp":1545067627960000000,"EdgeResponseBytes":1466,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067627952000000,"RayID":"48ab1942bf92c7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com,"ClientRequestMethod":"GET","ClientRequestURI":"/assets/bootstrap-responsive.css","EdgeEndTimestamp":1545067627951000000,"EdgeResponseBytes":4797,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067627948000000,"RayID":"48ab1942af86c7a7"}
```

### Campos
{:#logpull-usecases-fields}

Si no se especifica `fields` en la solicitud, se devuelve un conjunto limitado de campos predeterminados. Puede ver la lista completa de todos los campos disponibles aquí:

**Solicitud**

```
ibmcloud cis logpull DNS_DOMAIN_ID --available-fields
```

Los campos se pasan como una lista separada por comas. Por ejemplo, para tener "ZoneID" y "RayID", utilice:

```
ibmcloud cis logpull DNS_DOMAIN_ID --start 2019-01-02T01:00:00+00:00 --end 2019-01-02T01:00:00+00:00 --fields ZoneId,RayID
```

**Lista de campos**

Campos disponibles actualmente (a partir de diciembre de 2018):
```
"CacheCacheStatus": "serie; unknown | miss | expired | updating | stale | hit | ignored | bypass | revalidated",
"CacheResponseBytes": "entero; número de bytes devueltos por la memoria caché",
"CacheResponseStatus": "entero; código de estado HTTP devuelto por la memoria caché al extremo: todas las solicitudes (incluyendo las que no se pueden almacenar en caché) pasan por la memoria caché: ver también el campo CacheStatus",
"CacheTieredFill": "booleano; se ha utilizado una memoria caché por niveles para servir esta solicitud",
"ClientASN": "entero; número de AS del cliente",
"ClientCountry": "serie; país de la dirección IP del cliente",
"ClientDeviceType": "serie; tipo de dispositivo del cliente",
"ClientIP": "serie; dirección IP del cliente",
"ClientIPClass": "serie; clase de IP del cliente",
"ClientRequestBytes": "entero; número de bytes en la solicitud del cliente",
"ClientRequestHost": "serie; host solicitado por el cliente",
"ClientRequestMethod": "serie; método HTTP de la solicitud del cliente",
"ClientRequestPath": "serie; vía de acceso de URI solicitada por el cliente",
"ClientRequestProtocol": "serie; protocolo HTTP de la solicitud del cliente",
"ClientRequestReferer": "serie; referenciador de la solicitud HTTP",
"ClientRequestURI": "serie; URI solicitado por el cliente",
"ClientRequestUserAgent": "serie; agente de usuario que ha notificado el cliente",
"ClientSSLCipher": "serie; cifrado SSL del cliente",
"ClientSSLProtocol": "serie; protocolo SSL (TLS) del cliente",
"ClientSrcPort": "entero ; puerto de origen del cliente",
"EdgeColoID": "entero ; id de colo de extremo de Cloudflare",
"EdgeEndTimestamp": "entero o serie; marca de tiempo en nanosegundos de unix en que el extremo ha terminado de enviar la respuesta al cliente",
"EdgePathingOp": "serie; indica el tipo de respuesta que se ha emitido para esta solicitud (desconocido = ninguna acción específica)",
"EdgePathingSrc": "serie; detalla cómo se ha clasificado la solicitud según las comprobaciones de seguridad (desconocido = no clasificación específica)", "EdgePathingStatus": "serie; indica los datos que se han utilizado para determinar el manejo de esta solicitud (desconocido = sin datos)",
"EdgeRateLimitAction": "serie; la acción realizada por la regla de bloqueo; vacío si no se ha realizado ninguna acción",
"EdgeRateLimitID": "entero; el ID de regla interno de la regla de limitación de velocidad que ha desencadenado un bloqueo (prohibición) o una acción de simulación. 0 si no se ha realizado ninguna acción",
"EdgeRequestHost": "serie; cabecera de host de la solicitud del extremo al origen",
"EdgeResponseBytes": "entero; número de bytes devueltos por el extremo al cliente",
"EdgeResponseCompressionRatio": "flotante; proporción de compresión de respuestas del extremo",
"EdgeResponseContentType": "serie; valor de cabecera de tipo de contenido de las respuestas del extremo",
"EdgeResponseStatus": "entero; código de estado HTTP devuelto por Cloudflare al cliente",
"EdgeServerIP": "serie; IP del servidor edge que hace una solicitud al origen",
"EdgeStartTimestamp": "entero o serie; indicación de fecha y hora en nanosegundos de unix en que el extremo ha recibido una solicitud del cliente",
"OriginIP": "serie; IP del servidor de origen",
"OriginResponseBytes": "entero; número de bytes devueltos por el servidor de origen",
"OriginResponseHTTPExpires": "serie; valor de la cabecera 'caduca el' del origen en formato RFC1123",
"OriginResponseHTTPLastModified": "serie; valor de la cabecera 'última modificación' del origen en formato RFC1123",
"OriginResponseStatus": "entero; estado devuelto por el servidor de origen",
"OriginResponseTime": "entero; número de nanosegundos que ha tardado el origen en devolver la respuesta al extremo",
"OriginSSLProtocol": "serie; protocolo SSL (TLS) utilizado para conectar con el origen",
"ParentRayID": "serie; ray ID de la solicitud padre si ésta se ha hecho a través de un script de trabajador",
"RayID": "serie; Ray ID de la solicitud",
"SecurityLevel": "serie; el nivel de seguridad configurado en el momento de esta solicitud. Se utiliza para determinar la sensibilidad del sistema de Reputación de IP. ",
"WAFAction": "serie; acción realizada por el WAF, si se ha desencadenado",
"WAFFlags": "serie; indicadores de configuración adicionales: simulate (0x1) | null",
"WAFMatchedVar": "serie; el nombre completo de la variable con la que se ha coincidido más recientemente",
"WAFProfile": "serie; perfil de WAF: low | med | high",
"WAFRuleID": "serie; ID de la regla de WAF aplicada",
"WAFRuleMessage": "serie; mensaje de regla asociado con la regla desencadenada",
"WorkerCPUTime": "entero; cantidad de tiempo en microsegundos dedicado a ejecutar un trabajador, si lo hay",
"WorkerStatus": "serie; estado devuelto por el daemon de trabajador",
"WorkerSubrequest": "booleano; si esta solicitud era o no una subsolicitud de un trabajador",
"WorkerSubrequestCount": "entero; número de subsolicitudes emitidas por un trabajador al manejar esta solicitud",
"ZoneID": "entero; ID de zona interno"
```

### Ejemplo
{:#logpull-usecases-example}
A continuación se muestra un ejemplo de llamada `logpull` y ejemplos de respuestas de tipos específicos.

**Solicitud**
```
ibmcloud cis logpull DNS_DOMAIN_ID --start 2019-01-02T01:00:00+00:00 --end 2019-01-02T01:00:00+00:00 --fields ClientRequestURI,CEdgeResponseBytes,CParentRayID,CWorkerStatus,COriginResponseTime,CEdgeResponseStatus,CWorkerSubrequest,CClientRequestProtocol,CWAFRuleID,CEdgePathingOp,CClientSrcPort,CWorkerSubrequestCount,CEdgeRequestHost,CClientSSLCipher,CEdgePathingSrc,COriginResponseStatus,CClientIPClass,CWAFAction,CEdgeColoID,CClientCountry,CClientRequestHost,CWAFFlags,CClientASN,CEdgeServerIP,CCacheCacheStatus,CSecurityLevel,CClientRequestUserAgent,CCacheResponseBytes,CWAFMatchedVar,CEdgeStartTimestamp,CClientSSLProtocol,CEdgeEndTimestamp,CEdgeResponseContentType,CClientRequestBytes,CCacheResponseStatus,CWorkerCPUTime,CRayID,CClientRequestMethod,CClientIP,CClientRequestPath,COriginResponseHTTPExpires,CCacheTieredFill,CWAFRuleMessage,CEdgePathingStatus,CClientDeviceType,COriginSSLProtocol,CEdgeRateLimitAction,COriginIP,CEdgeRateLimitID,CZoneID,CEdgeResponseCompressionRatio,CClientRequestReferer,CWAFProfile,COriginResponseHTTPLastModified,COriginResponseBytes --timestamps=rfc3339'
```

**Respuesta con el código de estado 200**
```
{
"CacheCacheStatus":"unknown",
"CacheResponseBytes":396,
"CacheResponseStatus":200,
"CacheTieredFill":false,
"ClientASN":56046,
"ClientCountry":"cn",
"ClientDeviceType":"desktop",
"ClientIP":"1.1.1.1",
"ClientIPClass":"noRecord",
"ClientRequestBytes":400,
"ClientRequestHost":"foo.com",
"ClientRequestMethod":"GET",
"ClientRequestPath":"/",
"ClientRequestProtocol":"HTTP/1.1",
"ClientRequestReferer":"",
"ClientRequestURI":"/",
"ClientRequestUserAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36",
"ClientSSLCipher":"NONE",
"ClientSSLProtocol":"none",
"ClientSrcPort":4532,
"EdgeColoID":134,
"EdgeEndTimestamp":"2019-01-03T01:54:11Z",
"EdgePathingOp":"wl",
"EdgePathingSrc":"macro",
"EdgePathingStatus":"nr",
"EdgeRateLimitAction":"",
"EdgeRateLimitID":0,
"EdgeRequestHost":"foo.com",
"EdgeResponseBytes":808,
"EdgeResponseCompressionRatio":1.57,
"EdgeResponseContentType":"text/html",
"EdgeResponseStatus":200,
"EdgeServerIP":"172.69.98.106",
"EdgeStartTimestamp":"2019-01-03T01:54:11Z",
"OriginIP":"2.2.2.2",
"OriginResponseBytes":0,
"OriginResponseHTTPExpires":"",
"OriginResponseHTTPLastModified":"Tue, 31 Jan 2017 15:01:11 UTC",
"OriginResponseStatus":200,
"OriginResponseTime":7000000,
"OriginSSLProtocol":"unknown",
"ParentRayID":"00",
"RayID":"4931d60516c0b0b0",
"SecurityLevel":"med",
"WAFAction":"unknown",
"WAFFlags":"0",
"WAFMatchedVar":"",
"WAFProfile":"unknown",
"WAFRuleID":"",
"WAFRuleMessage":"",
"WorkerCPUTime":0,
"WorkerStatus":"unknown",
"WorkerSubrequest":false,
"WorkerSubrequestCount":0,
"ZoneID":******
}
```

**Respuesta con el código de estado 404**
```
{
"CacheCacheStatus":"miss",
"CacheResponseBytes":209,
"CacheResponseStatus":404,
"CacheTieredFill":false,
"ClientASN":56046,
"ClientCountry":"cn",
"ClientDeviceType":"desktop",
"ClientIP":"1.1.1.1",
"ClientIPClass":"noRecord",
"ClientRequestBytes":433,
"ClientRequestHost":"foo.com",
"ClientRequestMethod":"GET",
"ClientRequestPath":"/favicon.ico",
"ClientRequestProtocol":"HTTP/1.1",
"ClientRequestReferer":"foo.com/",
"ClientRequestURI":"/favicon.ico",
"ClientRequestUserAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36",
"ClientSSLCipher":"NONE",
"ClientSSLProtocol":"none",
"ClientSrcPort":4532,
"EdgeColoID":134,
"EdgeEndTimestamp":"2019-01-03T01:54:12Z",
"EdgePathingOp":"wl",
"EdgePathingSrc":"macro",
"EdgePathingStatus":"nr",
"EdgeRateLimitAction":"",
"EdgeRateLimitID":0,
"EdgeRequestHost":"foo.com",
"EdgeResponseBytes":556,
"EdgeResponseCompressionRatio":2.87,
"EdgeResponseContentType":"text/html",
"EdgeResponseStatus":404,
"EdgeServerIP":"172.69.98.148",
"EdgeStartTimestamp":"2019-01-03T01:54:12Z",
"OriginIP":"2.2.2.2",
"OriginResponseBytes":0,
"OriginResponseHTTPExpires":"",
"OriginResponseHTTPLastModified":"",
"OriginResponseStatus":404,
"OriginResponseTime":7000000,
"OriginSSLProtocol":"unknown",
"ParentRayID":"00",
"RayID":"4931d60a16c8b0b0",
"SecurityLevel":"med",
"WAFAction":"unknown",
"WAFFlags":"0",
"WAFMatchedVar":"",
"WAFProfile":"unknown",
"WAFRuleID":"",
"WAFRuleMessage":"",
"WorkerCPUTime":0,
"WorkerStatus":"unknown",
"WorkerSubrequest":false,
"WorkerSubrequestCount":0,
"ZoneID":******
}
```

**La solicitud ha coincidido con una regla WAF (ataque SQLj)**
```
{
"CacheCacheStatus":"unknown",
"CacheResponseBytes":0,
"CacheResponseStatus":0,
"CacheTieredFill":false,
"ClientASN":56046,
"ClientCountry":"cn",
"ClientDeviceType":"desktop",
"ClientIP":"1.1.1.1",
"ClientIPClass":"noRecord",
"ClientRequestBytes":501,
"ClientRequestHost":"foo.com",
"ClientRequestMethod":"GET",
"ClientRequestPath":"/login.php",
"ClientRequestProtocol":"HTTP/1.1",
"ClientRequestReferer":"",
"ClientRequestURI":"/login.php?username=asdf&password=asdf",
"ClientRequestUserAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:60.0) Gecko/20100101 Firefox/60.0",
"ClientSSLCipher":"NONE",
"ClientSSLProtocol":"none",
"ClientSrcPort":48718,
"EdgeColoID":134,
"EdgeEndTimestamp":"2019-01-04T02:22:26Z",
"EdgePathingOp":"wl",
"EdgePathingSrc":"macro",
"EdgePathingStatus":"nr",
"EdgeRateLimitAction":"",
"EdgeRateLimitID":0,
"EdgeRequestHost":"",
"EdgeResponseBytes":1849,
"EdgeResponseCompressionRatio":2.82,
"EdgeResponseContentType":"text/html",
"EdgeResponseStatus":403,
"EdgeServerIP":"",
"EdgeStartTimestamp":"2019-01-04T02:22:26Z",
"OriginIP":"",
"OriginResponseBytes":0,
"OriginResponseHTTPExpires":"",
"OriginResponseHTTPLastModified":"",
"OriginResponseStatus":0,
"OriginResponseTime":0,
"OriginSSLProtocol":"unknown",
"ParentRayID":"00",
"RayID":"493a3cc9463eb0d4",
"SecurityLevel":"med",
"WAFAction":"drop",
"WAFFlags":"0",
"WAFMatchedVar":"ARGS:USERNAME",
"WAFProfile":"off",
"WAFRuleID":"100008",
"WAFRuleMessage":"SQLi probing",
"WorkerCPUTime":0,
"WorkerStatus":"unknown",
"WorkerSubrequest":false,
"WorkerSubrequestCount":0,
"ZoneID":******
}
```

**La solicitud ha coincidido con una regla de cortafuegos**
```
{
"CacheCacheStatus":"unknown",
"CacheResponseBytes":0,
"CacheResponseStatus":0,
"CacheTieredFill":false,
"ClientASN":36351,
"ClientCountry":"us",
"ClientDeviceType":"desktop",
"ClientIP":"1.1.1.1",
"ClientIPClass":"noRecord",
"ClientRequestBytes":90,
"ClientRequestHost":"foo.com",
"ClientRequestMethod":"GET",
"ClientRequestPath":"/",
"ClientRequestProtocol":"HTTP/1.1",
"ClientRequestReferer":"",
"ClientRequestURI":"/",
"ClientRequestUserAgent":"curl/7.47.0",
"ClientSSLCipher":"NONE",
"ClientSSLProtocol":"none",
"ClientSrcPort":57260,
"EdgeColoID":26,
"EdgeEndTimestamp":"2019-01-03T08:48:42Z",
"EdgePathingOp":"ban",
"EdgePathingSrc":"user",
"EdgePathingStatus":"ip",
"EdgeRateLimitAction":"",
"EdgeRateLimitID":0,
"EdgeRequestHost":"",
"EdgeResponseBytes":3556,
"EdgeResponseCompressionRatio":0,
"EdgeResponseContentType":"text/html",
"EdgeResponseStatus":403,
"EdgeServerIP":"",
"EdgeStartTimestamp":"2019-01-03T08:48:42Z",
"OriginIP":"",
"OriginResponseBytes":0,
"OriginResponseHTTPExpires":"",
"OriginResponseHTTPLastModified":"",
"OriginResponseStatus":0,
"OriginResponseTime":0,
"OriginSSLProtocol":"unknown",
"ParentRayID":"00",
"RayID":"493a6341d02565e7",
"SecurityLevel":"med",
"WAFAction":"unknown",
"WAFFlags":"0",
"WAFMatchedVar":"",
"WAFProfile":"unknown",
"WAFRuleID":"",
"WAFRuleMessage":"",
"WorkerCPUTime":0,
"WorkerStatus":"unknown",
"WorkerSubrequest":false,
"WorkerSubrequestCount":0,
"ZoneID":******
}
```

**La solicitud se ha limitado en velocidad**
```
{
"CacheCacheStatus":"unknown",
"CacheResponseBytes":0,
"CacheResponseStatus":0,
"CacheTieredFill":false,
"ClientASN":36351,
"ClientCountry":"us",
"ClientDeviceType":"desktop",
"ClientIP":"1.1.1.1",
"ClientIPClass":"noRecord",
"ClientRequestBytes":90,
"ClientRequestHost":"foo.com",
"ClientRequestMethod":"GET",
"ClientRequestPath":"/",
"ClientRequestProtocol":"HTTP/1.1",
"ClientRequestReferer":"",
"ClientRequestURI":"/",
"ClientRequestUserAgent":"curl/7.47.0",
"ClientSSLCipher":"NONE",
"ClientSSLProtocol":"none",
"ClientSrcPort":33186,
"EdgeColoID":26,
"EdgeEndTimestamp":"2019-01-03T08:59:55Z",
"EdgePathingOp":"ban",
"EdgePathingSrc":"user",
"EdgePathingStatus":"rateLimit",
"EdgeRateLimitAction":"ban",
"EdgeRateLimitID":1307134,
"EdgeRequestHost":"",
"EdgeResponseBytes":3559,
"EdgeResponseCompressionRatio":0,
"EdgeResponseContentType":"text/html",
"EdgeResponseStatus":429,
"EdgeServerIP":"",
"EdgeStartTimestamp":"2019-01-03T08:59:55Z",
"OriginIP":"",
"OriginResponseBytes":0,
"OriginResponseHTTPExpires":"",
"OriginResponseHTTPLastModified":"",
"OriginResponseStatus":0,
"OriginResponseTime":0,
"OriginSSLProtocol":"unknown",
"ParentRayID":"00",
"RayID":"493a73ad468419b6",
"SecurityLevel":"med",
"WAFAction":"unknown",
"WAFFlags":"0",
"WAFMatchedVar":"",
"WAFProfile":"unknown",
"WAFRuleID":"",
"WAFRuleMessage":"",
"WorkerCPUTime":0,
"WorkerStatus":"unknown",
"WorkerSubrequest":false,
"WorkerSubrequestCount":0,
"ZoneID":******
}
```

**El servidor de origen está inactivo (Error 521, el servidor web está inactivo)**
```
{
"CacheCacheStatus":"miss",
"CacheResponseBytes":177,
"CacheResponseStatus":521,
"CacheTieredFill":false,
"ClientASN":56046,
"ClientCountry":"cn",
"ClientDeviceType":"desktop",
"ClientIP":"1.1.1.1",
"ClientIPClass":"noRecord",
"ClientRequestBytes":1082,
"ClientRequestHost":"foo.com",
"ClientRequestMethod":"GET",
"ClientRequestPath":"/favicon.ico",
"ClientRequestProtocol":"HTTP/2",
"ClientRequestReferer":"",
"ClientRequestURI":"/favicon.ico",
"ClientRequestUserAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:60.0) Gecko/20100101 Firefox/60.0",
"ClientSSLCipher":"AEAD-AES128-GCM-SHA256",
"ClientSSLProtocol":"TLSv1.3",
"ClientSrcPort":3060,
"EdgeColoID":134,
"EdgeEndTimestamp":"2019-01-03T06:33:55Z",
"EdgePathingOp":"wl",
"EdgePathingSrc":"macro",
"EdgePathingStatus":"nr",
"EdgeRateLimitAction":"",
"EdgeRateLimitID":0,
"EdgeRequestHost":"foo.com",
"EdgeResponseBytes":5177,
"EdgeResponseCompressionRatio":0,
"EdgeResponseContentType":"text/html",
"EdgeResponseStatus":521,
"EdgeServerIP":"172.69.98.148",
"EdgeStartTimestamp":"2019-01-03T06:33:55Z",
"OriginIP":"2.2.2.2",
"OriginResponseBytes":0,
"OriginResponseHTTPExpires":"",
"OriginResponseHTTPLastModified":"",
"OriginResponseStatus":0,
"OriginResponseTime":3000000,
"OriginSSLProtocol":"unknown",
"ParentRayID":"00",
"RayID":"49336fc9397ab080",
"SecurityLevel":"med",
"WAFAction":"unknown",
"WAFFlags":"0",
"WAFMatchedVar":"",
"WAFProfile":"unknown",
"WAFRuleID":"",
"WAFRuleMessage":"",
"WorkerCPUTime":0,
"WorkerStatus":"unknown",
"WorkerSubrequest":false,
"WorkerSubrequestCount":0,
"ZoneID":******
}
```
