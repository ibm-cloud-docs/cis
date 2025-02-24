---

copyright:
  years: 2024, 2025
lastupdated: "2025-02-24"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# About rulesets
{: #about-rule-sets}

You can use the {{site.data.keyword.cis_short_notm}} Ruleset Engine to create and deploy rules and rulesets in {{site.data.keyword.cis_short_notm}} using the same basic syntax.
{: shortdesc}

## Main features
{: #rule-sets-main-features}

The following features apply to rulesets:

* **Powerful syntax**: Rule expressions use a powerful rules language similar to the [`wirefilter`](https://github.com/cloudflare/wirefilter){: external} syntax that allows you to create complex rules.
* **High-performance rule evaluation**: Allows you to have many rules in {{site.data.keyword.cis_short_notm}} with minimal impact on performance.
* **Engine powering {{site.data.keyword.cis_short_notm}}**: {{site.data.keyword.cis_short_notm}} will continue to build products on top of the Ruleset Engine, which means that you can use the same API methods for configuring different products with the same customization possibilities. The Ruleset Engine also supports the different phases of the request life cycle.

## Phases
{: #phases}

A phase defines a stage in the life of a request where you can execute rulesets. Phases are defined by {{site.data.keyword.cis_short_notm}} and can't be modified.

Phases exist at the instance level and at the zone level. For the same phase, rules defined at the instance level are evaluated before the rules defined at the zone level.

Each phase has, at most, one entry point ruleset at the instance and zone level.

Currently, only phases at the zone level are available. This page is updated as instance and zone level phases become available in subsequent releases.

### Phase list
{: #phase-list}

The following table lists the phases that are available within the Ruleset Engine APIs.

|Phase name|Description|Supported interfaces|
|----------|-----------|-------------------|
| `http_request_firewall_managed`| Web Application Firewall (WAF)| API, CLI, UI |
| `http_request_firewall_custom` | Firewall rules | API |
| `http_ratelimit` | Rate-limiting rules | API, CLI |
| `ddos_l7` | HTTP DDoS Attack Protection rules | API |
{: caption="Available phases" caption-side="bottom"}

## Rules language
{: #rules-language}

The {{site.data.keyword.cis_short_notm}} rules language is a flexible and intuitive specification for building rule expressions. Based on the [Wireshark display filters](https://www.wireshark.org/docs/wsug_html_chunked/ChWorkBuildDisplayFilterSection.html){: external}, the rules language allows you to precisely target HTTP requests with a syntax and semantics familiar to security engineers.

### Rules actions
{: #rules-actions}

The action of a rule determines how {{site.data.keyword.cis_short_notm}} handles matches for the rule expression.

The following table lists the actions available in the Rules language:

|Action|API value|Description|Stops rule evaluation?|
|------|---------|-----------|----------------------|
|Interactive challenge| `challenge`|Useful for ensuring that the visitor accessing the site is human, not automated.  \n The client that made the request must pass an interactive challenge. If successful, {{site.data.keyword.cis_short_notm}} accepts the matched request; otherwise, it is blocked.|Yes|
|JS Challenge|`js_challenge`| Useful for ensuring that bots and spam can't access the requested resource; browsers, however, are free to satisfy the challenge automatically.  \n The client that made the request must pass a JavaScript challenge before proceeding. If successful, {{site.data.keyword.cis_short_notm}} accepts the matched request; otherwise, it is blocked.|Yes|
|Managed challenge (recommended)|`managed_challenge`|Helps reduce the time spent solving CAPTCHAs across the Internet.  \n Depending on the characteristics of a request, {{site.data.keyword.cis_short_notm}} will dynamically choose the appropriate type of challenge from the following actions based on specific criteria:  \n * Show a non-interactive challenge page (similar to the current JS challenge).  \n * Show a custom interactive challenge (for example, clicking a button).|Yes|
|Block|`block`|Matching requests are denied access to the site.|Yes|
|Skip|`skip`|Allows user to dynamically skip one or more security features or products for a request.  \n Depending on the rule configuration, matching requests will skip the evaluation of one or more security features or products:  \n * Skip all remaining rules in the current ruleset  \n * Skip rulesets  \n * Skip rules of a ruleset  \n * Skip phases  \n * Skip specific security products that are not based on the ruleset engine   \n  \n The available skip options depend on the phase where you configure the rule.|No  \n (However, some rules might be skipped)|
|Log|`log`|Records matching requests in the {{site.data.keyword.cis_short_notm}} logs.  \n Only available on Enterprise plans.  \n Recommended for validating rules before committing to a more severe action.|No|
|Execute|`execute`|Executes the rules in the ruleset specified in the rule configuration. You can specify a managed ruleset or a custom ruleset to execute.  \n In the {{site.data.keyword.cis_short_notm}} UI, this action is not listed in action selection dropdowns.|No|
|Rewrite|`rewrite`|Adjusts the URI path, query string, and/or HTTP headers of requests and responses, according to the rule configuration.  \n Only available in:  \n * Transform Rules, in phases `http_request_transform`, `http_request_late_transform`, and `http_response_headers_transform`. In the {{site.data.keyword.cis_short_notm}} UI, this action is not listed in action selection dropdowns. To use this action, create a Transform rule.  \n * Custom rules checking for exposed credentials, in the `http_request_firewall_custom` phase at the instance level. In the {{site.data.keyword.cis_short_notm}} UI, this action is called Exposed-Credential-Check Header.|No|
{: caption="Available actions" caption-side="bottom"}

## Entry point ruleset
{: #entry-point-ruleset}

Entry point rulesets are abstracted away when using the {{site.data.keyword.cis_short_notm}} UI. They are required to deploy and override rulesets when using the API, CLI, SDK, or Terraform.
{: note}

An entry point ruleset contains a list of ordered rules that run in a phase at the instance or zone level. This ruleset is an entry point for all rules executed in a phase. Some of these rules might run other rulesets.

Each phase has, at most, one entry point ruleset at the instance level and at the zone level.

The `kind` field of a phase entry point ruleset has one of the following values:

* `root`: Used for a phase entry point ruleset at the instance level
* `zone`: Used for a phase entry point ruleset at the zone level

For WAF managed rules, see [Deploying rulesets](/docs/cis?topic=cis-deploying-rule-sets) for instructions on using entry point rulesets to deploy rulesets.

For WAF managed rules, see [Overriding rulesets](/docs/cis?topic=cis-override-rule-sets) for instructions on using entry point rulesets to override rulesets.
