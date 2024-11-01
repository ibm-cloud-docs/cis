---

copyright:
  years: 2024
lastupdated: "2024-11-01"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Converting a partial (CNAME) configuration to full
{: #convert-partial-cname-full}

[NEEDS REVIEW - ENTIRE]{: tag-red}

If you initially set up a partial domain, you can later migrate it to a full setup.
{: shortdesc}

## Before you begin
{: #before-you-begin-convert-partial-to-full}

When preparing Transport Layer Security (TLS), you can use Universal SSL. Keep in mind:

   * Universal certificates can take at least 15 minutes to be issued.
   * You will need to add {{site.data.keyword.cis_short_notm}} name servers to your registrar within 72 hours of the conversion process.
   * Universal SSL supports only first-level subdomains.
   * To minimize downtime, it is recommended that you have a certificate in place before you start the conversion process.

## Converting to a full CNAME configuration
{: #convert-to-full-configuration}

To convert from a partial to a full CNAME configuration, follow these steps:

1. Prepare TLS. In the {{site.data.keyword.cis_short_notm}} instance, order an advanced certificate or upload a custom SSL certificate for your website or application.

   Verify that the status of your SSL certificate is `Active`.
   {: note}
   
1. Update settings in your authoritative DNS:

   1. Disable DNSSEC at your authoritative DNS provider at least 24 hours prior to converting your zone.
   1. As a best practice, you should also delete the previous zone activation `TXT` record at your authoritative DNS provider. Locate this value in the {{site.data.keyword.cis_short_notm}} instance in **DNS > Records** where the value is listed as the Verification TXT Record.

1. Convert to a full setup:

   1. Go to **DNS > Settings**.
   1. Select **Convert to Primary DNS**. This action does not affect how your traffic is proxied.
   1. Import your records into {{site.data.keyword.cis_short_notm}} DNS and verify that the records have been configured correctly.
  
    It is recommended to import unproxied records.
    {: note}
 
1. Activate the full setup:

   1. Get your assigned {{site.data.keyword.cis_short_notm}} name servers from **DNS > Records** and update your name servers at your registrar.

   If you rely on Universal SSL certificates to cover your website or application, make sure to add {{site.data.keyword.cis_short_notm}} name servers to your registrar within 72 hours of the conversion process.
   {: important}

   1. It is recommended to enable DNSSEC from **DNS > Settings**, then add the `DS` record to your registrar.

      After all of the DNS TTLs expire, all of your DNS queries are answered by the {{site.data.keyword.cis_short_notm}} global network.

   1. Enable the proxy status for specific DNS records to begin proxying additional hostnames. Subdomains that were proxied previously continue to be proxied without any interruption.
