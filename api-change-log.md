---

copyright:
  years:  2024, 2024
lastupdated: "2024-12-18"

keywords: change log for cloud internet services API, updates to CIS API

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.cis_short_notm}} API change log
{: #api-change-log}

In this change log, you can learn about the latest changes, improvements, and updates for the [{{site.data.keyword.cis_full_notm}} API](/apidocs/cis). The change log lists changes that have been made, ordered by the date they were released. Changes to existing API versions are designed to be compatible with existing client applications.

## 17 December 2024
{: #17-dec-2024}

CIS Enterprise-level plans can use [Logpush](/docs/cis?topic=cis-logpush&interface=api) for detailed edge logs of HTTP, DNS, and Range traffic, as well as firewall events. Logpush allows you to push request logs to IBM Cloud Logs or a Cloud Object Storage bucket. For more information, see [Create a Logpush job](/apidocs/cis#create-logpush-job-v2).

## 12 June 2024
{: #12-jun-2024}

The [Managed rules feature](/docs/cis?topic=cis-managed-rules-overview) has been added to the {{site.data.keyword.cis_short_notm}} API. See [Zone rulesets](/apidocs/cis#get-zone-rulesets) for the available options.

## 30 May 2023
{: #30-may-2023}

The [zone hold](/apidocs/cis#get-zone-hold) feature has been added to the {{site.data.keyword.cis_short_notm}} API.

## 30 November 2022
{: #30-nov-2022}

The [Create rate limit](/apidocs/cis#create-zone-rate-limits) API updated the `period` parameter to change the time during which to count traffic.

- The minimum time in seconds changed from `1` to `10`
- The maximum time in seconds changed from `3600` to `86400`
