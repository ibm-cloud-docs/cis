---

copyright:
  years: 2018, 2020
lastupdated: "2020-06-12"

keywords: Plan Comparison, Cloud Internet Services, Free Trial, enterprise

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:term: .term}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Plan comparison
{: #cis-plan-comparison}

{{site.data.keyword.cis_full}} offers several plans to choose from: Free Trial, Standard, and Enterprise variations.
{: shortdesc}

The Free Trial Plan is the same as the Standard Plan, but it expires after 30 days. Only one free trail is available per account.
{: note}

The following table compares each offering to help you choose the one that's right for you.

Scroll to the right to view the rest of the table!
{: tip}

|         | Standard<br>(30 day no-cost <br>trial available) | Enterprise Package or Usage | Enterprise GLB | Enterprise Security|  
| :------- | :--------- | :------------ | :--------- | :--------- |
|**Time**|Monthly Billing |Monthly Billing|Monthly Billing|Monthly Billing|
|**Domain**|1|Up to 1000, but recommend no more than 20|2|3|
|**DNS**|3500 records |Multiple Domains (3500 records per Domain) |Same as Enterprise |Same as Enterprise|
|**GLB**|<ul><li>5 Pools</li><li>6 origin servers</li><li>5 Health checks</li><li>60 sec health checks</li><li>Geo Routing</li><li>Health checks from single region</li><li>60s minimum TTL for non-proxied GLBs</li></ul>|<ul><li>Up to 100 pools</li><li>100 origin servers</li><li>Up to 100 health checks</li><li>5 sec health checks</li><li>Smart Routing</li><li>Health checks from multiple regions</li><li>10s minimum TTL for non-proxied GLBs</li></ul>|<ul><li>Up to 100 pools</li><li>18 origin servers</li><li>Up to 100 health checks</li><li>60 sec health checks</li><li>Health checks from multiple regions</li><li>10s minimum TTL for non-proxied GLBs</li></ul>|Not available|
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

| Feature |Standard<br> (30 day no-cost <br>trial available)|Enterprise <br> (Usage & Package <br>plans available)| Enterprise GLB| Enterprise Security|
| :------ | :---------: | :----------: | :---------: | :---------: |
|**Enterprise Logs**|No|Yes|Yes|Yes|
|**Enterprise Analytics**|No|Yes|Yes|Yes|
|**Included Domains**|1|10|2|3|
|**Edge Functions**|1|Unlimited|0|0|
|**Protected Traffic**|5 TB|5 TB|5 TB|10 TB|
|**Custom WAF Rules**|No|Yes|No|Yes|
|**Range<br>(HTTP(S) & TCP <br>Protection**|None |1 TB |None|0.1 TB|
|**Mutual TLS <br>Authentication**|No|Yes|No|No|
|**Role Based<br> Access Control**|Yes|Yes|Yes|Yes|
|**Rate Limiting**|No|Yes|No|No|
|**Smart Routing**|No|Yes|No|No|
|**GLB Origin Limit**|6|Unlimited|0|6|
|**GLB Lowest Health<br> Check Interval**|60s|5s|5s|Not available|
|**Page Rules<br> (Caching/Security)**|50|100|0|0|
