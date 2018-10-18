---

copyright:
  years: 2018
lastupdated: "2018-04-12"

---

# Global Load Balancer (GLB) Concepts

This document contains some concepts and definitions related to the Global Load Balancer (GLB) and how it affects your IBM CIS deployment.

## Global Load Balancer

The Global Load Balancer (GLB) manages traffic across server resources located in multiple regions. The origin server can serve up all of the content for a website, provided that the web traffic does not extend beyond the server's processing capabilities and latency is not a primary concern. The GLB utilizes a _pool_ implementation that allows for the traffic to be distributed to multiple origins. This pool capability provides many benefits including:

  * Minimizes response time
  * Creates higher availability through redundancy
  * Maximizes traffic throughput

The GLB routes traffic to the pool with the highest priority, distributing the load among its origin servers. See the following _Pool_ section for how traffic is distributed within a pool. If the primary pool becomes unavailable, traffic is routed automatically to the next pool in the list based on priority.

If pools are set up for specific regions, traffic from those regions is sent to the pools for the specified region first. Only if all pools for a given region are down will traffic fall back to the default pools. In this case the fallback pool is the pool with the lowest priority. 

## Pool

A pool is a group of origin servers that traffic is intelligently routed to when attached to a GLB. The minimum number of available origin servers for the pool to be marked healthy is configurable by the user along with which specific health check to use. The origin pool can be associated with a specific region or it can be made available to all regions.

### Distribution of traffic within a pool

By default, all traffic is distributed evenly among the origins in the pool using round-robin protocol. This is also true for non-proxied GLBs.

The origins can be configured with weights, and for proxied GLBs, the weights determine how much traffic each origin server receives relative to other origins in the pool. Weights are configured as numbers between 0 and 1, and specify what fraction of traffic will go to the origin. 

For each origin: 

` Percent of traffic to the origin = origin weight / sum of all origin weights`

If all origins have weight `1`, traffic is distributed evenly. 

Origins with weight `0` do not receive any traffic for this pool. However, session affinity might still override this until all sessions are closed. If the origin is a member in another pool, it might still receive traffic for that pool.

**Example:** 

An origin pool is setup with 3 origins that have the following weights: origin-A: 0.4, origin-B: 0.3, and origin-C: 0.3. 

* Initially, all origins are healthy. The amount of traffic each origin receives is: origin-A: 40%, origin-B: 30%, and origin-C: 30%.
* Then origin-A turns critical; it no longer receives traffic. The remaining origins have the same weight and therefore traffic is distributed evently, each receiving 50%.
* The administrator changes the weight for origin-C to `0`. Now 100% of new traffic goes to origin-B. But with session-affinity turned on, traffic for existing sessions on origin-C continues to go to origin-C until those sessions close (max. 24 hours).

## Health Check

A health check helps gain insight into the availability of pools so that traffic can be routed to the healthy ones. These checks periodically send HTTP, HTTPS, or TCP requests and monitor the responses. They can be configured with a customized port, interval, timeout, status code, and more. As soon as a pool is marked unhealthy, traffic is intelligently rerouted to another available pool.
**Note**: Be aware that your logs have references to Cloudflare because of IBM's partnership with Cloudflare to power CIS.

### Health Check Events
Health Check Events are status changes from pools with connected health checks and their associated origin servers. If an origin's status degrades, a new item appears in a table, with the event's description. Navigate to **Reliability > Global Load Balancer > Health Check Events** to see a table of Health Check Events. You can filter by date, health of the pool or origin, pool name, and origin name by selecting the filter parameters from the drop down menus. Columns within the table are sortable by clicking on the column name.
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
