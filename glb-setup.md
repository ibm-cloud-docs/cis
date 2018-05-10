---
copyright:
  years: 2018
lastupdated: "2018-05-08"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Set up and configure your load balancers
 
 IBM CIS provides global load balancing as a service.

![IMAGE](images/glb-screen.png)

## GLB Dashboard
On your dashboard, you'll see three lists that show the load balancers, origin pools, and health checks. The lists display the new or updated global load balancer or one of its components after you've provisioned or updated it. Initially the lists are empty, and before you create a load balancer you must take a few actions.

### GLB Quick setup
You can directly create pools and health checks from the **Create Load Balancer** menu option. Navigate to **Reliability > Global Load Balancer > Create load balancer > Add pool**, and select the option to **Create New** under Origin pool. 

![IMAGE](images/create-new-origin-pool.png)

Input a pool name, origins, and select a health check. You can create a new health check here by choosing **Create New** in the Health Check dropdown menu, and entering the information to create the health check. 

For fully configurable options, use the longer setup method in the sections that follow. 

### Create
**Note**: <sup>`*`</sup> indicates this step is optional

1) <sup>`*`</sup>Create a health check, click **Create health check**.
  ![IMAGE](images/glb-health-check-list.png)
    <ul>
      <li><b>Path</b>: The endpoint path to health check against.</li> 
      <li><b>Type</b>: The protocol to use for the health check.</li>
      <li><b>Description</b>: User provided description.</li>
    </ul>

2) Create a pool, click **Create pool**. 
  ![IMAGE](images/glb-pool-list.png)
    <ul>
      <li><b>Health</b>: Status of the pool.</li>
      <li><b>Name</b>: User provided name.</li>
      <li><b>Origins</b>: Count of healthy origins in the pool.</li>
      <li><b>Health Check</b>: Path of the attached health check, if any.</li>
    </ul>

3) Create a load balancer, click **Create load balancer**.
  ![IMAGE](images/glb-load-balancer-list.png)
    <ul>
      <li><b>Health</b>: Status of the load balancer.</li>
      <li><b>Hostname</b>: Name prepended to the domain name.</li>
      <li><b>Available Pools</b>: Count of healthy pools.</li>
      <li><b>TTL</b>: Time To Live.</li>
      <li><b>Proxy</b>: Enable or disable proxy traffic flow.</li>
      <li><b>Status</b>: Enable or disable the load balancer.</li>
    </ul>

**Note**: IBM's geographic regions differ from Cloudflare's regions. For details about the geographic regions Cloudflare uses, see [Load Balancing: Geographic Regions ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://support.cloudflare.com/hc/en-us/articles/115000540888-Load-Balancing-Geographic-Regions){:new_window}.     

### Edit/Delete
To edit or delete a load balancer or one of its components click the overflow menu button located on the far right of each row.

Overflow menu button:

![IMAGE](images/overflow.png)

The following options are provided for each list.

* Health Check
    * **View health check**: This option shows a short summary of the health check, with a link that takes you to the edit flow.
    * **Edit health check**: This option redirects the user to the edit flow. 
    * **Delete health check**: This option brings up the confirmation dialog box for the deletion flow.

* Pool
    * **View pool details**: This option brings up a modal dialog box with information about the pool.
    * **Edit pool**: This option redirects the user to the edit flow.
    * **Delete pool**: This option brings up the confirmation dialog box for the deletion flow.

* Load Balancer
    * **Disable/Enable**: Enable or disable a load balancer.
    * **Edit load balancer**: Redirects to the edit flow. 
    * **Delete load balancer**: Brings up the confirmation dialog box for the deletion flow.

## Add a Health Check

Health checks are optional attachments for origin pools. They use a custom repeating interval to probe for a specific response body, or for a status code, to monitor the pool's health. Once created, health checks can be added to a new or an existing origin pool.

When creating a health check, only one field is required:
 * **Reponse Code**: The expected HTTP response code or code range of the health check. This value must be between 200-299 with wildcards denoted by an 'x'.

Additional optional fields:
 * **Path**: The endpoint path against which to perform the health check (defaults to /).
 * **Type**: The protocol to use for the health check (defaults to HTTP).
 * **Description**: Health check description.
 * **Interval**: The interval (in seconds) between each health check. Shorter intervals may improve failover time, but increase load on the origins as checks come from multiple locations (defaults to 60).
 * **Method**: The HTTP method to use for the health check (defaults to GET).
 * **Timeout**: The time (in seconds) before marking the health check as failed (defaults to 5).
 * **Retries**: The number of retries to attempt in case of a timeout before marking the origin as unhealthy. Retries are attempted immediately (defaults to 2).
 * **Response Body**: A case-insensitive sub-string to match against in the response body. If this string is not found, the origin is marked as unhealthy.
 * **Request Headers**: The HTTP request headers to send in the health check. It is recommended you set a Host header by default. The `User-Agent` header cannot be overridden.

## Add a Pool

At least one pool is required for each provisioned load balancer. Pools group your origins for the load balancer to use.

When creating a pool, two fields are required:
 * **Name**: A short name (tag) for the pool. Only alphanumeric characters, hyphens, and underscores are allowed.
 * **Origins**: The list of origins within this pool. Traffic directed at this pool is balanced across all currently healthy origins, provided the pool itself is healthy.

Additional optional fields:
 * **Description**: A human-readable description of the pool.
 * **Enabled**: Whether to enable (the default) this pool. Disabled pools do not receive traffic and are excluded from health checks. Disabling a pool causes any load balancers using it to failover to the next pool, if any (default to true).
 * **Healthy Origin Threshold**: The minimum number of origins that must be healthy for this pool to serve traffic. If the number of healthy origins falls below this number, the pool is marked unhealthy and will fail over to the next available pool. (defaults to 1)
 * **Health Check Regions**: Region from which the health check will perform monitoring. **Note**: IBM's geographic regions differ from Cloudflare's regions. For details about the geographic regions Cloudflare uses, see [Load Balancing: Geographic Regions ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://support.cloudflare.com/hc/en-us/articles/115000540888-Load-Balancing-Geographic-Regions){:new_window}. 
 * **Health Check**: The health check to use for checking origins within this pool. (defaults to no health check)
 * **Notification Email**: The email address that should receive health status notifications. This address can be an individual mailbox or a mailing list.

## Add a Load Balancer

Load balancers help to distribute your proxied traffic across multiple origin pools using a round-robin distribution.

When creating a load balancer, the required fields are:
 * **Name**: The DNS hostname to associate with your Load Balancer. If this hostname already exists as a DNS record in IBM's DNS, the Load Balancer takes precedence and the DNS record will not be used.
 * **Default Pools**: A list of pool IDs. The list is ordered by their failover priority. Pools defined here are used by default, or when region pools are not configured for a given region.

Optionally, the following fields can be configured:
 * **Proxy**: Route traffic through IBM's performance and metrics service.
 * **Session Affinity**: Always route through the same performance and metrics instance. This option is available only if proxy is enabled.
 * **TTL**: Time to live (TTL) of the DNS entry for the IP address returned by this load balancer. This option  applies only to unproxied load balancers, otherwise it defaults to `Automatic`.
 * **Region Pools**: A mapping of region or country codes to a list of pools (ordered by their failover priority) for the given region. Any regions not explicitly defined will fall back to using the default pools. **Note**: IBM's geographic regions differ from Cloudflare's regions. For details about the geographic regions Cloudflare uses, see [Load Balancing: Geographic Regions ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://support.cloudflare.com/hc/en-us/articles/115000540888-Load-Balancing-Geographic-Regions){:new_window}. 
 
