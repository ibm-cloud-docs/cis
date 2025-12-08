---

copyright:
  years: 2018, 2025
lastupdated: "2025-12-08"

keywords: IBM Cloud Internet Services, IBM CIS application, CIS

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Configuring your name servers with the registrar or existing DNS provider
{: #name-servers} 

To begin receiving the benefits of {{site.data.keyword.cis_short_notm}}, you must delegate your domain to {{site.data.keyword.cis_short_notm}}. To delegate a domain, create an NS record with the name servers provided by {{site.data.keyword.cis_short_notm}} at your domain's registrar or existing DNS provider. If you are unsure of who the registrar is for your domain, you can look it up at [lookup.icann.org](https://lookup.icann.org/en){: external}.

If you delegate a subdomain (for instance, `subdomain.example.com`) from another DNS provider, you must replace the existing name server (NS) records and replace them with a name server record for each of the name servers that are provided by {{site.data.keyword.cis_short_notm}}. See [Managing DNS records in Cloudflare](https://developers.cloudflare.com/dns/manage-dns-records/how-to/create-dns-records/){: external} for instructions by provider.

After you configure your registrar or DNS provider, it can take up to 24 hours for the changes to take effect. When we verify that the specified name servers were configured correctly for your domain or subdomain, the domain's status changes from `Pending` to `Active`.

Your domain must move to `Active` state within 60 days or your domain and any configuration data is removed.
{: important}
