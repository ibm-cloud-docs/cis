---

copyright:
  years: 2019, 2023
lastupdated: "2023-09-02"

keywords: firewall rule actions

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Assigning firewall rule actions
{: #actions}

Firewall rule actions tell {{site.data.keyword.cis_short_notm}} how to respond to requests that match the criteria you define. 
{: shortdesc}

For lightweight firewall rules, go to **Security > IP firewall**, which contains IP rules, User Agent rules, and Domain Lockdown rules. Firewall rules are based on IP address, IP address range, Autonomous System Number (ASN), or country/region. 

Domain lockdown rules specify a list of IP addresses, CIDR ranges, or networks that can access a domain, subdomain, or URL. Anything not on the list is blocked.
{: tip}

For more robust firewall rules, go to **Security > Firewall rules**, where you can create rules that examine incoming HTTP traffic against a set of filters to block, challenge, log, or allow matching requests. 

The following table describes the actions that you can assign to your rules. The priority column shows what precedence the action receives. If a request matches two different rules that have the same priority, precedence determines the action to take.

|Action| Available in | Description |Priority|
| ------- | ------- | :--------- |:------:|
|Log|* Firewall rules|Logs matching requests on the {{site.data.keyword.cis_short_notm}} edge for access with Enterprise Logpush and Logpull. Recommended for testing rule effectiveness you commit to a more severe action. Available to Enterprise customers only.|1|
|Bypass|* Firewall rules|Allows dynamic disabling of security features for a request. Exempts matching requests from evaluation, based on a user-defined list that contains one or more of the following features: `Browser Integrity Check`, `Domain Lockdown`, `Hotlink Protection`, `Rate Limiting`, `Security Level`, `User Agent Block`, `WAF Managed Rules`. Matching requests are still subject to evaluation within Firewall Rules, based on order of execution.|2|
|Allow|* Firewall rules  \n * IP firewall|Allows matching requests to access the site, on condition that no other {{site.data.keyword.cis_short_notm}} firewall features block the request, such as IP firewall or access rules.|3|
|Challenge (Captcha)|* Firewall rules  \n * IP firewall  \n * User agent rules|Requires a user to pass a Google reCaptcha Challenge before proceeding. If successful, {{site.data.keyword.cis_short_notm}} accepts the matched request; otherwise, it is blocked.|4|
|JS Challenge|* Firewall rules  \n * IP firewall  \n * User agent rules|JS Challenge|Requires a user to pass a {{site.data.keyword.cis_short_notm}} JavaScript Challenge before proceeding. If successful, {{site.data.keyword.cis_short_notm}} accepts the matched request; otherwise, it is blocked.|5|
|Block|* Firewall rules  \n * IP firewall  \n * User agent rules|Blocks a matching request from accessing the site.|6|
{: caption="Table 1. Firewall rule actions and priority" caption-side="bottom"}
