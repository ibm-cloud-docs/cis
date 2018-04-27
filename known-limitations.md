---
copyright:
  years: 2018
lastupdated: "2018-04-25"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Known Limitations

 * We recommend using Chrome.

 * Editing the URL match for a page rule causes that rule to be placed at the lowest priority.
 
 * Without a configured domain, you can navigate to **Reliability > Global Load Balancers** to create your load balancer pools and health checks. However, if you select **Create load balancer**, configure the load balancer, and click **Provision 1 Resource**, the request will be rejected because a domain is required. This functional limitation helps the user understand the purpose of pools and monitors in the load balancer creation flow.
 
 * The Early Access program is limited to one instance per account. After you create a resource instance and add a domain to it, you are not allowed to add new resource instances for CIS. This restriction is enforced even if you delete a trial domain and then attempt to add a domain again to the same resource instance. You'll encounter an error if you attempt to do so.

 * When you add a new domain, our system currently does not gather or import your existing domain records.

 * For this Early Access program, we support subdomain delegation only using NS records from another provider. CNAME delegation is not supported.
 
 * At this time, LOC records cannot be imported. As a workaround, use the UI or API to create any LOC records.
 
 * If you import records, the UI may display DDoS as "inactive", and you may not be able to modify caching features even when you have proxied records. This issue only occurs if you import records, and a fix is currently under development.
