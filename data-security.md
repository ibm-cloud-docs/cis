---

copyright:
  years: 2020
lastupdated: "2020-07-19"

keywords: data encryption in cis, data storage for cis, data deletion for cis, data in cis, data security in cis

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

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

The {{site.data.keyword.cis_short_notm}} data retention policy describes how long your data is stored after you delete the service. The data retention policy is included in the {{site.data.keyword.cis_short_notm}} service description, which you can find in [{{site.data.keyword.cloud_notm}} Terms](/docs/overview?topic=overview-terms). When a {{site.data.keyword.cis_short_notm}} instance is deleted by the UI, CLI, or API, the instance data is retained for seven days from deletion.

Before deleting an instance, all the domains in the instance must be removed.
{: note}

Deleting the {{site.data.keyword.cis_short_notm}} instance removes all data.

### Restoring deleted data for {{site.data.keyword.cis_short_notm}}
{: #data-restore}

{{site.data.keyword.cis_short_notm}} can currently restore the deleted instance. 
After you delete an instance of {{site.data.keyword.cis_short_notm}}, you can restore the deleted service instance within the data retention period of seven days. After the seven-day period expires, the service instance is permanently deleted.

To view which service instances are available for restoration, use the `ibmcloud resource reclamations` command. To restore a deleted service instance, use the `ibmcloud resource reclamation-restore` command.
