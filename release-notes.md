---

copyright:
  years: 2021, 2025
lastupdated: "2025-07-29"

keywords:

subcollection: cis

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.cis_short_notm}}
{: #release-notes}

Use these release notes to learn about the latest updates to {{site.data.keyword.cis_full}} that are grouped by date.
{: shortdesc}

## 15 July 2025
{: #cis-july1525}

Custom and managed lists
:   Released support for custom lists and managed lists to enhance control over security and traffic management policies.

    * [Custom lists](/apidocs/cis#get-custom-lists) let you define and manage ASN, IP, and hostname entries for use in access rules and other policy configurations.

    * [Managed lists](/apidocs/cis#get-managed-lists) provide preconfigured threat intelligence and reputation data maintained by IBM to simplify policy enforcement. The specific managed lists available depend on your subscription plan.

    These features enable more accurate policy targeting and improve operational efficiency within CIS. For more information, see [Working with lists](/docs/cis?group=lists).

## 28 February 2025
{: #cis-feb2825}
{: release-note}

Ruleset Engine migration
:   Two existing features are now part of the Ruleset Engine rules language, and have been updated to use the [Rulesets API](/apidocs/cis#get-zone-rulesets) (similar to WAF managed rules).

    * Firewall rules: Now known as WAF custom rules, these rules provide similar protections to the previous handling, but also include a few extra features. For more information, see [Migrating to WAF custom rules](/docs/cis?topic=cis-migrating-to-custom-rules).

    * Rate-limiting rules: The new version of these rules allows you to apply rate-limiting to more specific kinds of traffic. For more information, see [Migrating to new rate-limiting rules](/docs/cis?topic=cis-migrating-to-rate-limiting).

## 21 October 2024
{: #cis-oct2124}
{: release-note}

Enhanced security
:   Released support for [SSL.com as a Certificate Authority](/docs/cis?topic=cis-managing-edge-certs#certificate-authorities), offering you more trusted SSL certificate options.

## 12 June 2024
{: #cis-jun1224}
{: release-note}

Managed Rules
:   Released the new [managed rules](/docs/cis?topic=cis-managed-rules-overview) feature, which replaces the current WAF. Enterprise plans will have a [Migration to managed rules](/docs/cis?topic=cis-migrating-to-managed-rules) that allows an intermediary step where you can compare security events. Standard Next plans migrate directly to Managed rules without the intermediary review step.

## 21 June 2023
{: #cis-jun2123}
{: release-note}

Enterprise Tier plans released
:   Released the new [Enterprise Tier plans](/docs/cis?topic=cis-transition-plans), which replaces the current Enterprise Package, Enterprise GLB, and Enterprise Security plans.

## 16 March 2023
{: #cis-mar1623}
{: release-note}

Standard Next plan released
:   Released the new [Standard Next plan](/docs/cis?topic=cis-transition-plans), which replaces the current Standard plan.
