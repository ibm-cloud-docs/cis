---

copyright:
  years: 2024
lastupdated: "2024-05-07"

keywords: managed rules, rulesets, waf

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Managed Rules overview
{: #managed-rules-overview}

You can use WAF managed rules to deploy pre-configured managed rulesets that provide immediate protection against the following threats:

* Zero-day vulnerabilities
* Top-10 attack techniques
* Use of stolen and exposed credentials
* Extraction of sensitive data



## Benefits
{: #managed-rules-benefit}

Managed rules provide the following benefits over the previous WAF version:

New matching engine
:   Managed rules use the ruleset engine, which allows faster managed rule deployments so that you can check more traffic without scaling issues, while improving performance and security. The rules follow the same syntax that is used in other {{site.data.keyword.cis_short_notm}} security features such as WAF custom rules.

Updated managed rulesets
:   The OWASP core ruleset is based on the latest version (v3.x), which adds paranoia levels and improves false positives rates compared to the version used in WAF managed rules (2.x). You also have more control over the sensitivity score, with a clear indication of how much each rule contributes to the score and what the total score of a triggered request was. The updated rulesets also provide better controls to separate rule status from rule action, which makes it easier to configure both, independently.

Better rule browsing and configuration
:   The default configuration of Managed rules has a low false positive rate while providing a food security baseline for your web applications. For the best possible security, enable as many rules as possible. You might need to customize the ruleset behavior based on the underlying application. Bulk editing controls in addition to inline single rule controls contribute to faster configuration changes based on specific use cases.

## Rulesets
{: #managed-rulesets}

These managed rulesets are regularly updated. You can adjust the behavior of specific rules in these rulesets, choosing from several possible actions.

|Ruleset name | Description | Ruleset ID|
|:------------| :-----------|:----------|
|CIS managed ruleset | This ruleset provides fast and effective protection for all of your applications. The ruleset is updated frequently to cover new vulnerabilities and reduce false positives. |`efb7b8c949ac4650a09736fc376e9aee` |
|OWASP core ruleset |The Open Web Application Security Project, or OWASP ModSecurity Core Rule Set. CIS routinely monitors for updates from OWASP from the official code repository.|`4814384a9e5d4991b9815dcfc25d2f1f` |
|Exposed credentials check | Deploy an automated credentials check on your end-user authentication endpoints. For any credential pair, the CIS WAF performs a lookup against a public database of stolen credentials.|`c2e184081120413c86c3ab7e14069605` |
{: caption="Table 1. Available rulesets and Ruleset IDs" caption-side="bottom"}
