---

copyright:
  years: 2023
lastupdated: "2023-03-15"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Transitioning from a Standard plan to a Standard Next plan
{: #transitioning-next-plan}

Starting 30 April 2023, the {{site.data.keyword.cis_full}} current Standard plan will no longer be available for new instances. Any instance that is created on or after this date will use the Standard Next plan.
{: shortdesc}

By moving to a more metered model, the base cost of the Standard Next plan is smaller than the original Standard plans. The following table shows what changed from the Standard to the Standard Next plans.

|Feature|Standard|Standard Next|Overage|
|--------|-------------|-----|----|
|Domain|1|1|Each additional domain incurs a fee|
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
