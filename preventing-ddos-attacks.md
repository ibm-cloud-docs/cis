---

copyright:
  years: 2024
lastupdated: "2025-01-09"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Preventing DDoS attacks
{: #preventing-ddos-attacks}

An effective way to prevent DDoS attacks targeting your web servers is to reduce the requests that reach those servers. Requests can come to your origin server from your web application and from direct connections to the server itself.
{: shortdesc}

![Request paths](images/ddos0overview.svg "Request path options"){: caption="The paths requests can take to your servers" caption-side="bottom"}

## Reducing application requests to the origin
{: #reduce-app-requests-to-origin}

### Caching
{: #ddos-prevent-cache}

A cache stores copies of frequently accessed resources such as images and CSS files.

When a resource is cached, whether on a user’s browser or Content Delivery Network (CDN) server, requests for that resource do not have to go to your origin server. These resources are instead served directly by the cache. During a DDoS attack, caching reduces the number of requests going to your origin server, which makes it harder for your server to get overwhelmed by traffic.

![Reduce requests with caching](images/ddos-caching.svg "Reduce requests with caching"){: caption="Reduce requests to the origin by using caching" caption-side="bottom"}

### Web application firewall (WAF)
{: #ddos-prevent-waf}

A WAF creates a shield between a web application and the internet. The WAF checks incoming web requests and filters potentially malicious traffic to mitigate common attacks.

![Reduce requests with WAF](images/ddos-waf.svg "Reduce requests with WAF"){: caption="Reduce requests to the origin by using WAF" caption-side="bottom"}

### Prevent external connections
{: #prevent-external-connections}

Generally, your origin server should accept only requests that come from your web application, but especially in context of DDoS attacks. Traffic that bypasses your web application also bypasses any WAF or caching you have, and has a stronger chance of overwhelming your origin.

![Prevent external connections](images/ddos-external-connections.svg "Prevent external connections"){: caption="Prevent external connection requests to the origin" caption-side="bottom"}
