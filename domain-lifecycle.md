---

copyright:
  years: 2021, 2025
lastupdated: "2025-06-03"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Domain lifecycle and state transitions
{: #domain-lifecycle-concepts}

Domains that are configured in {{site.data.keyword.cis_short_notm}} begin in **Pending** state, and become **Active** after the domain's authoritative name servers are configured correctly at the DNS provider or registrar.
{: shortdesc}

The following diagram shows a sample domain lifecycle, with labels that correspond to the list of domain state transitions:

1. Adding a domain to a {{site.data.keyword.cis_short_notm}} instance puts the domain in **Pending** state. Authoritative name servers are assigned but not yet configured at the DNS provider or registrar.
1. After the authoritative name server records are configured correctly at the DNS provider or registrar, the domain becomes **Active**.
1. (Enterprise only): Deleting the domain sets its status as **Deletion pending**. For Enterprise plan domains, deletion is not immediate and can take up to 24 hours.
1. (Enterprise only): After the deletion period, the domain is fully deleted.
1. (Standard): A Standard plan level instance can be deleted immediately.
1. The domain's name server configuration is regularly monitored. If the authoritative name server's settings change at the DNS provider or registrar, the domain enters the **Moved** state. This condition might occur when moving the domain to a different {{site.data.keyword.cis_short_notm}} instance, or when the name server configuration is incorrect.

   A domain in the **Moved** state might stop serving traffic and can be deleted. If you believe that your domain is incorrectly marked as **Moved**, [contact IBM Support](/docs/cis?topic=cis-gettinghelp).
   {: important}

1. Domains in the **Moved** state might be deleted automatically or can be deleted by the user.

![Diagram of domain lifecycle](images/domain-lifecycle-lt.png "Diagram of domain lifecycle"){: caption="Domain lifecycle" caption-side="bottom"}

## Domain lifecycle states
{: #domain-lifecycle-states}

You might encounter the following domain lifecycle states:

- **Pending** - The zone was added to a {{site.data.keyword.cis_short_notm}} instance, and the DNS configuration is being verified at the DNS provider or registrar to activate the domain. After the correct name servers (or the CNAME validation records) are confirmed, the domain changes to **Active**. Otherwise, it remains **Pending**.
- **Active** - The DNS configuration was successfully verified and the domain is actively serving traffic.
- **Moved** - The zone was previously **Active**, but DNS validation detected that the domain is no longer configured for the assigned authoritative name servers only, for a number of repeated checks. This state indicates the start of zone deprovisioning. The domain stays in **Moved** state for 7 days, or indefinitely if an active subscription on the zone exists. If the same domain becomes **Active** or **Pending** in a different account, this domain no longer serves traffic because **Pending** or **Active** zones take precedence.
- **Deletion pending** - (Enterprise only) The customer initiated the deletion of this domain from the {{site.data.keyword.cis_short_notm}} instance. Enterprise domains can take up to 24 hours to be removed.
- **Deleted** - This state indicates that the domain was removed from a customer's dashboard and its services are deprovisioned, but not removed from the Cloudflare database.
