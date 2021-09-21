---

copyright:
  years: 2021
lastupdated: "2021-02-05"

keywords: 

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
{:note:.deprecated}
{:external: target="_blank" .external}
{:table: .aria-labeledby="caption"}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:support: data-reuse='support'}
{:troubleshoot: data-hd-content-type='troubleshoot'}


# Why is my website offline?
{: #troubleshooting-cis-website-offline}

Here is what you might see: `IBM CIS cannot connect to the origin server (error 521, 522, 523)`.

**Website offline - no cached version**
{: tsSymptoms}


1. The server is online, but it is blocking the {{site.data.keyword.cis_short_notm}} request.
2. The origin server is offline and {{site.data.keyword.cis_short_notm}}S does not have a backup website image
{: tsCauses}


* Verify that the {{site.data.keyword.cis_short_notm}} IP addresses are allowlisted.
* Make sure that {{site.data.keyword.cis_short_notm}} IPs are not being rate-limited.
* Review the list of [IPs to allowlist](/docs/cis?topic=cis-cis-allowlisted-ip-addresses).
{: tsResolve}
