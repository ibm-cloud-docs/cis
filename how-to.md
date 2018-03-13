---
copyright:
  years: 2018
lastupdated: "2018-02-16"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Managing your IBM Cloud CIS deployment

You'll begin by using the Overview screen as your working base of operations. It shows all of the current parameters for your deployment.

Once you've set up your DNS and configured it, you are ready to go!

## Using the Overview screen

Using  the Overview screen, you can see the status of all your selections. You can change the settings directly from the Overview screen, just click on the underlined name of the setting you'd like to change, for example, you could click on the `Load Balancers` field to add a Load Balancer.

On the Overview screen, you may see that your domain name configuration is in **Pending** status, or in **Active** status as shown in the following figure.

![overview screen image](images/overview-screen-configuration-summary.png)


## Configuring and managing your DNS

Go to your DNS page and add a record (most likely an A record). Type in the information about your DNS record and then click `Add record` to implement your changes.

![add-DNS](images/add-domain-records-screen.png)

## Set up and manage your caching

Next, you can set up caching. 

![IMAGE](images/caching-screen.png)

You have the option of 3 types of caching, available from the caching screen dropdown menu: 

 * No query string :  Only delivers resources from cache when there is no query string.
 * Query string independent : Delivers the same resource to everyone independent of the query string. (Note: The Ignore Query String setting applies only to static file extensions. This setting removes the query string when generating the cache key, so that a request for `style.css?something` is normalized to `style.css` when serving from the cache.)
 * Query string dependent : Delivers a different resource each time the query string changes.
  
## Purge Cache
 
At any time you can purge your cache to make way for updates by entering the URL into the purge cache field. You can purge a single file or multiple files (up to 30 at a time).
 
 ## Cache expiration
 
You can use the dropdown menu to select the time of cache expiration that you require, for example 8 hours, or 1 day.

![caching image](images/caching-screen.png)
 
 ## Using Development Mode
 
Development mode is intended for use when major updates or new file uploads are required, so you do not want the end users to work from the cache at all, but to retrieve files directly from the origin servers. Development mode expires automatically after 3 hours.

![IMAGE](images/development-mode-toggle.png)

To begin using Development Mode, toggle the switch to "Enabled" position. To stop using Development Mode, toggle the switch to "Disabled" position.

## Managing your Page Rules
 
You can enable 50 Page Rules per page. Use the drop down menus to configure the Page Rules. The Page Rules are divided into three categories: Security, Performance, and Reliability.

Notice that when certain rules are enabled, other options become grayed out, if they are in conflict with the other rules you've just selected. After you've selected the Page Rules you desire, click "Provision" to enable them. They will take effect immediately, and they can be viewed immediately on the Overview screen.
 
 ![PAGE RULES MENUS](images/page-rule-dropdown-settings.png)
 
 You also can enable or disable your Page Rules from the table displayed in the Overview screen. See [Using Page Rules](using-page-rules.html) for more information.
 
 ## Security settings
 
By default, DDoS protection is enabled for all IBM Cloud CIS accounts. Also, IBM Cloud CIS provides 25 default rules for WAF, which you can toggle on and off as you desire, or you can upload your own WAF rules. The 25 rules are enabled for you, even if you have no DNS records in our DNS management system. When you toggle the rules on or off, the changes are applied immediately.

![IMAGE](images/ddos-waf-ssl-screen.png)

## Certificates

When you deploy into a Zone, IBM Cloud CIS automatically deploys a universal certificate for that zone. Thus, you don't need to do anything to have certificate-based protection in that zone. If you desire, you can upload your own certificate. You'll need a separate certificate for each zone, and you'll see an error message if the certificate you are uploading does not match your zone.
 
 ## Set up and configure your load balancers
 
 IBM Cloud CIS provides global load balancing as a service.

![IMAGE](images/glb-screen.png)

### GLB Dashboard
There will be three lists that contain the load balancers, pools, and health checks. The lists will display the new or updated global load balancer or one of it's components after provisioning or updating. Initially they are empty, but before creating a load balancer there are a few actions that must be taken.

#### Create
>Note: <sup>`*`</sup> indicates this step is optional
1) <sup>`*`</sup>Create a health check, click "Create health check".
  ![IMAGE](images/glb-health-check-list.png)
    * **Path**: The endpoint path to health check against.
    * **Type**: The protocol to use for the health check.
    * **Description**: User provided description.

2) Create a pool, click "Create pool". 
  ![IMAGE](images/glb-pool-list.png)
    * **Health**: Status of the pool.
    * **Name**: User provided name.
    * **Origins**: Count of healthy origins in the pool.
    * **Health Check**: Path of the attached health check, if any.

