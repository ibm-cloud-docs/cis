---

copyright:
  years: 2021
lastupdated: "2021-03-01"

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

# Why do I see a privacy warning?
{: #troubleshooting-cis-privacy-warning}

The certificates issued by {{site.data.keyword.cis_short_notm}} cover the root domain (`example.com`) and one level of subdomain (`*.example.com`).
{: shortdesc}

A privacy warning appears in your browser if your new certificate has not yet been issued.
{: tsSymptoms}

If you’re trying to reach a second-level subdomain (`*.*.example.com`) a privacy warning appears in your browser, because these host names are not added to the SAN.
{: tsCauses}

Allow up to 15 minutes for one of our partner Certificates Authorities (CAs) to issue a new certificate.
{: tsResolve}
