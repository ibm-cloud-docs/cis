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

# Why am I not seeing any network traffic?
{:#troubleshooting-cis-network-traffic}
{: help}
{: support}

You don't see any network traffic.
{:tsSymptoms}

There might be a redirect that is routing the traffic to the root domain.
{:tsCauses}

If you’re not seeing traffic, and you’re using a CNAME, make sure that there are no redirects in place that are routing the traffic to the root domain. 
{:tsResolve}


Remember that some DNS propagations can take up to 48 hours to complete.