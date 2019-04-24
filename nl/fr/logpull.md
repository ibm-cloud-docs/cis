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

Les clients IBM peuvent accéder au service Logpull sur des comptes Enterprise. Ce service permet aux utilisateurs de consommer des journaux de requêtes via HTTP à l'aide d'une interface [CLI](/docs/cis-cli-plugin?topic=cis-cli-plugin-cis-cli-commands#log).

Ces journaux contiennent des données relatives au client qui se connecte, au chemin de demande via le réseau et à la réponse du serveur Web d'origine. 


## Cas d'utilisation
{:#logpull-usecases}

### Basé sur RayID 
{:#logpull-usecases-rayid}

Si un utilisateur reçoit un message d'erreur après avoir exécuté une commande, il peut utiliser le RayID fourni dans l'en-tête de la réponse pour obtenir les journaux liés à la commande. 

Si vous disposez d'un RAY_ID avec `-XXX` à la fin, veillez à le supprimer. Par exemple, `12ab34cdef567gh8-XXX` devient `12ab34cdef567gh8`.
{.note}

**Demande**

```
ibmcloud cis logpull DNS_DOMAIN_ID --ray-id RAY_ID
```

**Réponse**

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

### Basé sur la durée 
{:#logpull-usecases-time-duration}

Si un utilisateur reçoit un message d'erreur après avoir exécuté une commande mais ne connaît pas le RayID de la réponse, il peut utiliser une durée. Il reçoit tous les journaux de la zone donnée pendant la fenêtre où l'erreur s'est produite et peut effectuer une recherche dans les résultats. 


**Paramètres obligatoires**

Heure de début et de fin sous la forme d'un horodatage Unix (en secondes ou nanosecondes) ou d'un horodatage absolu conforme à la norme RFC 3339, avec une durée d'une minute ou d'une heure. 

**Demande**
```
ibmcloud cis logpull DNS_DOMAIN_ID --start 2019-01-02T01:00:00+00:00 --end 2019-01-02T01:00:00+00:00
```
**Réponse**
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

### Zones 
{:#logpull-usecases-fields}

Si les `zones` ne sont pas spécifiées dans la demande, un jeu limité de zones par défaut est renvoyé. Retrouvez la liste complète de toutes les zones disponibles ici : 

**Demande**

```
ibmcloud cis logpull DNS_DOMAIN_ID --available-fields
```

Les zones sont transmises sous forme de liste de valeurs séparées par des virgules. Par exemple, pour obtenir "ZoneID" et "RayID", utilisez :

```
ibmcloud cis logpull DNS_DOMAIN_ID --start 2019-01-02T01:00:00+00:00 --end 2019-01-02T01:00:00+00:00 --fields ZoneId,RayID
```

**Liste de zones**

Zones actuellement disponibles (depuis décembre 2018) : 
```
"CacheCacheStatus": "chaîne ; unknown | miss | expired | updating | stale | hit | ignored | bypass | revalidated",
"CacheResponseBytes": "ent ; nombre d'octets renvoyés par le cache",
"CacheResponseStatus": "ent ; code d'état HTTP renvoyé par le cache au bord: toutes les demandes (y compris celles qui ne peuvent pas être mises en cache) passent par le cache: voir aussi la zone CacheStatus",
"CacheTieredFill": "bool ; un cache hiérarchisé a été utilisé pour répondre à cette demande",
"ClientASN": "ent ; numéro d'AS client",
"ClientCountry": "chaîne ; pays de l'adresse IP du client",
"ClientDeviceType": "chaîne ; type de périphérique client",
"ClientIP": "chaîne ; adresse IP du client",
"ClientIPClass": "chaîne ; classe IP du client",
"ClientRequestBytes": "ent ; nombre d'octets dans la demande du client",
"ClientRequestHost": "chaîne ; hôte demandé par le client",
"ClientRequestMethod": "chaîne ; méthode HTTP de requête client",
"ClientRequestPath": "chaîne ; chemin d'accès URI demandé par le client",
"ClientRequestProtocol": "chaîne ; protocole HTTP de requête client",
"ClientRequestReferer": "chaîne ; référent de requête HTTP",
"ClientRequestURI": "chaîne ; adresse URI demandée par le client",
"ClientRequestUserAgent": "chaîne ; agent utilisateur signalé par le client",
"ClientSSLCipher": "chaîne ; chiffrement SSL client",
"ClientSSLProtocol": "chaîne ; protocole client SSL (TLS)",
"ClientSrcPort": "ent ; port source du client",
"EdgeColoID": "ent ; ID colo périphérie Cloudflare",
"EdgeEndTimestamp": "ent ou chaîne ; horodatage unix nanosecondes où la périphérie a fini d'envoyer la réponse au client",
"EdgePathingOp": "chaîne ; indique quel type de réponse a été émis pour cette demande (inconnu = pas d'action spécifique)",
"EdgePathingSrc": "chaîne ; explique comment la requête a été classée en fonction des contrôles de sécurité (inconnu = pas de classification spécifique)",
"EdgePathingStatus": "chaîne ; indique les données utilisées pour déterminer le traitement de cette demande (inconnu = pas de données)",
"EdgeRateLimitAction": "chaîne ; action entreprise par la règle de blocage ; vide si aucune action n'est entreprise",
"EdgeRateLimitID": "ent ; ID de règle interne de la règle de limitation de débit qui a déclenché un blocage (interdiction) ou une action simulée. 0 si aucune action n'a été prise",
"EdgeRequestHost": "chaîne ; en-tête d'hôte sur la requête de la périphérie à l'origine",
"EdgeResponseBytes": "ent ; nombre d'octets renvoyés par la périphérie au client",
"EdgeResponseCompressionRatio": "flottant ; taux de compression de la réponse de périphérie",
"EdgeResponseContentType": "chaîne ; valeur de l'en-tête Content-Type de la réponse de périphérie",
"EdgeResponseStatus": "ent ; code d'état HTTP renvoyé par Cloudflare au client",
"EdgeServerIP": "chaîne ; IP du serveur de périphérie effectuant une demande à l'origine",
"EdgeStartTimestamp": "ent ou chaîne ; horodatage unix nanosecondes de la requête reçue du client",
"OriginIP": "chaîne ; IP du serveur d'origine",
"OriginResponseBytes": "ent ; nombre d'octets renvoyés par le serveur d'origine",
"OriginResponseHTTPExpires": "chaîne ; valeur de l'en-tête 'expires' d'origine au format RFC1123",
"OriginResponseHTTPLastModified": "chaîne ; valeur de l'en-tête d'origine" dernière modification "au format RFC1123",
"OriginResponseStatus": "ent ; statut renvoyé par le serveur d'origine",
"OriginResponseTime": "ent ; nombre de nanosecondes nécessaires à l'origine pour renvoyer la réponse à la périphérie",
"OriginSSLProtocol": "chaîne ; protocole SSL (TLS) utilisé pour se connecter à l'origine",
"ParentRayID": "chaîne ; Ray ID de la requête parent si cette requête a été effectuée via un script de travail",
"RayID": "chaîne ; Ray ID de la requête",
"SecurityLevel": "chaîne ; niveau de sécurité configuré au moment de cette demande. Il est utilisé pour déterminer la sensibilité du système de réputation IP",
"WAFAction": "chaîne ; action entreprise par le WAF, si elle est déclenchée",
"WAFFlags": "chaîne ; indicateurs de configuration supplémentaires : simulate (0x1) | null",
"WAFMatchedVar": "chaîne ; nom complet de la dernière variable vérifiée",
"WAFProfile": "chaîne ; WAF profile: low | med | high",
"WAFRuleID": "chaîne ; ID de la règle WAF appliquée",
"WAFRuleMessage": "chaîne ; message de règle associé à la règle déclenchée",
"WorkerCPUTime": "ent ; temps, en microsecondes, consacré à l'exécution d'un travailleur, le cas échéant",
"WorkerStatus": "chaîne ; statut renvoyé par le démon d'agent",
"WorkerSubrequest": "bool ; si cette requête est ou non une sous-demande d'agent",
"WorkerSubrequestCount": "ent ; nombre de sous-demandes émises par un agent lors du traitement de cette demande",
"ZoneID": "ent ; ID de zone interne"
```

### Exemple 
{:#logpull-usecases-example}
Vous trouverez ci-dessous un exemple d'appel `logpull` et des exemples de réponses de types spécifiques. 

**Demande**
```
ibmcloud cis logpull DNS_DOMAIN_ID --start 2019-01-02T01:00:00+00:00 --end 2019-01-02T01:00:00+00:00 --fields ClientRequestURI,CEdgeResponseBytes,CParentRayID,CWorkerStatus,COriginResponseTime,CEdgeResponseStatus,CWorkerSubrequest,CClientRequestProtocol,CWAFRuleID,CEdgePathingOp,CClientSrcPort,CWorkerSubrequestCount,CEdgeRequestHost,CClientSSLCipher,CEdgePathingSrc,COriginResponseStatus,CClientIPClass,CWAFAction,CEdgeColoID,CClientCountry,CClientRequestHost,CWAFFlags,CClientASN,CEdgeServerIP,CCacheCacheStatus,CSecurityLevel,CClientRequestUserAgent,CCacheResponseBytes,CWAFMatchedVar,CEdgeStartTimestamp,CClientSSLProtocol,CEdgeEndTimestamp,CEdgeResponseContentType,CClientRequestBytes,CCacheResponseStatus,CWorkerCPUTime,CRayID,CClientRequestMethod,CClientIP,CClientRequestPath,COriginResponseHTTPExpires,CCacheTieredFill,CWAFRuleMessage,CEdgePathingStatus,CClientDeviceType,COriginSSLProtocol,CEdgeRateLimitAction,COriginIP,CEdgeRateLimitID,CZoneID,CEdgeResponseCompressionRatio,CClientRequestReferer,CWAFProfile,COriginResponseHTTPLastModified,COriginResponseBytes --timestamps=rfc3339'
```

**Réponse avec code d'état 200**
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

**Réponse avec code d'état 404**
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

**Requête correspondant à une règle WAF (attaque SQLj)**
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

**Demande correspondant à une règle de pare-feu**
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

**Demande limitée par le débit**
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

**Le serveur d'origine est en panne (erreur 521, le serveur Web est en panne)**
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
