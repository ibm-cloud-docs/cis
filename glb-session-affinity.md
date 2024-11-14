---

copyright:
  years: 2020, 2024
lastupdated: "2024-11-14"

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

1. Log in to your IBM Cloud account.
1. Create a global load balancer.
1. Set the following CLI variables:

`session_affinity`
:   Valid values are `cookie`, `none`.
`ttl`
:   Time, in seconds, until this load balancer's session affinity cookie expires after being created. Valid values between `1800`, `604800`. Default is `82800`.

`session_affinity_attributes`
:   Cookie attributes for a session affinity cookie.

   `samesite`
   :   Valid values are:
      * `Auto` (default): If **Always Use HTTPS** is enabled, session affinity cookies use `Lax` mode; if disabled, cookies use `None` mode.
      *  `None`: Cookies are sent with all requests.
      *  `Lax`: Cookies are sent only to the apex domain (such as `example.com`).
      *  `Strict`: Cookies are created by the first party (the visited domain).
      
   `secure`
   :   Valid values are:
      *  `Auto` (default): If **Always Use HTTPS** is enabled, session affinity cookies use `secure` in the `samesite` attribute; if disabled, cookies don't use `secure`.
      *  `Always`: `secure` is always set, meaning the cookie is only sent over HTTPS connections.
      *  `Never`: `secure` is never set, allowing cookies to be sent over both HTTPS and HTTP connections.
      
   `drain-duration`
   :  Optional. Time, in seconds, where the origin will drain active sessions. After the time elapses, all existing sessions are ended, This field is only used when session affinity is enabled on the load balancer.

If you require a specific SameSite configuration in your session affinity cookies, CIS recommends that you provide values for `samesite `and `secure` different from `Auto`, instead of relying on the default behavior. This way, the value of the SameSite cookie attribute does not change due to configuration changes (namely **Always Use HTTPS**).
{: note}

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

Session affinity is a property of global load balancers, which you can set with the following endpoints:

* [Create a load balancer](/apidocs/cis#create-load-balancer)
* [Edit a load balancer](https://cloud.ibm.com/apidocs/cis#edit-load-balancer)

Customize the behavior of session affinity by using the `session_affinity`, `session_affinity_ttl`, and `session_affinity_attributes` parameters.

To enable session affinity by HTTP header, set the `session_affinity` value to `header` and add your
HTTP header names to `session_affinity_attributes.headers`.

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

If you set `samesite` to `None` in your API request, you cannot set `secure` to `Never`.
{: note}

## Zero-Downtime Failover
{: #zero-downtime-failover}

Zero-Downtime Failover automatically sends traffic to endpoints within a pool during transient network issues. This helps reduce errors shown to your users when issues occur in between active health monitors.

You can enable one of three options:

* **None**: No failover will take place and errors might show to your users.
* **Temporary**: Traffic will be sent to other endpoints until the originally pinned endpoint is available.
* **Sticky**: The session affinity cookie is updated and subsequent requests are sent to the new endpoint moving forward as needed.

Sticky Zero-Downtime Failover is not supported for session affinity by HTTP header.
{: note}
