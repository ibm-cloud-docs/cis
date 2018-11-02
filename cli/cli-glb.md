---

copyright:
  years: 2018
lastupdated: "2018-06-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Global Load Balancer (GLB)

The following `glb` commands are available:

* Create GLB
* Update GLB
* Show GLB
* Delete GLB
* List GLB
* List GLB pools
* Create GLB pool
* Show GLB pool
* Delete GLB pool
* Update GLB pool
* List GLB monitors
* Create GLB monitor
* Show GLB monitor
* Delete GLB monitor
* Update GLB monitor

## Create GLB
**NAME**

   glb-create - Create a global load balancer under a given DNS domain.

**USAGE**

   ibmcloud cis glb-create DNS_DOMAIN_ID (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]

**ARGUMENTS**

   DNS_DOMAIN_ID is the ID of DNS domain.

**OPTIONS**

   -s, --json-str  The JSON data describing a global load balancer.

                   The required fields in JSON data are name, fallback_pool, default_pools:

                       "name":the DNS hostname to associate with your Load Balancer.
                       "fallback_pool":the pool ID to use when all other pools are detected as unhealthy.
                       "default_pools":a list of pool IDs ordered by their failover priority.

                   The optional fields are description, ttl, region_pools, proxied, enabled, session_affinity:

                       "ttl":time to live (TTL) of the DNS entry for the IP address returned by this load balancer.
                       "region_pools":a mapping of region/country codes to a list of pool IDs (ordered by their failover priority) for the given region.
                       "proxied":Control whether or not traffic should flow through the security and performance functions on CIS.
                       "session_affinity":valid values are "cookie", "none".

                   Sample JSON data:

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
   -j, --json-file  A file contains input JSON data.
   
   -i, --instance   Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' will be used.
   
   -o, --output     Specify output format, only JSON is supported now.


**Output Table Columns**

  *  ID
  *  Name
  *  TTL
  *  Proxied
  *  Enabled
  *  Session Affinity
  *  Default Pools
  *  Region Pools

## Update GLB
**NAME**

   glb-update - Update a global load balancer under a given DNS domain.

**USAGE**

   ibmcloud cis glb-update DNS_DOMAIN_ID GLB_ID (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]

**OPTIONS**

   -s, --json-str  The JSON data describing a global load balancer.

                   The required fields in JSON data are name, fallback_pool, default_pools:

                       "name":the DNS hostname to associate with your Load Balancer.
                       "fallback_pool":the pool ID to use when all other pools are detected as unhealthy.
                       "default_pools":a list of pool IDs ordered by their failover priority.

                   The optional fields are description, ttl, region_pools, proxied, enabled, session_affinity:

                       "ttl":time to live (TTL) of the DNS entry for the IP address returned by this load balancer.
                       "region_pools":a mapping of region/country codes to a list of pool IDs (ordered by their failover priority) for the given region.
                       "proxied":Control whether or not traffic should flow through the security and performance functions on CIS.
                       "session_affinity":valid values are "cookie", "none".

                   Sample JSON data:

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
   -j, --json-file  A file contains input JSON data.
   
   -i, --instance   Instance name. If not set, the context instance specified by 'ibmcloud  cis instance-set' will be used.
   
   -o, --output     Specify output format, only JSON is supported now.

**Output Table Columns**

   * ID
   * Name
   * TTL
   * Proxied
   * Enabled
   * Session Affinity
   * Default Pools
   * Region Pools

## Show GLB
**NAME**

   glb - Show a global load balancer under a given DNS domain.

**USAGE**

   ibmcloud cis glb DNS_DOMAIN_ID GLB_ID [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]

**ARGUMENTS**

   DNS_DOMAIN_ID is the ID of DNS domain.
   GLB_ID is the ID of global load balancer.

**OPTIONS**

   -i, --instance  Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' will be used.
   
   -o, --output    Specify output format, only JSON is supported now.

**Output Table Columns**

  *  ID
  *  Name
  *  Created_On
  *  Modified_On
  *  Description
  * TTL
  *  Proxied
  *  Enabled
  * Session Affinity
  *  Default Pools
  * Region Pools

## Delete GLB
**NAME**

   glb-delete - Delete a global load balancer under a given DNS domain.

