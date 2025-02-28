---

copyright:
  years: 2024, 2025
lastupdated: "2025-02-28"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Ruleset Engine rules language
{: #cis-ruleset-engine}

The {{site.data.keyword.cis_short_notm}} Ruleset Engine rules language is a flexible and intuitive specification for building rule expressions. Based on the [Wireshark display filters](https://www.wireshark.org/docs/wsug_html_chunked/ChWorkBuildDisplayFilterSection.html){: external}, the rules language allows you to precisely target HTTP requests with a syntax and semantics familiar to security engineers.
{: shortdesc}

## Ruleset Engine rules actions
{: #ruleset-engine-actions}

The action of a rule determines how {{site.data.keyword.cis_short_notm}} handles matches for the rule expression.

The following table lists the actions available in the Ruleset Engine language:

|Action|API value|Description|Stops rule evaluation?|
|------|---------|-----------|----------------------|
|Interactive challenge| `challenge`|Useful for ensuring that the visitor accessing the site is human, not automated.  \n The client that made the request must pass an interactive challenge. If successful, {{site.data.keyword.cis_short_notm}} accepts the matched request; otherwise, it is blocked.|Yes|
|JS Challenge|`js_challenge`| Useful for ensuring that bots and spam can't access the requested resource; browsers, however, are free to satisfy the challenge automatically.  \n The client that made the request must pass a JavaScript challenge before proceeding. If successful, {{site.data.keyword.cis_short_notm}} accepts the matched request; otherwise, it is blocked.|Yes|
|Managed challenge (recommended)|`managed_challenge`|Helps reduce the time spent solving CAPTCHAs across the Internet.  \n Depending on the characteristics of a request, {{site.data.keyword.cis_short_notm}} will dynamically choose the appropriate type of challenge from the following actions based on specific criteria:  \n * Show a non-interactive challenge page (similar to the current JS challenge).  \n * Show a custom interactive challenge (for example, clicking a button).|Yes|
|Block|`block`|Matching requests are denied access to the site.|Yes|
|Skip|`skip`|Allows user to dynamically skip one or more security features or products for a request.  \n Depending on the rule configuration, matching requests will skip the evaluation of one or more security features or products:  \n * Skip all remaining rules in the current ruleset  \n * Skip rulesets  \n * Skip rules of a ruleset  \n * Skip phases  \n * Skip specific security products that are not based on the Ruleset Engine   \n  \n The available skip options depend on the phase where you configure the rule.|No  \n (However, some rules might be skipped)|
|Log|`log`|Records matching requests in the {{site.data.keyword.cis_short_notm}} logs.  \n Only available on Enterprise plans.  \n Recommended for validating rules before committing to a more severe action.|No|
|Execute|`execute`|Executes the rules in the ruleset specified in the rule configuration. You can specify a managed ruleset or a custom ruleset to execute.  \n In the {{site.data.keyword.cis_short_notm}} UI, this action is not listed in action selection dropdowns.|No|
|Rewrite|`rewrite`|Adjusts the URI path, query string, and/or HTTP headers of requests and responses, according to the rule configuration.  \n Only available in WAF custom rules checking for exposed credentials, in the `http_request_firewall_custom` phase at the instance level. In the {{site.data.keyword.cis_short_notm}} UI, this action is called Exposed-Credential-Check Header.|No|
{: caption="Available actions" caption-side="bottom"}
