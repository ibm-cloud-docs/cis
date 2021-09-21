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


# Setting up origin pools
{: #glb-features-pools}

An origin pool is a group of origin servers that traffic is intelligently routed to when attached to a global load balancer. 
{: shortdesc}

The minimum number of available origin servers for the pool to be marked healthy is configurable by the user along with which specific health check to use. The origin pool can be associated with a specific region or it can be made available to all regions.

A {{site.data.keyword.cis_short_notm}} load balancer pool represents a group of origin servers, each identified by their IP address or hostname. You can configure multiple pools, as well as failover priority (Pool A > Pool B > Pool C). If you're familiar with DNS terminology, think of a pool as a "record set", except that only addresses that are considered healthy are returned. You can attach health checks to individual pools to tailor monitoring for collections of origin servers.

* When adding origin servers to a pool, you can identify the origin by hostname or IP address.
* The order of pools in the load balancer determines the standard failover priority. When the number of healthy origins in a pool drops below the configured threshold, the load balancer routes traffic to the next available pool.
* By default, pools are ordered by date created. You can reorder them from the global load balancer dashboard and via {{site.data.keyword.cis_short_notm}} API (use the Update Pools command to set a new `origins` array).
* Dynamic steering uses Round Trip Time (RTT) profiles to determine pool priority. If there is no RTT data for a pool in a region or colocation center, the load balancer uses pool order to determine failover priority.
* Geo steering directs traffic to pools based on the client’s region or point of presence. If there is no geo steering configuration for a region or pool, the load balancer uses pool order to determine failover priority.

## Distribution of traffic within a pool
{: #distribution-of-traffic-within-a-pool}

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

## Fallback pool
{: #fallback-pool}

The origin pool with the lowest priority (the largest number) is the designated "fallback pool." When all pools for a region are down, traffic is routed to the fallback pool, regardless of its health.

When all pools are disabled, the fallback pool is not available.
{: note}
