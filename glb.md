---

copyright:
  years: 2018, 2019
lastupdated: "2019-10-31"

keywords: origin server, pool implementation, origin servers

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Global Load Balancer (GLB) Concepts
{:#global-load-balancer-glb-concepts}

This document contains some concepts and definitions related to the Global Load Balancer (GLB) and how it affects your {{site.data.keyword.cis_full}} deployment.
{: shortdesc}

## Global Load Balancer
{:#global-load-balancer-cis}

The Global Load Balancer (GLB) manages traffic across server resources located in multiple regions. The origin server can serve up all of the content for a website, provided that the web traffic does not extend beyond the server's processing capabilities and latency is not a primary concern. The GLB utilizes a _pool_ implementation that allows for the traffic to be distributed to multiple origins. This pool capability provides many benefits including:

  * Minimizes response time
  * Creates higher availability through redundancy
  * Maximizes traffic throughput

The GLB routes traffic to the pool with the highest priority, distributing the load among its origin servers. See the following _Pool_ section for how traffic is distributed within a pool. If the primary pool becomes unavailable, traffic is routed automatically to the next pool in the list based on priority.

If pools are set up for specific regions, traffic from those regions is sent to the pools for the specified region first. Only if all pools for a given region are down will traffic fall back to the default pools. In this case the fallback pool is the pool with the lowest priority.

### How it works
{:#how-glb-works}
When the GLB is created a DNS record is automatically added for it with the name of the load balancer. The GLB then returns one of the origin IP addresses to a client making a DNS request.

For example, an origin pool is created with two origins identifying IP addresses `169.61.244.18` and `169.61.244.19`. If a global load balancer is created with the name **`glbcust.ibmmo.com`** using the origin pool, then a client on the internet can execute the command:
```
$ ping glbcust.ibmom.com
PING glbcust.ibmom.com (169.61.244.18): 56 data bytes
```
{:pre}

In this example, {{site.data.keyword.cis_short_notm}}:

   * created a DNS record named `glbcust.ibmmo.com`
   * used the GLB to resolve the DNS name to one of the IP addresses identified in the origin pool

Notice that the global load balancer does not terminate the TCP connection.
{:note}

Setting a DNS element or GLB to "proxy" changes the behavior.
If, for example, you turn on proxy and **Security > TLS > Mode** to something besides `Off`, the {{site.data.keyword.cis_short_notm}} now terminates the TCP connection and establishes a second connection between {{site.data.keyword.cis_short_notm}} and the originator.

In this example, {{site.data.keyword.cis_short_notm}}:

  * created a DNS record named: `glbcust.ibmmo.com`
  * used the GLB to resolve the DNS name to a {{site.data.keyword.cis_short_notm}} provided IP address

Now, connections to `glbcust.ibmmo.com` are terminated by {{site.data.keyword.cis_short_notm}}, and HTTPS certificates are hosted by {{site.data.keyword.cis_short_notm}} (which is required for TCP termination).

After the client connects to the application the picture looks like this:

`[client]<--tls-->[cis]<-->[origin server]`


## Pool
{:#glb-pools}

A pool is a group of origin servers that traffic is intelligently routed to when attached to a GLB. The minimum number of available origin servers for the pool to be marked healthy is configurable by the user along with which specific health check to use. The origin pool can be associated with a specific region or it can be made available to all regions.

### Distribution of traffic within a pool
{:#distribution-of-traffic-within-a-pool}

By default, all traffic is distributed evenly among the origins in the pool using round-robin protocol. This is also true for non-proxied GLBs.

The origins can be configured with weights, and for proxied GLBs, the weights determine how much traffic each origin server receives relative to other origins in the pool. Weights are configured as numbers between 0 and 1, and specify what fraction of traffic will go to the origin.

For each origin:

` Percent of traffic to the origin = origin weight / sum of all origin weights`

If all origins have weight `1`, traffic is distributed evenly.

Origins with weight `0` do not receive any traffic for this pool. However, session affinity might still override this until all sessions are closed. If the origin is a member in another pool, it might still receive traffic for that pool.

**Example:**

An origin pool is setup with 3 origins that have the following weights: origin-A: 0.4, origin-B: 0.3, and origin-C: 0.3.

* Initially, all origins are healthy. The amount of traffic each origin receives is: origin-A: 40%, origin-B: 30%, and origin-C: 30%.
* Then origin-A turns critical; it no longer receives traffic. The remaining origins have the same weight and therefore traffic is distributed evenly, each receiving 50%.
* The administrator changes the weight for origin-C to `0`. Now 100% of new traffic goes to origin-B. But with session-affinity turned on, traffic for existing sessions on origin-C continues to go to origin-C until those sessions close (max. 24 hours).
* Finally, the weight for origin-B is changed to `0`. The pool will no longer receive traffic until origin-A returns to a healthy status or the weights for origin-C and origin-B are set to a non-zero value.

### Fallback Pool
{:#fallback-pool}

The origin pool with the lowest priority (the largest number) is the designated "fallback pool." When all pools for a given region are down, traffic is routed to the fallback pool, regardless of its health.

When all pools are disabled, the fallback pool is not available.
{:note}

## Health Check
{:#cis-health-check}

A health check helps gain insight into the availability of pools so that traffic can be routed to the healthy ones. These checks periodically send HTTP, HTTPS, or TCP requests and monitor the responses. They can be configured with a customized port, interval, timeout, status code, and more. As soon as a pool is marked unhealthy, traffic is intelligently rerouted to another available pool.
Be aware that your logs have references to Cloudflare because of IBM's partnership with Cloudflare to power {{site.data.keyword.cis_short_notm}}.
{:note}

### Health Check Events
{:#health-check-events}

Health Check Events are status changes from pools with connected health checks and their associated origin servers. If an origin's status degrades, a new item appears in a table, with the event's description. Navigate to **Reliability > Global Load Balancer > Health Check Events** to see a table of Health Check Events. You can filter by date, health of the pool or origin, pool name, and origin name by selecting the filter parameters from the list menus. Columns within the table are sortable by clicking on the column name.
![Health Check Events table](images/health-check-events-table.png)

Individual rows within the table expand with more information about the entry. If the pool is healthy, only the **Pool Details** tile is visible. When the row has an origin that is critical, or a pool that is degraded, the **Affected Origin Details** tile also appears.

![Health Check Events details](images/health-check-events-details.png)

#### Pool Details:
* Pool Name - Name of the pool
* Healthy Origins - Ratio of health origins/total origins in a pool
* Healthy Threshold - Number of origins that need to be healthy in order to consider the pool healthy
* Healthy Origins - Names of the health origins
* Critical Origins - Names of the unhealthy origins

#### Affected Origin Details:
* Origin Name - Name of the origin
* Origin Address - Address of the origin
