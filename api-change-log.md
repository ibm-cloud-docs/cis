---

copyright:
  years:  2024, 2026
lastupdated: "2026-07-06"

keywords: change log for cloud internet services API, updates to CIS API

subcollection: cis

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.cis_short_notm}} API change log
{: #api-change-log}

In this change log, you can learn about the latest changes, improvements, and updates for the [{{site.data.keyword.cis_full_notm}} API](/docs/apis/cis). The change log lists changes that have been made, ordered by the date they were released. Changes to existing API versions are designed to be compatible with existing client applications.

## 3 May 2026
{: #cis-may-030326}

Support for RayID log lookup
:    Support has been added to the CIS API for retrieving logs associated with a specific RayID from your domain's traffic. For more information, see [Get logs by RayID](https://cloud.ibm.com/docs/apis/cis?code=go#get-logs-by-rayid).

## 28 April 2026
{: #cis-april-2826}

Batch DNS records API enhancements
:    The Batch DNS records API has been updated to improve consistency and expand record support. The operation ID is now `batch_dns_records`, and the request and response schemas have been renamed for better clarity. Support for DNS record types `PTR` and `DS` has been added, while `SPF` is no longer supported. For more information, see [Batch DNS Records API](/docs/apis/cis#batch-dns-records) to understand the updated schema and supported record types.

Custom list items API improvements
:    The `GET` custom list items endpoint now supports additional query parameters to enhance pagination and filtering. You can use `cursor` and `per_page` for pagination, and the `search` parameter to filter results based on specific criteria. For more information, see [Custom list items API](/docs/apis/cis?code=go#get-list-items).

Zone settings API enhancements
:    Support has been added to the CIS API for retrieving and updating zone-level settings, including the security level and email address obfuscation. For more information, see [Get email address obfuscation](/docs/apis/cis#get-email-obfuscation),[Update email address obfuscation](/docs/apis/cis#update-email-obfuscation), and [Set security-level setting](/docs/apis/cis#set-security-level-setting).

## 03 December 2025
{: #cis-dec-0325}

Custom and CIS-managed list support
:    You can now create and manage custom lists or use CIS-managed lists through the API. You can list all [managed](/docs/apis/cis#get-managed-lists) and [custom lists](/docs/apis/cis#get-custom-lists), [create](/docs/apis/cis#create-custom-lists) a custom list, [retrieve](/docs/apis/cis#get-custom-list) or [update](/docs/apis/cis#update-custom-list) an existing custom list, or [delete](/docs/apis/cis#delete-custom-list) one you no longer need. List items can also be managed with the API: you can [get](/docs/apis/cis#get-list-items), [create](/docs/apis/cis#create-list-items), [update](/docs/apis/cis#update-list-items), or [delete](/docs/apis/cis#delete-list-items) individual items, update all items at once, [retrieve](/docs/apis/cis#get-list-item) a single list item, or [check the status](/docs/apis/cis#get-operation-status) of a list operation.

For more information, see [managed and custom lists](/docs/cis?group=lists) and explore the available API methods to start integrating these capabilities into your workflow.

## 28 February 2025
{: #cis-febr2825}
{: release-note}

Ruleset Engine migration
:   Two existing features are now part of the Ruleset Engine rules language, and have been updated to use the [Rulesets API](/docs/apis/cis#get-instance-rulesets) (similar to WAF-managed rules):

    * Firewall rules: Now known as WAF custom rules, these rules provide similar protections to the previous handling, but also include a few extra features. For more information, see [Migrating to WAF custom rules](/docs/cis?topic=cis-migrating-to-custom-rules).

    * Rate-limiting rules: The new version of these rules allows you to apply rate-limiting to more specific kinds of traffic. For more information, see [Migrating to new rate-limiting rules](/docs/cis?topic=cis-migrating-to-rate-limiting).

## 16 December 2024
{: #16-dec-2024}

CIS Enterprise-level plans can now configure the [Logpush jobs](/docs/cis?topic=cis-logpush&interface=api) to push request logs to IBM Cloud Logs with the API. For more information, see [Create a Logpush job](/docs/apis/cis#create-logpush-job-v2).

## 12 June 2024
{: #12-jun-2024}

The [Managed rules feature](/docs/cis?topic=cis-managed-rules-overview) has been added to the {{site.data.keyword.cis_short_notm}} API. See [Zone rulesets](/docs/apis/cis#get-zone-rulesets) for the available options.

## 30 May 2023
{: #30-may-2023}

The [zone hold](/docs/apis/cis#get-zone-hold) feature has been added to the {{site.data.keyword.cis_short_notm}} API.

## 30 November 2022
{: #30-nov-2022}

The [Create rate limit](/docs/apis/cis#create-zone-rate-limits) API updated the `period` parameter to change the time during which to count traffic.

- The minimum time in seconds changed from `1` to `10`
- The maximum time in seconds changed from `3600` to `86400`
