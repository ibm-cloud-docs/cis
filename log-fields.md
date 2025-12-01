
---

copyright:
  years: 2025
lastupdated: "2025-12-01"

keywords: log fields

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Accessing log fields
{: #log-fields}

If `fields` are not specified in the request, a limited set of default fields are returned. Find the full list of all available fields using the following request.

```sh
ibmcloud cis logpush-available-fields DNS_DOMAIN_ID [--dataset DATASET] [-i, --instance INSTANCE]
```
{: pre}

## Datasets
{: #log-datasets}

These available datasets describe the fields available by log category:

- HTTP/ HTTPS requests (`http_requests`)
- Firewall events (`firewall_events`)
- Range events (`range_events`)
- DNS logs (`dns_logs`)

## Available Fields
{: #logpull-available-fields}

The following tables indicate the fields available by dataset. Log fields are subject to change, so it is recommended to use the [Available Log Fields API](/apidocs/cis#list-fields-for-dataset-v2) to pull the most up-to-date version of the available fields.


### HTTP requests
 {: #http-requests}

This table contains the fields available for http_requests.

| Field | Description | Type |
|-------|-------------|------|
|BotDetectionIDs|List of IDs that correlate to the Bot Management Heuristic detections made on a request. Available only for Bot Management customers. To enable this feature, contact your account team.|array[int]|
|BotDetectionTags|List of tags that correlate to the Bot Management Heuristic detections made on a request. Available only for Bot Management customers. To enable this feature, contact your account team.|array[string]|
|BotScore|Cloudflare Bot Score. Scores below 30 are commonly associated with automated traffic. Available only for Bot Management customers. To enable this feature, contact your account team.|int|
|BotScoreSrc|`Heuristics` \| Machine Learning \| Behavioral Analysis \| Verified Bot \| JS Fingerprinting \| Cloudflare Service. Available only for Bot Management customers. To enable this feature, contact your account team.|string|
|BotTags|Type of bot traffic (if available).  Available only for Bot Management customers. To enable this feature, contact your account team.|array[string]|
|CacheCacheStatus|`miss` \| `expired` \| `updating` \| `stale` \| `hit` \| `ignored` \| `bypass` \| `revalidated` \| `dynamic` \| `stream_hit` \| deferred "dynamic" means that a request is not eligible for cache. This can mean, for example that it was blocked by the firewall.|string|
|CacheReserveUsed|Cache Reserve was used to serve this request.|bool|
|CacheResponseBytes|Number of bytes returned by the cache.|int|
|CacheResponseStatus|HTTP status code returned by the cache to the edge. All requests (including non-cacheable ones) go through the cache. Refer also to CacheCacheStatus field.|int|
|CacheTieredFill|Tiered Cache was used to serve this request.|bool|
|ClientASN|Client AS number.|int|
|ClientCity|Approximate city of the client.|string|
|ClientCountry|2-letter ISO-3166 country code of the client IP address.|string|
|ClientDeviceType|Client device type.|string|
|ClientIP|IP address of the client.|string|
|ClientIPClass|`badHost` \| `searchEngine` \| `allowlist` \| `monitoringService` \| `noRecord` \| `scan` \| `tor`.|string|
|ClientLatitude|Approximate latitude of the client.|string|
|ClientLongitude|Approximate longitude of the client.|string|
|ClientMTLSAuthCertFingerprint|The SHA256 fingerprint of the certificate presented by the client during mTLS authentication. Only populated on the first request on an mTLS connection.|string|
|ClientMTLSAuthStatus|`ok` \| `absent` \| `untrusted` \| `notyetvalid` \| `expired`.|string|
|ClientRegionCode|The ISO-3166-2 region code of the client IP address.|string|
|ClientRequestBytes|Number of bytes in the client request.|int|
|ClientRequestHost|Host requested by the client.|string|
|ClientRequestMethod|HTTP method of client request.|string|
|ClientRequestPath|URI path requested by the client, which includes only the path portion of the requested URL, without the query string.|string|
|ClientRequestProtocol|HTTP protocol of client request.|string|
|ClientRequestReferer|HTTP request referrer.|string|
|ClientRequestScheme|The URL scheme requested by the visitor.|string|
|ClientRequestSource|Identifies requests as coming from an external source or another service within Cloudflare.|string|
|ClientRequestURI|URI requested by the client, which includes the TLS Mode: End-to-End flexible path and query string of the requested URL.|string|
|ClientRequestUserAgent|User agent reported by the client.|string|
|ClientSSLCipher|Client SSL cipher.|string|
|ClientSSLProtocol|Client SSL (TLS) protocol. The value "none" means that SSL was not used.|string|
|ClientSrcPort|Client source port.|int|
|ClientTCPRTTMs|The smoothed average of TCP round-trip time (SRTT). For the initial request on a connection, this is measured only during connection setup. For a subsequent request on the same connection, it is measured over the entire connection lifetime up until the time that request is received.|int|
|ClientXRequestedWith|X-Requested-With HTTP header.|string|
|ContentScanObjResults|List of content scan results.|array[string]|
|ContentScanObjSizes|List of content object sizes.|array[int]|
|ContentScanObjTypes|List of content types.|array[string]|
|Cookies|String key-value pairs for Cookies.|object|
|EdgeCFConnectingO2O|True if the request looped through multiple zones on the Cloudflare edge. This is considered an orange to orange (O2O) request.|bool|
|EdgeColoCode|IATA airport code of the data center that received the request.|string|
|EdgeColoID|Cloudflare edge data center ID.|int|
|EdgeEndTimestamp|Timestamp at which the edge finished sending response to the client.|int or string|
|EdgePathingOp|Indicates what type of response was issued for this request (unknown = no specific action).|string|
|EdgePathingSrc|Details how the request was classified based on security checks (unknown = no specific classification).|string|
|EdgePathingStatus|Indicates what data was used to determine the handling of this request (unknown = no data).|string|
|EdgeRequestHost|Host header on the request from the edge to the origin.|string|
|EdgeResponseBodyBytes|Size of the HTTP response body returned to clients.|int|
|EdgeResponseBytes|Number of bytes returned by the edge to the client.|int|
|EdgeResponseCompressionRatio|The edge response compression ratio is calculated as the ratio between the sizes of the original and compressed responses.|float|
|EdgeResponseContentType|Edge response Content-Type header value.|string|
|EdgeResponseStatus|HTTP status code returned by Cloudflare to the client.|int|
|EdgeServerIP|IP of the edge server making a request to the origin. Possible responses are string in IPv4 or IPv6 format, or empty string. Empty string means that there was no request made to the origin server.|string|
|EdgeStartTimestamp|Timestamp at which the edge received request from the client.|int or string|
|EdgeTimeToFirstByteMs|Total view of Time To First Byte as measured at Cloudflare's edge. Starts after a TCP connection is established and ends when Cloudflare begins returning the first byte of a response to eyeballs. Includes TLS handshake time (for new connections) and origin response time.|int|
|JA3Hash|The MD5 hash of the JA3 fingerprint used to profile SSL/TLS clients. Available only for Bot Management customers. To enable this feature, contact your account team.|string|
|JA4|The JA4 fingerprint used to profile SSL/TLS clients. Available only for Bot Management customers. To enable this feature, contact your account team.|string|
|JA4Signals|Inter-request statistics computed for this JA4 fingerprint. JA4Signals field is organized in key:value pairs, where values are numbers. Available only for Bot Management customers. To enable this feature, contact your account team.|object|
|JSDetectionPassed|`failed` \| missing. Available only for Bot Management customers. To enable this feature, contact your account team.|string|
|OriginDNSResponseTimeMs|Time taken to receive a DNS response for an origin name. Usually takes a few milliseconds, but may be longer if a CNAME record is used.|int|
|OriginIP|IP of the origin server.|string|
|OriginRequestHeaderSendDurationMs|Time taken to send request headers to origin after establishing a connection. Note that this value is usually `0`.|int|
|OriginResponseBytes|Number of bytes returned by the origin server.|int|
|OriginResponseDurationMs|Upstream response time, measured from the first datacenter that receives a request. Includes time taken by Smart Routing and Tiered Cache, plus time to connect and receive a response from origin servers. This field replaces OriginResponseTime.|int|
|OriginResponseHTTPExpires|Value of the origin 'expires' header in RFC1123 format.|string|
|OriginResponseHTTPLastModified|Value of the origin 'last-modified' header in RFC1123 format.|string|
|OriginResponseHeaderReceiveDurationMs|Time taken for origin to return response headers after Cloudflare finishes sending request headers.|int|
|OriginResponseStatus|Status returned by the upstream server. The value `0` means that there was no response received from the origin server and the response was served by Cloudflare's Edge. However, if the zone has a Edge function running on it, the value `0` could be the result of a Edge functions subrequest made to the origin.|int|
|OriginResponseTime|Number of nanoseconds it took the origin to return the response to edge.|int|
|OriginSSLProtocol|SSL (TLS) protocol used to connect to the origin.|string|
|OriginTCPHandshakeDurationMs|Time taken to complete TCP handshake with origin. This will be `0` if an origin connection is reused.|int|
|OriginTLSHandshakeDurationMs|Time taken to complete TLS handshake with origin. This will be `0` if an origin connection is reused.|int|
|ParentRayID|Ray ID of the parent request if this request was made using a Edge function script.|string|
|RayID|ID of the request.|string|
|RequestHeaders|String key-value pairs for RequestHeaders.|object|
|ResponseHeaders|String key-value pairs for ResponseHeaders.|object|
|SecurityAction|Action of the security rule that triggered a terminating action, if any.|string|
|SecurityActions|`allow` \| `block` \| `challenge` \| `jschallenge` \| `log` \| `connectionClose` \| `challengeSolved` \| `challengeBypassed` \| `jschallengeSolved` \| `jschallengeBypassed` \| `bypass` \| `managedChallenge` \| `managedChallengeNonInteractiveSolved` \| `managedChallengeInteractiveSolved` \| `managedChallengeBypassed` \| `rewrite` \| `forceConnectionClose` \| `skip`.|array[string]|
|SecurityRuleDescription|Description of the security rule that triggered a terminating action, if any.|string|
|SecurityRuleID|Rule ID of the security rule that triggered a terminating action, if any.|string|
|SecurityRuleIDs|Array of rule IDs of the security product that matched the request. The security product associated with the rule ID can be found in SecuritySources. The length of the array is the same as SecurityActions and SecuritySources.|array[string]|
|SecuritySources|`asn` \| `country` \| `ip` \| `ipRange` \| `securityLevel` \| `zoneLockdown` \| `waf` \| `firewallRules` \| `uaBlock` \| `rateLimit` \| `bic` \| `hot` \| `l7ddos` \| `validation` \| `botFight` \| `apiShield` \| `botManagement` \| `dlp` \| `firewallManaged` \| `firewallCustom` \| `apiShieldSchemaValidation` \| `apiShieldTokenValidation` \| `apiShieldSequenceMitigation`.|array[string]|
|SmartRouteColoID|The Cloudflare data center used to connect to the origin server if Smart Routing is used.|int|
|UpperTierColoID|The "upper tier" data center that was checked for a cached copy if Tiered Cache is used.|int|
|VerifiedBotCategory|The category of verified bot.|string|
|WAFAttackScore|Overall request score generated by the WAF detection module.|int|
|WAFFlags|`null`.|string|
|WAFMatchedVar|The TLS Mode: End-to-End flexible name of the most-recently matched variable.|string|
|WAFRCEAttackScore|WAF score for an RCE attack.|int|
|WAFSQLiAttackScore|WAF score for an SQLi attack.|int|
|WAFXSSAttackScore|WAF score for an XSS attack.|int|
|WorkerCPUTime|Amount of time in microseconds spent executing a Edge function, if any.|int|
|WorkerScriptName|The Edge function script name that made the request.|string|
|WorkerStatus|Status returned from Edge function daemon.|string|
|WorkerSubrequest|Whether or not this request was a Edge function subrequest.|bool|
|WorkerSubrequestCount|Number of subrequests issued by a Edge function when handling this request.|int|
|WorkerWallTimeUs|The elapsed time in microseconds between the start of a Edge function invocation, and when the Edge functions Runtime determines that no more JavaScript needs to run. Specifically, this measures the wall-clock time that the JavaScript context remained open. For example, when returning a response with a large body, the Edge functions runtime can, in some cases, determine that no more JavaScript needs to run, and closes the JS context before all the bytes have passed through and been sent. Alternatively, if you use the `waitUntil()` API to perform work without blocking the return of a response, this work may continue executing after the response has been returned, and will be included in `Edge functionWallTimeUs`.|int|
|ZoneName|The human-readable name of the zone (for example, 'cloudflare.com').|string|
{: caption="Available log fields for HTTP requests" caption-side="bottom"}

### DNS logs
 {: #dns-logs}

This table contains the fields available for dns_logs.

| Field | Description | Type |
|-------|-------------|------|
|ColoCode|IATA airport code of the data center that received the request.|string|
|EDNSSubnet|IPv4 or IPv6 address information corresponding to the [EDNS Client Subnet (ECS)](https://www.rfc-editor.org/rfc/rfc7871.html#section-4){: external} forwarded by recursive resolvers. Not all resolvers send this information.|string|
|EDNSSubnetLength|Size of the EDNS Client Subnet (ECS) in bits. For example, if the last octet of an IPv4 address is omitted (`192.0.2.x.`), the subnet length will be `24`.|int|
|QueryName|Name of the query that was sent.|string|
|QueryType|Integer value of query type. For more information refer to [Query type](https://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml#dns-parameters-4).|int|
|ResponseCached|Whether the response was cached or not.|bool|
|ResponseCode|Integer value of response code. For more information refer to  [Response code](https://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml#dns-parameters-6).|int|
|SourceIP|IP address of the client (IPv4 or IPv6).|string|
|Timestamp|Timestamp at which the query occurred.|int or string|
{: caption="Available log fields for DNS logs" caption-side="bottom"}

### Range requests
 {: #range-requests}

This table contains the fields available for range_events.

| Field | Description | Type |
|-------|-------------|------|
|Application|The unique public ID of the application on which the event occurred.|string|
|ClientAsn|Client AS number.|int|
|ClientBytes|The number of bytes read from the client by the Range service.|int|
|ClientCountry|Country of the client IP address.|string|
|ClientIP|Client IP address.|string|
|ClientMatchedIpFirewall|`ALLOW` \| `BLOCK_ERROR` \| `BLOCK_IP` \| `BLOCK_COUNTRY` \| `BLOCK_ASN` \| `WHITELIST_IP` \| `WHITELIST_COUNTRY` \| `WHITELIST_ASN`.|string|
|ClientPort|Client port.|int|
|ClientProto|`udp` \| `unix`.|string|
|ClientTcpRtt|The TCP round-trip time in nanoseconds between the client and Range.|int|
|ClientTlsCipher|The cipher negotiated between the client and Range. An unknown cipher is returned as "UNK."|string|
|ClientTlsClientHelloServerName|The server name in the Client Hello message from client to Range.|string|
|ClientTlsProtocol|`none` \| `SSLv3` \| `TLSv1` \| `TLSv1.1` \| `TLSv1.2` \| `TLSv1.3`.|string|
|ClientTlsStatus|`OK` \| `INTERNAL_ERROR` \| `INVALID_CONFIG` \| `INVALID_SNI` \| `HANDSHAKE_FAILED` \| `KEYLESS_RPC`.|string|
|ColoCode|IATA airport code of the data center that received the request.|string|
|ConnectTimestamp|Timestamp at which both legs of the connection (client/edge, edge/origin or nexthop) were established.|int or string|
|DisconnectTimestamp|Timestamp at which the connection was closed.|int or string|
|Event|`connect` \| `disconnect` \| `clientFiltered` \| `tlsError` \| `resolveOrigin` \| `originError`.|string|
|IpFirewall|Whether IP Firewall was enabled at time of connection.|bool|
|OriginBytes|The number of bytes read from the origin by Range.|int|
|OriginIP|Origin IP address.|string|
|OriginPort|Origin port.|int|
|OriginProto|`udp` \| `unix`.|string|
|OriginTcpRtt|The TCP round-trip time in nanoseconds between Range and the origin.|int|
|OriginTlsCipher|The cipher negotiated between Range and the origin. An unknown cipher is returned as "UNK."|string|
|OriginTlsFingerprint|SHA256 hash of origin certificate. An unknown SHA256 hash is returned as an empty string.|string|
|OriginTlsMode|`off` \| TLS Mode: Client-to-Edge \| TLS Mode: End-to-End flexible \| TLS Mode: End-to-End CA signed.|string|
|OriginTlsProtocol|`none` \| `SSLv3` \| `TLSv1` \| `TLSv1.1` \| `TLSv1.2` \| `TLSv1.3`.|string|
|OriginTlsStatus|`OK` \| `INTERNAL_ERROR` \| `INVALID_CONFIG` \| `INVALID_SNI` \| `HANDSHAKE_FAILED` \| `KEYLESS_RPC`.|string|
|ProxyProtocol|`v1` \| `v2` \| `simple`.|string|
|Status|A code indicating reason for connection closure.|int|
|Timestamp|Timestamp at which the event took place.|int or string|
{: caption="Available log fields for Range requests" caption-side="bottom"}

### Firewall events
 {: #firewall-events}

This table contains the fields available for firewall_events.

| Field | Description | Type |
|-------|-------------|------|
|Action|`allow` \| `block` \| `challenge` \| `jschallenge` \| `log` \| `connectionclose` \| `challengesolved` \| `challengebypassed` \| `jschallengesolved` \| `jschallengebypassed` \| `bypass` \| `managedchallenge` \| `managedchallengenoninteractivesolved` \| `managedchallengeinteractivesolved` \| `managedchallengebypassed`.|string|
|ClientASN|The ASN number of the visitor.|int|
|ClientASNDescription|The ASN of the visitor as string.|string|
|ClientCountry|Country from which request originated.|string|
|ClientIP|The visitor's IP address (IPv4 or IPv6).|string|
|ClientIPClass|`badHost` \| `searchEngine` \| `allowlist` \| `monitoringService` \| `noRecord` \| `scan` \| `tor`.|string|
|ClientRefererHost|The referer host.|string|
|ClientRefererPath|The referer path requested by visitor.|string|
|ClientRefererQuery|The referer query-string was requested by the visitor.|string|
|ClientRefererScheme|The referer URL scheme requested by the visitor.|string|
|ClientRequestHost|The HTTP hostname requested by the visitor.|string|
|ClientRequestMethod|The HTTP method used by the visitor.|string|
|ClientRequestPath|The path requested by visitor.|string|
|ClientRequestProtocol|The version of HTTP protocol requested by the visitor.|string|
|ClientRequestQuery|The query-string was requested by the visitor.|string|
|ClientRequestScheme|The URL scheme requested by the visitor.|string|
|ClientRequestUserAgent|Visitor's user-agent string.|string|
|ContentScanObjResults|List of content scan results.|array[string]|
|ContentScanObjSizes|List of content object sizes.|array[int]|
|ContentScanObjTypes|List of content types.|array[string]|
|Datetime|The date and time the event occurred at the edge.|int or string|
|Description|The description of the rule triggered by this request.|string|
|EdgeColoCode|The airport code of the Cloudflare data center that served this request.|string|
|EdgeResponseStatus|HTTP response status code returned to browser.|int|
|Kind|The kind of event, currently only possible values are: firewall.|string|
|MatchIndex|Rules match index in the chain. The last matching rule will have MatchIndex `0`. If another rule matched before the last one, it will have MatchIndex 1. The same applies to any other matching rules, which will have a MatchIndex value of 2, 3, and so on.|int|
|Metadata|Additional product-specific information. Metadata is organized in key:value pairs. Key and Value formats can vary by Cloudflare security product and can change over time.|object|
|OriginResponseStatus|HTTP origin response status code returned to browser.|int|
|OriginatorRayID|The RayID of the request that issued the challenge/jschallenge.|string|
|RayID|The RayID of the request.|string|
|Ref|The user-defined identifier for the rule triggered by this request. Use refs to label your rules individually alongside the Cloudflare-provided RuleID. You can set refs via the Rulesets API for some security products.|string|
|RuleID|The Cloudflare security product-specific RuleID triggered by this request.|string|
|Source|`asn` \| `country` \| `ip` \| `iprange` \| `securitylevel` \| `zonelockdown` \| `waf` \| `firewallrules` \| `uablock` \| `ratelimit` \| `bic` \| `hot` \| `l7ddos` \| `validation` \| `botfight` \| `apishield` \| `botmanagement` \| `dlp` \| `firewallmanaged` \| `firewallcustom` \| `apishieldschemavalidation` \| `apishieldtokenvalidation` \| `apishieldsequencemitigation`.|string|
{: caption="Available log fields for Firewall events" caption-side="bottom"}
