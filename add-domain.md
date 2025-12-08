---

copyright:
  years: 2025
lastupdated: "2025-12-08"

keywords: domains

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Configuring a full (authoritative) zone
{: #domains}

FROM EXISTING GETTING STARTED

Next, begin protecting and improving the performance of your web service by entering your domain or a subdomain.

Note: Specify DNS zones. You can configure the name servers for these domains or subdomains at the domain's registrar or DNS provider. Do not use CNAMEs.

The Overview page shows your domain in Pending status and remains Pending until you complete configuring your name servers with the registrar or existing DNS provider, which is covered in Step 4.

Tip: You can't delete the CIS instance after you add a domain. To delete the instance, delete the domain from the instance first.

FROM DAVID LENTZ

1. If there are no domains in the  {{site.data.keyword.cis_short_notm}} instance press the blue 'Add Domain' button and skip to **Step 3**.
1. If there are domains listed at the top of the  {{site.data.keyword.cis_short_notm}} instance page click the "..." overflow menu on the same row as the Domain and select **New Domain**.
1. A section will appear on the right side of the page which will step you through Connecting the domain,
1. Enter the name of the Domain and click Next
1. It is recommended that you import or recreate your DNS records in {{site.data.keyword.cis_short_notm}} . Import the DNS records you've exported from your current DNS, or manually create your DNS records. To import records, select Import records.
1. Delegate your Domain to {{site.data.keyword.cis_short_notm}}  in order to receive all benefits of your chosen plan. [Learn more about delegating domain management](https://cloud.ibm.com/docs/cis?topic=cis-getting-started#configure-your-name-servers-with-the-registrar-or-existing-dns-provider)

The {{site.data.keyword.cis_short_notm}} instance will detect when the domain delegation is complete automatically. Domain delegation can take several hours to a day depending on the DNS service being used to delegate.

At this point the Domain is added to {{site.data.keyword.cis_short_notm}} however it will remain in `Pending` status until {{site.data.keyword.cis_short_notm}} detects the domain delegation is complete.

If you lose connection to the IBM Cloud console, or close your web browser you can check the status of the Domain by navigating to the {{site.data.keyword.cis_short_notm}} instance page on the IBM Cloud console.
