---

copyright:
  years: 2023, 2024
lastupdated: "2024-10-18"

keywords:

subcollection: cis

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is my domain still in `Moved` status?
{: #domain-moved-status}
{: troubleshoot}

You have a domain that should be `Active`, but is still in the `Moved` status.
{: tsSymptoms}

{{site.data.keyword.cis_short_notm}} becomes the authoritative DNS provider for your domain when your domain points to {{site.data.keyword.cis_short_notm}} name servers. During the setup process {{site.data.keyword.cis_short_notm}} detects the name servers and activates the domain.
{: tsCauses}

- If the name servers no longer point to {{site.data.keyword.cis_short_notm}}, the system automatically mark your domain as `Moved` after 7 days. An email to inform you of this status change is sent to the email address on file. A domain in `Moved` status remains in the system for an additional 7 days before it is permanently deleted.
- Conflicting NS records can cause a domain to change to `Moved` status.

To resolve the condition where your domain remains in `Moved` status longer than expected, take the following troubleshooting steps.
{: tsResolve}

- Check your DNS registrar and ensure that the NS records match with the NS records given by {{site.data.keyword.cis_short_notm}}.
    - Find the NS records in the **CIS name servers** section of the **DNS** tab in the **Reliability** page. For more information, see [Step 4. Configure your name servers with the registrar or existing DNS provider](/docs/cis?topic=cis-getting-started#configure-your-name-servers-with-the-registrar-or-existing-dns-provider).
- Run the activation check API again. You can use the [API endpoint](/apidocs/cis#zone-activation-check) first to initiate the recheck.
    - As long as the NS values for the domain are pointed in the correct direction by a dig, and the reactivation check is done by using the API, the domain should go from `Moved` status to `Active`.
- Remove and replace any previous NS records with the {{site.data.keyword.cis_short_notm}}-provided records in your DNS registrar.

If the domain is still stuck in a `Moved` status after taking these steps, [open a Support](/docs/cis?topic=cis-gettinghelp) case with details about which steps you took.