**USAGE**

   ibmcloud cis glb-delete DNS_DOMAIN_ID GLB_ID [-i, --instance INSTANCE_NAME]

**ARGUMENTS**

   DNS_DOMAIN_ID is the ID of DNS domain.
   
   GLB_ID is the ID of global load balancer.

**OPTIONS**

   -i, --instance  Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' will be used.

## List GLB
**NAME**

   glbs - List all load balancers for the given domain.

**USAGE**

   ibmcloud cis glbs DNS_DOMAIN_ID [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]

**ARGUMENTS**

   DNS_DOMAIN_ID is the ID of DNS domain.

**OPTIONS**

   -i, --instance  Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' will be used.
   
   -o, --output    Specify output format, only JSON is supported now.

**Output Table Columns**

  * ID
  * Name
  * Available Pools
  * TTL
  * Proxied
  * Enabled

## List GLB pools
**NAME**

   glb-pools - List all GLB pools for a given service instance.

**USAGE**

   ibmcloud cis glb-pools [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]

**OPTIONS**

   -i, --instance  Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' will be used.
   
   -o, --output    Specify output format, only JSON is supported now.


**Output Table Columns**

   * ID
   * Name
   * Enabled
   * Minimum Origins
   * Monitor
   * Healthy Status
   * Notification Email
   
## Create GLB pool
**NAME**

   glb-pool-create - Create a GLB pool for a given service instance.

**USAGE**

   ibmcloud cis glb-pool-create (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]

**OPTIONS**

   -s, --json-str  The JSON data used to describe a GLB pool.

                   The required fields in JSON data are name, origins, check_regions:

                       "name":a short name (tag) for the pool.
                       "origins":a list of origins within this pool.
                       "check_regions":a list of geographic region code.

                   The optional fields are description, minimum_origins, enabled, monitor, notification_email:


                   Sample JSON data:

                   {
                       "name": "us-pool",
                       "description": "application server pool in US",
                       "origins": [
                           {
                               "name": "us-app-dal01",
                               "address": "1.1.1.1",
                               "enabled": true
                           },
                           {
                               "name": "us-app-dal02",
                               "address": "2.2.2.2",
                               "enabled": true
                           }
                       ],
                       "minimum_origins": 1,
                       "check_regions": [ "WNAM" ],
                       "monitor": "f1aba936b94213e5b8dca0c0dbf1f9cc",
                       "enabled": true,
                       "notification_email": "someone@example.com"
                   }
   -j, --json-file  A file contains input JSON data.
   
   -i, --instance   Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' will be used.
   
   -o, --output     Specify output format, only JSON is supported now.
   
  **Output Table Columns**

   * ID
   * Name
   * Created On
   * Modified On
   * Description
   * Enabled
   * Minimum Origins
   * Monitor
   * Healthy Status
   * Origins
   * Notification Email
   * Check Regions
   
## Show GLB pool
**NAME**

   glb-pool - Show the details of a given GLB pool.

**USAGE**

   ibmcloud cis glb-pool GLB_POOL_ID [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]

**ARGUMENTS**

   GLB_POOL_ID is the ID of global load balancer pool.

**OPTIONS**

   -i, --instance  Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' will be used.
   
   -o, --output    Specify output format, only JSON is supported now.

**Output Table Columns**

   * ID
   * Name
   * Created On
   * Modified On
   * Description
   * Enabled
   * Minimum Origins
   * Monitor
   * Healthy Status
   * Origins
   * Notification Email
   * Check Regions
   
## Delete GLB pool
**NAME**

   glb-pool-delete - Delete a given GLB pool.

**USAGE**

   ibmcloud cis glb-pool-delete GLB_POOL_ID [-i, --instance INSTANCE_NAME]

**ARGUMENTS**

   GLB_POOL_ID is the ID of global load balancer pool.

**OPTIONS**

   -i, --instance  Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' will be used.
   
## Update GLB pool
**NAME**

   glb-pool-update - Update the details of a given GLB pool.

