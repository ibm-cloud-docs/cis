---

copyright:
  years: 2018, 2020
lastupdated: "2020-07-23"

keywords: health checks, origin pools, load balancers, IBM CIS

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


# Working with global load balancers
{:#set-up-and-configure-your-load-balancers}

{{site.data.keyword.cis_full}} provides global load balancing as a service. On your dashboard, you'll see three lists that show the [load balancers](#x2788902){: term}, origin pools, and [health checks](#x4571658){: term}. The lists display the new or updated global load balancer, or one of its components after you've provisioned or updated it. Initially, the lists are empty, and before you create a load balancer you must take a few actions.
{: shortdesc}

{{site.data.keyword.cis_short_notm}} does not support load balancer pools that use a private IP address or a record that resolves to a private IP address.
{:important}

Refer to the [Quick setup](#global-load-balancer-quick-setup) if you already know what to do!

## Adding a health check
{:#add-a-health-check}

Health checks are optional attachments for origin pools. They use a custom repeating interval to probe for a specific response body, or for a status code, to monitor the pool's health. After you create a health check, you can add it to a new or existing origin pool. Navigate to **Reliability > Global Load Balancer > Health Check Events** to see a table of health check events. You can filter by date, health of the pool or origin, pool name, and origin name.

Health check fields:
 * **Monitor type**: The protocol to use for the health check (defaults to HTTP).
 * **Path**: The endpoint path against which to perform the health check (defaults to `/`).
 * **Port**: Click the arrow buttons to increase or decrease the port number.
 * **Description**: Health check description.

Expand the **Advanced options** section to see more settings.

 * **Test interval**: The interval (in seconds) between each health check. Shorter intervals can improve failover time, but increase load on the origins as checks come from multiple locations (defaults to 60).
 * **Method**: The HTTP method to use for the health check (defaults to GET).
 * **Timeout**: The time (in seconds) before marking the health check as failed (defaults to 5).
 * **Number of retries**: The number of retries to attempt in case of a timeout before marking the origin as unhealthy. Retries are attempted immediately (defaults to 2).
 * **Expected Response Code**: The expected HTTP response code or code range of the health check. This value must be between 200-299 with wildcards denoted by an 'x'.
 * **Response Body**: A case-insensitive sub-string to match against in the response body. If this string is not found, the origin is marked as unhealthy.

Expand the **Configure request headers** section to add and configure HTTP request headers to send in the health check.
It is recommended that you set a Host header by default. The `User-Agent` header cannot be overridden.

## Adding a pool
{:#add-a-pool}

At least one pool is required for each provisioned load balancer. Pools group your origins for the load balancer to use.

When creating a pool, two fields are required:
 * **Name**: A short name (tag) for the pool. Only alphanumeric characters, hyphens, and underscores are allowed.
 * **Origins**: The list of origins within this pool. Traffic directed at this pool is balanced across all currently healthy origins, provided the pool itself is healthy.

Additional optional fields:
 * **Health Check**: The health check to use for checking origins within this pool. (defaults to no health check)
 * **Healthy Origin Threshold**: The minimum number of origins that must be healthy for this pool to serve traffic. If the number of healthy origins falls below this number, the pool is marked unhealthy and fails over to the next available pool. (defaults to 1)
 * **Health check region**: Region from which the health check performs monitoring.

   IBM's geographic regions differ from Cloudflare's regions. For details about the geographic regions Cloudflare uses, see "Geo Steering (Enterprise plans only)" in [Traffic steering](https://developers.cloudflare.com/load-balancing/understand-basics/traffic-steering/#geo-steering-enterprise-plans-only){:external}.  
   {:note}

 * **Notification Email**: The email address that should receive health status notifications. This address can be an individual mailbox or a mailing list.
 * **Enabled**: Whether to enable (the default) this pool. Disabled pools do not receive traffic and are excluded from health checks. Disabling a pool causes any load balancers using it to failover to the next pool, if any (default to true).

## Adding a global load balancer
{:#add-a-load-balancer}

Load balancers help to distribute your proxied traffic across multiple origin pools using a round-robin distribution.
{: shortdesc}

When creating a load balancer, the required fields are:
 * **Balancer hostname**: The DNS hostname to associate with your load balancer. If this hostname already exists as a DNS record in IBM's DNS, the load balancer takes precedence and the DNS record is not used.
 * **Default origin pools**: A list of pool IDs. The list is ordered by their failover priority. Pools defined here are used by default, or when region pools are not configured for a given region.

Optionally, you can configure the following fields:
 * **Proxy**: Route traffic through IBM's performance and metrics service.
 * **Session Affinity**: Always route through the same performance and metrics instance. This option is available only if proxy is enabled.
 * **TTL**: Time-to-live (TTL) of the DNS entry for the IP address returned by this load balancer. This option applies only to unproxied load balancer; otherwise, it defaults to `Automatic`.
 * **Geo routes**: A mapping of region or country codes to a list of pools (ordered by their failover priority) for the given region. Any regions not explicitly defined fall back to using the default pools.

   IBM's geographic regions differ from Cloudflare's regions. For details about the geographic regions Cloudflare uses, see "Geo Steering (Enterprise plans only)" in [Traffic steering](https://developers.cloudflare.com/load-balancing/understand-basics/traffic-steering/#geo-steering-enterprise-plans-only){:external}.  
   {:note}

### Global load balancer quick setup
{:#global-load-balancer-quick-setup}

You can directly create pools and health checks from the **Create Load Balancer** menu option. Navigate to **Reliability > Global Load Balancer > Create load balancer > Add pool**, then select **Create New** from the Origin pool list.
{: shortdesc}

Input a pool name, [origins](#x2210603){:term}, and select a health check. You can create a new health check here by choosing **Create New** in the **Health Check** list menu, and entering the information to create the health check.

## Editing or deleting a global load balancer
{:#edit-delete-load-balancer}

To edit or delete a load balancer, or one of its components, click the overflow menu ![overflow icon](/images/horizontal-overflow-icon.png) located on the right of the row.

The following options are provided for each list.

* Health Check
  * **View health check**: Shows a short summary of the health check with a link that takes you to the edit flow.
  * **Edit health check**: Redirects the user to the edit flow.
  * **Delete health check**: Shows the confirmation dialog box for the deletion flow.

* Origin Pools
  * **View pool details**: Shows a modal dialog box with information about the pool.
  * **Edit pool**: Redirects the user to the edit flow.
  * **Delete pool**: Shows the confirmation dialog box for the deletion flow.

* Load Balancers
  * **Edit load balancer**: Redirects to the edit flow.
  * **Delete load balancer**: Brings up the confirmation dialog box for the deletion flow.
