---

copyright:
  years: 2018, 2026
lastupdated: "2026-05-20"

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

#### Working with health check events
{: #working-with-health-check-events}

Use the **Events** tab to monitor and investigate health status changes for origins and pools that are associated with a global load balancer. Health check events represent status changes that configured health checks detect. When an origin status changes, a corresponding event entry appears with details.

The following filtering options are available:

* Start date: Filters events by the beginning of a selected date range.
* End date: Filters events by the end of a selected date range.
* Origin health: Filters events by origin status (for example, Healthy or Critical).
* Origins: Filters events by a specific origin.
* Pool health: Filters events by pool status (for example, Healthy or Critical).
* Pools: Filters events by a specific origin pool.

To see health check events, click **Reliability > Global load balancers > Events**.

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

     IBM's geographic regions differ from the regions that {{site.data.keyword.cis_short_notm}} uses. For details about the geographic regions, see [Geo steering](/docs/cis?topic=cis-traffic-steering&interface=ui#geo-steering).
     {: note}

1. Click **Create** to complete the global load balancer configuration.

### Step 4: Verify connectivity
{: #global-load-balancer-verify-connectivity}

Finally, verify connectivity to your application by accessing the FQDN URL in a browser.

For more information about updating and deleting global load balancers, health checks, and origin pools in the console, see [Managing global load balancers](/docs/cis?topic=cis-configure-glb&interface=ui).
{: note}

## Configuring the global load balancers from the CLI
{: #configure-glb-cli}
{: cli}

To create and configure a global load balancer from the CLI, follow these steps in this order:

1. Create a health check. (optional)
1. Create an origin pool.
1. Create a global load balancer.

### Step 1: Creating a health check from the CLI (optional)
{: #create-glb-monitor-cli}

Health checks are optional attachments for origin pools. If you don't define any custom health checks, the system uses `/` as your default health check path.

To create a health check from the CLI, run the following command:

```sh
ibmcloud cis glb-monitor-create (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
```
{: codeblock}

Where:

`--json`
:   The JSON file or JSON string that is used to describe a health check. Required.
    - The required fields in JSON data are `type`.
        - `type` : The protocol to use for the healthcheck. Valid values are `HTTP`, `HTTPS`, and `TCP`.
    - The optional fields are `description`, `timeout`, `retries`, `interval`.
        - `description` : A description of the health check.
        - `timeout` : The timeout (in seconds) before marking the health check as failed.
        - `retries` : The number of retries to attempt if there is a timeout before the origin is marked as unhealthy.
        - `interval` : The interval between each health check.
    - For `TCP` type health check. Extra required fields are `port`.
        - `port` : The TCP port to use for the health check.
    - For `HTTP/HTTPS` type health check. Extra option fields are `port`, `expected_body`, `expected_codes`, `method`, `path`, `header`, `follow_redirects`, `allow_insecure`.
        - `port` : The TCP port to use for the health check.
        - `expected_body` : A case-insensitive substring to look for in the response body.
        - `expected_codes` : The expected HTTP response code or code range of the health check.
        - `method` : The HTTP method to use for the health check.
        - `path` : The endpoint path to health check against.
        - `header` : The HTTP request headers to send in the health check.
        - `follow_redirects` : Follow redirects if returned by the origin.
        - `allow_insecure` : Don't validate the certificate when monitor use HTTPS.
        - `probe_zone` : Assign this monitor to emulate the specified zone while probing.

    Sample JSON data:

    For HTTP/HTTPS:

    ```json
    {
      "description": "Health monitor of web service",
      "type": "https",
      "method": "GET",
      "path": "/health",
      "header": {
         "Host": [
            "example.com"
         ],
         "X-App-ID": [
            "abc123"
         ]
      },
      "timeout": 5,
      "retries": 2,
      "interval": 90,
      "follow_redirects": true,
      "allow_insecure": false,
      "expected_codes": "2xx",
      "expected_body": "alive",
      "probe_zone": "example.com"
    }
    ```
    {: codeblock}

    For TCP:

    ```json
    {
      "description": "Health monitor of TCP",
      "type": "tcp",
      "port": 80,
      "timeout": 5,
      "retries": 2,
      "interval": 90
    }
    ```
    {: codeblock}

`-i, --instance`
:   Instance name or ID. If you don't set the instance name or ID, the command uses the context instance (`ibmcloud cis instance-set INSTANCE`).

`--output`
:   The output format. Currently, `json` is the only supported value.

### Step 2: Creating an origin pool from the CLI
{: #create-glb-pool}

To create an origin pool from the CLI, run the following command:

```sh
ibmcloud cis glb-pool-create (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
```
{: codeblock}

Where:

`--json`
:    The JSON file or JSON string that is used to describe an origin pool. Required.
    - The required fields in JSON data are `name`, `origins` and `check_regions` :
        - `name` : A short name (tag) for the pool.
        - `origins` : A list of origins within this pool.
        - `check_regions` : A list of geographic region code.
    - The optional fields are `description`, `minimum_origins`, `enabled`, `monitor`.

Sample JSON data:

```json
{
   "name": "us-pool",
   "description": "application server pool in US",
   "origins": [
      {
            "name": "us-app-dal01",
            "address": "1.1.1.1",
            "enabled": true,
            "header": {
               "host": ["test.com"]
            }
      },
      {
            "name": "us-app-dal02",
            "address": "2.2.2.2",
            "enabled": true,
            "header": {
               "host": ["example.com"]
            }
      }
   ],
   "minimum_origins": 1,
   "check_regions": [ "WNAM" ],
   "monitor": "f1aba936b94213e5b8dca0c0dbf1f9cc",
   "enabled": true
}
```
{: codeblock}

`-i, --instance`
:   Instance name or ID. If you don't set the instance name or ID, the command uses the context instance (`ibmcloud cis instance-set INSTANCE`).

`--output`
:   The output format. Currently, `json` is the only supported value.

### Step 3: Creating a global load balancer from the CLI
{: #configure-load-bal-cli}

To create a global load balancer from the CLI, run the following command:

```sh
cis glb-create DNS_DOMAIN_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
```
{: codeblock}

Where:

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--json`
:   The JSON file or JSON string that is used to describe a global load balancer. Required.
    - The required fields in JSON data are `name`, `fallback_pool`, and `default_pools` :
        - `name` : The DNS hostname to associate with your load balancer.
        - `fallback_pool` : The pool ID to use when CIS detects all other pools as unhealthy.
        - `default_pools` : A list of pool IDs ordered by their failover priority.
    - The optional fields are `description`, `ttl`, `region_pools`, `proxied`, `enabled`, `session_affinity`, `session_affinity_ttl`, `steering_policy`:
        - `description` : A description of your load balancer.
        - `ttl`: Time to live (TTL) of the DNS entry for the IP address that this load balancer returns.
        - `region_pools` : A mapping of region and country codes to a list of pool IDs (ordered by their failover priority) for the region.
        - `proxied` : Control whether traffic flows through the security and performance functions on CIS.
        - `enabled` : Whether to enable (the default) this load balancer.
        - `session_affinity` : Helps ensure that CIS consistently directs a user's requests to the same backend server during a session. Valid values are `cookie` and `none`.
        - `session_affinity_ttl` : Time, in seconds, until this load balancer's session affinity cookie expires after CIS creates it. Valid value is between `[1800, 604800]`. The default value is `82800`.
        - `steering_policy` : Valid values for `steering_policy` are `off`, `geo`, `random`, `dynamic_latency`.
             - `off` : Use `default_pools`.
             - `geo` : Use `region_pools/pop_pools`.
             - `random` : Select a pool randomly.
             - `dynamic_latency` : Use round-trip time to select the closest pool in `default_pools` (requires pool health checks).

Sample JSON data:

```json
{
      "name": "www.example.com",
      "fallback_pool": "17b5962d775c646f3f9725cbc7a53df4",
      "default_pools": [
         "17b5962d775c646f3f9725cbc7a53df4",
         "9290f38c5d07c2e2f4df57b1f61d4196"
      ],
      "description": "Example global load balancer.",
      "ttl": 60,
      "region_pools": {
         "WNAM": [
               "de90f38ced07c2e2f4df50b1f61d4194",
               "9290f38c5d07c2e2f4df57b1f61d4196"
         ],
         "ENAM": [
               "00920f38ce07c2e2f4df50b1f61d4194"
         ]
      }
}
```
{: codeblock}

`-i, --instance`
:   Instance name or ID. If you don't set the instance name or ID, the command uses the context instance (`ibmcloud cis instance-set INSTANCE`).

`--output`
:   The output format. Currently, `json` is the only supported value.

For more information about creating, updating, and deleting global load balancers, health checks, and origin pools, see [Global load balancer CLI commands](/docs/cis?topic=cis-cis-cli#glb).
{: note}

## Configuring the global load balancers with the API
{: #configure-glb-api}
{: api}

To create and configure a global load balancer with the API, follow these steps in this order:

1. Create a health check. (optional)
1. Create an origin pool.
1. Create a global load balancer.

### Step 1: Creating a health check with the API (optional)
{: #create-glb-monitor-api}

Health checks are optional attachments for origin pools. If you don't define any custom health checks, the system uses `/` as your default health check path.

Follow these steps to create a health check with the API:

1. Set up your API environment with the correct variables.
1. Store the following value in variables to be used in the API command:

   `CRN`: The full URL-encoded CRN of the service instance.

1. When all variables are initiated, create the health check:

   ```sh
   curl -X POST https://api.cis.cloud.ibm.com/v1/:crn/load_balancers/monitors
     -H 'content-type: application/json'
     -H 'x-auth-user-token: Bearer xxxxxx'
     -d '{
       "description": "",
       "type": "http",
       "interval": 60,
       "retries": 2,
       "timeout": 5,
       "expected_body": "",
       "expected_codes": "200",
       "follow_redirects": true,
       "allow_insecure": false,
       "path": "/status",
       "header": {
    	   "Host": ["www.example.com"],
    	   "X-App-ID": ["abc123"]
       },
       "method": "GET"
   }'
   ```
   {: codeblock}

### Step 2: Creating an origin pool with the API
{: #create-glb-pool-with-api}

Follow these steps to create an origin pool with the API:

1. Set up your API environment with the correct variables.
1. Store the following value in variables to be used in the API command:

   `CRN`: The full URL-encoded CRN of the service instance.

1. When all variables are initiated, create the origin pool:

   ```sh
   curl -X POST https://api.cis.cloud.ibm.com/v1/:crn/load_balancers/pools
     -H 'content-type: application/json'
     -H 'x-auth-user-token: Bearer xxxxxx'
     -d '{
       "description": "",
       "enabled": true,
       "minimum_origins": 1,
       "monitor": "92859a0f6b4d3e55b953e0e29bb96338",
       "name": "eu-pool",
       "notification_email": "",
       "check_regions": [
           "EEU"
       ],
       "origins": [
           {
               "name": "eu-origin1",
               "address": "150.0.0.1",
               "enabled": true,
               "weight": 1
           },
           {
               "name": "eu-origin2",
               "address": "150.0.0.2",
               "enabled": true,
               "weight": 1
           }
       ]
   }'
   ```
   {: codeblock}

### Step 3: Creating a global load balancer with the API
{: #create-glb-with-api}

Follow these steps to create a global load balancer with the API:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded CRN of the service instance.

   `ZONE_ID`: The domain ID.

1. When all variables are initiated, create the global load balancers:

   ```sh
   curl -X POST https://api.cis.cloud.ibm.com/v1/:crn/zones/:zone_id/load_balancers
     -H 'content-type: application/json'
     -H 'x-auth-user-token: Bearer xxxxxx'
     -d '{
       "description": "",
       "proxied": true,
       "enabled": true,
       "name": "www.example.com",
       "session_affinity": "none",
       "session_affinity_ttl": 5000,
       "steering_policy": "geo",
       "fallback_pool": "4112ba6c2974ec43886f90736968e838",
       "default_pools": [
        "6563ebae141638f92ebbdc4a821bef8c",
        "4112ba6c2974ec43886f90736968e838"
       ],
       "pop_pools": {},
       "region_pools": {
           "EEU": [
               "4112ba6c2974ec43886f90736968e838"
           ],
           "ENAM": [
               "6563ebae141638f92ebbdc4a821bef8c"
           ],
           "WEU": [
               "4112ba6c2974ec43886f90736968e838"
           ],
           "WNAM": [
               "6563ebae141638f92ebbdc4a821bef8c"
           ]
       }
   }'
   ```
   {: codeblock}

For more information about creating, updating, and deleting global load balancers, health checks, and origin pools, see [API Global load balancer](/apidocs/cis#create-load-balancer).
{: note}

## Configuring global load balancers with Terraform
{: #configure-glb-terraform}
{: terraform}

Before you begin, make sure that you complete the steps to [set up Terraform for {{site.data.keyword.cis_short_notm}}](/docs/cis?topic=cis-terraform-setup-cis).

To create and configure a global load balancer with Terraform, follow these steps in order:

1. Create a health check
1. Create an origin pool
1. Create a global load balancer

### Step 1: Creating a health check with Terraform (optional)
{: #create-glb-monitor-terraform}

Health checks are optional attachments for origin pools. If you don't define any custom health checks, the system uses `/` as your default health check path.

To create a health check with Terraform, use the `ibm_cis_healthcheck` resource:

```terraform
resource "ibm_cis_healthcheck" "health_check" {
  cis_id         = ibm_cis.instance.id
  description    = "Health check for web servers"
  expected_body  = "alive"
  expected_codes = "200"
  method         = "GET"
  timeout        = 5
  path           = "/health"
  interval       = 60
  retries        = 2
  type           = "http"
  port           = 80
  allow_insecure = false
  follow_redirects = true
}
```
{: codeblock}

### Step 2: Creating an origin pool with Terraform
{: #create-glb-pool-terraform}

To create an origin pool with Terraform, use the `ibm_cis_origin_pool` resource:

```terraform
resource "ibm_cis_origin_pool" "origin_pool" {
  cis_id = ibm_cis.instance.id
  name   = "us-pool"

  origins {
    name    = "us-app-dal01"
    address = "1.1.1.1"
    enabled = true
  }

  origins {
    name    = "us-app-dal02"
    address = "2.2.2.2"
    enabled = true
  }

  description        = "Application server pool in US"
  enabled            = true
  minimum_origins    = 1
  monitor            = ibm_cis_healthcheck.health_check.id
  notification_email = ""

  check_regions = [
    "WNAM"
  ]
}
```
{: codeblock}

### Step 3: Creating a global load balancer with Terraform
{: #create-glb-terraform}

To create a global load balancer with Terraform, use the `ibm_cis_global_load_balancer` resource:

```terraform
resource "ibm_cis_global_load_balancer" "global_load_balancer" {
  cis_id           = ibm_cis.instance.id
  domain_id        = ibm_cis_domain.domain.id
  name             = "www.example.com"
  fallback_pool_id = ibm_cis_origin_pool.origin_pool.id
  default_pool_ids = [
    ibm_cis_origin_pool.origin_pool.id
  ]
  description      = "Global load balancer for example.com"
  proxied          = true
  enabled          = true
  session_affinity = "cookie"
  steering_policy  = "geo"

  pop_pools {
    pop = "LAX"
    pool_ids = [
      ibm_cis_origin_pool.origin_pool.id
    ]
  }

  region_pools {
    region = "WNAM"
    pool_ids = [
      ibm_cis_origin_pool.origin_pool.id
    ]
  }
}
```
{: codeblock}

For more information about the Terraform resources for global load balancers, health checks, and origin pools, see the following resources in the {{site.data.keyword.cloud_notm}} Provider Terraform registry:

- [ibm_cis_healthcheck](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_healthcheck){: external}
- [ibm_cis_origin_pool](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_origin_pool){: external}
- [ibm_cis_global_load_balancer](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_global_load_balancer){: external}
