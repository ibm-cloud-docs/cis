---

copyright:
  years: 2018
lastupdated: "2019-06-03"

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

Cloud Internet Services offers three plans to choose from: Free Trial, Standard, and Enterprise. The following table compares each offering to help you choose the one that's right for you. 

Scroll to the right to view the rest of the table!
{: tip}

|         | Free Trial | Standard | Enterprise Package or Usage  
| ------- | :--------- | :------------ | :--------- | 
|**Time**|30 Days Only|Monthly Billing|Monthly Billing|
|**Domain**|1|1|Up to 1000, but recommend no more than 20|
|**DNS**|3500 records per Domain| 3500 records per Domain| Multiple Domains and Subdomains|
|**GLB**|<ul><li>6 origin servers</li><li>60 sec health checks</li><li>Geo Routing</li><li>Health checks from single region</li><li>60s minimum TTL for non-proxied GLBs</li></ul>|<ul><li>6 origin servers</li><li>60 sec health checks</li><li>Geo Routing</li><li>Health checks from single region</li><li>60s minimum TTL for non-proxied GLBs</li></ul>|<ul><li>100 origin servers</li><li>5 sec health checks</li><li>Smart Routing</li><li>Health checks from multiple regions</li><li>10s minimum TTL for non-proxied GLBs</li></ul>|
|**WAF**|Preconfigured rules|Preconfigured rules|Preconfigured and custom rules|
|**DDoS**|On (with Proxy) or Off (no Proxy)|On (with Proxy) or Off (no Proxy)|On (with Proxy) or Off (no Proxy)|
|**TLS**|<ul><li>1 Universal wildcard</li><li>1 Dedicated wildcard</li><li>1 Dedicated custom</li><li>1 Uploaded custom</li></ul>|<ul><li>1 Universal wildcard</li> <li>1 Dedicated wildcard</li><li>1 Dedicated custom</li><li>1 Uploaded custom</li></ul>|<ul><li>1 Universal wildcard per domain. Up to 10 free certificates per CIS instance</li> <li>2 Dedicated wildcard with ability to request more</li><li>10 Dedicated custom</li><li>1 Uploaded custom</li></ul>
|**Page Rules**|50 Page Rules|50 Page Rules|<ul><li>100 Page Rules</li><li>Additional settings for fine-grained control</li></ul> |
|**Rate Limiting**|No|No|Yes|
|**IP Firewall**|<ul><li>Challenge</li><li>Block (Not available to `Country` filter)</li><li>JS Challenge</li><li>Whitelist</li></ul>|<ul><li>Challenge</li><li>Block (Not available to `Country` filter)</li><li>JS Challenge</li><li>Whitelist</li></ul>|<ul><li>Challenge</li><li>Block</li><li>JS Challenge</li><li>Whitelist</li></ul>|
|**Caching**|Browser cache minimum TTL 30 minutes|Browser cache minimum TTL 30 minutes|Browser cache minimum TTL 30 seconds|
|**Range**|No|No|Yes<br/>(at additional cost per GB)|
|**Edge Functions (Beta)**|1 action<br/>(must be named after domain)|1 action<br/>(must be named after domain)|Unlimited actions|
|**Firewall Rules**|<ul><li>100 active rules</li><li>Does not support _Log_ action</li><li>Does not support _matches_ operator</li><ul>|<ul><li>100 active rules</li><li>Does not support _Log_ action</li><li>Does not support _matches_ operator</li><ul>|<ul><li>1000 active rules</li><li>Supports all actions</li><li>Supports all operators</li><ul>|
|**Routing**|No|No|Yes|  
|**Origin Certificates**|Yes|Yes|Yes| 
|**Logpull/Logpush**|No|No|Yes|   
