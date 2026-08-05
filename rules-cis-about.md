---

copyright:
  years: 2026
lastupdated: "2026-08-05"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# About rules
{: #about-cis-rules}

Rules in CIS allow you to inspect incoming HTTP requests and apply actions based on matching conditions. Rules are evaluated by the Ruleset Engine, which processes requests through a series of execution phases before traffic reaches the origin server.
{: shortdesc}

A rule consists of the following components:

* Expression: Defines the conditions that determine whether a request matches the rule.
* Action: Specifies what action to take when the request matches the expression.
* Phase: Defines when the rule is evaluated during request processing.

{{site.data.keyword.cis_short_notm}} supports several rule-based capabilities through the Rulesets API, including:

* Configuration rules (`http_config_settings`)
* Origin rules (`http_request_origin`)
* Custom rules
* Rate-limiting rules
* Other Ruleset Engine features that are supported by the CIS Rulesets API implementation.

Rules are organized into rulesets. Each ruleset belongs to a specific phase and contains one or more ordered rules that are evaluated when requests reach that phase. Rulesets are versioned, and updates to a ruleset create a new version of the configuration.

The Rulesets API enables you to create, manage, and update rulesets at the zone level. By using rules, you can customize traffic handling, modify origin behavior, apply configuration settings, and implement security controls without changing your applications or origin infrastructure.
