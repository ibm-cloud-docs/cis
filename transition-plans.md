---

copyright:
  years: 2023
lastupdated: "2023-11-17"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Transitioning to updated plans
{: #transition-plans}

In 2023, the original {{site.data.keyword.cis_full}} plans are being updated to reflect new plans and associated features.
{: shortdesc}

Migrating from one plan to another is considered a modification of an existing resource, and not a destruction or creation of a resource.
{: note}

## Transitioning from a Standard plan to a Standard Next plan
{: #transitioning-next-plan}

Starting 30 April 2023, the {{site.data.keyword.cis_short_notm}} current Standard plan will no longer be available for new instances. Any instance that is created on or after this date will use the Standard Next plan.

By moving to a more metered model, the base cost of the Standard Next plan is smaller than the original Standard plans. The following table shows what changed from the Standard to the Standard Next plans.

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
|Logpush/Logpull|No|No|Not applicable|
|Page rules per domain|50|50|Not applicable|
|Firewall rules|100|100|Not applicable|
{: caption="Table 1. Comparison of CIS Standard and Standard Next plans" caption-side="bottom"}

### Migration to Standard Next plans
{: #migration-to-standard-next}

To migrate from your current Standard plan to a Standard Next plan, take the following steps.

1. Enter your existing {{site.data.keyword.cis_short_notm}} instance
1. Navigate to the **Plan** page in left side panel
1. Select Standard Next plan
1. Check the box to acknowledge the terms and conditions
1. Click **Create** and follow any prompts that might block this plan change

## Transitioning to Enterprise Tier plans
{: #transitioning-enterprise-plans}

Starting 31 August 2023, the current {{site.data.keyword.cis_short_notm}} Enterprise Package, Enterprise GLB, and Enterprise Security plans will no longer be available for new instances. Any instance that is created on or after this date will use the new Enterprise Tier plans.
{: shortdesc}

By moving to a more metered model, the base cost of the Enterprise Tier plans are smaller than the original Enterprise plans. The following table shows what features are available in the Enterprise Tier plans.

|Features|Enterprise Essential|Enterprise Advanced|Enterprise Premier|
|:-------|:-------------------|:------------------|:-----------------|
|Included domains|1 included  \n More available for monthly cost per domain|2 included  \n More available for monthly cost per domain|2 included  \n More available for monthly cost per domain|
|Included DNS records|3500|3500|3500|
|Protected traffic included (DDoS, CDN, DNS, WAF, GLB)|5 TB|5 TB|5 TB|
|Requests included (CDN, WAF, GLB) in millions|150|150|150|
|Custom uploaded certificates|25|25|25|
|GLB: Origins, pools, GLB included|20|20|20|
|Range (Layer 3/4) | No | Yes | Yes |
|Advanced rate limiting| No | Yes | Yes |
|Advanced WAF| No | Yes | Yes |
|Bot management| No | No | Yes |
{: caption="Table 2. Comparison of CIS Enterprise Tier plans" caption-side="bottom"}

### Migration to Enterprise Tiers plans
{: #migration-to-enterprise-tiers}

To migrate from your current Enterprise Package, Enterprise GLB, and Enterprise Security plans, take the following steps.

1. Enter your existing {{site.data.keyword.cis_short_notm}} instance
1. Navigate to the **Plan** page in left side panel
1. Select desired Enterprise Tier plan
1. Check the box to acknowledge the terms and conditions
1. Click **Create** and follow any prompts that might block this plan change
