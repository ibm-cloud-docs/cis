---

copyright:
  years: 2018, 2025
lastupdated: "2025-07-07"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Comparing CIS plans
{: #cis-plan-comparison}

{{site.data.keyword.cis_full}} offers several plans to choose from: no-cost Trial, Standard Next, and Enterprise Tier variations.
{: shortdesc}

The no-cost Trial plan is the same as the Standard Next plan, except that it expires after 30 days. Only one trial is available per account. After the Trial plan expires, it is automatically subject to reclamation.
{: note}

The no-cost Trial and Standard plans are not Financial Services regulatory compliant. All other plans are fully compliant. 

The following table compares each offering to help you choose the one that's right for you. Enterprise Tier plans are available with different pricing models.

The numbers in these tables are quotas or resource limits for the associated feature. Features are pay-as-you-go, except for Trial and Standard Next plans.
{: tip}

| |Standard Next|Enterprise Essentials|Enterprise Advanced|Enterprise Premier|Enterprise Usage|
| :------ | :------ | :----- | :----- | :----- | :----- |
|**Domain** \n \n Overage charges apply|1 included  \n More available for monthly cost per domain|1 included  \n More available for monthly cost per domain|2 included  \n More available for monthly cost per domain|2 included  \n More available for monthly cost per domain|Up to 1000, but recommend no more than 20|
|**Included protected traffic**  \n (does not include traffic that is related to an attack)  \n \n Overage charges apply|0.5 TB |5 TB|5 TB|5 TB |Not applicable  \n (usage based)|
|**Included requests and queries**  \n \n Overage charges apply|5 M requests \n 1 M queries|150 requests and queries combined|150 requests and queries combined|150 requests and queries combined|Not applicable  \n (usage based)|
|**DNS**|250 records|3500 records|3500 records|3500 records|3500 records|
|**Global load balancers**|* 3 pools \n * 3 origin servers \n * 5 Health checks \n * 60s health checks \n * Geo Routing \n * Health checks from single region \n * 60s minimum TTL for nonproxied global load balancers |* 20 pools  \n * 20 origin servers \n (more origins available for charge) \n * 100 health checks \n * 5s health checks \n * Smart Routing \n * Health checks from multiple regions \n * 10s minimum TTL for nonproxied global load balancers |* 20 pools  \n * 20 origin servers  \n (more origins available for charge) \n  * 100 health checks \n * 5s health checks \n * Smart Routing \n * Health checks from multiple regions \n * 10s minimum TTL for nonproxied global load balancers|* 20 pools  \n * 20 origin servers  \n (more origins available for charge)  \n * 100 health checks  \n * 5s health checks  \n * Smart Routing  \n * Health checks from multiple regions  \n * 10s minimum TTL for nonproxied global load balancers|* Up to 100 pools \n * 100 origin servers \n * Up to 100 health checks \n * 5s health checks \n * Smart Routing \n * Health checks from multiple regions \n * 10s minimum TTL for nonproxied global load balancers|
|**WAF**|OWASP and CIS ruleset|OWASP and CIS ruleset|OWASP and CIS ruleset|OWASP and CIS ruleset|OWASP and CIS ruleset|
|**Custom certificate**|1 uploaded custom certificate per domain|25 included custom certificates  \n More certificates can be added at a monthly rate|25 included custom certificates  \n More certificates can be added at a monthly rate|25 included custom certificates  \n More certificates can be added at a monthly rate|1 uploaded custom certificate per domain|
|**Page rules**|50 page rules per domain|* 100 page rules per domain \n * More settings for fine-grained control|* 100 page rules per domain \n * More settings for fine-grained control|* 100 page rules per domain \n * More settings for fine-grained control|* 100 page rules per domain \n * More settings for fine-grained control|
|**IP firewall**|* [All IP firewall rule actions](/docs/cis?topic=cis-actions) \n * Block is not available to Country filter \n * 10 Domain lockdown rules \n * 250 User agent rules|* [All IP firewall rule actions](/docs/cis?topic=cis-actions) \n * 200 Domain lockdown rules \n * 1000 User agent rules|* [All IP firewall rule actions](/docs/cis?topic=cis-actions) \n * 200 Domain lockdown rules \n * 1000 User agent rules|* [All IP firewall rule actions](/docs/cis?topic=cis-actions) \n * 200 Domain lockdown rules \n * 1000 User agent rules|* [All IP firewall rule actions](/docs/cis?topic=cis-actions) \n * 200 Domain lockdown rules \n * 1000 User agent rules|
|**Caching**|Basic caching options|Browser cache minimum TTL 30 seconds|Browser cache minimum TTL 30 seconds|Browser cache minimum TTL 30 seconds|Advanced caching options|
|**Range**|Not included|Not included|Included \n * 10 unique FQDNs \n * Overage fees incurred past 5 TB of traffic|Included \n * 10 unique FQDNs \n * Overage fees incurred past 5 TB of traffic|Included \n * 10 unique FQDNs|
|**Edge functions**|1 action \n (must be named after domain) \n \n 1 M Edge function requests|Unlimited actions|Unlimited actions|Unlimited actions|Unlimited actions|
|**Firewall rules**|* 100 active rules \n * Does not support Log action \n * Does not support matches operator|* 1000 active rules \n * Supports all actions \n * Supports all operators|* 1000 active rules \n * Supports all actions \n * Supports all operators|* 1000 active rules \n * Supports all actions \n * Supports all operators  \n * Supports bot management|* 1000 active rules \n * Supports all actions \n * Supports all operators|
|**GraphQL**|Not included|Included|Included|Included|Included|
|**Smart routing**|Not included|Included|Included|Included|Included|
|**Logging**|Not included|Included|Included|Included|Included|
|**Alerts**|Not included|Included|Included|Included|Included|
|**Rate limiting**|Not included|Not included|Included|Included|Included|
|**Bot management**|Not included|Not included|Not included|Included|Not included|
{: caption="CIS plan comparison" caption-side="bottom"}

## Additional details
{: #additional-details}

* Traffic is protected when it is traffic through proxied CIS components, metered as traffic from the edge to the origin
* HTTP request made on proxied resources (for example, DNS records and load balancers) count toward your protected traffic
* When traffic is not proxied, it will only consume DNS queries during hostname resolution

## Deprecated plans
{: #deprecated-plans}

The following plans are scheduled for deprecation or deprecated.

* The Standard plan reached the end of marketing on 30 April 2023. The end of support is not yet determined.
* Enterprise Package, Enterprise GLB, and Enterprise Security plans will reach the end of marketing on 31 August 2023. The end of support is not yet determined.

For more information about changing to a new plan if you are currently on a deprecated plan, see [Transitioning to updated plans](/docs/cis?topic=cis-transition-plans).
