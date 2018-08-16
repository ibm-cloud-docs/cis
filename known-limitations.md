---
copyright:
  years: 2018
lastupdated: "2018-08-10"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Known Limitations

 * We recommend using Chrome.
 
 * The Free Trial plan is limited to one instance per account. After you create a resource instance and add a domain to it, you are not allowed to add new resource instances for CIS. This restriction is enforced even if you delete a trial domain and then attempt to add a domain again to the same resource instance. You'll encounter an error if you attempt to do so.

 * For this service, we support subdomain delegation only using NS records from another provider. CNAME delegation is not supported.
  
 * Wildcard A, AAAA, and CNAME records (*) cannot be proxied.

 * When you delete a dedicated certificate, it may reappear in the list for a short time before the deletion is complete.
 
 * To modify your custom dedicated certificate’s hostnames after ordering, you must order a new certificate and then delete the old one. 

## Global Load Balancer
 * Cloud Internet Services allows you to use the character `_` in load balancer hostnames, however, Kubernetes clusters cannot use `_`. 

 * The Standard plan permits a maximum of 5 load balancers, pools, and health checks. Each pool can have a total of 6 origins, but only 6 unique origins are permitted throughout each CIS instance.

* Health check events for deleted pools and origins cannot be filtered, but they still appear in the table.

* If you filter Health check events by `Pool Health`, `Degraded` pools are included because they technically are healthy, but may contain 1 or more critical origins.

* When adding the request header name for a health check, use `Host`. Using lower-case `host` for a health check fails.
