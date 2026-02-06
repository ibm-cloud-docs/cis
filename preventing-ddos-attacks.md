---

copyright:
  years: 2024, 2026
lastupdated: "2026-02-06"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Preventing DDoS attacks
{: #preventing-ddos-attacks}

An effective way to prevent DDoS attacks targeting your web servers is to reduce the requests that reach those servers. Requests can come to your origin server from your web application and from direct connections to the server itself.
{: shortdesc}

![Request paths](images/ddos0overview.svg "Request path options"){: caption="The paths requests can take to your servers" caption-side="bottom"}

## Reducing application requests to your origin server
{: #reduce-app-requests-to-origin}

### Using caching to offload traffic
{: #ddos-prevent-cache}

A cache stores copies of frequently accessed resources such as images and CSS files. When a resource is cached—whether on a user’s browser or a Content Delivery Network (CDN) server—requests for that resource do not have to go to your origin server. These resources are instead served directly by the cache.

During a DDoS attack, caching reduces the number of requests that go to your origin server, which makes it harder for your server to get overwhelmed by traffic.

![Reduce requests with caching](images/ddos-caching.svg "Reduce requests with caching"){: caption="Reduce requests to the origin by using caching" caption-side="bottom"}

### Using a Web Application Firewall (WAF) to filter malicious traffic
{: #ddos-prevent-waf}

A WAF creates a shield between a web application and the internet. The WAF checks incoming web requests and filters potentially malicious traffic to mitigate common attacks.

![Reduce requests with WAF](images/ddos-waf.svg "Reduce requests with WAF"){: caption="Reduce requests to the origin by using WAF" caption-side="bottom"}

### Prevent external connections
{: #prevent-external-connections}

Generally, your origin server should accept only requests that come from your web application, especially in the context of DDoS attacks. Traffic that bypasses your web application also bypasses any WAF or caching you have and has a stronger chance of overwhelming your origin.

![Prevent external connections](images/ddos-external-connections.svg "Prevent external connections"){: caption="Prevent external connection requests to the origin" caption-side="bottom"}

### Related links
{: #ddos-related-links}

* [DDoS attack concepts](/docs/cis?topic=cis-distributed-denial-of-service-ddos-attack-concepts)
* [Responding to DDoS attacks](/docs/cis?topic=cis-responding-to-ddos-attacks)
* [Defense mode during a DDoS attack](/docs/cis?topic=cis-defense-mode-attack-ddos)
