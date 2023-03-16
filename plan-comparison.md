---

copyright:
  years: 2018, 2023
lastupdated: "2023-03-09"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Plan comparison
{: #cis-plan-comparison}

{{site.data.keyword.cis_full}} offers several plans to choose from: no-cost Trial, Standard, and Enterprise variations.
{: shortdesc}

The no-cost Trial plan is the same as the Standard plan, except that it expires after 30 days. Only one trial is available per account. After the Trial plan has expired, it is automatically subject to reclamation.
{: note}

The numbers in these tables are quotas or resource limits for the associated feature. Features are pay-as-you-go, except for Trial and Standard plans.
{: tip}

The following table compares each offering to help you choose the one that's right for you. Enterprise usage and package plans are available with different pricing models.

| | Standard  \n (30 day no-cost  \n trial available) |Standard Next| Enterprise Package | Enterprise Usage | Enterprise GLB | Enterprise Security|
| :------- | :------- | :--------- | :------------ | :--------- | :--------- | :--------- |
|**Billing interval**|Monthly prorated | |Daily prorated | Based on consumption |Monthly prorated |Monthly prorated|
|**Domain**|1| 1|Up to 1000, but recommend no more than 20|Up to 1000, but recommend no more than 20| 2|3|
|**DNS**|3500 records |250 records |Multiple domains (3500 records per domain) |3500 records |Multiple domains (3500 records per domain) |Same as Enterprise |Same as Enterprise|
|**Global load balancers**|* 5 Pools  \n * 6 origin servers  \n * 5 Health checks  \n * 60s health checks  \n * Geo Routing  \n * Health checks from single region  \n * 60s minimum TTL for non-proxied global load balancers |* 3 Pools  \n * 3 origin servers  \n * 5 Health checks  \n * 60s health checks  \n * Geo Routing  \n * Health checks from single region  \n * 60s minimum TTL for non-proxied global load balancers |* Up to 100 pools  \n * 100 origin servers  \n * Up to 100 health checks  \n * 5s health checks  \n * Smart Routing  \n * Health checks from multiple regions  \n * 10s minimum TTL for non-proxied global load balancers|* Up to 100 pools  \n * 100 origin servers  \n * Up to 100 health checks  \n * 5s health checks  \n * Smart Routing  \n * Health checks from multiple regions  \n * 10s minimum TTL for non-proxied global load balancers|* Up to 100 pools  \n * 18 origin server  \n * Up to 100 health checks  \n * 60s health checks  \n * Health checks from multiple regions  \n * 10s minimum TTL for non-proxied global load balancers |Not available|
|**WAF**|Yes (OWASP and CIS rule set)|Yes (OWASP and CIS rule set)| Yes (OWASP and CIS rule set)|Yes (OWASP and CIS rule set)|Not available |Yes (OWASP and CIS rule set)|
|**DDoS**|On (with proxy) or Off (no proxy)|On (with proxy) or Off (no proxy) |On (with proxy) or Off (no proxy)|Yes (proxy)|Yes (proxy) |Yes|
|**TLS**|* 100 Universal certificates  \n * 100 Advanced/Dedicated certificates (combination of dedicated wildcard and dedicated custom)  \n * 1 Uploaded custom per domain|* 100 Universal certificates  \n * 100 Advanced/Dedicated certificates (combination of dedicated wildcard and dedicated custom)  \n * 1 Uploaded custom per domain|* 100 Universal certificates  \n * 100 Advanced/Dedicated certificates (combination of dedicated wildcard and dedicated custom)  \n * 1 Uploaded custom per domain|* 100 Universal certificates  \n * 100 Advanced/Dedicated certificates (combination of dedicated wildcard and dedicated custom)  \n * 1 Uploaded custom per domain|* 100 Universal certificates  \n * 100 Advanced/Dedicated certificates (combination of dedicated wildcard and dedicated custom)  \n * 1 Uploaded custom per domain|* 100 Universal certificates  \n * 100 Advanced/Dedicated certificates (combination of dedicated wildcard and dedicated custom)  \n * 1 Uploaded custom per domain|
|**Logpull/Logpush**|No|No |Yes|Yes|Yes|Yes|
|**Page rules**|50 page rules per domain|50 page rules per domain |* 100 page rules per domain  \n * Additional settings for fine-grained control|* 100 page rules per domain  \n * Additional settings for fine-grained control|Not available |Same as Enterprise|
|**Rate limiting rules**|No|No |100|100|Not available |Not available|
|**IP firewall**|* [All IP firewall rule actions](/docs/cis?topic=cis-actions)  \n * Block is not available to `Country` filter  \n * 100 Domain lockdown rules  \n * 250 User agent rules|* [All IP firewall rule actions](/docs/cis?topic=cis-actions)  \n * Block is not available to `Country` filter  \n * 100 Domain lockdown rules  \n * 250 User agent rules|* [All IP firewall rule actions](/docs/cis?topic=cis-actions)  \n * 1000 Domain lockdown rules  \n * 1000 User agent rules|* [All IP firewall rule actions](/docs/cis?topic=cis-actions)  \n * 1000 Domain lockdown rules  \n * 1000 User agent rules|Not available |Same as Enterprise|
|**Caching**|Browser cache minimum TTL 30 minutes|Browser cache minimum TTL 30 minutes|Browser cache minimum TTL 30 seconds|Browser cache minimum TTL 30 seconds|Not available |Same as Enterprise|
|**Range**|No|No |Yes  \n Up to 10 applications  \n Total of 10 TB  \n 5 TB HTTPS  \n 5 TB Range|Yes  \n Up to 10 applications  \n Total of 10 TB  \n 5 TB HTTPS  \n 5 TB Range|No |Same as Enterprise|
|**Edge functions**|1 action  \n (must be named after domain)  \n 1M Edge function requests|1 action  \n (must be named after domain)  \n 1M Edge function requests |Unlimited actions|Unlimited actions|Not available |Not available|
|**Firewall rules**|* 100 active rules  \n * Does not support _Log_ action  \n * Does not support _matches_ operator|* 100 active rules  \n * Does not support _Log_ action  \n * Does not support _matches_ operator |* 1000 active rules  \n * Supports all actions  \n * Supports all operators|* 1000 active rules  \n * Supports all actions  \n * Supports all operators|No |Same as Enterprise|
|**Routing**|No|No |Yes|Yes|No|No|
|**Origin certificates**|Yes|Yes|Yes|Yes|Yes| Yes|
|**Alerts**|No|No|Yes|Yes|Yes |Yes |
{: caption="Table 1. CIS plan comparison" caption-side="bottom"}

|Domain lockdown rules||* 100 active rules|* 1000 active rules|* 1000 active rules|* 1000 active rules|* 1000 active rules|

## Key plan differences
{: #key-plan-differences}

The following table describes the key differences among the available plans. Enterprise Usage and Package plans are available with different pricing models.

| Feature |Standard  \n  (30 day no-cost  \n trial available)|Standard Next|Enterprise Package|Enterprise Usage| Enterprise GLB| Enterprise Security|
| :------ | :-------- |:---------: | :----------: | :---------: | :---------: | :---------: |
|**Enterprise logs**|No|No |Yes|Yes|Yes|Yes|
|**Enterprise analytics**|No|No |Yes|Yes|Yes |Yes|
|**Included domains**|1|1 |10|0|2 |3|
|**Edge functions**|1|1|Unlimited|Unlimited| 0 |0|
|**Protected traffic**   \n (does not include traffic that is related to an attack)|5 TB|0.5 TB |5 TB|0 |5 TB |10 TB|
|**Range  \n (HTTP(S) & TCP protection)**|None |None |5 TB |0|None |0.1 TB|
|**Mutual TLS authentication**|No|No|Yes|Yes |No |Yes|
|**Role based access control**|Yes|Yes|Yes|Yes|Yes |Yes|
|**Rate limiting**|No|No |Yes|Yes|No |No|
|**Smart routing**|No|No |Yes|Yes|No |No|
|**Global load balancers  \n  origin limit**|6|3 |100|100|18 |6|
|**Global load balancers  \n  lowest health check interval**|60s|60s|5s|5s|5s |Not available|
|**Page rules  \n (Caching/Security)**|50|50|100|100|0 |100|
{: caption="Table 2. Key plan differences" caption-side="bottom"}