**USAGE**

   ibmcloud cis glb-pool-update GLB_POOL_ID [-s, --json-str JSON_STR | -j, --json-file JSON_FILE] [--enable-origin ORIGIN_NAME --enable-origin ORIGIN_NAME ...] [--disable-origin ORIGIN_NAME --disable-origin ORIGIN_NAME ...] [--add-origin ORIGIN_PARAMETER --add-origin ORIGIN_PARAMETER ...] [--remove-origin ORIGIN_NAME --remove-origin ORIGIN_NAME ...] [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]


**ARGUMENTS**

   GLB_POOL_ID is the ID of global load balancer pool.

**OPTIONS**

   -s, --json-str  The JSON data used to describe a GLB pool.

                   The required fields in JSON data are name, origins, check_regions:

                       "name":a short name (tag) for the pool.
                       "origins":a list of origins within this pool.
                       "check_regions":a list of geographic region code.

                   The optional fields are description, minimum_origins, enabled, monitor, notification_email:


                   Sample JSON data:

                   {
                       "name": "us-pool",
                       "description": "application server pool in US",
                       "origins": [
                           {
                               "name": "us-app-dal01",
                               "address": "1.1.1.1",
                               "enabled": true
                           },
                           {
                               "name": "us-app-dal02",
                               "address": "2.2.2.2",
                               "enabled": true
                           }
                       ],
                       "minimum_origins": 1,
                       "check_regions": [ "WNAM" ],
                       "monitor": "f1aba936b94213e5b8dca0c0dbf1f9cc",
                       "enabled": true,
                       "notification_email": "someone@example.com"
                   }
   -j, --json-file  A file contains input JSON data.
   
   --enable-origin value        Enable the origin within the Pool. The value can be ORIGIN_NAME or ORIGIN_ADDRESS.
   
   --disable-origin value       Disable the origin within the Pool. The value can be ORIGIN_NAME or ORIGIN_ADDRESS.
   
   --add-origin value           Add an origin into the Pool. ORIGIN_NAME and ORIGIN_ADDRESS are required.
                                Eg: --add-origin name=us-app-dal01,address=1.1.1.1,enabled=true,weight=0.5
                                
   --remove-origin value       Remove an origin from the Pool. The value can be ORIGIN_NAME or ORIGIN_ADDRESS.
   
   -i, --instance   Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' will be used.
   
   -o, --output     Specify output format, only JSON is supported now.

**Output Table Columns**

   * ID
   * Name
   * Created On
   * Modified On
   * Description
   * Enabled
   * Minimum Origins
   * Monitor
   * Healthy Status
   * Origins
   * Notification Email
   * Check Regions
   
## List GLB monitors   
**NAME**

   glb-monitors - List GLB monitors for a given service instance.

**USAGE**

   ibmcloud cis glb-monitors [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]

**OPTIONS**

   -i, --instance  Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' will be used.
   
   -o, --output    Specify output format, only JSON is supported now.

**Output Table Columns**

   * ID
   * Type
   * Method
   * Path
   * Expected Body
   * Expected Codes
   
## Create GLB monitor
**NAME**

   glb-monitor-create - Create a GLB monitor for a given service instance.

**USAGE**

   ibmcloud cis glb-monitor-create (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]

**OPTIONS**

   -s, --json-str  The JSON data used to describe a GLB monitor.

                   The required fields in JSON data are "type".

                       "type": The protocol to use for the healthcheck. Valid values: "HTTP", "HTTPS", "TCP".

                   The optional fields are "description", "timeout", "retries", "interval".

                       "description": Description.
                       "timeout": The timeout (in seconds) before marking the health check as failed.
                       "retries": The number of retries to attempt in case of a timeout before marking the origin as unhealthy.
                       "interval": The interval between each health check.

                   For "TCP" type health check:

                       Extra required fields are "port".

                           "port": The TCP port to use for the health check.

                   For "HTTP/HTTPS" type health check:

                       Extra option fields are "port", "expected_body", "expected_codes", "method", "path", "header", "follow_redirects", "allow_insecure".

                           "port": The TCP port to use for the health check.
                           "expected_body": A case-insensitive sub-string to look for in the response body.
                           "expected_codes": The expected HTTP response code or code range of the health check.
                           "method": The HTTP method to use for the health check.
                           "path": The endpoint path to health check against.
                           "header": The HTTP request headers to send in the health check.
                           "follow_redirects": Follow redirects if returned by the origin.
                           "allow_insecure": Do not validate the certificate when monitor use HTTPS.


                   Sample JSON data:

                       For HTTP/HTTPS:

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
                               "expected_body": "alive"
                           }

                       For TCP:

                           {
                               "description": "Health monitor of TCP",
                               "type": "tcp",
                               "port": 80,
                               "timeout": 5,
                               "retries": 2,
                               "interval": 90
                           }

   -j, --json-file  A file contains input JSON data.
   
   -i, --instance   Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' will be used.
   
   -o, --output     Specify output format, only JSON is supported now.

