---

copyright:
  years: 2024, 2025
lastupdated: "2025-07-10"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Deploying managed rulesets
{: #deploying-rule-sets}

You can deploy managed rulesets at the zone or instance level by using the CLI, API, or Terraform.
{: shortdesc}

You can deploy a managed ruleset with customized behavior (changes that are executed in addition to the default configuration) by overriding it. For more information, see [Overriding managed rulesets](/docs/cis?topic=cis-overriding-rulesets&interface=cli).
{: tip}

## Deployment workflow
{: #deployment-workflow}

Use the following workflow to deploy a managed ruleset to a phase at the zone level:

1. Get your zone ID.
1. Run the **List zone** rulesets operation to obtain the available rulesets.
1. Find the ruleset ID of the managed ruleset that you want to deploy.
1. Identify the phase where you want to deploy the managed ruleset. Make sure that the managed ruleset belongs to the same phase where you want to deploy it.
1. Add a rule to the zone-level phase entry point ruleset that runs the managed ruleset.

## Deploying managed rulesets in the console
{: #ui-deploy-rule-sets}
{: ui}

To deploy managed rulesets in the CIS console, follow these steps:

1. In the CIS console, navigate to the **Security** section.
1. Select the **WAF** tab.
1. Click **Add exception** to open the Add exception side panel.
1. Enter a name for your managed rules exception.
1. Define the match condition by building an expression:
   * Choose the request field, select an operator, and provide a value.
   * You can also use the Expression Builder to manually write expressions
   * Combine multiple conditions using **And** and **Or** operators to create complex logic.
1. Choose whether to log requests that match the expression.
1. Decide how the ruleset should behave for matching requests:
   * Skip all remaining rules, or
   * Skip specific rules from a managed ruleset

      If you select to skip specific rules, click **Browse rules**, select a ruleset, and then select the specific rules to skip.
1. Click **Deploy** to activate the configuration.

   After deployment, you can return at any time to edit your managed ruleset configuration.

## Deploying managed rulesets from the CLI
{: #cli-deploy-rule-sets}
{: cli}

You can deploy managed rulesets from the CLI.

### Listing managed rulesets from the CLI
{: #cli-list-rule-sets}

To list all zone-managed rulesets from the CLI, follow these steps:

1. [Set up your CLI environment](/docs/cis?topic=cis-cis-cli#-cli-prereqs).

1. Log in to your account with the CLI. After you enter the password, the system prompts for the account and region that you want to use:

    ```sh
    ibmcloud login --sso
    ```
    {: pre}

1. Run the following command to create a custom rule:

   ```sh
   ibmcloud cis managed-waf rulesets DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
   ```
   {: pre}

   **Command options**

   `DNS_DOMAIN_ID`
   :   The ID of the domain.

   `-i, --instance`
   :   Instance name or ID.

   `--output`
   :   Specifies the output format; only JSON is supported.


### Updating deployed ruleset from the CLI
{: #cli-update-entry-point-rule-set}

To update a deployed ruleset from the CLI, follow these steps:

1. [Set up your CLI environment](/docs/cis?topic=cis-cis-cli#-cli-prereqs).

1. Log in to your account with the CLI. After you enter the password, the system prompts for the account and region that you want to use:

    ```sh
    ibmcloud login --sso
    ```
    {: pre}

1. Run the following command to create a custom rule:

   ```sh
   ibmcloud cis managed-waf deployment-add-ruleset DNS_DOMAIN_ID RULESET_ID [--match EXPRESSION] [--enabled true|false] [--override-action ACTION] [--override-status STATUS] [--paranoia-level LEVEL] [--override-rules RULE] [-i, --instance INSTANCE] [--output FORMAT]
   ```
   {: pre}

   **Command options**

   `DNS_DOMAIN_ID`
   :   The ID of the domain.

   `--match`
   :   The conditions that must be matched for the rule to run. See [Using fields, functions, and expressions](/docs/cis?topic=cis-fields-and-expressions) for a list of values to match.

   `--enabled`
   :   Indicates whether the rule is active. The default is `true`.

   `--overide-action`
   :   The ruleset action of any overrides. Valid values are `managed_challenge`, `block`, `js_challenge`, `log`, `challenge`.

   `--paranoia-level`
   :   The OWASP paranoia level. Valid values are `PL1`, `PL2`, `PL3`, `PL4`. This is only available for the `CIS OWASP Core Ruleset`.

   `override-rules`
   :   The rules options of the overrides. For example `--override-rules rule=RULE_ID,action=ACTION,enabled=STATUS`.

   `-i, --instance`
   :   The instance name or ID.

   `--output`
   :   specifies the output format; only JSON is supported.

### Command example
{: #command-example-deploy-managed-rulesets}

This example shows how to deploy the ruleset `efb7b8c949ac4650a09736fc376e9aee` and the overriding the rule present inside the ruleset. It is also overriding rules with category wordpress.

`ibmcloud cis managed-waf deployment-add-ruleset $domain efb7b8c949ac4650a09736fc376e9aee --match "(http.cookie eq \"example.com/contact?page=1234\")" --action execute --enabled false --override-action block --override-status false --override-rules rule=5de7edfa648c4d6891dc3e7f84534ffa,action=log,enabled=true --override-rules action=managed_challenge,rule=e3a567afc347477d9702d9047e97d760`

## Deploying managed rulesets with the API
{: #api-deploy-rule-sets}
{: api}

You can deploy managed rulesets with the API.

### Getting the custom rule entry point for the API
{: #get-rule-entry-point-api-2}

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

### Listing managed rulesets with the API
{: #api-list-rule-sets}

Follow these steps to list managed rulesets with the API:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded Cloud Resource Name (CRN) of the service instance.

   `ZONE_ID`: The domain ID.

   `RULESET_ID`: The ID of the custom rule entrypoint ruleset.

1. When all variables are initiated, list all zone-managed rulesets:

```sh
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/$CRN/zones/$ZONE_ID/rulesets \
  -H 'content-type: application/json' \
  -H 'accept: application/json' \
  -H 'x-auth-user-token: Bearer xxxxxx'
```
{: codeblock}

### Updating entry point rulesets with the API
{: #api-update-entry-point-rule-set}

Follow these steps to update an entry point ruleset with the API:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded Cloud Resource Name (CRN) of the service instance.

   `ZONE_ID`: The domain ID.

   `RULESET_ID`: The ID of the custom rule entrypoint ruleset.

1. When all variables are initiated, update the entry point ruleset:

```sh
curl -X PUT \
  https://api.cis.cloud.ibm.com/v1/$CRN/zones/$ZONE_ID/rulesets/phases/$RULESET_PHASE/entrypoint \
  -H 'content-type: application/json' \
  -H 'accept: application/json' \
  -H 'x-auth-user-token: Bearer xxxxxx' \
  -d '{"rules":[{"action":"execute","action_parameters":{"id":"4814384a9e5d4991b9815dcfc25d2f1f"},"expression":"true","description":"Execute WAF OWASP ruleset"}]}'
```
{: codeblock}

Where:
- **$RULESET_PHASE** is the ruleset phase that will be deployed. Use `http_request_firewall_managed` to deploy managed WAF rulesets.
- **-d** is the object of attributes that are required to create the ruleset.
   - **rules** is the array of rules to deploy with the ruleset. For example:
     - **action** is the action for the rule to take. See [Rules actions](/docs/cis?topic=cis-waf-actions) for a description of actions that can be used.
     - **action_parameters** is the object for defining what the action should operate on.
       - **id** is the ID of the ruleset to run. This ID is retrieved from the `list zone rulesets` operation.
   - **expression** is the condition under which the rule runs. Using `true` means that this rule always run.
   - **description** defines the summary of what your rule is accomplishing.

## Deploying managed rulesets with Terraform
{: #working-with-managed-rules-tf}
{: terraform}

### Listing managed rulesets with Terraform
{: #listing-managed-rule-tf}

The following example lists managed rulesets by using Terraform:

```terraform
data "ibm_cis_rulesets" "tests" {
    cis_id    = ibm_cis.instance.id
    domain_id = data.ibm_cis_domain.cis_domain.domain_id
    }
```
{: codeblock}

For more information about the arguments and attributes, see [`ibm_cis_rulesets`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_rulesets){: external} in the Terraform registry.

### Listing all rules of a managed ruleset
{: #listing-all-rules-tf}

The following example lists all rules of a managed ruleset by using Terraform:

```terraform
resource "ibm_cis_ruleset" "config" {
    cis_id    = ibm_cis.instance.id
    domain_id = data.ibm_cis_domain.cis_domain.domain_id
    ruleset_id = "943c5da120114ea5831dc1edf8b6f769"
}
```
{: codeblock}

For more information about the arguments and attributes, see [`ibm_cis_ruleset`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_ruleset){: external} in the Terraform registry.

### Overriding rule
{: #overriding-rule}

The following example overrides a rule by using Terraform:

```terraform
resource "ibm_cis_ruleset_entrypoint_version" "test" {
    cis_id    = ibm_cis.instance.id
    domain_id = data.ibm_cis_domain.cis_domain.domain_id
    phase = "http_request_firewall_managed"
    rulesets {
      description = "Entrypoint ruleset for managed ruleset"
      rules {
        action =  "execute"
        description = "Deploy CIS managed ruleset"
        enabled = true
        expression = "true"
        action_parameters  {
          id = "efb7b8c949ac4650a09736fc376e9aee"
          overrides {
            action = "block"
            enabled = true
            override_rules {
              rule_id = "var.overriden_rule.id"
              enabled = true
              action = "block"
            }
            categories {
              category = "wordpress"
              enabled = true
              action = "block"
            }
          }
        }
      }
    }
  }
```
{: codeblock}

For more information about the arguments and attributes, see [`ibm_cis_ruleset_entrypoint_version`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_ruleset_entrypoint_version){: external} in the Terraform registry.
