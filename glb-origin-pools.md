---

copyright:
  years: 2020, 2026
lastupdated: "2026-06-05"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Setting up origin pools
{: #glb-features-pools}

An origin pool is a group of origin servers that receive traffic from a global load balancer. Origins can be identified by IP address or hostname, and pools can be associated with a specific region or made available globally.
{: shortdesc}

You can configure the minimum number of healthy origins that must be available for a pool to be considered healthy, as well as the health check used to monitor the pool.

If you're familiar with DNS terminology, think of a pool as a record set, except that only healthy origins are returned. You can configure multiple pools and define their failover priority.

* When adding origin servers to a pool, you can identify the origin by hostname or IP address.
* The order of pools in the load balancer determines the standard failover priority. When the number of healthy origins in a pool drops below the configured threshold, the load balancer routes traffic to the next available pool.
* By default, pools are ordered by date created. You can reorder them from the global load balancer dashboard and by using {{site.data.keyword.cis_short_notm}} API (use the Update Pools command to set a new `origins` array).
* Dynamic steering uses Round Trip Time (RTT) profiles to determine pool priority. If there is no RTT data for a pool in a region or colocation center, the load balancer uses pool order to determine failover priority.
* Geo steering directs traffic to pools based on the client’s region or point of presence. If there is no geo steering configuration for a region or pool, the load balancer uses pool order to determine failover priority.

## Distribution of traffic within a pool
{: #distribution-of-traffic-within-a-pool}

By default, traffic is distributed evenly among the origins in the pool using a round-robin algorithm. This is also true for non-proxied global load balancers.

The origins can be configured with weights, and for proxied global load balancers, the weights determine how much traffic each origin server receives relative to other origins in the pool. Weights are configured as decimal values between 0 and 1, and specify what fraction of traffic goes to the origin.

For each origin:

`Percent of traffic to the origin = origin weight / sum of all origin weights`

If all origins have weight `1`, traffic is distributed evenly.

Origins with weight `0` do not receive any traffic for this pool. However, session affinity might still override this until all sessions are closed. If the origin is a member in another pool, it might still receive traffic for that pool.

For example, an origin pool is set up with 3 origins that have the following weights: origin-A: 0.4, origin-B: 0.3, and origin-C: 0.3.

* Initially, all origins are healthy. The amount of traffic each origin receives is: origin-A: 40%, origin-B: 30%, and origin-C: 30%.
* Then origin-A turns critical and it no longer receives traffic. The remaining origins have the same weight, and so traffic is distributed evenly, each receiving 50%.
* The administrator changes the weight for origin-C to `0`. Now 100% of new traffic goes to origin-B. With session-affinity turned on, traffic for existing sessions on origin-C continues to go to origin-C until those sessions close (for a maximum of 24 hours).
* Finally, the weight for origin-B is changed to `0`. The pool no longer receives traffic until origin-A returns to a healthy status or the weights for origin-C and origin-B are set to a non-zero value.

## Fallback pool
{: #fallback-pool}

A fallback pool is the lowest-priority pool in a load balancer configuration. It receives traffic when higher-priority pools are unavailable and can also receive traffic during normal operation depending on the selected traffic-steering mode. It is not limited to error handling.

Traffic distribution to a fallback pool depends on the configured traffic‑steering mode and the priority that is assigned to each pool. Under certain configurations, the fallback pool can receive traffic even when other pools are healthy.

The fallback pool is defined as the origin pool with the lowest priority, which is represented by the highest numerical value. This designation determines its role when other pools become unavailable. When all primary pools for a region are unavailable, traffic is directed to the fallback pool. This routing occurs regardless of the fallback pool’s health state.

If all pools are disabled, the fallback pool is not available.
{: note}
