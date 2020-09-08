---

copyright:
  years: 2018, 2020
lastupdated: "2020-08-07"


keywords: log push, logpush, time-based

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

# Using the Logpush service
{:#logpush}

{{site.data.keyword.cis_full}} Enterprise-level plans have access to detailed logs of HTTP and range requests for their domains. These logs are helpful for debugging and analytics, especially when combined with other data sources, such as ingress or application server logs at the origin.
{: shortdesc}

The data from Logpush is the same as that from [Logpull](/docs/cis?topic=cis-logpull#logpull). However, unlike Logpull, which allows you to download request logs, Logpush provides the option to push the request logs to {{site.data.keyword.cos_full}} ({{site.data.keyword.cos_short}}) buckets. You’re free to choose the method that’s most convenient.

Range logs are not included in HTTP(s) logs and require a separate job. These jobs can be pushed to the same {{site.data.keyword.cos_short}} bucket, but must have a different path.
{:tip}

Logpush uses HTTPS endpoints for {{site.data.keyword.cos_full_notm}}, so the log data is encrypted while in motion.

## Setting up Logpush using the console
{:#logpush-setup-ui}

**Prerequisite**: Before you create a Logpush job, you must have an [{{site.data.keyword.cos_full_notm}}](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage) instance with a bucket that has **write access** granted to {{site.data.keyword.cloud}} account `cislogp@us.ibm.com`. This enables {{site.data.keyword.cis_short_notm}} to write request logs into the {{site.data.keyword.cos_short}} bucket.

Follow these steps to add an application.

You can configure one log push job for each {{site.data.keyword.cos_short}} object (also known as a destination). This means that you can have two log pushes at a time going to the same bucket, but to different objects. For example, one with HTTP and another with Range, both referring to different objects in same bucket.
{:note}

1. Navigate to **Account** in your {{site.data.keyword.cis_short_notm}} instance and select the **Logs** tab.
1. In the **Log push** section, select the **HTTP/HTTPS** or **Range** tab.
1. Click **Create**.
1. Select a Cloud Object Storage instance from the list menu.
1. Select a bucket from the Bucket list menu.
1. Optionally, enter a bucket path.
1. Select the checkbox if you want to organize logs into daily subfolders.
1. Add a policy in your **Cloud Object Storage Instance** bucket with `cislogp@us.ibm.com` as a user with writer role.
1. Click the **Send ownership verification** button.
1. Download the object you received in your bucket, paste the token in the text area, then click **Verify ownership**.
1. Select the log fields that you want included in the log push, then click **Save**.

## Setting up Logpush using the CLI
{:#logpush-setup-cli}

**Prerequisite**: Before you create a Logpush job, you must have an {{site.data.keyword.cos_full_notm}} instance with a bucket that has **write access** granted to {{site.data.keyword.cloud}} account `cislogp@us.ibm.com`. This enables {{site.data.keyword.cis_short_notm}} to write request logs into the {{site.data.keyword.cos_short}} bucket.

To create a Logpush job for a specific domain and enable the job, run the following command:
```
ibmcloud cis logpush-job-create DNS_DOMAIN_ID --destination BUCKET_PATH --name JOB_NAME --fields all --enable true
```
{:pre}

Where:

* **--destination** specifies the path to the {{site.data.keyword.cos_short}} bucket.

   It follows the syntax: `cos://<bucket_path>?region=xxx&instance-id=xxxx`, where `bucket_path` is the bucket name followed by an optional path-like structure, `region` and {{site.data.keyword.cos_short}} `instance-id` are the {{site.data.keyword.cos_short}} bucket region and instance ID, which are required arguments.

   For example, `cos://mybucket/cislog?region=us-south&instance-id=c84e2a79-ce6d-3c79-a7e4-7e7ab3054cfe`.

* **--name** specifies the Logpush job name.
* **--enable** is the flag to enable or disable the Logpush job. Valid values are `true` or `false` (default).
* **--fields** specifies the list of log fields to be included in log files. Use commas to separate multiple fields.

   Use command `ibmcloud cis logpull DNS_DOMAIN_ID --available-fields` to get a comprehensive list of available log fields, or use `all` to include all available fields in the log files.

* **--timestamps** sets the format in which response timestamps are returned. Valid values are `unix`, `unixnano`, and `rfc3339` (default).
* **--dataset** is the category of logs that you want to receive. Valid values are `range_events` and `http_requests` (default).

   You cannot change this value after the job is created.

* **-i** or **--instance** is the instance name. If not set, the context instance specified by `ibmcloud cis instance-set INSTANCE` is used.

A domain can only have one Logpush job. Use the command line to interactively address the {{site.data.keyword.cos_short}} bucket ownership challenge. When a challenge token is written to a file in the given {{site.data.keyword.cos_short}} bucket, you must:

   * Download the file from your {{site.data.keyword.cos_short}} bucket and open it.
   * Copy and paste the challenge token in the command prompt to address the ownership challenge.

A Logpush job is created successfully after {{site.data.keyword.cis_short_notm}} validates the ownership challenge. The Logpush job pushes request logs to your {{site.data.keyword.cos_short}} bucket every 5 minutes.

You can use the token `{DATE}` in the bucket path to make the Logpush job push request logs in daily folders in the bucket path. For example: `cos://mybucket/cislog/{DATE}?region=us-south&instance-id=c84e2a79-ce6d-3c79-a7e4-7e7ab3054cfe`
{:note}

## Available Fields
{:logpush-fields}

The following tables describe the fields available by log category.

### HTTP requests
{:http-requests}

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
|EdgeRequestHost|Host header on the request from the edge to the origin|string
|EdgeResponseBytes|Number of bytes returned by the edge to the client|int
|EdgeResponseCompressionRatio|Edge response compression ratio|float
|EdgeResponseContentType|Edge response Content-Type header value|string
|EdgeResponseStatus|HTTP status code returned by Cloudflare to the client|int
|EdgeServerIP|IP of the edge server making a request to the origin|string
|EdgeStartTimestamp|Timestamp at which the edge received request from the client|int or string
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

### Range requests
{:range-requests}

This table contains the fields available for Range requests.

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
|OriginTlsMode|If and how the upstream connection is encrypted; `unknown` `off` `flexible` `full` `strict`|string
|OriginTlsProtocol|The TLS version negotiated between Spectrum and the origin; `unknown` `none` `SSLv3` `TLSv1` `TLSv1.1` `TLSv1.2` `TLSv1.3`|string|
|OriginTlsStatus|The state of the TLS session from Spectrum to the origin; `UNKNOWN` `OK` `INTERNAL_ERROR` `INVALID_CONFIG` `INVALID_SNI` `HANDSHAKE_FAILED` `KEYLESS_RPC`|string|
|ProxyProtocol|Which form of proxy protocol is applied to the given connection; `off` `v1` `v2` `simple`|string
|Status|A code indicating reason for connection closure|int|
|Timestamp|Timestamp at which the event took place|string|
