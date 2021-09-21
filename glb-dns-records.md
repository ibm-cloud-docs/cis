---

copyright:
  years: 2018, 2020
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


# Working with load balancers and existing DNS records
{: #existing-dns-records}

A {{site.data.keyword.cis_full}} load balancer is identified by the DNS hostname whose traffic you want to balance (for example, `www.example.com`). The load balancer defines which origin server pools to use, the order in which they are used, and how to geographically distribute traffic among pools.
{: shortdesc}

When you create a load balancer on {{site.data.keyword.cis_short_notm}}, you can do one of the following:

* Use a unique hostname with no existing DNS record
* Use a hostname that has an existing DNS record (an A, AAAA, or CNAME record)

If a hostname has an existing DNS record, the load balancer supersedes the DNS record if the DNS record is an A, AAAA, or canonical name (CNAME) record. It does not supersede other record types.

If the load balancer is disabled, preexisting DNS records are served.

If there is no preexisting DNS record with the same name, disabling the load balancer prevents clients from resolving the host, and requests fail.

If a load balancer is manually disabled, traffic is not served to the associated origins or the fallback. If all pools in a load balancer are manually disabled, the fallback origin is used unless the fallback is also disabled. If the fallback is also disabled, the SOA record is served. Otherwise, if there is one pool in the load balancer and the pool is unhealthy, {{site.data.keyword.cis_short_notm}} sends traffic to the fallback pool regardless of the fallback pool's health.

## HTTP keep-alive (persistent HTTP connection)
{: #http-keep-alive}

{{site.data.keyword.cis_short_notm}} maintains keep-alive connections to improve performance and to reduce the cost of recurring TCP connects in the request transaction as {{site.data.keyword.cis_short_notm}} proxies customer traffic from its edge network to the site's origin.

Ensure that HTTP keep-alive connections are enabled on your origin. {{site.data.keyword.cis_short_notm}} reuses open TCP connections for up to 15 minutes (900 seconds) after the last HTTP request. Origin web servers close TCP connections if too many are open. HTTP keep-alive helps avoid the premature reset of connections for requests that are proxied by {{site.data.keyword.cis_short_notm}}.

## Session cookies
{: #session-cookies}

Configure [Session Affinity](/docs/cis?topic=cis-session-affinity) to parse HTTP requests by cookie header when you use HTTP cookies to track and bind user sessions to a specific server. Doing so directs each request to the correct application server even when HTTP requests share a TCP connection due to keep-alive.

