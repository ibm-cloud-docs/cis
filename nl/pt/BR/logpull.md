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

Os clientes IBM podem acessar o serviço Logpull nas contas Corporativas. Esse serviço permite que os usuários consumam logs de solicitação por meio de HTTP com o uso de uma [CLI](/docs/cis-cli-plugin?topic=cis-cli-plugin-cis-cli-commands#log).

Esses logs contêm dados relacionados ao cliente da conexão, ao caminho da solicitação por meio da rede e à resposta do servidor da web de origem.


## Casos de uso
{:#logpull-usecases}

### Com base no RayID
{:#logpull-usecases-rayid}

Se um usuário receber uma mensagem de erro depois de executar um comando, poderá usar o RayID fornecido no cabeçalho de resposta para obter os logs relacionados ao comando.

Se tiver um RAY_ID com `-XXX` no final, certifique-se de removê-lo. Por exemplo, `12ab34cdef567gh8-XXX` torna-se `12ab34cdef567gh8`.
{.note}

**Solicitação**

```
ibmcloud cis logpull DNS_DOMAIN_ID --ray-id RAY_ID
```

**Resposta**

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

### Com base na duração de tempo
{:#logpull-usecases-time-duration}

Se um usuário receber uma mensagem de erro após a execução de um comando, mas não souber o RayID da resposta, ele poderá usar uma duração de tempo. Ele recebe todos os logs para a zona especificada durante o intervalo no qual o erro ocorreu e pode realizar procuras entre os resultados.


**Parâmetros necessários**

Horário de Início e Encerramento como um registro de data e hora do UNIX (em segundos ou nanossegundos) ou um registro de data e hora absoluto que está em conformidade com o RFC 3339, com uma duração de tempo de um minuto ou uma hora.

**Solicitação**
```
ibmcloud cis logpull DNS_DOMAIN_ID -- start 2019-01-02T01:00:00 + 00:00 -- final 2019-01-02T01:00:00 + 00:00
```
**Resposta**
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
{ "ClientIP ":" 2620:8c5: :1f: 949e:c04d "," ClientRequestHost ":" GET "," ClientRequestURI ":" /assets/bios.gif", "EdgeResponseBytes": 1121237, "EdgeResponseStatus": 200, "EdgeStartTimestamp": 1545067628046000000, "RayID": "48ab194348943489ec7a7" }
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/bootstrap-modal.js","EdgeEndTimestamp":1545067628046000000,"EdgeResponseBytes":2569,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067628043000000,"RayID":"48ab1943488ac7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/holder.js","EdgeEndTimestamp":1545067628053000000,"EdgeResponseBytes":4593,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067628046000000,"RayID":"48ab19434898c7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/old_school.png","EdgeEndTimestamp":1545067627960000000,"EdgeResponseBytes":1466,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067627952000000,"RayID":"48ab1942bf92c7a7"}
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com,"ClientRequestMethod":"GET","ClientRequestURI":"/assets/bootstrap-responsive.css","EdgeEndTimestamp":1545067627951000000,"EdgeResponseBytes":4797,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067627948000000,"RayID":"48ab1942af86c7a7"}
```

### Campos
{:#logpull-usecases-fields}

Se `campos` não forem especificados na solicitação, um conjunto limitado de campos padrão será retornado. Localize a lista completa de todos os campos disponíveis aqui:

**Solicitação**

```
ibmcloud cis logpull DNS_DOMAIN_ID --available-fields
```

Os campos são transmitidos como uma lista separada por vírgulas. Por exemplo, para ter "ZoneID" e "RayID", use:

```
ibmcloud cis logpull DNS_DOMAIN_ID --start 2019-01-02T01:00:00+00:00 --end 2019-01-02T01:00:00+00:00 --fields ZoneId,RayID
```

**Lista de campos**

Campos atualmente disponíveis (a partir de dezembro de 2018):
```
"CacheCacheStatus": "string; unknown | miss | expirou | atualização | stale | hit | ignore | bypass | bypass | revalidated", "CacheResponseBytes ":" int; número de bytes retornados pelo cache ","CacheResponseStatus ":" int; Código de status HTTP retornado pelo cache para a extremidade: todas as solicitações (incluindo aquelas não armazenáveis em cache) passam pelo cache: também consulte o campo CacheStatus ","CacheTieredFill ":" bool; Cache em camadas foi usado para atender a esse pedido ","ClientASN ":" int; cliente número AS ","ClientCountry ":" string; país do endereço IP do cliente ","ClientDeviceType ":" tipo de dispositivo cliente "string;", "ClientIP ":" string; endereço IP do cliente ","ClientIPClass ":" classe de IP de string; client ","ClientRequestBytes ":" int; número de bytes no pedido do cliente ","ClientRequestHost ": host; host solicitado pelo cliente", "ClientRequestMethod ":" string; método de HTTP da solicitação do cliente ","ClientRequestPath ":" string; caminho de URI solicitado pelo cliente ","ClientRequestProtocol ":" string; protocolo HTTP da solicitação do cliente ","ClientRequestReferer ":" string; referenciador de solicitação de HTTP ","ClientRequestURI ":" string; URI solicitado pelo cliente ","ClientRequestUserAgent ":" string; Agente do usuário relatado pelo cliente ","ClientSSLCipher ":" string; Cifra SSL do cliente ","ClientSSLProtocol ":" string; Protocolo SSL do Cliente (TLS) ","ClientSrcPort ":" int; porta de origem do cliente ","EdgeColoID ":" int; Cloudflare edge colo colo ","EdgeEndTimestamp ":" int ou string; unix nanosecond timestamp the edge concluiu o envio de resposta para o cliente ",
"EdgePathingOp": "string; indicates what type of response was issued for this request (unknown = no specific action)",
"EdgePathingSrc": "string; details how the request was classified based on security checks (unknown = no specific classification)",
"EdgePathingStatus": "string; indicates what data was used to determine the handling of this request (unknown = no data)",
"EdgeRateLimitAction": "string; the action taken by the blocking rule; empty if no action taken",
"EdgeRateLimitID": "int; the internal rule ID of the rate-limiting rule that triggered a block (ban) or simulate action. 0 if no action taken",
"EdgeRequestHost": "string; host header on the request from the edge to the origin",
"EdgeResponseBytes": "int; number of bytes returned by the edge to the client",
"EdgeResponseCompressionRatio": "float; edge response compression ratio",
"EdgeResponseContentType": "string; Edge response Content-Type header value",
"EdgeResponseStatus": "int; HTTP status code returned by Cloudflare to the client",
"EdgeServerIP": "string; IP of the edge server making a request to the origin",
"EdgeStartTimestamp": "int or string; unix nanosecond timestamp the edge received request from the client",
"OriginIP": "string; IP of the origin server",
"OriginResponseBytes": "int; number of bytes returned by the origin server",
"OriginResponseHTTPExpires": "string; value of the origin 'expires' header in RFC1123 format",
"OriginResponseHTTPLastModified": "string; value of the origin 'last-modified' header in RFC1123 format",
"OriginResponseStatus": "int; status returned by the origin server",
"OriginResponseTime": "int; number of nanoseconds it took the origin to return the response to edge",
"OriginSSLProtocol": "string; SSL (TLS) protocol used to connect to the origin",
"ParentRayID": "string; ray id of the parent request if this request was made through a worker script",
"RayID": "string; Ray ID of the request",
"SecurityLevel": "string; the security level configured at the time of this request. This is used to determine the sensitivity of the IP Reputation system.",
"WAFAction": "string; action taken by the WAF, if triggered",
"WAFFlags": "string; additional configuration flags: simulate (0x1) | null",
"WAFMatchedVar": "string; the full name of the most-recently matched variable",
"WAFProfile": "string; WAF profile: low | med | high",
"WAFRuleID": "string; ID of the applied WAF rule",
"WAFRuleMessage": "string; rule message associated with the triggered rule",
"WorkerCPUTime": "int; amount of time in microseconds spent executing a worker if any",
"WorkerStatus": "string; status returned from worker daemon",
"WorkerSubrequest": "bool; whether or not this request was a worker subrequest",
"WorkerSubrequestCount": "int; number of subrequests issued by a worker when handling this request",
"ZoneID": "int; internal zone ID"
```

### Exemplo
{:#logpull-usecases-example}
A seguir, há um exemplo de chamada `logpull` e exemplos de respostas de tipos específicos.

**Solicitação**
```
ibmcloud cis logpull DNS_DOMAIN_ID --start 2019-01-02T01:00:00+00:00 --end 2019-01-02T01:00:00+00:00 --fields ClientRequestURI,CEdgeResponseBytes,CParentRayID,CWorkerStatus,COriginResponseTime,CEdgeResponseStatus,CWorkerSubrequest,CClientRequestProtocol,CWAFRuleID,CEdgePathingOp,CClientSrcPort,CWorkerSubrequestCount,CEdgeRequestHost,CClientSSLCipher,CEdgePathingSrc,COriginResponseStatus,CClientIPClass,CWAFAction,CEdgeColoID,CClientCountry,CClientRequestHost,CWAFFlags,CClientASN,CEdgeServerIP,CCacheCacheStatus,CSecurityLevel,CClientRequestUserAgent,CCacheResponseBytes,CWAFMatchedVar,CEdgeStartTimestamp,CClientSSLProtocol,CEdgeEndTimestamp,CEdgeResponseContentType,CClientRequestBytes,CCacheResponseStatus,CWorkerCPUTime,CRayID,CClientRequestMethod,CClientIP,CClientRequestPath,COriginResponseHTTPExpires,CCacheTieredFill,CWAFRuleMessage,CEdgePathingStatus,CClientDeviceType,COriginSSLProtocol,CEdgeRateLimitAction,COriginIP,CEdgeRateLimitID,CZoneID,CEdgeResponseCompressionRatio,CClientRequestReferer,CWAFProfile,COriginResponseHTTPLastModified,COriginResponseBytes --timestamps=rfc3339'
```

**Resposta com Código de Status 200**
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

**Resposta com Código de Status 404**
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

**A solicitação correspondeu a uma regra do WAF (ataque SQLj)**
```
{
"CacheCacheStatus": "desconhecido", "CacheResponseBytes ": 0,"CacheResponseStatus ": 0,"CacheTieredFill ":false,"ClientASN ": 56046,"ClientCountry ":" cn ","ClientDeviceType ":" desktop ","ClientIP": "1.1.1.1", "ClientIPClass ":" noRecord ","ClientRequestBytes ": 501,"ClientRequestHost ":" foo.com ","ClientRequestMethod ":" GET ","ClientRequestPath ":" /login.php", "ClientRequestProtocol ":" HTTP/1.1 ","ClientRequestReferer ":" ","ClientRequestURI ":" /login.php?username = asdf&password = asdf", "ClientRequestUserAgent ":" Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv: 60.0) Gecko/20100101 Firefox/60.0 ","ClientSSLCipher ":" NENHUM ","ClientSSLProtocol ":" nenhum ","ClientSrcPort ": 48718,"EdgeColoID ": 134,"EdgeEndTimestamp ":" 2019-01-04T02:22:26Z ","EdgePathingOp ":" wl ","EdgePathingSrc ":" macro ","EdgePathingStatus ":" nr ","EdgeRateLimitAction ":" ","EdgeRateLimitID ": 0,"EdgeRequestHost ":" ","EdgeResponseBytes ": 1849",EdgeResponseCompressionRatio ": 2,82,"EdgeResponseContentType ":" text/html ","EdgeResponseStatus ": 403,"EdgeServerIP ":" ","EdgeStartTimestamp ":" 2019-01-04T02:22:26Z ",", "OriginIP ":" ","OriginResponseBytes ": 0,"OriginResponseHTTPExpires ":" ","OriginResponseHTTPLastModified ":" ","OriginResponseStatus ": 0,"OriginResponseTime ": 0,"OriginSSLProtocol ":" desconhecido ","ParentRayID ":" 00 ","RayID ":" 493a3cc9463eb0d4 ","SecurityLevel ":" med ","WAFAction ":" drop ","WAFFlags ":" 0 ","WAFMatchedVar ":" ARGS:USERNAME ","WAFProfile ":" off ","WAFRuleID ":" 100008 ","WAFRuleMessage ":" Sondagem SQLi ","WorkerCPUTime ": 0,"WorkerStatus ":" desconhecido ","WorkerSubrequest " :false,
"WorkerSubrequestCount":0,
"ZoneID":******
}
```

**A solicitação correspondeu a uma regra de firewall**
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

**A solicitação foi limitada por taxa**
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

**O Servidor de Origem está inativo (Erro 521, o Servidor da Web está inativo)**
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
