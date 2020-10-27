---

copyright:
  years: 2020
lastupdated: "2020-09-23"

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


# Using advanced global load balancer features
{: #glb-advanced}

The following global load balancer features are more advanced. Review [Using global load balancers](/docs/cis?topic=cis-using-global-load-balancers#glb-basics) if you have not done so already. 
{:shortdesc}

## Traffic steering
{: #traffic-steering}

Load balancing provides several traffic steering modes, which allow customers to optimize how load balancers route traffic. You can configure traffic steering from the load balancing dashboard, in the **Edit Load Balancer** panel. You can also configure traffic steering via the {{site.data.keyword.cis_short_notm}} API. Available steering options include standard failover (steering disabled), dynamic steering, and geo steering.

### Standard failover
{: #standard-failover}

Standard failover directs traffic from unhealthy pools to the next healthy pool in the configuration, using the pool order to determine failover priority (the failover order).

If all pools are marked unhealthy, the load balancer directs traffic to the fallback pool. The default fallback pool is the last pool listed in the load balancer configuration.

To nominate a specific fallback pool through the {{site.data.keyword.cis_short_notm}} API, use the **Update Load Balancers** command and set the `fallback_pool` parameter. If no monitors are attached to the load balancer, it directs traffic to the primary pool exclusively.


### Dynamic steering
{: #dynamic-steering}

Dynamic steering uses health check data to identify the fastest pool for a {{site.data.keyword.cis_short_notm}} region or point of presence (PoP).

Dynamic steering creates Round Trip Time (RTT) profiles based on an exponential weighted moving average (EWMA) of RTT to determine the fastest pool. If there is no current RTT data for your pool in a region or colocation center, {{site.data.keyword.cis_short_notm}} directs traffic to the pools in failover order.

Allow 10 minutes for {{site.data.keyword.cis_short_notm}} to build an RTT profile the first time you enable dynamic steering for a server pool.

If you are terminating TCP at a cloud provider edge location, the calculated latency might not reflect the true latency to the origin for TCP health checks.

The following diagram shows how {{site.data.keyword.cis_short_notm}} routes traffic to the pool with the lowest EWMA among three regions: Eastern North America, Europe, and Australia. In this case, the ENAM pool is selected, because it has the lowest RTT.

![Figure showing traffic steering](images/cis-traffic-steering.svg "Figure showing traffic steering"){: caption="Figure 1. Traffic steering in {{site.data.keyword.cis_short_notm}}" caption-side="top"}

### Geo Steering
{: #geo-steering}

Geo steering directs traffic to pools based on the client’s region or PoP. Only domains on Enterprise plans can perform geo steering by PoP. Users specify the pools to which the load balancer directs traffic for a geographical region or PoP. You can assign multiple pools to the same region, and the load balancer uses them in failover order. If there is no configuration for a region or pool, the load balancer uses the default failover order.

Our partners at Cloudflare have 13 geographic regions. The region of a client is determined by the region of the Cloudflare data center that answers the client’s DNS query. These regions are listed in the following table, along with their region codes.

|Region Code|	Region|
|----|----|----|
|WNAM|Western North America|
|ENAM|Eastern North America|
|WEU|Western Europe|
|EEU|Eastern Europe|
|NSAM|Northern South America|
|SSAM|Southern South America|
|OC|Oceania|
|ME|Middle East|
|NAF|Northern Africa|
|SAF|Southern Africa|
|SAS|Southern Asia|
|SEAS|Southeast Asia|
|NEAS|Northeast Asia|


## Pools
{:#pools}

A {{site.data.keyword.cis_short_notm}} load balancer pool represents a group of origin servers, each identified by their IP address or hostname. You can configure multiple pools, as well as failover priority (Pool A > Pool B > Pool C). If you're familiar with DNS terminology, think of a pool as a "record set", except that only addresses that are considered healthy are returned. You can attach health checks to individual pools to tailor monitoring for collections of origin servers.

* When adding origin servers to a pool, you can identify the origin by hostname or IP address.
* The order of pools in the load balancer determines the standard failover priority. When the number of healthy origins in a pool drops below the configured threshold, the load balancer routes traffic to the next available pool.
* By default, pools are ordered by date created. You can reorder them from the global load balancer dashboard and via {{site.data.keyword.cis_short_notm}} API (use the Update Pools command to set a new `origins` array).
* Dynamic steering uses Round Trip Time (RTT) profiles to determine pool priority. If there is no RTT data for a pool in a region or colocation center, the load balancer uses pool order to determine failover priority.
* Geo steering directs traffic to pools based on the client’s region or point of presence. If there is no geo steering configuration for a region or pool, the load balancer uses pool order to determine failover priority.

### Distribution of traffic within a pool
{:#distribution-of-traffic-within-a-pool}

By default, all traffic is distributed evenly among the origins in the pool using round-robin protocol. This is also true for non-proxied global load balancers.

The origins can be configured with weights, and for proxied global load balancers, the weights determine how much traffic each origin server receives relative to other origins in the pool. Weights are configured as numbers between 0 and 1, and specify what fraction of traffic goes to the origin.

For each origin:

`Percent of traffic to the origin = origin weight / sum of all origin weights`

If all origins have weight `1`, traffic is distributed evenly.

Origins with weight `0` do not receive any traffic for this pool. However, session affinity might still override this until all sessions are closed. If the origin is a member in another pool, it might still receive traffic for that pool.

For example, an origin pool is setup with 3 origins that have the following weights: origin-A: 0.4, origin-B: 0.3, and origin-C: 0.3.

* Initially, all origins are healthy. The amount of traffic each origin receives is: origin-A: 40%, origin-B: 30%, and origin-C: 30%.
* Then origin-A turns critical and it no longer receives traffic. The remaining origins have the same weight, and so traffic is distributed evenly, each receiving 50%.
* The administrator changes the weight for origin-C to `0`. Now 100% of new traffic goes to origin-B. With session-affinity turned on, traffic for existing sessions on origin-C continues to go to origin-C until those sessions close (for a maximum of 24 hours).
* Finally, the weight for origin-B is changed to `0`. The pool no longer receives traffic until origin-A returns to a healthy status or the weights for origin-C and origin-B are set to a non-zero value.

### Fallback pool
{:#fallback-pool}

The origin pool with the lowest priority (the largest number) is the designated "fallback pool." When all pools for a region are down, traffic is routed to the fallback pool, regardless of its health.

When all pools are disabled, the fallback pool is not available.
{:note}

## Proxy modes
{: #proxy-modes}

Load balancers supports DNS-only and HTTP proxy modes. You can have HTTP Proxy and DNS-Only domains in the same load balancer region, but the traffic routing behavior differs as follows:

  * Traffic for domains using HTTP Proxy mode is routed based on the data center associated with the user making the request.
  * Traffic for domains using DNS-Only mode is routed based on the data center associated with the user’s recursive resolver (DNS recursor).

### HTTP Proxy mode
{: #http-proxy-mode}

In HTTP Proxy mode, load balancers have an automatic TTL. {{site.data.keyword.cis_short_notm}} announces IBM IP addresses externally, but protects (mask) your origin server IP addresses. Any changes to your load balancer propagate within seconds inside {{site.data.keyword.cis_short_notm}}, including any failover events.

Setting the load balancer to HTTP Proxy mode offers the following benefits:

* Failover is faster, because external DNS caches that don't respect short DNS TTLs do not impact failover performance.
* The "automatic" TTL (five minutes) reduces the number of authoritative queries made against {{site.data.keyword.cis_short_notm}} without impacting failover performance. 

### DNS-Only mode
{: #dns-only-mode}

In DNS-Only mode, you can configure load balancers to set a TTL from 30 seconds to 10 minutes. {{site.data.keyword.cis_short_notm}} serves the addresses of the healthy origin servers directly, but relies on DNS resolvers respecting the short TTL to re-query the {{site.data.keyword.cis_short_notm}} DNS for an updated list of healthy addresses.

## Session affinity
{:#session-affinity}

Loading a website usually requires fetching multiple assets from a web server. {{site.data.keyword.cis_short_notm}} session affinity minimizes redundant network requests by automatically directing requests from the same client to the same origin web server. {{site.data.keyword.cis_short_notm}} sets a cookie on the initial response to the client. Using the cookie in subsequent client requests ensures those requests are sent to the same origin, unless the origin is unavailable.

When enabled, {{site.data.keyword.cis_short_notm}} session affinity does the following:

* When a client makes its first request, {{site.data.keyword.cis_short_notm}} sets a `CFLib` cookie on the client. The cookie encodes the origin to which the request is forwarded.
* Subsequent requests by the same client are forwarded to that origin for the duration of the cookie and as long as the origin server remains healthy.
* If the cookie expires or the origin server is unhealthy, {{site.data.keyword.cis_short_notm}} sets a new cookie encoding the appropriate failover origin.

All sessions default to 23 hours unless a custom session TTL is specified (in seconds) between 30 minutes and 7 days. A session affinity cookie is required to honor the TTL. The session cookie is secure when `Always Use HTTPS` is enabled. Additionally, `HttpOnly` is always enabled for the cookie to prevent cross-site scripting attacks.

## Health checks
{:#health-checks}

{{site.data.keyword.cis_short_notm}} health checks track the health of pools. They are configured through monitors, which define what type of health check to run and how frequently to run them. {{site.data.keyword.cis_short_notm}} monitors your servers from each of the IBM data centers.

Health checks that result in a status change for an origin server are recorded as events in the load balancer event logs. You can create, attach, and configure health checks from either the global load balancer dashboard or the {{site.data.keyword.cis_short_notm}} API.

### Health check considerations
{:#health-check-notes}

* Availability monitoring checks the health of origin servers every 15 seconds. It reports results via email notifications and the {{site.data.keyword.cis_short_notm}} API.
* The default retry rate is 5 retries per second, and is completely configurable. It is not recommend to increase the retry rate significantly. Retries use exponential backoff (1, 2, 4, 8, and 16 seconds, by default).
* You can configure monitoring for specific URLs by sending periodic HTTP requests to the load balancer, taking advantage of customizable intervals, timeouts, and status codes. After an origin server is marked unhealthy, multi-region failover reroutes traffic to the next available server in failover order.
* Load balancer monitors use the following HTTP user-agent: `"Mozilla/5.0 (compatible; Cloudflare-Traffic-Manager/1.0; +https://www.cloudflare.com/traffic-manager/; pool-id: $poolid)"`. The `$poolid` contains the first 16 characters of the load balancer pool that is the target of the health check.
* To prevent health checks from failing, and to secure user infrastructure against spoofed checks from bad actors, it is recommended that you do the following:
  * Only accept connections to hosts listed in the {{site.data.keyword.cis_short_notm}} IP ranges in your firewall or web-server.
  * Use the {{site.data.keyword.cis_short_notm}} user agent to reject HTTP requests that don't come from these ranges.
  * Ensure that your firewall or web server does not block or rate limit {{site.data.keyword.cis_short_notm}} health checks.