**Output Table Columns**

   * ID
   * Created On
   * Modified On
   * Type
   * Description
   * Method
   * Path
   * Header
   * Timeout
   * Retries
   * Interval
   * Expected Body
   * Expected Codes
   
## Show GLB monitor 
**NAME**

   glb-monitor - Show the GLB monitor for a given service instance.

**USAGE**

   ibmcloud cis glb-monitor GLB_MON_ID [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]

**ARGUMENTS**

   GLB_MON_ID is the ID of global load balancer monitor.

**OPTIONS**

   -i, --instance  Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' will be used. 
   
   -o, --output    Specify output format, only JSON is supported now.

**Output Table Columns**

   * ID
   * Created On
   * Modified On
   * Type
   * Description
   * Method
   * Path
   * Header
   * Timeout
   * Retries
   * Interval
   * Expected Body
   * Expected Codes
   
## Delete GLB Monitor
**NAME**

   glb-monitor-delete - Delete the GLB monitor for a given service instance.

**USAGE**

   ibmcloud cis glb-monitor-delete GLB_MON_ID [-i, --instance INSTANCE_NAME]

**ARGUMENTS**

   GLB_MON_ID is the ID of global load balancer monitor.

**OPTIONS**

   -i, --instance  Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' will be used.


## Update GLB monitor

**NAME**

   glb-monitor-update - Update the GLB monitor for a given service instance.

**USAGE**

   ibmcloud cis glb-monitor-update GLB_MON_ID (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]

**ARGUMENTS**

   GLB_MON_ID is the ID of global load balancer monitor.

**OPTIONS**

   -s, --json-str  The JSON data used to describe a GLB monitor.

                   The required fields in JSON data are "type".

                       "type": The protocol to use for the healthcheck. Valid values: "HTTP", "HTTPS", "TCP".

                   The optional fields are "description", "timeout", "retries", "interval".

                       "description": Description.
                       "timeout": The timeout (in seconds) before marking the health check as failed.
                       "retries": The number of retries to attempt in case of a timeout before marking the origin as unhealthy.
                       "interval": The interval between each health check.

                   For "TCP" type health check:

                       Extra required fields are "port".

                           "port": The TCP port to use for the health check.

                   For "HTTP/HTTPS" type health check:

                       Extra option fields are "port", "expected_body", "expected_codes", "method", "path", "header", "follow_redirects", "allow_insecure".

                           "port": The TCP port to use for the health check.
                           "expected_body": A case-insensitive sub-string to look for in the response body.
                           "expected_codes": The expected HTTP response code or code range of the health check.
                           "method": The HTTP method to use for the health check.
                           "path": The endpoint path to health check against.
                           "header": The HTTP request headers to send in the health check.
                           "follow_redirects": Follow redirects if returned by the origin.
                           "allow_insecure": Do not validate the certificate when monitor use HTTPS.


                   Sample JSON data:

                       For HTTP/HTTPS:

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
                               "expected_body": "alive"
                           }

                       For TCP:

                           {
                               "description": "Health monitor of TCP",
                               "type": "tcp",
                               "port": 80,
                               "timeout": 5,
                               "retries": 2,
                               "interval": 90
                           }
   -j, --json-file  A file contains input JSON data.
   
   -i, --instance   Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' will be used.
   
   -o, --output     Specify output format, only JSON is supported now.

**Output Table Columns**

   * ID
   * Created On
   * Modified On
   * Type
   * Description
   * Method
   * Path
   * Header
   * Timeout
   * Retries
   * Interval
   * Expected Body
   * Expected Codes
