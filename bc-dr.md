---

copyright:
  years: 2024
lastupdated: "2024-11-12"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Understanding business continuity and disaster recovery for CIS
{: #bc-dr}

[Disaster recovery](#x2113280){: term} involves a set of policies, tools, and procedures for returning a system, an application, or an entire data center to full operation after a catastrophic interruption. It includes procedures for copying and storing an installed system's essential data in a secure location, and for recovering that data to restore normalcy of operation.
{: shortdesc}

## Responsibilities
{: #bc-dr-responsibilities}

To find out more about responsibility ownership for using {{site.data.keyword.cloud}} products between {{site.data.keyword.IBM_notm}} and customer see [Understanding your responsibilities when using CIS](/docs/cis?topic=cis-responsibilities-cis).

## Disaster recovery strategy
{: #bc-dr-strategy}

{{site.data.keyword.cloud_notm}} has [business continuity](#x3026801){: term} plans in place to provide for the recovery of services within hours if a disaster occurs. You are responsible for your data backup and associated recovery of your content.

CIS provides mechanisms to protect your data and restore service functions. Business continuity plans are in place to achieve targeted [recovery point objective](#x3429911){: term} (RPO) and [recovery time objective](#x3167918){: term} (RTO) for the service. The following table outlines the targets for CIS.

| Disaster recovery objective | Target value |
|---|---|
|  RPO | Failover happens almost instantly (within seconds) if internal, as it switches to another cluster. However, if Cloudflare experiences downtime or issues, data will be unavailable until they are back online, as CIS is a stateless service. |
|  RTO |  Recovery time for CIS is approximately 1 hour per cluster, including verification and other processes, with a best-case recovery time of 3 hours, or up to 4 hours if padding time is added. |
{: caption="Table 1. RPO and RTO for CIS" caption-side="bottom"}

## Locations
{: #bcdr-locations}

For more information about service availability within regions and data centers, see [Service and infrastructure availability by location](/docs/overview?topic=overview-services_region).
