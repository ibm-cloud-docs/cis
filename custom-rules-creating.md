---

copyright:
  years: 2025
lastupdated: "2025-09-04"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Working with WAF custom rules
{: #about-waf-custom-rules}

WAF custom rules offer power and flexibility by targeting HTTP traffic and applying custom criteria to block, challenge, log, or allow certain requests.
{: shortdesc}

You can create many types of WAF custom rules. However, the number of active rules on your site is limited by your customer plan. For more information on entitlements, see [Comparing CIS plans](/docs/cis?topic=cis-cis-plan-comparison).

The number of active rules per plan is fixed. Currently, you can't purchase more active rules.

Before getting started, it's a good idea to review [Using fields, functions, and expressions](/docs/cis?topic=cis-custom-rules-fields-and-expressions&interface=cli).
{: important}

You can create, update, and delete a custom rule by using the UI, CLI, API, or Terraform.

## Creating a custom rule in the console
{: #create-custom-rule-ui}
{: ui}

Follow these steps to create a custom rule in the console:

WAF custom rules are configured using the existing Firewall rules page. Any legacy firewall rules that were previously created on your domain are automatically converted into WAF custom rules.
{: note}

1. In the CIS console, navigate to the **Security**.
1. Select the **Custom rules** tab and then click **Create**.
1. Enter an optional description.
1. Optionally, input a priority, if necessary. A priority of zero is a null priority and is evaluated last.
1. Use the UI builder in the **Incoming requests** section to add a condition.
    To build an expression with multiple conditions, click either:
    * **And** - to evaluate conditions that use _and_ logic
    * **Or** - to evaluate conditions or groups of previously _and_'ed conditions that use _or_ logic

    You can see that as you build a condition, the Expression Preview shows the expression in plain text.

    In the Expression Preview, you can click to edit your expression manually instead of using the Visual Expression Builder, or switch between the two. However, depending on the complexity of a manually constructed expression, the Visual Expression Builder might be unable to render it.
    {: note}

1. Pick an action from the **Response** list menu.
1. To save your rule, choose the most appropriate option by clicking either:
    * **Save as draft** to save your rule, but keep it disabled.
    * **Save and deploy** to save your rule and activate it.

## Updating a custom rule in the console
{: #update-custom-rule-ui}
{: ui}

Follow these steps to update an existing custom rule in the console:

1. In the CIS console, navigate to the **Security**.
1. Select the **Custom rules** tab.
1. In the Custom rules table, locate the rule that you want to modify, then click the Actions menu on the right of the row.
1. Select **Edit**.
1. Make your changes to the rule.
1. To save your rule, choose the most appropriate option by clicking either:
    * **Save as draft** to save your rule, but keep it disabled.
    * **Save and deploy** to save your rule and activate it.

To pause or activate any rule in the list of existing rules, click the **Enabled** toggle.
{: note}

## Deleting a custom rule in the console
{: #delete-custom-rule-ui}
{: ui}

Follow these steps to delete an existing custom rule in the console:

1. In the CIS console, navigate to the **Security**.
1. In the Custom rules table, locate the rule to delete and click the Actions menu on the right of the row.
1. Select **Delete** from the action menu.
1. Click **Delete WAF custom rule** to delete the rule.

## Creating a custom rule from the CLI
{: #create-custom-rule-cli}
{: cli}

To create a custom rule from the CLI, follow these steps:

1. [Set up your CLI environment](/docs/cis?topic=cis-cis-cli#-cli-prereqs).

1. Log in to your account with the CLI. After you enter the password, the system prompts for the account and region that you want to use:

    ```sh
    ibmcloud login --sso
    ```
    {: pre}

1. Run the following command to create a custom rule:

   ```sh
   ibmcloud cis custom-waf rule-create DNS_DOMAIN_ID --match EXPRESSION --action ACTION [--description DESCRIPTION] [--enabled true|false] [-i, --instance INSTANCE] [--output FORMAT]
   ```
   {: pre}

   ```sh
   ibmcloud cis custom-waf rule-create DNS_DOMAIN_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
   ```
   {: pre}

   Where:

`DNS_DOMAIN_ID`
:   The ID of the DNS domain.

`--match`
:   Specifies the conditions that must be matched for the rule to run. For match value, see [Using fields, functions, and expressions](/docs/cis?topic=cis-fields-and-expressions).

`--action`
:   The rule action to perform. Valid values: "block", "challenge", "js_challenge", "managed_challenge", "log", "skip". For "block" and "skip" actions, use JSON file or JSON string instead.

`--enabled`
:  Indicates if the rule is active. The default is "false".

`--description`
:  A brief description of the rule.

`--json`
:  The JSON file or JSON string used to describe a custom rule.

   - The required fields in JSON data are `expression`, `action`.

      `expression`: Specifies the conditions that must be matched for the rule to run.
      `action`: The rule action to perform. Valid values: "block", "challenge", "js_challenge", "managed_challenge", "log", "skip".

   - The optional fields are `description`, `enabled`, `logging`, `action_parameters`.

      `action_parameters`: The rule action parameters.
        `ruleset`: Skip all remaining rules or one or more WAF-managed rulesets. Valid value: `current`.
        `phases`: Skips WAF components for matching requests. Valid values: "http_ratelimit", "http_request_firewall_managed", "http_request_sbfm".
        `products`: Skips specific security products for matching requests. Valid values: "waf", "rateLimit", "securityLevel", "hot", "bic", "uaBlock", "zoneLockdown".
        `response`:  Define a custom response for 'block' action.
            `status_code`:  Choose an HTTP status code for the response, in the range 400-499.
            `content_type`: The content type of a custom response. Valid response types are :`text/html`,`text/plain`, `application/json`, `text/xml`.
            `content`: The response body.
      `description`: Briefly describes the rule.
      `enabled`: Indicates if the rule is active.
      `logging`: Log requests matching the skip rule. This field is only available for the "skip" action.
         - `enabled`: When disabled, matched requests don't appear in firewall events.

   Sample JSON data:

```json

         {
           "description": "test-custom-rule",
           "expression": "(http.cookie contains \"test\")",
           "action": "skip",
           "logging": {
                   "enabled": true
               },
           "action_parameters": {
             "ruleset": "current",
               "phases": [
                       "http_ratelimit",
                       "http_request_firewall_managed",
                       "http_request_sbfm"
                   ],
                   "products": [
                       "waf",
                       "rateLimit",
                       "securityLevel",
                       "hot",
                       "bic",
                       "uaBlock",
                       "zoneLockdown"
                   ]
           },
           "enabled": true
         }
```
{: codeblock}

`-i, --instance`
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   Specify output format, only `JSON` is supported.

## Updating a custom rule from the CLI
{: #update-custom-rule-cli}
{: cli}

Run the following command to update a custom rule in the CLI:

```sh
ibmcloud cis custom-waf rule-update DNS_DOMAIN_ID [--match EXPRESSION] [--action ACTION] [--description DESCRIPTION] [--enabled true|false] [-i, --instance INSTANCE] [--output FORMAT]


ibmcloud cis custom-waf rule-update DNS_DOMAIN_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

`DNS_DOMAIN_ID`
:   The ID of the DNS domain.

`RULE_ID`
:  The ID of the rule.

`--match`
:   Specifies the conditions that must be matched for the rule to run. For match value, see [Using fields, functions, and expressions](/docs/cis?topic=cis-fields-and-expressions).

`--action`
:   The rule action to perform. Valid values: "block", "challenge", "js_challenge", "managed_challenge", "log", "skip".For "block" and "skip" actions, use JSON file or JSON string instead.

`--enabled`
:  Indicates if the rule is active. The default value is "false".

`--description`
:  A brief description of the rule.

`--json`
:  The JSON file or JSON string used to describe a custom rule.

   - The required fields in JSON data are `expression`, `action`.

      `expression`: Specifies the conditions that must be matched for the rule to run.
      `action`: The rule action to perform. Valid values: "block", "challenge", "js_challenge", "managed_challenge", "log", "skip".

   - The optional fields are `description`, `enabled`, `logging`, `action_parameters`.

      `action_parameters`: The rule action parameters.
        `ruleset`: Skip all remaining rules or one or more WAF-managed rulesets. Valid values: `current`.
        `phases`: Skips WAF components for matching requests. Valid values: "http_ratelimit", "http_request_firewall_managed", "http_request_sbfm".
        `products`: Skips specific security products for matching requests. Valid values: "waf", "rateLimit", "securityLevel", "hot", "bic", "uaBlock", "zoneLockdown".
        `response`:  Define a custom response for 'block' action.
            `status_code`:  Choose an HTTP status code for the response, in the range 400-499.
            `content_type`: The content type of a custom response. Valid response types are :`text/html`,`text/plain`, `application/json`, `text/xml`.
            `content`: The response body.
      `description`: Briefly describes the rule.
      `enabled`: Indicates if the rule is active.
      `logging`: Log requests matching the skip rule. This field is only available for the "skip" action.
         - `enabled`: When disabled, matched requests don't appear in firewall events.

   Sample JSON data:

```json
         {
           "description": "test-custom-rule",
           "expression": "(http.cookie contains \"test\")",
           "action": "block",
           "action_parameters": {
             "response": {
             "status_code": 429,
             "content_type": "text/xml",
             "content": "reject"
             }
           },
           "enabled": true
         }
```
{: codeblock}

`-i, --instance`
:   Instance name or ID. If not set, the context instance specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   Specify output format, only `JSON` is supported.

## Deleting a custom rule from the CLI
{: #delete-custom-rule-cli}
{: cli}

Run the following command to delete a custom rule in the CLI:

```sh
ibmcloud cis custom-waf rule-delete DNS_DOMAIN_ID RULE_ID [-f, --force] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

`DNS_DOMAIN_ID`
:   The ID of the DNS domain.

`RULE_ID`
:  The ID of the custom rule.

`-i, --instance`
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`-f, --force`
:   Attempt to delete a custom rule without prompting for confirmation.

`--output`
:   Specify output format, only `JSON` is supported.

## Command examples
{: #command-examples-create-update-delete}
{: cli}

*  To create a custom rule:

   `ibmcloud cis custom-waf rule-create 601b728b86e630c744c81740f72570c3 --action challenge --description "rule 1" --enabled true --match "(http.host eq \"www.example.com\")"`

*  To update a custom rule:

   `ibmcloud cis custom-waf rule-update 601b728b86e630c744c81740f72570c3 4d37cb6f87654e96a18bc531628a4d27 --enabled true`

*  To delete a custom rule:

   `ibmcloud cis custom-waf rule-delete 601b728b86e630c744c81740f72570c3 4d37cb6f87654e96a18bc531628a4d27`

## Getting the custom rule entry point for the API
{: #get-rule-entry-point-api}
{: api}

All custom rule API operations require a `RULESET_ID` of the entry point ruleset for the custom rules phase. This entry point ruleset might already exist or needs to be created if it does not exist.

Follow these steps to get the custom rule entry point ruleset:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded Cloud Resource Name (CRN) of the service instance.

   `ZONE_ID`: The domain ID.

1. When all variables are initiated, get the entry point ruleset:

```sh
curl -X GET "https://api.cis.cloud.ibm.com/v1/$CRN/zones/$ZONE_ID/rulesets/phases/http_request_firewall_custom/entrypoint" \
--header "X-Auth-User-Token: Bearer <API_TOKEN>" \
--header "Content-Type: application/json"
```
{: pre}

The ruleset ID is in the response of the successful request. If the preceding call returns a 404 Not Found response, use the following API to create the entrypoint ruleset for the custom rule phase:

```sh
curl -x POST https://api.cis.cloud.ibm.com/v1/$CRN/zones/$ZONE_ID/rulesets \
--header "X-Auth-User-Token: Bearer <API_TOKEN>" \
--header "Content-Type: application/json" \
--data '{
   "name": "Zone-level phase entry point",
   "kind": "zone",
   "description": "Custom rule entry point ruleset.",
   "phase": "http_request_firewall_custom"
}'
```
{: pre}

## Creating a custom rule with the API
{: #create-custom-rule-api}
{: api}

Follow these steps to create a custom rule with the API:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded Cloud Resource Name (CRN) of the service instance.

   `ZONE_ID`: The domain ID.

   `RULESET_ID`: The ID of the custom rule entrypoint ruleset.

1. When all variables are initiated, create the custom rule:

   ```sh
   curl -X POST "https://api.cis.cloud.ibm.com/v1/$CRN/zones/$ZONE_ID/rulesets/$RULESET_ID/rules" \
   --header "X-Auth-User-Token: Bearer <API_TOKEN>" \
   --header "Content-Type: application/json" \
   --data '{
     "description": "My custom rule with plain text response",
     "expression": "(ip.src.country eq \"GB\" or ip.src.country eq \"FR\") and cf.waf.score lt 20",
     "action": "block",
     "action_parameters": {
       "response": {
         "status_code": 403,
         "content": "Your request was blocked.",
         "content_type": "text/plain"
       }
     }
     }'
   ```
   {: pre}

## Updating a custom rule with the API
{: #update-custom-rule-api}
{: api}

Follow these steps to update an existing custom rule with the API:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded Cloud Resource Name (CRN) of the service instance.

   `ZONE_ID`: The domain ID.

   `RULESET_ID`: The ID of the custom rule entrypoint ruleset.

   `RULE_ID`: The ID of the custom rule to be modified.

1. When all variables are initiated, update the custom rule:

```sh
curl -X PATCH "https://api.cis.cloud.ibm.com/v1/$CRN/zones/$ZONE_ID/rulesets/$RULESET_ID/rules/$RULE_ID" \
--header "X-Auth-User-Token: Bearer <API_TOKEN>" \
--header "Content-Type: application/json" \
--data '{
   "enabled": false,
   "description": "block GB and FR or based on IP Reputation (temporarily disabled)"
}'
```
{: pre}

## Deleting a custom rule with the API
{: #delete-custom-rule-api}
{: api}

Follow these steps to delete an existing custom rule with the API:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded Cloud Resource Name (CRN) of the service instance.

   `ZONE_ID`: The domain ID.

   `RULESET_ID`: The ID of the custom rule entrypoint ruleset.

   `RULE_ID`: The ID of the custom rule to be modified.

1. When all variables are initiated, delete the custom rule:

```sh
curl -X DELETE "https://api.cis.cloud.ibm.com/v1/$CRN/zones/$ZONE_ID/rulesets/$RULESET_ID/rules/$RULE_ID" \
--header "X-Auth-User-Token: Bearer <API_TOKEN>" \
--header "Content-Type: application/json"
```
{: pre}

## Creating a custom rule with Terraform
{: #create-custom-rule-tf}
{: terraform}

To create a custom rule, you need to create an entry point first and then create the custom rule. The following example creates a custom rule with Terraform.

To create an entry point ruleset, run the following command:

```terraform
resource "ibm_cis_ruleset_entrypoint_version" "test" {
    cis_id    = "<cis-id>"
    domain_id = "<domain-id>"
    phase = "http_request_firewall_custom"
    rulesets {
      description = "Entry point ruleset for custom ruleset"
    }
    lifecycle {
      ignore_changes = [
        rulesets
      ]
  }
}
```
{: pre}

To create a custom rule, run the following command:

```terraform
   resource ibm_cis_ruleset_rule "config" {
      cis_id    = ibm_cis.instance.id
      domain_id = data.ibm_cis_domain.cis_domain.domain_id
      ruleset_id = resource.ibm_cis_ruleset_entrypoint_version.rulesets[0].ruleset_id
      rule {
        action =  "block"
        description = "var.description"
        expression = "true"
        enabled = "false"
        action_parameters {
          response {
            status_code = var.status_code
            content =  var.content
            content_type = "text/plain"
          }
        }
        position {
          index = var.index
          after = <id of any existing rule>
          before = <id of any existing rule>
        }
      }
    }
```
{: codeblock}

The following example shows how to create an entry point and WAF custom rule with Terraform:

```sh
resource ibm_cis_ruleset_entrypoint_version test {
cis_id    = ibm_cis.instance.id
domain_id = data.ibm_cis_domain.cis_domain.domain_id
phase = "http_request_firewall_custom"
rulesets {
   description = "Entrypoint ruleset for custom ruleset"
   }
   lifecycle {
   ignore_changes = [
      rulesets
   ]
  }
}
data ibm_cis_ruleset_entrypoint_versions custom_rule_ep {
  cis_id    = ibm_cis.instance.id
  domain_id = data.ibm_cis_domain.cis_domain.domain_id
  phase = "http_request_firewall_custom"
  depends_on = [
  ibm_cis_ruleset_entrypoint_version.test
  ]
}

resource ibm_cis_ruleset_rule "custom_rule1" {
    cis_id    = ibm_cis.instance.id
    domain_id = data.ibm_cis_domain.cis_domain.domain_id
    ruleset_id = data.ibm_cis_ruleset_entrypoint_versions.custom_rule_ep.rulesets[0].ruleset_id
      rule {
        action =  "skip"
        description = "adding custom rule via terraform"
        expression = "true"
        enabled = "true"
        action_parameters{
          ruleset = "current"
          phases = ["http_ratelimit", "http_request_sbfm","http_request_firewall_managed"]
          products = ["zoneLockdown","uaBlock", "bic", "hot", "securityLevel", "rateLimit","waf"]
        }
      }
}

resource ibm_cis_ruleset_rule "custom_rule2" {
    cis_id    = ibm_cis.instance.id
    domain_id = data.ibm_cis_domain.cis_domain.domain_id
    ruleset_id = data.ibm_cis_ruleset_entrypoint_versions.custom_rule_ep.rulesets[0].ruleset_id
      rule {
        action =  "block"
        description = "adding custom rule via terraform2"
        expression = "(http.request.uri.path eq \"/path1\")"
        enabled = "false"
      }
}
```
{: codeblock}

For more information about the arguments and attributes, see [`ibm_cis_ruleset_rule`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_ruleset_rule){: external} in the Terraform registry.

You can update a custom rule with Terraform by modifying the preceding example and running the `terraform apply` command. To delete the rule, simply remove the configuration and run `terraform apply`.
{: note}
