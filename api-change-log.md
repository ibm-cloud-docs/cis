---

copyright:
  years:  2024, 2025
lastupdated: "2025-07-02"

keywords: change log for cloud internet services API, updates to CIS API

subcollection: cis

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.cis_short_notm}} API change log
{: #api-change-log}

In this change log, you can learn about the latest changes, improvements, and updates for the [{{site.data.keyword.cis_full_notm}} API](/apidocs/cis). The change log lists changes that have been made, ordered by the date they were released. Changes to existing API versions are designed to be compatible with existing client applications.

## 28 February 2025
{: #cis-feb2825}
{: release-note}

Ruleset Engine migration
:   Two existing features are now part of the Ruleset Engine rules language, and have been updated to use the [Rulesets API](/apidocs/cis#get-instance-rulesets) (similar to WAF-managed rules):

    * Firewall rules: Now known as WAF custom rules, these rules provide similar protections to the previous handling, but also include a few extra features. For more information, see [Migrating to WAF custom rules](/docs/cis?topic=cis-migrating-to-custom-rules).

    * Rate-limiting rules: The new version of these rules allows you to apply rate-limiting to more specific kinds of traffic. For more information, see [Migrating to new rate-limiting rules](/docs/cis?topic=cis-migrating-to-rate-limiting).

## 16 December 2024
{: #16-dec-2024}

CIS Enterprise-level plans can now configure the [Logpush jobs](/docs/cis?topic=cis-logpush&interface=api) to push request logs to IBM Cloud Logs using the API. For more information, see [Create a Logpush job](/apidocs/cis#create-logpush-job-v2).

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
