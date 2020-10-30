---

copyright:
  years: 2020
lastupdated: "2020-10-30"

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


# Setting session affinity
{:#session-affinity}

Loading a website usually requires fetching multiple assets from a web server. {{site.data.keyword.cis_short_notm}} session affinity minimizes redundant network requests by automatically directing requests from the same client to the same origin web server. 
{:shortdesc}

{{site.data.keyword.cis_short_notm}} sets a cookie on the initial response to the client. Using the cookie in subsequent client requests ensures those requests are sent to the same origin, unless the origin is unavailable.

When enabled, {{site.data.keyword.cis_short_notm}} session affinity does the following:

* When a client makes its first request, {{site.data.keyword.cis_short_notm}} sets a `CFLib` cookie on the client. The cookie encodes the origin to which the request is forwarded.
* Subsequent requests by the same client are forwarded to that origin for the duration of the cookie and as long as the origin server remains healthy.
* If the cookie expires or the origin server is unhealthy, {{site.data.keyword.cis_short_notm}} sets a new cookie encoding the appropriate failover origin.

All sessions default to 23 hours unless a custom session TTL is specified (in seconds) between 30 minutes and 7 days. A session affinity cookie is required to honor the TTL. The session cookie is secure when `Always Use HTTPS` is enabled. Additionally, `HttpOnly` is always enabled for the cookie to prevent cross-site scripting attacks.