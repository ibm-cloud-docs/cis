---

copyright:
  years: 2025
lastupdated: "2025-08-07"

keywords:

subcollection: cis

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# How can I help IBM Support trace my CLI API request?
{: #uuid-support}
{: troubleshoot}

When investigating CLI-related issues, effective traceability depends on receiving complete and properly formatted request data. The new `X-Request-ID` header in the CIS CLI improves transparency and traceability across systems, making it easier for IBM Support to pinpoint and resolve issues efficiently. 
{: shortdesc}

IBM Support might encounter difficulty tracing specific CLI-initiated API calls if the necessary request identifiers are missing from the logs you share.
{: tsSymptoms}

Although the CLI automatically includes the `X-Request-ID` header in every API request, this information might be inadvertently excluded when you collect and share trace logs. Without it, support teams may be unable to track the request across back-end systems.
{: tsCauses}

To ensure that IBM Support can trace and analyze the request properly, follow these steps when capturing and sharing CLI logs:
{: tsResolve}

1. Enable trace logging in the CLI before reproducing the issue.
1. Capture and share the full API request and response logs, including the `X-Request-ID` and, if available, the `X-Correlation-Id` from the response.
1. Look for details similar to the following:

   ```sh
   REQUEST: [2025-07-17T19:47:24+05:30]
   POST /v1/crn:v1:staging:public:internet-svcs-ci:global:a/01652b251c3ae2787110a995d8db0135:1a9174b6-0106-417a-844b-c8eb43a72f63::/rules/lists HTTP/1.1
   Host: api-int.cis.dev.cloud.ibm.com
   Accept: application/json
   Authorization: [PRIVATE DATA HIDDEN]
   Content-Type: application/json
   X-Auth-User-Token: [PRIVATE DATA HIDDEN]

   {"name":"ac","kind":"asn"}

   RESPONSE: [2025-07-17T19:47:25+05:30] Elapsed: 1189ms
   HTTP/2.0 200 OK
   Cache-Control: no-cache, no-store, must-revalidate
   Cf-Cache-Status: DYNAMIC
   Cf-Ray: 960a5cd87e565520-DEL
   Content-Security-Policy: frame-ancestors 'none'; default-src 'self'; form-action 'self'
   Content-Type: application/json
   Date: Thu, 17 Jul 2025 14:17:25 GMT
   Server: cloudflare
   Strict-Transport-Security: max-age=31536000; includeSubdomains
   X-Content-Type-Options: nosniff
   X-Correlation-Id: f9e06c3c-8276-4436-9ad3-0bf63c27291c
   X-Envoy-Upstream-Service-Time: 842
   ```
   {: screen}
   
1. Attach this information to your support case to assist IBM Support in isolating and debugging the issue quickly.

   Make sure to redact sensitive data, such as Authorization tokens, before sharing logs externally.
   {: note}
 
