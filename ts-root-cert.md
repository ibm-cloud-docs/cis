---

copyright:
  years: 2021
lastupdated: "2021-02-05"

keywords: 

subcollection: cis

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# What do I do if I use the Cloudflare Origin root certificate, and it's expiring?
{: #update-origin-root-ca}
{: troubleshoot}

Your origin root certificate has expired, or will soon expire,
{: tsSymptoms}

Some origin web servers (such as IIS and cPanel) validate origin root CA certificates and require you to upload one.
If you are using an expired version of the Cloudflare origin root CA, you must take the following actions to avoid site disruptions.
{: tsCauses}


Select one of the following root certificates to download and install.
{: tsResolve}

* [RSA version certificate](https://cloud.ibm.com/media/docs/downloads/cis/origin_ca_rsa_root.pem) 
* [ECC version certificate](https://cloud.ibm.com/media/docs/downloads/cis/origin_ca_ecc_root.pem) 
