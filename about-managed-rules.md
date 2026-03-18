---

copyright:
  years: 2024, 2026
lastupdated: "2026-03-18"

keywords: managed rules, rulesets, waf, owasp

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# About WAF managed rules
{: #managed-rules-overview}

You can use managed rules to deploy pre-configured managed rulesets that provide immediate protection against the following threats:
{: shortdesc}

* Zero-day vulnerabilities
* Top-10 attack techniques
* Use of stolen and exposed credentials
* Extraction of sensitive data

## Benefits
{: #managed-rules-benefit}

Managed rules provide the following benefits over the previous WAF version:

New matching engine
:   Managed rules use the Ruleset Engine feature suite, which allows faster managed rule deployments so that you can check more traffic without scaling issues, while improving performance and security. The rules follow the same syntax that is used in other {{site.data.keyword.cis_short_notm}} security features, such as WAF custom rules.

Updated managed rulesets
:   The CIS OWASP Core Ruleset is an implementation of version 3.3.0 of the [OWASP ModSecurity Core Rule Set (CRS)](https://owasp.org/www-project-modsecurity-core-rule-set/){: external}. This version introduces paranoia levels and reduces false positives rates compared to the version used in WAF managed rules (2.x). It also provides greater control over sensitivity scoring, with clear visibility into how individual rules contribute to the score and the total score for a triggered request. In addition, the updated ruleset separates rule status from rule action, which makes it easier to configure both independently.

Better rule browsing and configuration
:   The default configuration of managed rules has a low false positive rate while providing a food security baseline for your web applications. For the best possible security, enable as many rules as possible. You might need to customize the ruleset behavior based on the underlying application. Bulk editing controls in addition to inline single rule controls contribute to faster configuration changes based on specific use cases.

## Rulesets
{: #managed-rulesets}

These managed rulesets are regularly updated. You can adjust the behavior of specific rules in these rulesets, choosing from several possible actions.

|Ruleset name | Description | Ruleset ID|
|:------------| :-----------|:----------|
|CIS Managed Ruleset | This ruleset provides fast and effective protection for all of your applications. The ruleset is updated frequently to cover new vulnerabilities and reduce false positives. |`efb7b8c949ac4650a09736fc376e9aee` |
|CIS OWASP Core Ruleset |Based on the Open Web Application Security Project (OWASP) ModSecurity Core Rule Set (v3.3.0).|`4814384a9e5d4991b9815dcfc25d2f1f` |
|Exposed credentials check | Deploy an automated credentials check on your user authentication endpoints. For any credential pair, the CIS WAF performs a lookup against a public database of stolen credentials.|`c2e184081120413c86c3ab7e14069605` |
{: caption="Available rulesets and ruleset IDs" caption-side="bottom"}

## Request body inspection limit
{: #request-body-inspection-limit}

The WAF inspects HTTP request bodies up to 128 KB by default. This limit applies to all managed rulesets, including the CIS Managed Ruleset and OWASP Core Ruleset, and determines how much of each request the WAF can evaluate. Customers can request an increase of the inspection limit to 1 MB by [creating a support case](/docs/account?topic=account-open-case&interface=ui).

Increasing the inspection limit can affect how managed rules evaluate traffic and could impact rule matches. Review ruleset behavior if higher limits are required.
{: note}
