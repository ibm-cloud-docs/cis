---

copyright:
  years: 2018
lastupdated: "2019-08-19"

keywords: Plan Comparison, Cloud Internet Services, Free Trial, enterprise

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}

# Plan Comparison
{: #cis-plan-comparison}

{{site.data.keyword.cis_full}} offers several plans to choose from: Free Trial, Standard, and Enterprise variations.
{: shortdesc}

The Free Trial Plan is the same as the Standard Plan, but it expires after 30 days.
{: note}

The following table compares each offering to help you choose the one that's right for you.

Scroll to the right to view the rest of the table!
{: tip}

|         | Standard | Enterprise Package or Usage | Enterprise GLB | Enterprise Security|  
| :------- | :--------- | :------------ | :--------- | :--------- |
|**Time**|Monthly Billing |Monthly Billing|Monthly Billing|Monthly Billing|
|**Domain**|1|Up to 1000, but recommend no more than 20|2|3|
|**DNS**|3500 records |Multiple Domains (3500 records per Domain) |Same as Enterprise |Same as Enterprise|
|**GLB**|<ul><li>6 origin servers</li><li>60 sec health checks</li><li>Geo Routing</li><li>Health checks from single region</li><li>60s minimum TTL for non-proxied GLBs</li></ul>|<ul><li>100 origin servers</li><li>5 sec health checks</li><li>Smart Routing</li><li>Health checks from multiple regions</li><li>10s minimum TTL for non-proxied GLBs</li></ul>|<ul><li>18 origin servers</li><li>5 sec health checks</li><li>Health checks from multiple regions</li><li>10s minimum TTL for non-proxied GLBs</li></ul>|Not available|
|**WAF**|Preconfigured rules|Preconfigured and custom rules|Not available|Same as Enterprise|
|**DDoS**|On (with Proxy) or Off (no Proxy)|On (with Proxy) or Off (no Proxy)|Yes (Proxy)|Yes|
|**TLS**|<ul><li>1 Universal wildcard</li><li>1 Dedicated wildcard</li><li>1 Dedicated custom</li><li>1 Uploaded custom</li></ul>|<ul><li>1 Universal wildcard per domain. Up to 10 free certificates per {{site.data.keyword.cis_short_notm}} instance</li> <li>2 Dedicated wildcard with ability to request more</li><li>10 Dedicated custom</li><li>1 Uploaded custom</li></ul>|<ul><li>1 Universal wildcard per domain. Up to 10 free certificates per {{site.data.keyword.cis_short_notm}} instance</li> <li>2 Dedicated wildcard with ability to request more</li><li>2 Dedicated custom</li><li>1 Uploaded custom</li></ul>|<ul><li>1 Universal wildcard per domain. Up to 10 free certificates per {{site.data.keyword.cis_short_notm}} instance</li> <li>2 Dedicated wildcard with ability to request more</li><li>3 Dedicated custom</li><li>1 Uploaded custom</li></ul>|
|**Logpull/Logpush**|No|Yes|Yes|Yes|
|**Page Rules**|50 Page Rules|<ul><li>100 Page Rules</li><li>Additional settings for fine-grained control</li></ul>|Not available |Same as Enterprise|
|**Rate Limiting**|No|Yes|Not available|Not available|
|**IP Firewall**|<ul><li>Challenge</li><li>Block (Not available to `Country` filter)</li><li>JS Challenge</li><li>Whitelist</li></ul>|<ul><li>Challenge</li><li>Block</li><li>JS Challenge</li><li>Whitelist</li></ul>|Not available|Same as Enterprise|
|**Caching**|Browser cache minimum TTL 30 minutes|Browser cache minimum TTL 30 seconds|Not available|Same as Enterprise|
|**Range**|No|Yes<br>Total of 10 TB<br>5 TB HTTPS<br>5 TB Range|No|Same as Enterprise|
|**Edge Functions**|1 action<br/>(must be named after domain)|Unlimited actions|Not available|Not available|
|**Firewall Rules**|<ul><li>100 active rules</li><li>Does not support _Log_ action</li><li>Does not support _matches_ operator</li></ul>|<ul><li>1000 active rules</li><li>Supports all actions</li><li>Supports all operators</li></ul>|No|Same as Enterprise|
|**Routing**|No|Yes|No|No |
|**Origin Certificates**|Yes|Yes|Yes| Yes|



## Key plan differences
{: #key-plan-differences}

The following table describes the key differences among the available plans.

| Feature | CIS Enterprise <br> (Usage & Package <br>plans available)| CIS GLB| CIS Security| CIS Standard<br> (30 day no-cost <br>trial available)|
| :-------: | :---------: | :----------: | :---------: | :---------: |
|Enterprise Logs|Yes|Yes|Yes|No|
|Enterprise Analytics|Yes|Yes|Yes|No|
|Included Domains|10|2|3|1|
|Edge Functions|Unlimited|No|No|1|
|Protected Traffic|5 TB|5 TB|10 TB|5 TB|
|Custom WAF Rules| Yes|No| Yes|No|
|CIS Range<br>(HTTP(S) & TCP <br>Protection|1 TB |No |0.1 TB| No|
|Mutual TLS <br>Authentication|Yes|No|No|No|
|Role Based<br> Access Control|Yes|Yes|Yes|Yes|
|Rate Limiting| Yes| No| No|No|
|Smart Routing| Yes| No| No|No|
|GLB Origin Limit| Unlimited|18|0|6|
|GLB Lowest Health<br> Check Interval|5s|5s|No|60s|
|Page Rules<br> (Caching/Security)|100|No|No|50|