3) Create a load balancer, click "Create load balancer".
  ![IMAGE](images/glb-load-balancer-list.png)
    * **Health**: Status of the load balancer.
    * **Hostname**: Name prepended to the domain name.
    * **Available Pools**: Count of healthy pools.
    * **TTL**: Time To Listen.
    * **Proxy**: Enable or disable proxy traffic flow.
    * **Status**: Enable or disable the load balancer.

#### Edit/Delete
To edit or delete a load balancer or one of it's components click the overflow menu button located on the far right of each row.

Overflow menu button:

![IMAGE](images/overflow.png)

The following options will be provided for each list.

* Health Check

  ![IMAGE](images/health-check-overflow.png)
    * **Edit health check**: This will redirect the user to the edit flow. 
    * **Delete health check**: This will bring up the confirmation dialog for the deletion flow.

* Pool

  ![IMAGE](images/pool-overflow.png)
    * **View pool details**: This will bring up a modal with information about the pool.
    * **Edit pool**: Redirects the user to the edit flow.
    * **Delete pool**: Brings up the confirmation dialog for the deletion flow.

* Load Balancer

  ![IMAGE](images/load-balancer-overflow.png)
    * **Disable/Enable**: Enable or disable a load balancer.
    * **Edit load balancer**: Redirects to the edit flow. 
    * **Delete load balancer**: Brings up the confirmation dialog for the deletion flow.

### Add a Health Check

Health checks are optional attachments for origin pools that use a custom repeating interval to probe for a specific response body or status code to monitor the pool's health. Once created, they can be added to a new or existing origin pool.

When creating a health check, there is only one required field:
 * **Reponse Code**: The expected HTTP response code or code range of the health check. This must be between 200-299 with wildcards denoted by an 'x'.

However, there are also additional optional fields:
 * **Path**: The endpoint path to health check against (defaults to /).
 * **Type**: The protocol to use for the healthcheck (defaults to HTTP).
 * **Description**: Health check description.
 * **Interval**: The interval (in seconds) between each health check. Shorter intervals may improve failover time, but will increase load on the origins as we check from multiple locations (defaults to 60).
 * **Method**: The HTTP method to use for the health check (defaults to GET).
 * **Timeout**: The timeout (in seconds) before marking the health check as failed (defaults to 5).
 * **Retries**: The number of retries to attempt in case of a timeout before marking the origin as unhealthy. Retries are attempted immediately (defaults to 2).
 * **Response Body**: A case-insensitive sub-string to look for in the response body. If this string is not found, the origin will be marked as unhealthy.
 * **Request Headers**: The HTTP request headers to send in the health check. It is recommended you set a Host header by default. The User-Agent header cannot be overridden.

### Add a Pool

At least one pool is required for each provisioned load balancer. Pools are used to group your origins for the laod balancer to use.

When creating a pool, there are two required field:
 * **Name**: A short name (tag) for the pool. Only alphanumeric characters, hyphens and underscores are allowed.
 * **Origins**: The list of origins within this pool. Traffic directed at this pool is balanced across all currently healthy origins, provided the pool itself is healthy.

However, there are also additional optional fields:
 * **Description**: A human-readable description of the pool.
 * **Enabled**: Whether to enable (the default) this pool. Disabled pools will not receive traffic and are excluded from health checks. Disabling a pool will cause any load balancers using it to failover to the next pool, if any (default to true).
 * **Healthy Origin Threshold**: The minimum number of origins that must be healthy for this pool to serve traffic. If the number of healthy origins falls below this number, the pool will be marked unhealthy and we wil failover to the next available pool. (defaults to 1)
 * **Health Check Regions**: Region from where the health check will monitor from.
 * **Health Check**: The health check to use for checking origins within this pool. (defaults to no health check)
 * **Notification Email**: The email address to send health status notifications to. This can be an individual mailbox or a mailing list.

 ### Add a Load Balancer

Load balancers help to distribute your proxied traffic across multiple origin pools using a round robin distribution.

When creating a load balancer, the required fields are:
 * **Name**: The DNS hostname to associate with your Load Balancer. If this hostname already exists as a DNS record in IBM's DNS, the Load Balancer will take precedence and the DNS record will not be used.
 * **Default Pools**: A list of pool IDs ordered by their failover priority. Pools defined here are used by default, or when region pools are not configured for a given region.

Optionally, the following can also be configured:
 * **Proxy**: Route traffic through IBM's performance and metrics service.
 * **Session Affinity**: Always route through the same performance and metrics instance. This is only available if proxy is enabled.
 * **TTL**: Time to live (TTL) of the DNS entry for the IP address returned by this load balancer. This only applies to unproxied load balancers, otherwise it defaults to Automatic.
 * **Region Pools**: A mapping of region/country codes to a list of pools (ordered by their failover priority) for the given region. Any regions not explicitly defined will fall back to using default pools.