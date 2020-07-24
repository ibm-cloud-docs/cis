---

copyright:
  years: 2020
lastupdated: "2020-07-06"

keywords: data encryption in cis, data storage for cis, bring your own keys for dns services, BYOK for dns services, key management for dns services, key encryption for dns services, personal data in dns services, data deletion for dns services, data in dns services, data security in dns services

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



# Securing your data in {{site.data.keyword.cis_short_notm}}
{: #mng-data}

To ensure that you can securely manage your data when you use {{site.data.keyword.cis_full}}, it is important to know exactly what data is stored and encrypted and how to delete any stored personal data.
{: shortdesc}

## How your data is stored and encrypted in {{site.data.keyword.cis_short_notm}}
{: #data-storage}

{{site.data.keyword.cis_short_notm}} interacts with Cloudflare services using a channel that is fully encrypted end-to-end using Transport Layer Security (TLS) 1.2. {{site.data.keyword.cis_short_notm}} does not store any customer data. Configuration data about your specific {{site.data.keyword.cis_short_notm}} configuration is encrypted in transit and at rest. {{site.data.keyword.cis_short_notm}} configuration data is deleted on your request through the UI, CLI, or API.

## Protecting your sensitive data in {{site.data.keyword.cis_short_notm}}
{: #data-encryption}

All data related to {{site.data.keyword.cis_short_notm}} configuration is not considered sensitive data. The configuration data is encrypted at rest. No customer-managed keys are managed by the {{site.data.keyword.cis_short_notm}} offering. Therefore, neither Key Protect nor Hyper Protect Crypto Services are used.

### Working with customer-managed keys for {{site.data.keyword.cis_short_notm}}
{: #working-with-keys}

No customer-managed keys are managed by the {{site.data.keyword.cis_short_notm}} offering.

## Deleting your data in {{site.data.keyword.cis_short_notm}}
{: #data-delete}

The {{site.data.keyword.cis_short_notm}} configuration data is deleted on request through the UI, CLI or API.

### Deleting {{site.data.keyword.cis_short_notm}} instances
{: #service-delete}

The {{site.data.keyword.cis_short_notm}} data retention policy describes how long your data is stored after you delete the service. The data retention policy is included in the {{site.data.keyword.cis_short_notm}} service description, which you can find in [{{site.data.keyword.cloud_notm}} Terms](/docs/overview?topic=overview-terms).

Deleting the {{site.data.keyword.cis_short_notm}} instance removes all data.

### Restoring deleted data for {{site.data.keyword.cis_short_notm}}
{: #data-restore}

{{site.data.keyword.cis_short_notm}} cannot currently restore deleted data.
