---

copyright:
  years: 2020, 2022
lastupdated: "2022-04-12"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Setting session affinity
{: #session-affinity}

Loading a website usually requires fetching multiple assets from a web server. {{site.data.keyword.cis_short_notm}} session affinity minimizes redundant network requests by automatically directing requests from the same client to the same origin web server. 
{: shortdesc}

{{site.data.keyword.cis_short_notm}} sets a cookie on the initial response to the client. Using the cookie in subsequent client requests ensures those requests are sent to the same origin, unless the origin is unavailable.

When enabled, {{site.data.keyword.cis_short_notm}} session affinity does the following:

* When a client makes its first request, {{site.data.keyword.cis_short_notm}} sets a `CFLib` cookie on the client. The cookie encodes the origin to which the request is forwarded.
* Subsequent requests by the same client are forwarded to that origin for the duration of the cookie and as long as the origin server remains healthy.
* If the cookie expires or the origin server is unhealthy, {{site.data.keyword.cis_short_notm}} sets a new cookie encoding the appropriate failover origin.

All sessions default to 23 hours unless a custom session TTL is specified (in seconds) between 30 minutes and 7 days. A session affinity cookie is required to honor the TTL. The session cookie is secure when `Always Use HTTPS` is enabled. Additionally, `HttpOnly` is always enabled for the cookie to prevent cross-site scripting attacks.

## Setting session affinity using the CLI
{: #cli-set-session-affinity}
{: cli}

When you create a global load balancer using the CLI, take the following steps to set the session affinity:

1. Log in to your IBM Cloud account
2. Create a global load balancer
3. Set the following variables:
    * Session affinity: Valid values are `cookie`, `none`. 
    * Session Affinity TTL: Time, in seconds, until this load balancers session affinity cookie expires after being created. Valid values between `1800`, `604800`. Default is `82800`.   
    * Session Affinity Attributes are cookie attributes for session affinity cookie.   
        * Samesite: Valid values are `Auto`, `None`, `Lax`, `Strict`.  
        * Secure: Valid values are `Auto`, `Always`, `Never`.
        * Drain Duration (optional): Configures the drain duration in seconds. This field is only used when session affinity is enabled on the load balancer. 
  

For example:

```sh
ibmcloud cis glb-update fc72db47cee8290eaef292cda6e1619a 12b68758126546e0d129c7bbadfa87f0  -s '{
        "name": "lbtest-updated.cindyuitest01.alan501.cns-foo.com",
        "fallback_pool": "c7e717109b7cf9240dd10fffc0bd146f",
        "default_pools": [
                "c7e717109b7cf9240dd10fffc0bd146f"
        ],
        "description": "Load Balancer for www.example.com",
        "ttl": 30,
        "region_pools": {
                "WNAM": [
                        "c7e717109b7cf9240dd10fffc0bd146f"
                ],
                "ENAM": [
                        "c7e717109b7cf9240dd10fffc0bd146f"
                ]
        },
        "proxied": true,
        "enabled": true,
        "session_affinity": "ip_cookie",
        "session_affinity_attributes": {
                "samesite": "None",
                "secure": "Always",
                "drain_duration": 100
        }
}'
```
{: codeblock}

## Setting session affinity using the API
{: #api-set-session-affinity}
{: api}

When you create a global load balancer using the API, take the following steps to set the session affinity:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `session_affinity`, which specifies the type of session affinity the load balancer uses, unless specified as "none" or "default". Valid values are none, `cookie`, `ip_cookie`.
    * `session_affinity_ttl`, which is the time-to-live of the session affinity.
    * `session_affinity_attributes` which include:
        * `samesite` configures the SameSite attribute on the affinity cookie. Valid values are `Auto`, `Lax`, `None`, `Strict`; default `Auto`
        * `secure` configures the Secure attribute on the session affinity cookie. Valid values are `Auto`, `Always`, `Never` ; default `Auto`
        * `drain_duration` is the value of the drain duration, in seconds. 
1. When all variables are initiated, create the global load balancer with session affinity:

```sh
curl -X POST   https://api.cis.cloud.ibm.com/v1/:crn/zones/:zone_id/load_balancers   -H 'content-type: application/json'   -H 'x-auth-user-token: Bearer xxxxxx'   -d '{
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
