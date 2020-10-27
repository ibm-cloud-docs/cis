---

copyright:
  years: 2020
lastupdated: "2020-09-29"

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


# Using basic global load balancer features
{: #glb-basics}

A {{site.data.keyword.cis_full}} load balancer is identified by the DNS hostname whose traffic you want to balance (for example, `www.example.com`). The load balancer defines which origin server pools to use, the order in which they are used, and how to geographically distribute traffic among pools.
{:shortdesc}

## Load balancers and existing DNS records
{: #existing-dns-records}

When you create a load balancer on {{site.data.keyword.cis_short_notm}}, you can do one of the following:

* Use a unique hostname with no existing DNS record
* Use a hostname that has an existing DNS record (an A, AAAA, or CNAME record)

If a hostname has an existing DNS record, the load balancer supersedes the DNS record if the DNS record is an A, AAAA, or canonical name (CNAME) record. It does not supersede other record types.

If the load balancer is disabled, preexisting DNS records are served.

If there is no preexisting DNS record with the same name, disabling the load balancer prevents clients from resolving the host, and requests fail.

If a load balancer is manually disabled, traffic is not served to the associated origins or the fallback. If all pools in a load balancer are manually disabled, the fallback origin is used unless the fallback is also disabled. If the fallback is also disabled, the SOA record is served. Otherwise, if there is one pool in the load balancer and the pool is unhealthy, {{site.data.keyword.cis_short_notm}} sends traffic to the fallback pool regardless of the fallback pool's health.

### HTTP keep-alive (persistent HTTP connection)
{: #http-keep-alive}

{{site.data.keyword.cis_short_notm}} maintains keep-alive connections to improve performance and to reduce the cost of recurring TCP connects in the request transaction as {{site.data.keyword.cis_short_notm}} proxies customer traffic from its edge network to the site's origin.

Ensure that HTTP keep-alive connections are enabled on your origin. {{site.data.keyword.cis_short_notm}} reuses open TCP connections for up to 15 minutes (900 seconds) after the last HTTP request. Origin web servers close TCP connections if too many are open. HTTP keep-alive helps avoid the premature reset of connections for requests that are proxied by {{site.data.keyword.cis_short_notm}}.

### Session cookies
{: #session-cookies}

Configure Session Affinity to parse HTTP requests by cookie header when you use HTTP cookies to track and bind user sessions to a specific server. Doing so directs each request to the correct application server even when HTTP requests share a TCP connection due to keep-alive.

## Pools
{:#glb-pools}

A pool is a group of origin servers that traffic is intelligently routed to when attached to a global load balancer. The minimum number of available origin servers for the pool to be marked healthy is configurable by the user along with which specific health check to use. The origin pool can be associated with a specific region or it can be made available to all regions.

## Health check
{:#cis-health-check}

A health check helps gain insight into the availability of pools so that traffic can be routed to the healthy ones. These checks periodically send HTTP, HTTPS, or TCP requests and monitor the responses. They can be configured with a customized port, interval, timeout, status code, and more. As soon as a pool is marked unhealthy, traffic is intelligently rerouted to another available pool.

Be aware that your logs have references to Cloudflare because IBM is partnering with Cloudflare to provide {{site.data.keyword.cis_short_notm}}.
{:note}

### Health check events
{:#health-check-events}

Health Check Events are status changes from pools with connected health checks and their associated origin servers. If an origin's status degrades, a new item appears in a table, with the event's description.
