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

# What do I do if I use the Cloudflare Origin root certificate, and it's expiring?
{: #update-origin-root-ca}

Your origin root certificate has expired, or will soon expire,
{:tsSymptoms}

Some origin web servers (such as IIS and cPanel) validate origin root CA certificates and require you to upload one.
If you are using an expired version of the Cloudflare origin root CA, you must take the following actions to avoid site disruptions.
{:tsCauses}


Select one of the following root certificates to download and install.
{:tsResolve}

  * [RSA version certificate.](https://cloud.ibm.com/media/docs/downloads/cis/origin_ca_rsa_root.pem) 
  * [ECC version certificate.](https://cloud.ibm.com/media/docs/downloads/cis/origin_ca_ecc_root.pem) The previous version expires on 2021-02-22T00:24:00Z.
