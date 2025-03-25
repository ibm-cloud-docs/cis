---

copyright:
  years: 2025
lastupdated: "2025-03-25"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Working with WAF custom rules
{: #about--waf-custom-rules}

WAF custom rules offer power and flexibility by targeting HTTP traffic and applying custom criteria to block, challenge, log, or allow certain requests.
{: shortdesc}

You can create many types of WAF custom rules. However, the number of active rules on your site is limited by your customer plan. See [Comparing CIS plans](/docs/cis?topic=cis-cis-plan-comparison) for more information on entitlements.

The number of active rules per plan is fixed. Currently, you can't purchase more active rules.

Before getting started, it's a good idea to review [Using fields, functions, and expressions](/docs/cis?topic=cis-custom-rules-fields-and-expressions&interface=cli).
{: important}

You can create, update, and delete a custom rule by using the UI, CLI, API, or Terraform. 

## Working with WAF custom rules in the UI
{: #working-with-waf-custom-rules}
{: ui}

INTRODUCTION HERE

### Creating a custom rule in the UI
{: #create-custom-rule-ui}

Follow these steps to create a custom rule in the UI:

WAF custom rules are configured using the existing Firewall rules page. Any legacy firewall rules that were previously created on your domain are automatically converted into WAF custom rules.
{: note}

1. Navigate to **Security > Firewall rules**.
1. Click **Create**.
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
    * **Save as draft** to save your rule, but leave it disabled.
    * **Save and deploy** to save your rule and activate it.

### Updating a custom rule in the UI
{: #update-custom-rule-ui}

Follow these steps to update an existing custom rule in the UI:

1. Navigate to **Security > Firewall rules**.
1. In the firewall rules table, locate the rule that you want to modify, then click the Actions menu on the right of the row.
1. Select **Edit**.
1. Make your changes to the rule.
1. To save your rule, choose the most appropriate option by clicking either:
    * **Save as draft** to save your rule, but leave it disabled.
    * **Save and deploy** to save your rule and activate it.

To pause or activate any rule in the list of existing rules, click the **Enabled** toggle.
{: note}

### Deleting a custom rule in the UI
{: #delete-custom-rule-ui}

Follow these steps to delete an existing custom rule in the UI:

1. Navigate to **Security > Firewall rules**.
1. In the firewall rules table, locate the rule to modify and click the Actions menu on the right of the row.
1. Select **Delete**.
1. Confirm the rule deletion.

## Working with WAF custom rules from the CLI
{: #working-with-waf-custom-rules-cli}
{: cli}

INTRODUCTION HERE

### Creating a custom rule from the CLI
{: #create-custom-rule-cli}

To create a custom rule from the CLI, follow these steps:

1. [Set up your CLI environment](/docs/cis?topic=cis-cis-cli#-cli-prereqs). 
   
1. Log in to your account with the CLI. After you enter the password, the system prompts for the account and region that you want to use:

    ```sh
    ibmcloud login --sso
    ```
    {: pre}

1. Run the following command to create a custom rule:

   ```sh
   ibmcloud cis XXXX
   ```
   {: pre}

   Where:

   `--xxx`
   :   Description. Required. 

   `--xxx`
   :   Description. Required. 

### Updating a custom rule from the CLI
{: #update-custom-rule-cli}

Run the following command to update a custom rule in the CLI:

```sh
ibmcloud cis XXXX
```
{: pre}

Where:

   `--xxx`
   :   Description. Required. 

   `--xxx`
   :   Description. Required. 

### Deleting a custom rule from the CLI
{: #delete-custom-rule-cli}

Run the following command to delete a custom rule in the CLI:

```sh
ibmcloud cis XXXX
```
{: pre}

Where:

   `--xxx`
   :   Description. Required. 

   `--xxx`
   :   Description. Required. 

### Command examples
{: #command-examples-create-update-delete}

*  `here`
*  `here`
*  `here`

## Working with WAF custom rules with the API
{: #working-with-waf-custom-rules-api}
{: api}

INTRODUCTION HERE

### Getting the custom rule entry point for the API
{: #get-rule-entry-point-api}

All custom rule API operations require a `RULESET_ID` of the entry point ruleset for the custom rules phase. This entry point ruleset may already exist or needs to be created if it does not exist.

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

The ruleset ID will be in the response of the successful request. If the above call returns a 404 Not Found response, use the following API to create the entrypoint ruleset for the custom rule phase:

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

### Creating a custom rule with the API
{: #create-custom-rule-api}

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

### Updating a custom rule with the API
{: #update-custom-rule-api}

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

### Deleting a custom rule with the API
{: #delete-custom-rule-api}

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

## Working with WAF custom rules with Terraform
{: #working-with-waf-custom-rules-tf}
{: terraform}

INTRODUCTION HERE

### Creating a custom rule with Terraform
{: #create-custom-rule-tf}

The following example creates a custom rule by using Terraform:

```
HERE
```
{: codeblock}

For more information about the arguments and attributes, see [XXXX] in the Terraform registry{: external}.

### Updating a custom rule with Terraform
{: #update-custom-rule-tf}

The following example updates a custom rule by using Terraform:

```
HERE
```
{: codeblock}

For more information about the arguments and attributes, see [XXXX] in the Terraform registry{: external}.

### Deleting a custom rule with Terraform
{: #delete-custom-rule-tf}

The following example deletes a custom rule by using Terraform:

```
HERE
```
{: codeblock}

For more information about the arguments and attributes, see [XXXX] in the Terraform registry{: external}.
