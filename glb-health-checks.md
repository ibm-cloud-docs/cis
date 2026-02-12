---

copyright:
  years: 2020, 2026
lastupdated: "2026-02-12"

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

Good call — combining them makes it cleaner and avoids artificial separation between “create” and “attach,” since users conceptually think of this as one task.

Below is a **single, cohesive IBM Docs–style procedure** you can drop into the topic.

---

# Creating and attaching a health check in the console
{: #create-attach-health-check-ui}
{: ui}

To set up a health check, create a monitor and attach it to a load balancer pool.

## Before you begin
{: #before-you-begin-health-check}

Ensure you meet the following prerequisites: 

* A {{site.data.keyword.cis_short_notm}} instance is provisioned.
* At least one load balancer pool exists.
* Origin servers are added to the pool.

To create and attach a health check in the console, follow these steps:

1. In the {{site.data.keyword.cis_short_notm}} console, select your instance.
1. Go to **Load Balancing > Monitors**.
1. Click **Create monitor**.
1. Enter a **Name** for the monitor.
1. Select a **Type**:
   * **HTTP**
   * **HTTPS**
   * **TCP**
   * **ICMP**
1. Configure the monitor settings based on the selected type:
   * **Port** (if different from the default)
   * **Path** (for HTTP or HTTPS)
   * **Method** (GET or HEAD)
   * **Expected status codes**
   * **Interval**
   * **Timeout**
   * **Retry count**

1. Click **Create**.
1. Go to **Load Balancing > Pools**.
1. Select the pool that you want to monitor, then click **Edit**.
1. In the **Health monitor** section, select the monitor that you created.
1. Click **Save**.

After the monitor is attached, {{site.data.keyword.cis_short_notm}} begins checking the health of each origin server in the pool. If an origin fails the configured number of health checks, it is marked unhealthy and traffic is routed to healthy origins based on your traffic steering configuration. 

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

## Monitoring health check failures with alert policies
{: #monitor-health-check-failures-with-alert-policies}

Enterprise plan users can configure alert policies to receive notifications when load balancer health checks fail.

To create an alert policy:

1. Fron the CIS console, go to **Account > Alerts**. 
1. In the Alerting policies view, click **Create** to create an alert policy.
1. Select the appropriate load balancer health metrics.
1. Configure notification channels.

For more information, see [Configuring CIS alert policies](/docs/cis?topic=cis-configuring-policies&interface=ui).

## Supported health check types
{: #health-check-types-supported}

| Type            | Description                                                   |
| --------------- | ------------------------------------------------------------- |
| **HTTP      | Sends HTTP requests and validates response codes and content. |
| HTTPS       | Sends HTTPS requests and validates TLS-secured responses.     |
| TCP         | Verifies that a TCP connection can be established.            |
| ICMP (Ping) | Verifies host reachability using ICMP echo requests.          |

Depending on the selected monitor type, additional configuration options might be available, such as:

* HTTP method (GET, HEAD)
* Expected response codes
* Request path
* Host header override
* Timeout
* Interval
* Retry count

Choose the monitor type that best matches your application protocol and availability requirements.
