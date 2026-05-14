---

copyright:
  years: 2018, 2026
lastupdated: "2026-05-14"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Creating global load balancers
{: #configure-glb}

If you have an e-commerce website or host an application that must remain accessible, you're likely concerned about its availability and performance.{: shortdesc}

Global load balancer capabilities available with {{site.data.keyword.cis_full_notm}} ({{site.data.keyword.cis_short_notm}}) help improve application reliability and scalability while delivering the best possible user experience.

A global load balancer distributes user traffic across multiple geographic regions to improve availability and performance.

You can configure a global load balancer by using the console, CLI, API, or Terraform.

## Before you begin
{: #before-you-create-glbs}

* Provision a {{site.data.keyword.cis_short_notm}} instance.
* Configure your domain in {{site.data.keyword.cis_short_notm}}.
* Identify the IP addresses or FQDNs for your application origins.

{{site.data.keyword.cis_short_notm}} can support load balancer pools that use a private IP address. However, private IP pools don't support proxy services or health checks; only DNS-based load balancing is supported. For pools with public IPs, health checks can be configured as described in ([Step 1: Create a health check](#create-health-check)).
{: important}

## Quick setup
{: #quick-setup}
{: ui}

If you already know your pools and health checks, you can create them inline when you create a load balancer:

1. In the CIS console, click **Reliability > Global load balancers > Origin pools**, then click **Create**.
1. Input a pool name, origins, and select a health check.

   You can create a new health check here by selecting **Create new** in the Health Check list menu and completing the information.

1. Click **Save**.

The following steps provide the full procedure for creating health checks, pools, and a global load balancer.

## Creating a global load balancer in the console
{: #configure-load-bal-ui}
{: ui}

When you open the Global load balancers page (**Reliability > Global load balancers**), the page shows tabs for [Load balancers](#x2788902){: term}, Origin pools, [Health checks](#x4571658){: term}, and Events. These tabs display global load balancers and their components as you create or update them.

In the following step-by-step procedure, learn how to configure a setup similar to the following diagram. In this example, application resources are deployed in two data centers (US West and US East), with users accessing the application globally. Users might be accessing this application from all over the world.

To create and configure a global load balancer in the console, follow these steps:

### Step 1: Create a health check (optional)
{: #create-health-check}

Health checks are optional attachments for origin pools. They run at a configurable interval to check for a specific response body or status code and monitor pool health. After you create a health check, you can add it to a new or existing origin pool.

If you don't define any custom health checks, CIS uses `/` as your default health check path.
{: note}

1. In the CIS console, click **Reliability > Global load balancers > Health checks**, then click **Create**.
1. Configure the following fields:

   * **Name**: Name of the health check.
   * **Monitor type**: The protocol to use for the health check. (Default: `HTTP`).
   * **Port**: Click the arrows to increase or decrease the port number.
   * **Path**: The endpoint path against which to perform the health check. (Default: `/`)

1. Expand **Advanced options** to configure:

   * **Test interval**: The interval (in seconds) between each health check. Shorter intervals can improve failover time, but increase load on the origins as checks come from multiple locations. (Default: `60`).
   * **Method**: The HTTP method to use for the health check. (Default: `GET`)
   * **Timeout (seconds)**: The time before marking the health check as failed. (Default: `5`)
   * **Number of retries**: The number of retries to attempt if there is a timeout before marking the origin as unhealthy. CIS attempts retries immediately. (Default: `2`)
   * **Expected response codes**: The expected HTTP response code or code range of the health check. This value must be between 200-299 with wildcards that are denoted with an `x`.
   * **Response body**: A case-insensitive substring to match against in the response body. If CIS does not find this string, it marks the origin as unhealthy.
   * **Healthy threshold**: The number of consecutive successful health check responses that CIS must receive before marking an origin as healthy. This setting prevents CIS from marking an origin healthy after a single successful probe and helps avoid flapping during intermittent recovery. (Default: `1`)
   * **Unhealthy threshold**: The number of consecutive failed health check responses that must occur before CIS marks an origin as unhealthy. This setting helps prevent temporary network or application issues from immediately triggering failover. (Default: `1`)
   * **Follow redirects**: Determines whether the health check automatically follows HTTP 3xx redirect responses. When enabled, the health check continues to the redirected location and evaluates the final response against the configured success criteria (status code and optional response body). When disabled, redirect responses are evaluated directly against the expected response codes.

1. Expand **Configure request headers (optional)** to add and configure HTTP request headers to send in the health check.

   It is recommended that you set a Host header by default. The `User-Agent` header can't be overridden.

1. Click **Create** to complete your health check configuration.

### Step 2: Create an origin pool
{: #create-origin-pool-glb}

At least one pool is required for each provisioned load balancer. Pools group origins for the load balancer to use.

1. In the CIS console, click **Reliability > Global load balancers > Origin pools**, then click **Create**.
1. Select whether to enable this pool. Disabled pools don't receive traffic and CIS excludes them from health checks. When you disable a pool, any load balancers that use it fail over to the next pool, if any.
1. Configure the required fields:

   * **Name**: A short name (tag) for the pool. Only alphanumeric characters, hyphens, and underscores are allowed.
   * **Origins**: The list of origins within this pool. CIS balances traffic directed at this pool across all currently healthy origins, provided the pool itself is healthy.

   If your application servers sit behind a local load balancer, such as an {{site.data.keyword.cloud_notm}} load balancer, then add your load balancer’s FQDN or virtual IP as your origin instead of adding your individual servers.
   {: note}

1. Configure optional fields as needed:

   * **Healthy origin threshold**: The minimum number of origins that must be healthy for this pool to serve traffic. If the number of healthy origins falls below this number, CIS marks the pool as unhealthy and fails over to the next available pool. (Default: `1`)
   * **Pool health check region**: Region from which the health check performs monitoring.
   * **Health check**: The health check to use for checking origins within this pool. (Default: **No health check**)

1. Click **Save** to complete origin pool configuration.

The origin pool initially appears as **Unhealthy**. This state changes to **Healthy** after a successful health check by CIS. You might need to refresh your browser to see the state change.
{: note}

Define as many origin pools as the number of application farms that you have. These farms might be within the same or different geographic regions.

### Step 3: Configure the global load balancer
{: #global-load-balancer-configuration}

Load balancers help to distribute traffic across multiple origin pools.

1. In the CIS console, click **Reliability > Global load balancers > Load balancers**, then click **Create**.
1. Enable the load balancer.
1. For Proxy, determine whether traffic flows through the security and performance functions on CIS. 'Off' bypasses these systems.
1. Configure the following information:

   * **Name (optional)**: The name to associate with your load balancer.
   * **TTL**: Time-to-live (TTL) of the DNS entry for the IP address returned by this load balancer. This option applies only to unproxied load balancer; otherwise, it defaults to `Automatic`.
   * **Traffic steering**: Controls how incoming user requests are distributed across your configured origin pools by determining the algorithm CIS uses to decide which data center (pool) serves each request. For more information, see [Optimizing traffic steering](/docs/cis?topic=cis-traffic-steering&interface=ui).
   * **Session Affinity**: Always route through the same performance and metrics instance. This option is available only if **Proxy** is enabled.
   * **Geo routes**: A mapping of region or country codes to a list of pools (ordered by their failover priority) for the specified region. Any regions not explicitly defined fall back to using the default pools.

     IBM's geographic regions differ from the regions that {{site.data.keyword.cis_short_notm}} uses. For details about the geographic regions, see "Geo Steering" in [Traffic steering](https://developers.cloudflare.com/load-balancing/understand-basics/traffic-steering/steering-policies/geo-steering/){: external}.
     {: note}

1. Click **Create** to complete the global load balancer configuration.

### Step 4: Verify connectivity
{: #global-load-balancer-verify-connectivity}

Finally, verify connectivity to your application by accessing the FQDN URL in a browser.

For more information about updating and deleting global load balancers, health checks, and origin pools in the console, see [Managing global load balancers](/docs/cis?topic=cis-glb-features).
{: note}
