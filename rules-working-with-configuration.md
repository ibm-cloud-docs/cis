---

copyright:
  years: 2018, 2026
lastupdated: "2026-08-05"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# About configuration rules
{: #about-config-rules}

Configuration rules allow you to customize how {{site.data.keyword.cis_short_notm}} processes matching HTTP requests. Configuration rules are evaluated in the `http_config_settings` phase of the Ruleset Engine and can modify request-processing settings based on request attributes such as hostnames, URL paths, or request headers.
{: shortdesc}

Each configuration rule consists of an expression that identifies matching requests and a set_config action that applies the specified configuration settings. Configuration rules are managed through the Rulesets API and are evaluated before origin rules in the request-processing workflow.

## Rule execution order
{: #config-rule-execution-order}

Configuration rules are evaluated in the Ruleset Engine during the `http_config_settings` phase. Ruleset Engine rules take precedence over Page Rules. If a request matches both a Page Rule and a Ruleset Engine rule, the Ruleset Engine rule is applied.
