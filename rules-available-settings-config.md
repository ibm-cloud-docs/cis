---

copyright:
  years: 2018, 2026
lastupdated: "2026-08-05"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Configuration rules settings
{: #config-available-settings}

You can configure the following settings in a configuration rule.

## Automatic HTTPS Rewrites
{: #automatic-https-rewrites}

It rewrites URLs from `HTTP` to `HTTPS` for resources that can be served over HTTPS.

Use this setting to enable or disable Automatic HTTPS Rewrites for requests that match the rule expression.

API example:

```sh
"action_parameters": {
  "automatic_https_rewrites": true
}
```
{: pre}

API configuration property name: `automatic_https_rewrites` (boolean).

## Browser integrity check
{: #browser-integrity-check}

Browser Integrity Check blocks requests based on HTTP headers that are commonly associated with malicious traffic.

Use this setting to enable or disable Browser Integrity Check for requests that match the rule expression.

API example:

```sh
"action_parameters": {
  "bic": true
}
```
{: pre}

API configuration property name: `bic` (boolean).

## Email obfuscation
{: #email-obfuscation}

Email Obfuscation prevents spam by hiding email addresses from bots and harvesters while keeping them visible to human visitors to your site.

Use this setting to enable or disable Email Obfuscation for requests that match the rule expression.

API example:

```sh
"action_parameters": {
  "email_obfuscation": false
}
```
{: pre}

API configuration property name: `email_obfuscation` (boolean).

## Hotlink protection
{: #hotlink-protection}

Hotlink Protection prevents other websites from embedding images hosted on your domain.

Use this setting to enable or disable Hotlink Protection for requests that match the rule expression.

API example:

```sh
"action_parameters": {
  "hotlink_protection": true
}
```
{: pre}

API configuration property name: `hotlink_protection` (boolean).

## Under defense mode
{: #under-defense-mode}

Under defense mode performs additional security checks to help mitigate Layer 7 DDoS attacks. Validated users access your website and suspicious traffic is blocked.

Use this setting to enable or disable Under defense mode for requests that match the rule expression.

API example:

```sh
"action_parameters": {
  "security_level": "under_defense"
}
```
{: pre}

API configuration property name: `security_level` (string).
API values: `off`, `essentially_off`, and `under_defense`.

## Request body buffering
{: #request-body-buffering}

Use the Request body buffering setting to configure how CIS buffers HTTP request bodies for requests that match the rule expression.

The following values are supported:

* Standard (default): Allows CIS features, such as the WAF, to inspect a portion of the request body when required.
* Full: Buffers the entire request body before forwarding it to the origin server.
* None: Does not buffer the request body. The request body is streamed directly to the origin server without inspection.

Setting the value to `none` can affect features that inspect request bodies, such as WAF and other security features. Use this option only when request body inspection is not required.
{: important}

API example:

```sh
"action_parameters": {
  "request_body_buffering": "full"
}
```
{: pre}

API configuration property name: `request_body_buffering` (string).
API values: `standard`, `full`, and `none`.

## Response body buffering
{: #response-body-buffering}

Use the Response body buffering setting to configure how CIS buffers HTTP response bodies for requests that match the rule expression.

The following values are supported:

* Standard (default): Allows CIS features, such as WAF, to inspect a portion of the response body when required.
* None: Does not buffer the response body. The response body is streamed directly to the client without inspection.

Setting the value to `none` can affect features that inspect response bodies, such as the Web Application Firewall (WAF) and other security features. Use this option only when response body inspection is not required.
{: important}

API example:

```sh
"action_parameters": {
  "response_body_buffering": "standard"
}
```
{: pre}

API configuration property name: `response_body_buffering` (string).
API values: `standard` and `none`.

## SSL mode
{: #ssl-mode}

Use the SSL setting to configure the SSL/TLS encryption mode for requests that match the rule expression. The SSL/TLS encryption mode determines how CIS connects to your origin server and validates the SSL certificates presented by the origin. For more information, see [SSL mode](/docs/cis?topic=cis-cis-tls-options#tls-encryption-modes).

API example:

```sh
"action_parameters": {
  "ssl": "flexible"
}
```
{: pre}

API configuration property name: `ssl` (string).
API values: "off", "flexible", `full`, `strict`, and `origin_pull`.

For complete API examples, see `Creatin a configuration rule via API`.
