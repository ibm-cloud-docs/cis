---

copyright:
  years: 2018
lastupdated: "2018-04-12"

---

# Global Load Balancer (GLB) Concepts

This document contains some concepts and definitions related to the Global Load Balancer (GLB) and how it affects your IBM CIS deployment.

## Global Load Balancer

The Global Load Balancer (GLB) manages traffic across server resources located in multiple regions. The GLB utilizes a pool which allows for the traffic to be distributed to multiple origins. This provides many benefits including:

  * Minimize response time
  * Higher availability through redundancy
  * Maximize traffic throughput

The GLB routes traffic to the pool with the highest priority and distributes the load among its origin evenly, using round-robin protocol. If the primary pool becomes unavailable, traffic is routed automatically to the next pool in the list based on priority.

If pools are set up for specific regions, traffic from those regions is sent to the pools for the specified region first. Only if all pools for a given region are down will traffic fall back to the default pools. In this case the fallback pool is the pool with the lowest priority. 

## Pool

A pool is a group of origin servers that traffic is intelligently routed to when attached to a GLB. The minimum number of available origin servers for the pool to be marked healthy is configurable by the user along with which specific health check to use. The origin pool can be associated with a specific region or it can be made available to all regions.

## Health Check

A health check helps gain insight into the availability of pools so that traffic can be routed to the healthy ones. These checks periodically send HTTP/HTTPS requests and monitor the responses. They can be configured with customized intervals, timeouts, status codes, and more. As soon as a pool is marked unhealthy, traffic will be intelligently rerouted to another available pool, if available.
**Note**: Be aware that your logs have references to Cloudflare because of IBM's partnership with Cloudflare to power CIS.

### Health Check Events
Health Check Events are status changes from pools with connected health checks and their associated origin servers. If an origin's status degrades, a new item appears in a table, with the event's description. Navigate to **Reliability > Global Load Balancer > Health Check Events** to see a table of Health Check Events. You can filter by date, health of the pool or origin, pool name, and origin name by selecting the filter parameters from the drop down menus. Columns within the table are sortable by clicking on the column name.
![Health Check Events table](images/health-check-events-table.png)

Individual rows within the table expand with more information about the entry. If the pool is healthy, only the **Pool Details** tile is visible. When the row has an origin that is critical, or a pool that is degraded, the **Affected Origin Details** tile also appears. 

![Health Check Events details](images/health-check-events-details.png)

#### Pool Details:
* Pool Name - Name of the pool
* Healthy Origins - ratio of health origins/total origins in a pool
* Healthy Threshold - number of origins that need to be healthy in order to consider the pool healthy
* Healthy Origins - names of the health origins
* Critical Origins - names of the unhealthy origins

#### Affected Origin Details:
* Origin Name - Name of the origin
* Origin Address - Address of the origin
