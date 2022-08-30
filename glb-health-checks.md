---

copyright:
  years: 2020
lastupdated: "2020-10-30"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Setting up health checks
{: #glb-features-healthchecks}

A health check helps gain insight into the availability of pools so that traffic can be routed to the healthy ones.
{: shortdesc}

These checks periodically send HTTP, HTTPS, or TCP requests and monitor the responses. They can be configured with a customized port, interval, timeout, status code, and more. As soon as a pool is marked unhealthy, traffic is intelligently rerouted to another available pool.

Be aware that your logs have references to Cloudflare because IBM is partnering with Cloudflare to provide {{site.data.keyword.cis_short_notm}}.
{: note}

{{site.data.keyword.cis_short_notm}} health checks track the health of pools. They are configured through monitors, which define what type of health check to run and how frequently to run them. {{site.data.keyword.cis_short_notm}} monitors your servers from each of the IBM data centers.

Health checks that result in a status change for an origin server are recorded as events in the load balancer event logs. You can create, attach, and configure health checks from either the global load balancer dashboard or the {{site.data.keyword.cis_short_notm}} API.

## Health check considerations
{: #health-check-notes}

* Availability monitoring checks the health of origin servers every 15 seconds. It reports results via email notifications and the {{site.data.keyword.cis_short_notm}} API.
* The default retry rate is 5 retries per second, and is completely configurable. It is not recommend to increase the retry rate significantly. Retries use exponential backoff (1, 2, 4, 8, and 16 seconds, by default).
* You can configure monitoring for specific URLs by sending periodic HTTP requests to the load balancer, taking advantage of customizable intervals, timeouts, and status codes. After an origin server is marked unhealthy, multi-region failover reroutes traffic to the next available server in failover order.
* Load balancer monitors use the following HTTP user-agent: `"Mozilla/5.0 (compatible; Cloudflare-Traffic-Manager/1.0; +https://www.cloudflare.com/traffic-manager/; pool-id: $poolid)"`. The `$poolid` contains the first 16 characters of the load balancer pool that is the target of the health check.
* To prevent health checks from failing, and to secure user infrastructure against spoofed checks from bad actors, it is recommended that you do the following:
    * Only accept connections to hosts listed in the {{site.data.keyword.cis_short_notm}} IP ranges in your firewall or web-server.
    * Use the {{site.data.keyword.cis_short_notm}} user agent to reject HTTP requests that don't come from these ranges.
    * Ensure that your firewall or web server does not block or rate limit {{site.data.keyword.cis_short_notm}} health checks.


## Health check events
{: #health-check-events}

Health Check Events are status changes from pools with connected health checks and their associated origin servers. If an origin's status degrades, a new item appears in a table, with the event's description.
