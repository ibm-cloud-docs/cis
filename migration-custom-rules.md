---

copyright:
  years: 2024, 2025
lastupdated: "2025-05-09"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Migrating to WAF custom rules
{: #migrating-to-custom-rules}

{{site.data.keyword.cis_short_notm}} upgraded existing [firewall rules](/docs/cis?topic=cis-about-firewall-rules) to use the [Ruleset Engine](/docs/cis?topic=cis-about-rule-sets); where they are now known as [custom rules](/docs/cis?topic=cis-custom-rules-overview). With custom rules, users get as much protection with a few extra features. In the {{site.data.keyword.cis_short_notm}} dashboard, these rules can still be found in the **Security page > Firewall rules tab**.
{: shortdesc}

If you haven't migrated to WAF custom rules yet, you might have some invalid configuration that prevents the migration from happening. In this case, contact your account team to get help with the migration to WAF custom rules.
{: important}

## Main differences between firewall rules and custom rules
{: #custom-rules-main-differences}

The main differences between firewall rules and WAF custom rules are as follows:

* [Improved response for Block action](/docs/cis?topic=cis-migrating-to-custom-rules#improved-response-block-action)
* [Different error page for blocked requests](/docs/cis?topic=cis-migrating-to-custom-rules#different-error-page-blocked-requests)
* [New Skip action replacing both Allow and Bypass actions](/docs/cis?topic=cis-migrating-to-custom-rules#new-skip-action)
* [Custom rules are evaluated in order](/docs/cis?topic=cis-migrating-to-custom-rules#custom-rules-evaluated-in-order)
* [Logs and events](/docs/cis?topic=cis-migrating-to-custom-rules#logs-and-events) 
* [New API](/docs/cis?topic=cis-migrating-to-custom-rules#new-api)

### Improved response for Block action
{: #improved-response-block-action}

In custom rules, you can customize the response of the Block action.

The default block response is a {{site.data.keyword.cis_short_notm}} standard HTML page. If you need to send a custom response for Block actions, configure the custom rule to return a fixed response with a custom response code (403, by default) and a custom body (HTML, JSON, XML, or plain text).

To define a custom response for a single rule, go to **Security > WAF > Custom rules**, edit the custom rule, and complete the block-related options.

Custom block response configurations are not returned by the Firewall Rules API. Use the [Rulesets API](/apidocs/cis#get-instance-rulesets) to manage this new feature.
{: note}

### Different error page for blocked requests
{: #different-error-page-blocked-requests}

Requests blocked by a firewall rule with a Block action get a {{site.data.keyword.cis_short_notm}} [1020 error code](/docs/cis?topic=cis-html-1xxx-errors#1020-error) response. {{site.data.keyword.cis_short_notm}} users might customize this error page in **Custom Pages > 1000 Class Errors**.

Requests blocked by a WAF custom rule get a different response: the WAF block response. To customize the default block response, you can either:

* Define a custom WAF block response for your entire zone in **Custom Pages > WAF Block**. This custom page will always have an HTML content type.
* [Define a custom response](https://developers.cloudflare.com/waf/custom-rules/create-dashboard/#configure-a-custom-response-for-blocked-requests){: external} for requests blocked by a specific WAF custom rule. This custom response supports other content types besides HTML.

If you customized your 1xxx error page in Custom Pages for requests blocked by firewall rules, you must create a new response page for blocked requests by using one of the preceding methods.

### New Skip action replacing both Allow and Bypass actions
{: #new-skip-action}

Firewall Rules supported the Allow and Bypass actions, often used together. These actions were commonly used for handling known legitimate requests — for example, requests coming from trusted IP addresses.

When a request triggered Allow, all remaining firewall rules are not evaluated, effectively allowing the request to continue to the next security product. The Bypass action was designed to specify which security products (such as WAF managed rules, rate-limiting rules, and User Agent Blocking) should not run on the request triggering the action.

With Firewall Rules, if you wanted to stop running all security products for a given request, you would create two rules:

* One rule with Bypass action (selecting all security products).
* One rule with Allow action (to stop executing other firewall rules).

The requirement of having two rules to address this common scenario no longer applies to WAF custom rules. Now use the Skip action, which combines the Allow and Bypass actions. The Skip action fully replaces the Allow and Bypass actions, which are not supported in WAF custom rules.

With the Skip action you can do the following:

* Stop running all the remaining WAF custom rules (equivalent to the Allow action)
* Avoid running other security products (equivalent to the Bypass action)
* A combination of both.

You can also select whether you want to log events matching the custom rule with the Skip action or not. This is especially useful when creating a positive security model to avoid logging large amounts of legitimate traffic.

The Firewall Rules API does not support the Skip action. When you create a custom rule with Skip action, it is translated to Allow and Bypass in the Firewall Rules API. Use the [Rulesets API](/apidocs/cis#get-instance-rulesets) to fully use the new Skip action functionality.
{: note}

### Custom rules are evaluated in order
{: #custom-rules-evaluated-in-order}

Firewall rules actions had specific order of precedence when using [priority ordering](/docs/cis?topic=cis-priority). In contrast, WAF custom rules actions do not have such an order. Custom rules are always evaluated in order, and some actions, such as Block, stop the evaluation of other rules.

For example, if you use priority ordering and had the following firewall rules with the same priority both matching an incoming request:

* Firewall rule #1 — Priority: 2 / Action: Block
* Firewall rule #2 — Priority: 2 / Action: Allow

The request is allowed because the Allow action in Firewall Rules has precedence over the Block action.

In contrast, if you create two WAF custom rules where both rules match an incoming request:

* Custom rule #1 — Action: Block
* Custom rule #2 — Action: Skip (configured to skip all remaining custom rules)

The request is blocked because WAF custom rules are evaluated in order and the Block action stops the evaluation of other rules.

For the WAF custom rules converted from your existing firewall rules, {{site.data.keyword.cis_short_notm}} preserves your current order of execution.
{: note}

### Logs and events
{: #logs-and-events}

Events that are logged by WAF custom rules are available at **Security > Events**, with `Custom rules` as their source. For more information, see [Using the CIS Security Events capability](/docs/cis?topic=cis-using-the-cis-security-events-capability).

You might still find events that are generated by firewall rules in the Security Events page when you select a time frame including the days when the transition to WAF custom rules occurred. Similarly, you might still find events with both Skip and Allow actions in the same view during the transition period.

### New API 
{: #new-api}

The preferred API for managing WAF custom rules is the [Rulesets API](/apidocs/cis#get-instance-rulesets). The Rulesets API is used on all recent {{site.data.keyword.cis_short_notm}} security products to provide a uniform user experience when interacting with IBM API. For more information on migrating to the Rulesets API, see [Relevant changes for API users](/docs/cis?topic=cis-migrating-to-custom-rules#relevant-changes-api-users).

The Firewall Rules API and Filters API will still work until 2025-06-15. There will be a single list of rules for both firewall rules and custom rules, and this list contains WAF custom rules. Thanks to an internal conversion process, the Firewall Rules API, and Filters API return firewall rules/filters converted from these WAF custom rules.
{: note}

 
## Relevant changes for dashboard users
{: #relevant-changes-dashboard-users}

The **Firewall rules tab** will continue to exist and function as expected. The main difference is the APIs used in the background.

## Relevant changes for API users
{: #relevant-changes-api-users}

The [Firewall Rules API](/apidocs/cis#listallfirewallrules) and the associated [Filters API](/apidocs/cis#listallfilters) are now deprecated. These APIs will stop working on 30 July 2025. Migrate any automation based on the Firewall Rules API or Filters API to the [Rulesets API](/apidocs/cis#get-zone-entrypoint-ruleset) before this date to prevent any issues. Rule IDs are different between firewall rules and custom rules, which might affect automated processes dealing with specific rule IDs.
{: deprecated}

Until the deprecation date, all three APIs are available (Firewall Rules API, Filters API, and Rulesets API). {{site.data.keyword.cis_short_notm}} will internally convert your [Firewall Rules API](/apidocs/cis#listallfirewallrules) and [Filters API](/apidocs/cis#listallfilters) calls into the corresponding Rulesets API calls. There will be a single list of rules for both firewall rules and WAF custom rules.

Some new features of custom rules, like custom responses for blocked requests and the Skip action, are not supported in the legacy Firewall Rules API. To take advantage of these features, {{site.data.keyword.cis_short_notm}} recommends that you use the WAF custom rules page in the {{site.data.keyword.cis_short_notm}} dashboard or the Rulesets API.

See [About WAF custom rules](/docs/cis?topic=cis-custom-rules-overview) for examples of managing WAF custom rules that use the Rulesets API.
