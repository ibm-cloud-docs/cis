---

copyright:
  years: 2020
lastupdated: "2020-10-30"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Setting proxy modes
{: #proxy-modes}

Load balancers support DNS-only and HTTP proxy modes. You can have HTTP Proxy and DNS-Only domains in the same load balancer region, but the traffic routing behavior differs as follows:

* Traffic for domains using HTTP Proxy mode is routed based on the data center associated with the user making the request.
* Traffic for domains using DNS-Only mode is routed based on the data center associated with the user’s recursive resolver (DNS recursor).

## HTTP Proxy mode
{: #http-proxy-mode}

In HTTP Proxy mode, load balancers have an automatic TTL. {{site.data.keyword.cis_short_notm}} announces IBM IP addresses externally, but protects (mask) your origin server IP addresses. Any changes to your load balancer propagate within seconds inside {{site.data.keyword.cis_short_notm}}, including any failover events.

Setting the load balancer to HTTP Proxy mode offers the following benefits:

* Failover is faster, because external DNS caches that don't respect short DNS TTLs do not impact failover performance.
* The "automatic" TTL (five minutes) reduces the number of authoritative queries made against {{site.data.keyword.cis_short_notm}} without impacting failover performance. 

## DNS-Only mode
{: #dns-only-mode}

In DNS-Only mode, you can configure load balancers to set a TTL from 30 seconds to 10 minutes. {{site.data.keyword.cis_short_notm}} serves the addresses of the healthy origin servers directly, but relies on DNS resolvers respecting the short TTL to re-query the {{site.data.keyword.cis_short_notm}} DNS for an updated list of healthy addresses.
