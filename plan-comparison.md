---

copyright:
  years: 2018, 2021
lastupdated: "2021-09-28"

keywords: 

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Plan comparison
{: #cis-plan-comparison}

{{site.data.keyword.cis_full}} offers several plans to choose from: Free Trial, Standard, and Enterprise variations.
{: shortdesc}

The Free Trial plan is the same as the Standard plan, except that it expires after 30 days. Only one free trial is available per account.
{: note}

The numbers in these tables are quotas or resource limits for the associated feature. Features are pay-as-you-go, except for Free Trial and Standard plans.
{: tip}

The following table compares each offering to help you choose the one that's right for you. Enterprise usage and package plans are available with different pricing models.

| | Standard  \n (30 day no-cost  \n trial available) | Enterprise  \n Package or Usage  \n (different pricing models) | Enterprise GLB | Enterprise Security|  
| :------- | :--------- | :------------ | :--------- | :--------- |
|**Time**|Monthly billing |Monthly billing|Monthly billing|Monthly billing|
|**Domain**|1|Up to 1000, but recommend no more than 20|2|3|
|**DNS**|3500 records |Multiple domains (3500 records per Domain) |Same as Enterprise |Same as Enterprise|
|**Global load balancers**|* 5 Pools  \n * 6 origin servers  \n * 5 Health checks  \n * 60s health checks  \n * Geo Routing  \n * Health checks from single region  \n * 60s minimum TTL for non-proxied global load balancers |* Up to 100 pools  \n * 100 origin servers  \n * Up to 100 health checks  \n * 5s health checks  \n * Smart Routing  \n * Health checks from multiple regions  \n * 10s minimum TTL for non-proxied global load balancers|* Up to 100 pools  \n * 18 origin server  \n * Up to 100 health checks  \n * 60s health checks  \n * Health checks from multiple regions  \n * 10s minimum TTL for non-proxied global load balancers|Not available|
|**WAF**|Yes (OWASP and CIS rule set)|Yes (OWASP and CIS rule set)|Not available|Yes (OWASP and CIS rule set)|
|**DDoS**|On (with proxy) or Off (no proxy)|On (with proxy) or Off (no proxy)|Yes (proxy)|Yes|
|**TLS**|* 1 universal wildcard per domain  \n * 1 dedicated wildcard per domain  \n * 1 Dedicated custom per domain  \n * 1 Uploaded custom per domain|* 1 Universal wildcard per domain; up to 10 free certificates per {{site.data.keyword.cis_short_notm}} instance  \n * 2 dedicated wildcards per domain, with ability to request more  \n * 10 dedicated custom per domain  \n * 1 Uploaded custom per domain|* 1 universal wildcard per domain; up to 10 free certificates per {{site.data.keyword.cis_short_notm}} instance  \n * 2 dedicated wildcards per domain, with ability to request more  \n * 2 dedicated custom per domain  \n * 1 uploaded custom per domain|* 1 universal wildcard per domain; up to 10 free certificates per {{site.data.keyword.cis_short_notm}} instance  \n * 2 Dedicated wildcard per domain, with ability to request more  \n * 3 dedicated custom per domain  \n * 1 uploaded custom per domain|
|**Logpull/Logpush**|No|Yes|Yes|Yes|
|**Page rules**|50 page rules per domain|* 100 page rules per domain  \n * Additional settings for fine-grained control|Not available |Same as Enterprise|
|**Rate limiting rules**|No|100|Not available|Not available|
|**IP firewall**|* Challenge  \n * Block (Not available to `Country` filter)  \n * JS challenge  \n * Allowlist|* Challenge  \n * Block  \n * JS challenge  \n * Allowlist|Not available|Same as Enterprise|
|**Caching**|Browser cache minimum TTL 30 minutes|Browser cache minimum TTL 30 seconds|Not available|Same as Enterprise|
|**Range**|No|Yes  \n Up to 10 applications  \n Total of 10 TB  \n 5 TB HTTPS  \n 5 TB Range|No|Same as Enterprise|
|**Edge functions**|1 action  \n (must be named after domain)  \n 1M Edge function requests|Unlimited actions|Not available|Not available|
|**Firewall rules**|* 100 active rules  \n * Does not support _Log_ action  \n * Does not support _matches_ operator|* 1000 active rules  \n * Supports all actions  \n * Supports all operators|No|Same as Enterprise|
|**Routing**|No|Yes|No|No |
|**Origin certificates**|Yes|Yes|Yes| Yes|
{: caption="Table 1. CIS plan comparison" caption-side="bottom"}



## Key plan differences
{: #key-plan-differences}

The following table describes the key differences among the available plans. Enterprise Usage and Package plans are available with different pricing models.

| Feature |Standard  \n  (30 day no-cost   \n trial available)|Enterprise  \n (Usage and Package  \n plans available)| Enterprise GLB| Enterprise Security|
| :------ | :---------: | :----------: | :---------: | :---------: |
|**Enterprise logs**|No|Yes|Yes|Yes|
|**Enterprise analytics**|No|Yes|Yes|Yes|
|**Included domains**|1|10|2|3|
|**Edge functions**|1|Unlimited|0|0|
|**Protected traffic**|5 TB|5 TB|5 TB|10 TB|
|**Range  \n (HTTP(S) & TCP   \n protection**|None |1 TB |None|0.1 TB|
|**Mutual TLS  \n authentication**|No|Yes|No|Yes|
|**Role based  \n access control**|Yes|Yes|Yes|Yes|
|**Rate limiting**|No|Yes|No|No|
|**Smart routing**|No|Yes|No|No|
|**Global load balancers origin limit**|6|100|18|6|
|**Global load balancers lowest health  \n Check interval**|60s|5s|5s|Not available|
|**Page rules  \n (Caching/Security)**|50|100|0|100|
{: caption="Table 1. Key plan differences" caption-side="bottom"}
