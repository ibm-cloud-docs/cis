---

copyright:
  years: 2018, 2025
lastupdated: "2025-04-08"

keywords: log pull, logpull

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Using the Logpull service
{: #logpull}

IBM customers can access the Logpull service on Enterprise accounts. This service allows users to consume request logs over HTTP using the [Logpull command](/docs/cis?topic=cis-cis-cli#logpull-section). These logs contain data related to the connecting client, the request path through the network, and the response from the origin web server. Users can query for logs starting from 1 minute in the past (relative to the actual time that you make the query).
{: shortdesc}

## Enabling log retention
{: #log-retention}

Edge logs are not retained by default. Before you can pull logs using the Logpull CLI, you must enable log retention. To do so, you must check the current setting, then turn log retention on or off. When enabled, logs are retained for 7 days. If retention is turned off, previously saved logs will be available until the retention period expires.

1. To check whether log retention is currently turned off, use the `log-retention` CLI:

```sh
ibmcloud cis log-retention DNS_DOMAIN_ID
```
{: pre}

1. If the output shows that the flag is `off` (default), update the setting as follows.

```sh
ibmcloud cis log-retention-update DNS_DOMAIN_ID --flag on
```
{: pre}

## Logpull use cases
{: #logpull-usecases}

### Getting logs based on RayID
{: #logpull-usecases-rayid}

If you receive an error message after running a command, you can use the RayID provided in the response header to get the logs related to the command.

If you have a RAY_ID with `-XXX` on the end, be sure to remove it. For example, `12ab34cdef567gh8-XXX` becomes `12ab34cdef567gh8`.
{: note}

Use the following command for the request:

```sh
ibmcloud cis logpull DNS_DOMAIN_ID --ray-id RAY_ID
```
{: pre}

The response follows:

```sh
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
{: codeblock}

### Getting logs based on time duration
{: #logpull-usecases-time-duration}

If you receive an error message after running a command, but do not know the RayID of the response, you can use a time duration to get all logs for the time period when the error occurred.

Use the following command for the request:

```sh
ibmcloud cis logpull DNS_DOMAIN_ID --start 2019-01-02T01:00:00+00:00 --end 2019-01-02T01:00:00+00:00
```
{: pre}

Where `--start` and `--end` is entered as a UNIX timestamp (in seconds or nanoseconds), or as an absolute timestamp that conforms to RFC 3339, with a time duration of a minute or an hour.

The response follows:

```sh
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
{"ClientIP":"2620:1f7:8c5::1f:949e:c04d","ClientRequestHost":"test.logpull.load.com","ClientRequestMethod":"GET","ClientRequestURI":"/assets/bootstrap-responsive.css","EdgeEndTimestamp":1545067627951000000,"EdgeResponseBytes":4797,"EdgeResponseStatus":200,"EdgeStartTimestamp":1545067627948000000,"RayID":"48ab1942af86c7a7"}
```
{: codeblock}

### Available fields
{: #logpull-usecases-fields}

If `fields` are not specified in the request, a limited set of default fields are returned. Find the full list of all available fields here:

```sh
ibmcloud cis logpull DNS_DOMAIN_ID --available-fields
```
{: pre}

Fields are passed as a comma-separated list. For example, to have "ZoneName" and "RayID", use:

```sh
ibmcloud cis logpull DNS_DOMAIN_ID --start 2019-01-02T01:00:00+00:00 --end 2019-01-02T01:00:00+00:00 --fields ZoneName,RayID
```
{: pre}

#### Field list
{: #field-list}

Available fields:

```sh
"BotScore": "int; Cloudflare Bot Score. Scores below 30 are commonly associated with automated traffic. Available only for Bot Management customers. To enable this feature, contact your account team.",
"BotScoreSrc": "string; Detection engine responsible for generating the Bot Score. Possible values are Not Computed | Heuristics | Machine Learning | Behavioral Analysis | Verified Bot | JS Fingerprinting | Cloudflare Service. Available only for Bot Management customers. To enable this feature, contact your account team.",
"CacheCacheStatus": "string; Cache status. Possible values are unknown | miss | expired | updating | stale | hit | ignored | bypass | revalidated | dynamic | stream_hit | deferred \"dynamic\" means that a request is not eligible for cache. This can mean, for example that it was blocked by the firewall. Refer to [Cloudflare cache responses](https://developers.cloudflare.com/cache/concepts/cache-responses/) for more details.",
"CacheResponseBytes": "int; Number of bytes returned by the cache.",
"CacheResponseStatus": "int; HTTP status code returned by the cache to the edge. All requests (including non-cacheable ones) go through the cache. Refer also to CacheCacheStatus field.",
"CacheTieredFill": "bool; Tiered Cache was used to serve this request.",
"ClientASN": "int; Client AS number.",
"ClientCountry": "string; 2-letter ISO-3166 country code of the client IP address.",
"ClientDeviceType": "string; Client device type.",
"ClientIP": "string; IP address of the client.",
"ClientIPClass": "string; Client IP class. Possible values are unknown | badHost | searchEngine | allowlist | monitoringService | noRecord | scan | tor.",
"ClientRequestBytes": "int; Number of bytes in the client request.",
"ClientRequestHost": "string; Host requested by the client.",
"ClientRequestMethod": "string; HTTP method of client request.",
"ClientRequestPath": "string; URI path requested by the client.",
"ClientRequestProtocol": "string; HTTP protocol of client request.",
"ClientRequestReferer": "string; HTTP request referrer.",
"ClientRequestURI": "string; URI requested by the client.",
"ClientRequestUserAgent": "string; User agent reported by the client.",
"ClientSSLCipher": "string; Client SSL cipher.",
"ClientSSLProtocol": "string; Client SSL (TLS) protocol. The value \"none\" means that SSL was not used.",
"ClientSrcPort": "int; Client source port.",
"ClientXRequestedWith": "string; X-Requested-With HTTP header.",
"Cookies": "object; String key-value pairs for Cookies. This field is populated based on [Logpush Custom fields](https://developers.cloudflare.com/logs/reference/custom-fields/), which need to be configured.",
"EdgeColoCode": "string; IATA airport code of data center that received the request.",
"EdgeColoID": "int; Cloudflare edge colo id.",
"EdgeEndTimestamp": "int or string; Timestamp at which the edge finished sending response to the client.",
"EdgePathingOp": "string; Indicates what type of response was issued for this request (unknown = no specific action).",
"EdgePathingSrc": "string; Details how the request was classified based on security checks (unknown = no specific classification).",
"EdgePathingStatus": "string; Indicates what data was used to determine the handling of this request (unknown = no data).",
"EdgeRequestHost": "string; Host header on the request from the edge to the origin.",
"EdgeResponseBytes": "int; Number of bytes returned by the edge to the client.",
"EdgeResponseCompressionRatio": "float; The edge response compression ratio is calculated as the ratio between the sizes of the original and compressed responses.",
"EdgeResponseContentType": "string; Edge response Content-Type header value.",
"EdgeResponseStatus": "int; HTTP status code returned by Cloudflare to the client.",
"EdgeServerIP": "string; IP of the edge server making a request to the origin. Possible responses are string in IPv4 or IPv6 format, or empty string. Empty string means that there was no request made to the origin server.",
"EdgeStartTimestamp": "int or string; Timestamp at which the edge received request from the client.",
"OriginIP": "string; IP of the origin server.",
"OriginResponseBytes": "int; Number of bytes returned by the origin server.",
"OriginResponseHTTPExpires": "string; Value of the origin 'expires' header in RFC1123 format.",
"OriginResponseHTTPLastModified": "string; Value of the origin 'last-modified' header in RFC1123 format.",
"OriginResponseStatus": "int; Status returned by the upstream server. The value 0 means that there was no request made to the origin server and the response was served by Cloudflare's Edge. However, if the zone has a Worker running on it, the value 0 could be the result of a Workers subrequest made to the origin.",
"OriginResponseTime": "int; Number of nanoseconds it took the origin to return the response to edge.",
"OriginSSLProtocol": "string; SSL (TLS) protocol used to connect to the origin.",
"ParentRayID": "string; Ray ID of the parent request if this request was made using a Worker script.",
"RayID": "string; ID of the request.",
"RequestHeaders": "object; String key-value pairs for RequestHeaders. This field is populated based on [Logpush Custom fields](https://developers.cloudflare.com/logs/reference/custom-fields/), which need to be configured.",
"ResponseHeaders": "object; String key-value pairs for ResponseHeaders. This field is populated based on [Logpush Custom fields](https://developers.cloudflare.com/logs/reference/custom-fields/), which need to be configured.",
"WAFFlags": "string; Additional configuration flags: simulate (0x1) | null.",
"WAFMatchedVar": "string; The full name of the most-recently matched variable.",
"WorkerCPUTime": "int; Amount of time in microseconds spent executing a worker, if any.",
"WorkerStatus": "string; Status returned from worker daemon.",
"WorkerSubrequest": "bool; Whether or not this request was a worker subrequest.",
"WorkerSubrequestCount": "int; Number of subrequests issued by a worker when handling this request."
"ZoneName": "string; the human-readable name of the zone"
```
{: codeblock}

## Logpull example
{: #logpull-usecases-example}

The following is an example `logpull` call and examples of specific types of responses.

* **Request**

    ```sh
    ibmcloud cis logpull DNS_DOMAIN_ID --start 2019-01-02T01:00:00+00:00 --end 2019-01-02T01:00:00+00:00 --fields ClientRequestURI,EdgeResponseBytes,ParentRayID,WorkerStatus,    OriginResponseTime,EdgeResponseStatus,WorkerSubrequest,ClientRequestProtocol,EdgePathingOp,ClientSrcPort,WorkerSubrequestCount,EdgeRequestHost,    ClientSSLCipher,EdgePathingSrc,OriginResponseStatus,ClientIPClass,EdgeColoID,ClientCountry,ClientRequestHost,WAFFlags,ClientASN,EdgeServerIP,    CacheCacheStatus,SecurityLevel,ClientRequestUserAgent,CacheResponseBytes,EdgeStartTimestamp,ClientSSLProtocol,EdgeEndTimestamp,EdgeResponseContentType,    ClientRequestBytes,CacheResponseStatus,WorkerCPUTime,RayID,ClientRequestMethod,ClientIP,ClientRequestPath,OriginResponseHTTPExpires,CacheTieredFill,WAFRuleMessage,    EdgePathingStatus,ClientDeviceType,OriginSSLProtocol,EdgeRateLimitAction,OriginIP,EdgeRateLimitID,ZoneName,EdgeResponseCompressionRatio,ClientRequestReferer,    OriginResponseHTTPLastModified,OriginResponseBytes --timestamps=rfc3339'
    ```
    {: codeblock}

* **Response with Status Code 200**

    ```sh
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
    "WAFFlags":"0",
    "WAFMatchedVar":"",
    "WAFProfile":"unknown",
    "WAFRuleID":"",
    "WAFRuleMessage":"",
    "WorkerCPUTime":0,
    "WorkerStatus":"unknown",
    "WorkerSubrequest":false,
    "WorkerSubrequestCount":0,
    "ZoneName":"example.com"
    }
    ```
    {: codeblock}

* **Response with Status Code 404**

    ```sh
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
    "WAFFlags":"0",
    "WAFMatchedVar":"",
    "WAFProfile":"unknown",
    "WAFRuleMessage":"",
    "WorkerCPUTime":0,
    "WorkerStatus":"unknown",
    "WorkerSubrequest":false,
    "WorkerSubrequestCount":0,
    "ZoneName":"example.com"
    }
    ```
    {: codeblock}

* **Request matched a WAF rule (SQLj attack)**

    ```sh
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
    "WAFFlags":"0",
    "WAFMatchedVar":"ARGS:USERNAME",
    "WAFProfile":"off",
    "WAFRuleMessage":"SQLi probing",
    "WorkerCPUTime":0,
    "WorkerStatus":"unknown",
    "WorkerSubrequest":false,
    "WorkerSubrequestCount":0,
    "ZoneName":"example.com"
    }
    ```
    {: codeblock}

* **Request matched a firewall rule**

    ```sh
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
    "WAFFlags":"0",
    "WAFMatchedVar":"",
    "WAFProfile":"unknown",
    "WAFRuleMessage":"",
    "WorkerCPUTime":0,
    "WorkerStatus":"unknown",
    "WorkerSubrequest":false,
    "WorkerSubrequestCount":0,
    "ZoneName":"example.com"
    }
    ```
    {: codeblock}

* **Request was rate limited**

    ```sh
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
    "WAFFlags":"0",
    "WAFMatchedVar":"",
    "WAFProfile":"unknown",
    "WAFRuleMessage":"",
    "WorkerCPUTime":0,
    "WorkerStatus":"unknown",
    "WorkerSubrequest":false,
    "WorkerSubrequestCount":0,
    "ZoneName":"example.com"
    }
    ```
    {: codeblock}

* **Origin server is down (Error 521, Web Server is down)**

    ```sh
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
    "WAFFlags":"0",
    "WAFMatchedVar":"",
    "WAFProfile":"unknown",
    "WAFRuleMessage":"",
    "WorkerCPUTime":0,
    "WorkerStatus":"unknown",
    "WorkerSubrequest":false,
    "WorkerSubrequestCount":0,
    "ZoneName":"example.com"
    }
    ```
    {: codeblock}

## Limitations
{: #logpull-limitations}

The following usage restrictions apply when using the Logpull feature.

* **Rate limits:** Exceeding these limit results in a `429` error response:
    * 15 requests per minute per zone
    * 180 requests per minute per user
* **Time range:** The maximum difference between the start and end parameters can be 1 hour.
* **Response size:** The maximum response size is 10 GiB per request, which is equivalent to around 15 M records when about 55 fields are selected. More records can be retrieved when fewer fields are selected because the per-record size is smaller.
* **Timeout:** The response will fail with a terminated connection after 10 minutes.
* **Stream timeout:** The request will be terminated with a `408` error response if the connection is idle for 30 seconds. This timeout usually means that the request is too exhaustive (frequent timeouts - more than 12 per hour). Stream timeouts will result in subsequent queries getting blocked with a status code `429` for 1 hour. To avoid the timeout, try requesting records by using fewer number of fields, or try with smaller start and end parameters.
