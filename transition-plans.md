---

copyright:
  years: 2023, 2025
lastupdated: "2025-07-07"

keywords: plans, enterprise essential, enterprise advanced, enterprise premier, standard next

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Transitioning to updated plans
{: #transition-plans}

Although the transition to updated {{site.data.keyword.cis_full}} plans began in 2023, some users are still on the original plans. This topic remains available to assist users who have not yet migrated.
{: shortdesc}

Migrating from one plan to another is considered a modification of an existing resource, not a deletion or creation of a resource.
{: note}

## Transitioning from a Standard plan to a Standard Next plan
{: #transitioning-next-plan}

As of 30 April 2023, the original {{site.data.keyword.cis_short_notm}} Standard plan is no longer available for new instances. Any instance created on or after this date automatically uses the Standard Next plan.

The Standard Next plan follows a more metered pricing model, which reduces the base cost compared to the original Standard plan. The following table outlines the key differences between the two plans.

|Feature|Standard|Standard Next|Overage|
|--------|-------------|-----|----|
|Domain|1 included  \n More available for monthly cost per domain|1 included  \n More available for monthly cost per domain|Each additional domain incurs a fee|
|Protected traffic  \n (TB)|5|0.5|Traffic over the limit (per TB) incurs a fee|
|Range traffic|No|No|Not applicable|
|DNS queries  \n (million per domain)| 10|1|Fees assessed per additional million queries|
|HTTP requests  \n (million)|10|5|Fees assessed per additional million requests|
|Edge function requests  \n (million)|1|1|Fees assessed per additional million queries|
|DDoS protection|Yes|Yes|Not applicable |
|WAF  \n (million)|Not applicable|Yes|Part of HTTP requests |
|IP Firewall|Yes|Yes|Not applicable |
|DNS records per domain|3500|250|Upgrade plan to get more|
|GLB origin servers|6|3|Not applicable|
|Smart routing|No|No|Not applicable|
|Rate limiting|No|No|Not applicable|
|Logging|No|No|Not applicable|
|Page rules per domain|50|50|Not applicable|
|Firewall rules|100|100|Not applicable|
{: caption="Comparison of CIS Standard and Standard Next plans" caption-side="bottom"}

### Migrating to the Standard Next plan
{: #migration-to-standard-next}

To migrate from the Standard plan to the Standard Next plan:

1. Navigate to your existing {{site.data.keyword.cis_short_notm}} instance.
1. From the **Plan** page, select the Standard Next plan.
1. Accept the terms and conditions.
1. Click **Create** and follow any prompts.

## Transitioning to Enterprise Tier plans
{: #transitioning-enterprise-plans}

As of 31 August 2023, the original {{site.data.keyword.cis_short_notm}} Enterprise Package, Enterprise GLB, and Enterprise Security plans are no longer available for new instances. All new instances created on or after this date use one of the new Enterprise Tier plans.
{: shortdesc}

The Enterprise Tier plans adopt a more flexible, metered pricing model, lowering base costs compared to legacy Enterprise plans. The following table summarizes key features of the new plans.

|Features|Enterprise Essential|Enterprise Advanced|Enterprise Premier|
|:-------|:-------------------|:------------------|:-----------------|
|Included domains|1 included  \n More available for monthly cost per domain|2 included  \n More available for monthly cost per domain|2 included  \n More available for monthly cost per domain|
|Included DNS records|3500|3500|3500|
|Protected traffic included (DDoS, CDN, DNS, WAF, GLB)|5 TB|5 TB|5 TB|
|Requests included (CDN, WAF, GLB) in millions|150|150|150|
|Custom uploaded certificates|25|25|25|
|GLB: Origins, pools, GLB included|20|20|20|
|Range (Layer 3/4) | No | Yes | Yes |
|Logging| Yes | Yes | Yes |
|Rate limiting| No | Yes | Yes |
|Advanced WAF| No | Yes | Yes |
|Bot management| No | No | Yes |
{: caption="Comparison of CIS Enterprise Tier plans" caption-side="bottom"}

### Migrating to Enterprise Tier plans
{: #migration-to-enterprise-tiers}

To migrate from your current Enterprise package, Enterprise GLB, or Enterprise Security plans, follow these steps:

1. Navigate to your existing {{site.data.keyword.cis_short_notm}} instance.
1. From the **Plan** page, select the Enterprise Tier plan that you want.
1. Accept the terms and conditions.
1. Click **Create** and follow any prompts.

### All plans comparison
{: #all-plans-comparison}

For a detailed comparison of current plans, see [Comparing CIS plans](/docs/cis?topic=cis-cis-plan-comparison).
