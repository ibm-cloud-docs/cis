---

copyright:
  years: 2024, 2025
lastupdated: "2025-02-24"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Migrating to custom rules
{: #migrating-to-custom-rules}

{{site.data.keyword.cis_short_notm}} upgraded existing [firewall rules](/docs/cis?topic=cis-about-firewall-rules) to use the [Ruleset Engine](/docs/cis?topic=cis-about-rule-sets); where they are now known as **WAF custom rules** (Doc TBD with `custom-rules.md`). With custom rules, users get as much protection with a few extra features. In the {{site.data.keyword.cis_short_notm}} dashboard, these rules can still be found in the **Security page > Firewall rules tab**.
{: shortdesc}

Firewall Rules are now deprecated. The Firewall Rules API and Filters API, as well as the `cis_firewall_rule` and `cis_filter` Terraform resources, will be available until 15 June 2025. If you have any automation based on these APIs and resources, you must migrate to the new APIs and resources before 15 June 2025 to avoid any issues. On 15 June 2025, these APIs and resources will stop working. Any remaining active firewall rules will be disabled, and the **Firewall rules** tab in the dashboard will be removed.
{: deprecated}

If you haven't migrated to WAF custom rules yet, you might have some invalid configuration that prevents the migration from happening. In this case, contact your account team to get help with the migration to WAF custom rules.
{: important}

## Main differences between firewall rules and WAF custom rules
{: #custom-rules-main-differences}

The main differences between firewall rules and WAF custom rules are as follows:

* [Improved response for Block action](/docs/cis?topic=cis-migrating-to-custom-rules#improved-response-block-action)
* [Different error page for blocked requests](/docs/cis?topic=cis-migrating-to-custom-rules#different-error-page-blocked-requests)
* [New Skip action replacing both Allow and Bypass actions](/docs/cis?topic=cis-migrating-to-custom-rules#new-skip-action)
* [Custom rules are evaluated in order](/docs/cis?topic=cis-migrating-to-custom-rules#custom-rules-evaluated-in-order)
* [Logs and events](/docs/cis?topic=cis-migrating-to-custom-rules#logs-and-events)
* [New API and Terraform resources](/docs/cis?topic=cis-migrating-to-custom-rules#new-api-terraform-resources)

### Improved response for Block action
{: #improved-response-block-action}

In WAF custom rules, you can customize the response of the Block action{: external} [New topic?]{: tag-red}.

The default block response is a {{site.data.keyword.cis_short_notm}} standard HTML page. If you need to send a custom response for Block actions, configure the custom rule to return a fixed response with a custom response code (403, by default) and a custom body (HTML, JSON, XML, or plain text).

To define a custom response for a single rule, go to **Security > WAF > Custom rules**, edit the custom rule, and complete the block-related options.

Custom block response configurations will not be returned by the Firewall Rules API. You must use the [Rulesets API](https://developers.cloudflare.com/waf/custom-rules/create-api/#example-b){: external} [New topic?]{: tag-red} to manage this new feature.
{: note}

### Different error page for blocked requests
{: #different-error-page-blocked-requests}

Requests blocked by a firewall rule with a Block action get a {{site.data.keyword.cis_short_notm}} [1020 error code](/docs/cis?topic=cis-html-1xxx-errors#1020-error) response. {{site.data.keyword.cis_short_notm}} users might customize this error page in **Custom Pages > 1000 Class Errors**.

Requests blocked by a WAF custom rule get a different response: the WAF block response. To customize the default block response, you can either:

* Define a custom WAF block response for your entire zone in **Custom Pages > WAF Block**. This custom page will always have an HTML content type.
* [Define a custom response](https://developers.cloudflare.com/waf/custom-rules/create-dashboard/#configure-a-custom-response-for-blocked-requests){: external} for requests blocked by a specific WAF custom rule. This custom response supports other content types besides HTML.

If you customized your 1xxx error page in Custom Pages for requests blocked by firewall rules, you must create a new response page for blocked requests by using one of the preceding methods.

For more information about custom pages, see [Configuring custom pages](https://developers.cloudflare.com/support/more-dashboard-apps/cloudflare-custom-pages/configuring-custom-pages-error-and-challenge/). [New topic?]{: tag-red}

### New Skip action replacing both Allow and Bypass actions
{: #new-skip-action}

Firewall Rules supported the Allow and Bypass actions, often used together. These actions were commonly used for handling known legitimate requests — for example, requests coming from trusted IP addresses.

When a request triggered Allow, all remaining firewall rules are not evaluated, effectively allowing the request to continue to the next security product. The Bypass action was designed to specify which security products (such as WAF-managed rules, rate-limiting rules, and User Agent Blocking) should not run on the request triggering the action.

With Firewall Rules, if you wanted to stop running all security products for a given request, you would create two rules:

* One rule with Bypass action (selecting all security products).
* One rule with Allow action (to stop executing other firewall rules).

The requirement of having two rules to address this common scenario no longer applies to WAF custom rules. You should now use the [Skip action](https://developers.cloudflare.com/waf/custom-rules/skip/){: external} [New topic?]{: tag-red}, which combines the Allow and Bypass actions. The Skip action fully replaces the Allow and Bypass actions, which are not supported in WAF custom rules.

With the Skip action you can do the following:

* Stop running all the remaining custom rules (equivalent to the Allow action)
* Avoid running other security products (equivalent to the Bypass action)
* A combination of these.

You can also select whether you want to log events matching the custom rule with the Skip action or not. This is especially useful when creating a positive security model to avoid logging large amounts of legitimate traffic.

The Firewall Rules API does not support the Skip action. When you create a custom rule with Skip action, it is translated to Allow and Bypass in the Firewall Rules API. You must use the [Rulesets API](https://developers.cloudflare.com/waf/custom-rules/skip/api-examples/){: external} [New topic?]{: tag-red} to fully use the new Skip action functionality.
{: note}

### Custom rules are evaluated in order
{: #custom-rules-evaluated-in-order}

Firewall rules actions had a specific [order of precedence](https://developers.cloudflare.com/firewall/cf-firewall-rules/actions/){: external} [New topic?]{: tag-red} when using [priority ordering](https://developers.cloudflare.com/firewall/cf-firewall-rules/order-priority/#managing-rule-evaluation-by-priority-order){: external} [New topic?]{: tag-red}. In contrast, custom rules actions do not have such an order. Custom rules are always evaluated in order, and some actions like Block stop the evaluation of other rules.

For example, if you use priority ordering and had the following firewall rules with the same priority both matching an incoming request:

* Firewall rule #1 — Priority: 2 / Action: Block
* Firewall rule #2 — Priority: 2 / Action: Allow

The request is allowed because the Allow action in Firewall Rules has precedence over the Block action.

In contrast, if you create two custom rules where both rules match an incoming request:

* Custom rule #1 — Action: Block
* Custom rule #2 — Action: Skip (configured to skip all remaining custom rules)

The request is blocked because custom rules are evaluated in order and the Block action stops the evaluation of other rules.

For the custom rules converted from your existing firewall rules, {{site.data.keyword.cis_short_notm}} preserves your current order of execution.
{: note}

### Logs and events
{: #logs-and-events}

Events that are logged by custom rules are shown in [Security Events](/docs/cis?topic=cis-using-the-cis-security-events-capability), available at **Security > Events**, with `Custom rules` as their source.

You might still find events that are generated by Firewall Rules in the Security Events page when you select a time frame including the days when the transition to custom rules occurred. Similarly, you might still find events with both Skip and Allow actions in the same view during the transition period.

### New API and Terraform resources
{: #new-api-terraform-resources}

The preferred API for managing WAF custom rules is the [Rulesets API](https://developers.cloudflare.com/waf/custom-rules/create-api/){: external} [Where?]{: tag-red}. The Rulesets API is used on all recent {{site.data.keyword.cis_short_notm}} security products to provide a uniform user experience when interacting with our API. For more information on migrating to the Rulesets API, refer to [Relevant changes for API users](/docs/cis?topic=cis-migrating-to-custom-rules#relevant-changes-api-users).

The Firewall Rules API and Filters API will still work until 2025-06-15. There will be a single list of rules for both firewall rules and WAF custom rules, and this list contains WAF custom rules. Thanks to an internal conversion process, the Firewall Rules API and Filters API return firewall rules/filters converted from these WAF custom rules.

If you are using Terraform, the preferred way of configuring WAF custom rules is using `cis_ruleset` resources that are configured with the `http_request_firewall_custom` phase. For more information on updating your Terraform configuration, refer to [Relevant changes for Terraform users](/docs/cis?topic=cis-migrating-to-custom-rules#relevant-changes-terraform-users).

## Relevant changes for dashboard users
{: #relevant-changes-dashboard-users}

The **Firewall rules tab** will continue to exist and function as expected. The main difference is the APIs used in the background.

## Relevant changes for API users
{: #relevant-changes-api-users}

The [Firewall Rules API](/apidocs/cis#listallfirewallrules) and the associated [Filters API](/apidocs/cis#listallfilters) are now deprecated. These APIs will stop working on 15 June 2025. You must migrate any automation based on the Firewall Rules API or Filters API to the [Rulesets API](https://cloud.ibm.com/apidocs/cis#get-zone-entrypoint-ruleset) before this date to prevent any issues. Rule IDs are different between firewall rules and WAF custom rules, which might affect automated processes dealing with specific rule IDs.
{: deprecated}

Until the deprecation date, all three APIs are available (Firewall Rules API, Filters API, and Rulesets API). {{site.data.keyword.cis_short_notm}} will internally convert your [Firewall Rules API](/apidocs/cis#listallfirewallrules) and [Filters API](/apidocs/cis#listallfilters) calls into the corresponding Rulesets API calls. There will be a single list of rules for both firewall rules and WAF custom rules.

Some new features of WAF custom rules, like custom responses for blocked requests and the Skip action, are not supported in the legacy Firewall Rules API. To take advantage of these features, {{site.data.keyword.cis_short_notm}} recommends that you use the custom rules page in the {{site.data.keyword.cis_short_notm}} dashboard or the Rulesets API.

Refer to the WAF documentation for examples of managing WAF custom rules using the Rulesets API (Doc TBD with `custom-rules.md`).

## Relevant changes for Terraform users
{: #relevant-changes-terraform-users}

**TBD:** Get Arjun's assistance filling this out.

The following Terraform resources from the {{site.data.keyword.cis_short_notm}} provider are now deprecated:

* [cis_firewall_rule](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_firewall_rules){: external} [rules?]{: tag-red}
* [cis_filter](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_filter){: external}

These resources will stop working on 15 June 2025. If you are currently using these resources to manage your Firewall Rules configuration, you must manually migrate any Terraform configuration to [cis_ruleset](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_ruleset) resources before this date to prevent any issues.

For the time being, all three Terraform resources are available (`cis_firewall_rule`, `cis_filter`,`cis_ruleset`). There will be a single list of rules for both firewall rules and WAF custom rules.

Some new features of WAF custom rules are not supported in the deprecated Terraform resources. To take advantage of these features, {{site.data.keyword.cis_short_notm}} recommends that you use the `cis_ruleset` resource.

Refer to the documentation about Terraform for [examples of configuring WAF custom rules using Terraform](https://developers.cloudflare.com/terraform/additional-configurations/waf-custom-rules/){: external} [New topic?]{: tag-red}.

## Replace your configuration by using cf-terraforming
{: #replace-your-configuration-using-cf-terraforming}

**TBD:** Get Arjun's assistance filling this out.

[NEED?](https://developers.cloudflare.com/terraform/additional-configurations/waf-custom-rules/)

You can use the cf-terraforming tool to generate the Terraform configuration for your current WAF custom rules (converted by {{site.data.keyword.cis_short_notm}} from your firewall rules). Then, import the new resources to Terraform state.

The recommended steps for replacing your firewall rules (and filters) configuration in Terraform with a new ruleset configuration are the following.

1. Run the following command to generate all ruleset configurations for a zone:

      ```sh null {3,6}
   cf-terraforming generate --zone <ZONE_ID> --resource-type "cis_ruleset"

   resource "cis_ruleset" "terraform_managed_resource_3c0b456bc2aa443089c5f40f45f51b31" {
     kind    = "zone"
     name    = "default"
     phase   = "http_request_firewall_custom"
     zone_id = "<ZONE_ID>"
     rules {
       [...]
     }
     [...]
   }
   [...]
   ```
   {: codeblock}

1. The previous command might return additional ruleset configurations for other {{site.data.keyword.cis_short_notm}} products also based on the Ruleset Engine. Because you are migrating firewall rules to custom rules, keep only the Terraform resource for the `http_request_firewall_custom` phase and save it to a `.tf` configuration file. You require the full resource name in the next step.

1. Import the `cis_ruleset` resource that you previously identified into Terraform state by using the `terraform import` command. For example:

   ```sh
   terraform import cis_ruleset.terraform_managed_resource_3c0b456bc2aa443089c5f40f45f51b31 zone/<ZONE_ID>/3c0b456bc2aa443089c5f40f45f51b31
   ```
   {: codeblock}

```sh output
cis_ruleset.terraform_managed_resource_3c0b456bc2aa443089c5f40f45f51b31: Importing from ID "zone/<ZONE_ID>/3c0b456bc2aa443089c5f40f45f51b31"...
cis_ruleset.terraform_managed_resource_3c0b456bc2aa443089c5f40f45f51b31: Import prepared!
  Prepared cis_ruleset for import
cis_ruleset.terraform_managed_resource_3c0b456bc2aa443089c5f40f45f51b31: Refreshing state... [id=3c0b456bc2aa443089c5f40f45f51b31]

Import successful!

The resources that were imported are shown above. These resources are now in
your Terraform state and will henceforth be managed by Terraform.
```
{: screen}

1. Run `terraform plan` to validate that Terraform now checks the state of the new `cis_ruleset` resource, in addition to other existing resources already managed by Terraform. For example:

   ```sh
   terraform plan
   ```
   {: codeblock}

    ```sh output
   cis_ruleset.terraform_managed_resource_3c0b456bc2aa443089c5f40f45f51b31: Refreshing state... [id=3c0b456bc2aa443089c5f40f45f51b31]
   [...]
   cis_filter.my_filter: Refreshing state... [id=14a2524fd75c419f8d273116815b6349]
   cis_firewall_rule.my_firewall_rule: Refreshing state... [id=0580eb5d92e344ddb2374979f74c3ddf]
   [...]
   ```
   {: screen}

1. Remove any state that is related to firewall rules and filters from your Terraform state:

   **WARNING: Remove firewall rules and filters from Terraform state before you delete their configuration from `.tf` configuration files to prevent issues.**

   1. Run the following command to find all resources that are related to firewall rules and filters:

      ```sh
      terraform state list | grep -E '^cis_(filter|firewall_rule)\.'
      ```
      {: codeblock}

      ```sh output
      cis_filter.my_filter
      cis_firewall_rule.my_firewall_rule
      ```
      {: screen}

   1. Run the `terraform state rm ...` command in dry-run mode to understand the impact of removing those resources without performing any changes:

      ```sh
      terraform state rm -dry-run cis_filter.my_filter cis_firewall_rule.my_firewall_rule
      ```
      {: codeblock}

       ```sh output
      Would remove cis_filter.my_filter
      Would remove cis_firewall_rule.my_firewall_rule
      ```
      {: screen}

   1. If the impact looks correct, run the same command without the `-dry-run` parameter to remove the resources from Terraform state:

      ```sh
      terraform state rm cis_filter.my_filter cis_firewall_rule.my_firewall_rule
      ```
      {: codeblock}


      ```sh output
      Removed cis_filter.my_filter
      Removed cis_firewall_rule.my_firewall_rule
      Successfully removed 2 resource instance(s).
      ```
      {: screen}

1. After you remove firewall rules and filters resources from Terraform state, delete `cis_filter` and cis`_firewall_rule` resources from `.tf` configuration files.
1. Run `terraform plan` to verify that the resources you deleted from configuration files no longer appear. You should not have any pending changes.

      ```sh
      terraform plan
      ```
      {: codeblock}


      ```sh output
      cis_ruleset.terraform_managed_resource_3c0b456bc2aa443089c5f40f45f51b31: Refreshing state... [id=3c0b456bc2aa443089c5f40f45f51b31]
      [...]
      ```
      {: screen}

For details on importing {{site.data.keyword.cis_short_notm}} resources to Terraform and using the `cf-terraforming` tool, see the following resources:

* [Import CIS resources](https://developers.cloudflare.com/terraform/advanced-topics/import-cloudflare-resources/)
* [`cf-terraforming` GitHub repository](https://github.com/cloudflare/cf-terraforming)
