---

copyright:
  years: 2018, 2020
lastupdated: "2020-07-06"

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

The Free Trial Plan is the same as the Standard Plan, except that it expires after 30 days. Only one free trail is available per account.
{: note}

The following table compares each offering to help you choose the one that's right for you.

|         | Standard<br>(30 day no-cost <br>trial available) | Enterprise Package or Usage | Enterprise GLB | Enterprise Security|  
| :------- | :--------- | :------------ | :--------- | :--------- |
|**Time**|Monthly Billing |Monthly Billing|Monthly Billing|Monthly Billing|
|**Domain**|1|Up to 1000, but recommend no more than 20|2|3|
|**DNS**|3500 records |Multiple Domains (3500 records per Domain) |Same as Enterprise |Same as Enterprise|
|**Global load balancers**|<ul><li>5 Pools</li><li>6 origin servers</li><li>5 Health checks</li><li>60s health checks</li><li>Geo Routing</li><li>Health checks from single region</li><li>60s minimum TTL for non-proxied global load balancers</li></ul>|<ul><li>Up to 100 pools</li><li>100 origin servers</li><li>Up to 100 health checks</li><li>5s health checks</li><li>Smart Routing</li><li>Health checks from multiple regions</li><li>10s minimum TTL for non-proxied global load balancers</li></ul>|<ul><li>Up to 100 pools</li><li>18 origin servers</li><li>Up to 100 health checks</li><li>60s health checks</li><li>Health checks from multiple regions</li><li>10s minimum TTL for non-proxied global load balancers</li></ul>|Not available|
|**WAF**|Preconfigured rules|Preconfigured and custom rules|Not available|Same as Enterprise|
|**DDoS**|On (with proxy) or Off (no proxy)|On (with proxy) or Off (no proxy)|Yes (proxy)|Yes|
|**TLS**|<ul><li>1 universal wildcard</li><li>1 dedicated wildcard</li><li>1 Dedicated custom</li><li>1 Uploaded custom</li></ul>|<ul><li>1 Universal wildcard per domain; up to 10 free certificates per {{site.data.keyword.cis_short_notm}} instance</li> <li>2 dedicated wildcards with ability to request more</li><li>10 dedicated custom</li><li>1 Uploaded custom</li></ul>|<ul><li>1 universal wildcard per domain; up to 10 free certificates per {{site.data.keyword.cis_short_notm}} instance</li> <li>2 dedicated wildcards with ability to request more</li><li>2 dedicated custom</li><li>1 uploaded custom</li></ul>|<ul><li>1 universal wildcard per domain; up to 10 free certificates per {{site.data.keyword.cis_short_notm}} instance</li> <li>2 Dedicated wildcard with ability to request more</li><li>3 dedicated custom</li><li>1 uploaded custom</li></ul>|
|**Logpull/Logpush**|No|Yes|Yes|Yes|
|**Page Rules**|50 page rules|<ul><li>100 page rules</li><li>Additional settings for fine-grained control</li></ul>|Not available |Same as Enterprise|
|**Rate Limiting**|No|Yes|Not available|Not available|
|**IP Firewall**|<ul><li>Challenge</li><li>Block (Not available to `Country` filter)</li><li>JS challenge</li><li>Allowlist</li></ul>|<ul><li>Challenge</li><li>Block</li><li>JS challenge</li><li>Allowlist</li></ul>|Not available|Same as Enterprise|
|**Caching**|Browser cache minimum TTL 30 minutes|Browser cache minimum TTL 30 seconds|Not available|Same as Enterprise|
|**Range**|No|Yes<br>Total of 10 TB<br>5 TB HTTPS<br>5 TB range|No|Same as Enterprise|
|**Edge Functions**|1 action<br/>(must be named after domain)|Unlimited actions|Not available|Not available|
|**Firewall Rules**|<ul><li>100 active rules</li><li>Does not support _Log_ action</li><li>Does not support _matches_ operator</li></ul>|<ul><li>1000 active rules</li><li>Supports all actions</li><li>Supports all operators</li></ul>|No|Same as Enterprise|
|**Routing**|No|Yes|No|No |
|**Origin Certificates**|Yes|Yes|Yes| Yes|



## Key plan differences
{: #key-plan-differences}

The following table describes the key differences among the available plans.

| Feature |Standard<br> (30 day no-cost <br>trial available)|Enterprise <br> (Usage and Package <br>plans available)| Enterprise GLB| Enterprise security|
| :------ | :---------: | :----------: | :---------: | :---------: |
|**Enterprise logs**|No|Yes|Yes|Yes|
|**Enterprise analytics**|No|Yes|Yes|Yes|
|**Included domains**|1|10|2|3|
|**Edge functions**|1|Unlimited|0|0|
|**Protected traffic**|5 TB|5 TB|5 TB|10 TB|
|**Custom WAF rules**|No|Yes|No|Yes|
|**Range<br>(HTTP(S) & TCP <br>Protection**|None |1 TB |None|0.1 TB|
|**Mutual TLS <br>Authentication**|No|Yes|No|No|
|**Role based<br> Access Control**|Yes|Yes|Yes|Yes|
|**Rate limiting**|No|Yes|No|No|
|**Smart routing**|No|Yes|No|No|
|**Global load balancers origin limit**|6|Unlimited|0|6|
|**Global load balancersLB lowest health<br> Check interval**|60s|5s|5s|Not available|
|**Page rules<br> (Caching/Security)**|50|100|0|0|
