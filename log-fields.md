---

copyright:
  years: 2020
lastupdated: "2020-08-24"

keywords: 

subcollection: cis

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:term: .term}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Accessing log fields
{:#log-fields}

If `fields` are not specified in the request, a limited set of default fields are returned. Find the full list of all available fields using the following request.

**Request**

```
ibmcloud cis logpull DNS_DOMAIN_ID --available-fields
```
{:pre}

Fields are passed as a comma-separated list. For example, to have "ZoneID" and "RayID", use:

```
ibmcloud cis logpull DNS_DOMAIN_ID --start 2019-01-02T01:00:00+00:00 --end 2019-01-02T01:00:00+00:00 --fields ZoneId,RayID
```
{:pre}

## Available Fields
{:#available-fields}

The following tables describe the fields available by log category.

### HTTP requests
{:#http-requests}

This table contains the fields available for HTTP requests.

|Field|Value|Type|
|-----|-----|----|
|BotScore|Cloudflare Bot Score (available for Bot Management customers; please contact your account team to enable)|int|
|BotScoreSrc|Underlying detection engine or source on where a Bot Score is calculated. Possible values are `Not Computed` `Heuristics` `Machine Learning` `Behavioral Analysis` `Verified Bot`|string|
|CacheCacheStatus|`unknown` `miss` `expired` `updating` `stale` `hit` `ignored` `bypass` `revalidated`|string|
|CacheResponseBytes|Number of bytes returned by the cache|int|
|CacheResponseStatus|HTTP status code returned by the cache to the edge; all requests (including non-cacheable ones) go through the cache; also see CacheStatus field|int|
|CacheTieredFill|Tiered Cache was used to serve this request|bool|
|ClientASN|Client AS number|int|
|ClientCountry|Country of the client IP address|string|
|ClientDeviceType|Client device type|string|
|ClientIP|IP address of the client|string|
|ClientIPClass|`unknown` `clean` `badHost` `searchEngine` `whitelist` `greylist` `monitoringService` `securityScanner` `noRecord` `scan` `backupService` `mobilePlatform` `tor`|string|
|ClientRequestBytes|Number of bytes in the client request|int|
|ClientRequestHost|Host requested by the client|string|
|ClientRequestMethod|HTTP method of client request|string|
|ClientRequestPath|URI path requested by the client|string|
|ClientRequestProtocol|HTTP protocol of client request|string|
|ClientRequestReferer|HTTP request referrer|string|
|ClientRequestURI|URI requested by the client|string|
|ClientRequestUserAgent|User agent reported by the client|string|
|ClientSSLCipher|Client SSL cipher|string|
|ClientSSLProtocol|Client SSL (TLS) protocol|string|
|ClientSrcPort|Client source port|int|
|ClientXRequestedWith|X-Requested-With HTTP header|string|
|EdgeColoCode|IATA airport code of data center that received the request|string|
|EdgeColoID|Cloudflare edge colo id|int|
|EdgeEndTimestamp|Timestamp at which the edge finished sending response to the client|int or string|
|EdgePathingOp|Indicates what type of response was issued for this request (unknown = no specific action)|string|
|EdgePathingSrc|Details how the request was classified based on security checks (unknown = no specific classification)|string|
|EdgePathingStatus|Indicates what data was used to determine the handling of this request (unknown = no data)|string|
|EdgeRateLimitAction|The action taken by the blocking rule; empty if no action taken|string|
|EdgeRateLimitID|The internal rule ID of the rate-limiting rule that triggered a block (ban) or simulate action. 0 if no action taken|int|
|EdgeRequestHost|Host header on the request from the edge to the origin|string|
|EdgeResponseBytes|Number of bytes returned by the edge to the client|int|
|EdgeResponseCompressionRatio|Edge response compression ratio|float|
|EdgeResponseContentType|Edge response Content-Type header value|string|
|EdgeResponseStatus|HTTP status code returned by Cloudflare to the client|int|
|EdgeServerIP|IP of the edge server making a request to the origin|string|
|EdgeStartTimestamp|Timestamp at which the edge received request from the client|int or string|
|FirewallMatchesActions|Array of actions the Cloudflare firewall products performed on this request. The individual firewall products associated with this action be found in FirewallMatchesSources and their respective RuleIds can be found in FirewallMatchesRuleIDs. The length of the array is the same as FirewallMatchesRuleIDs and FirewallMatchesSources. Possible actions are `allow` `log` `simulate` `drop` `challenge` `jschallenge` `connectionClose` `challengeSolved` `challengeFailed` `challengeBypassed` `jschallengeSolved` `jschallengeFailed` `jschallengeBypassed` `bypass`|array of actions (strings)|
|FirewallMatchesRuleIDs|Array of RuleIDs of the firewall product that has matched the request. The firewall product associated with the RuleID can be found in FirewallMatchesSources. The length of the array is the same as FirewallMatchesActions and FirewallMatchesSources.|array of RuleIDs (strings)|
|FirewallMatchesSources|The firewall products that matched the request. The same product can appear multiple times, which indicates different rules or actions that were activated. The RuleIDs can be found in FirewallMatchesRuleIDs, the actions can be found in FirewallMatchesActions. The length of the array is the same as FirewallMatchesRuleIDs and FirewallMatchesActions. Possible sources are `asn` `country` `ip` `ipRange` `securityLevel` `zoneLockdown` `waf` `firewallRules` `uaBlock` `rateLimit` `bic` `hot`  `l7ddos` `sanitycheck` `protect`|array of product names (strings)|
|OriginIP|IP of the origin server|string|
|OriginResponseHTTPExpires|Value of the origin 'expires' header in RFC1123 format|string|
|OriginResponseHTTPLastModified|Value of the origin 'last-modified' header in RFC1123 format|string|
|OriginResponseStatus|Status returned by the origin server|int|
|OriginResponseTime|Number of nanoseconds it took the origin to return the response to edge|int|
|OriginSSLProtocol|SSL (TLS) protocol used to connect to the origin|string|
|ParentRayID|Ray ID of the parent request if this request was made using a Worker script|string|
|RayID|ID of the request|string|
|SecurityLevel|The security level configured at the time of this request. This is used to determine the sensitivity of the IP Reputation system|string|
|WAFAction|Action taken by the WAF, if triggered|string|
|WAFFlags|Additional configuration flags: `simulate (0x1)` `null`|string|
|WAFMatchedVar|The full name of the most-recently matched variable|string|
|WAFProfile|`low` `med` `high`|string|
|WAFRuleID|ID of the applied WAF rule|string|
|WAFRuleMessage|Rule message associated with the triggered rule|string|
|WorkerCPUTime|Amount of time in microseconds spent executing a worker, if any|int|
|WorkerStatus|Status returned from worker daemon|string|
|WorkerSubrequest|Whether or not this request was a worker subrequest|bool|
|WorkerSubrequestCount|Number of subrequests issued by a worker when handling this request|int|
|ZoneID|Internal zone ID|int|
{: caption="Table 1. HTTP events" caption-side="top"}


### Range requests
{:#range-requests}

The following table contains the fields available for Range requests.

|Field|Value|Type|
|-----|-----|----|
|Application|The unique public ID of the application on which the event occurred|string|
|ClientAsn|Client AS number|int|
|ClientBytes|The number of bytes read from the client by the Spectrum service|int|
|ClientCountry|Country of the client IP address|string|
|ClientIP|Client IP address|string|
|ClientMatchedIpFirewall|Whether the connection matched any IP Firewall rules; `UNKNOWN` `ALLOW` `BLOCK_ERROR` `BLOCK_IP` `BLOCK_COUNTRY` `BLOCK_ASN` `WHITELIST_IP` `WHITELIST_COUNTRY` `WHITELIST_ASN`|string|
|ClientPort|Client port|int|
|ClientProto|Transport protocol used by client; `tcp` `udp` `unix`|string|
|ClientTcpRtt|The TCP round-trip time in nanoseconds between the client and Spectrum|int|
|ClientTlsCipher|The cipher negotiated between the client and Spectrum|string|
|ClientTlsClientHelloServerName|The server name in the Client Hello message from client to Spectrum|string|
|ClientTlsProtocol|The TLS version negotiated between the client and Spectrum; `unknown` `none` `SSLv3` `TLSv1` `TLSv1.1` `TLSv1.2` `TLSv1.3`|string|
|ClientTlsStatus|Indicates state of TLS session from the client to Spectrum; `UNKNOWN` `OK` `INTERNAL_ERROR` `INVALID_CONFIG` `INVALID_SNI` `HANDSHAKE_FAILED` `KEYLESS_RPC`|string|
|ColoCode|IATA airport code of data center that received the request|string|
|ConnectTimestamp|Timestamp at which both legs of the connection (client/edge, edge/origin or nexthop) were established|int or string|
|DisconnectTimestamp|Timestamp at which the connection was closed|int or string|
|Event|`connect` `disconnect` `clientFiltered` `tlsError` `resolveOrigin`  `originError`|string|
|IpFirewall|Whether IP Firewall was enabled at time of connection|bool|
|OriginBytes|The number of bytes read from the origin by Spectrum|int|
|OriginIP|Origin IP address|string|
|OriginPort|Origin port|int|
|OriginProto|Transport protocol used by origin; `tcp` `udp` `unix`|string|
|OriginTcpRtt|The TCP round-trip time in nanoseconds between Spectrum and the origin|int|
|OriginTlsCipher|The cipher negotiated between Spectrum and the origin|string|
|OriginTlsFingerprint|SHA256 hash of origin certificate|string|
|OriginTlsMode|If and how the upstream connection is encrypted; `unknown` `off` `flexible` `full` `strict`|string|
|OriginTlsProtocol|The TLS version negotiated between Spectrum and the origin; `unknown` `none` `SSLv3` `TLSv1` `TLSv1.1` `TLSv1.2` `TLSv1.3`|string|
|OriginTlsStatus|The state of the TLS session from Spectrum to the origin; `UNKNOWN` `OK` `INTERNAL_ERROR` `INVALID_CONFIG` `INVALID_SNI` `HANDSHAKE_FAILED` `KEYLESS_RPC`|string|
|ProxyProtocol|Which form of proxy protocol is applied to the given connection; `off` `v1` `v2` `simple`|string|
|Status|A code indicating reason for connection closure|int|
|Timestamp|Timestamp at which the event took place|string|
{: caption="Table 2. Range events" caption-side="top"}

### Firewall events
{:#firewall-events}

|Field|Value|Type|
|-----|-----|----|
|Action|The code of the first-class action the Cloudflare Firewall took on this request|string|
|ClientASN|The ASN number of the visitor|int|
|ClientASNDescription|The ASN of the visitor as string|string|
|ClientCountry|Country from which request originated|string|
|ClientIP|The visitor's IP address (IPv4 or IPv6)|string|
|ClientIPClass|The classification of the visitor's IP address, possible values are: `unknown` `clean` `badHost` `searchEngine` `whitelist` `greylist` `monitoringService` `securityScanner` `noRecord` `scan` `backupService` `mobilePlatform` `tor`|string|
|ClientRefererHost|The referer host|string|
|ClientRefererPath|The referer path requested by visitor|string|
|ClientRefererQuery|The referer query-string was requested by the visitor|string|
|ClientRefererScheme|The referer url scheme requested by the visitor|string|
|ClientRequestHost|The HTTP hostname requested by the visitor|string|
|ClientRequestMethod|The HTTP method used by the visitor|string|
|ClientRequestPath|The path requested by visitor|string|
|ClientRequestProtocol|The version of HTTP protocol requested by the visitor|string|
|ClientRequestQuery|The query-string was requested by the visitor|string|
|ClientRequestScheme|The url scheme requested by the visitor|string|
|ClientRequestUserAgent|Visitor's user-agent string|string|
|Datetime|The date and time the event occurred at the edge|int or string|
|EdgeColoCode|The airport code of the Cloudflare datacenter that served this request|string|
|EdgeResponseStatus|HTTP response status code returned to browser|int|
|Kind|The kind of event, currently the only possible value is `firewall`|string|
|MatchIndex|Rules match index in the chain|int|
|Metadata|Additional product-specific information. Metadata is organized in key:value pairs. Key and Value formats can vary by Cloudflare security product and can change over time|object|
|OriginResponseStatus|HTTP origin response status code returned to browser|int|
|OriginatorRayID|The RayID of the request that issued the challenge/jschallenge|string|
|RayID|The RayID of the request|string|
|RuleID|The Cloudflare security product-specific RuleID triggered by this request|string|
|Source|The Cloudflare security product triggered by this request|string|
{: caption="Table 3. Firewall events" caption-side="top"}
