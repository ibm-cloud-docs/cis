---

copyright:
  years: 2024, 2025
lastupdated: "2025-06-24"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Overriding managed rulesets
{: #overriding-rulesets}

To customize the behavior of a managed ruleset, override it at deployment. When you override a ruleset, you specify changes to be executed in addition to the default configuration.

You can override a managed ruleset at the following levels:

* Ruleset overrides apply to all rules in the executed ruleset.
* Tag overrides apply to all rules with a specific tag. For example, use a tag override to customize the CIS Managed Ruleset so all rules with the wordpress tag are set to Block. If multiple tags have overrides and if a rule has more than one of these tags, the tag overrides order determines the behavior. For rules tagged with multiple overridden tags, the last tag’s overrides apply.
* Rule overrides apply to specific rules in a managed ruleset, referenced by their Rule ID.

Specific overrides take precedence over more general ones, and rule overrides take precedence over tag overrides, which take precedence over ruleset overrides.
{: important}

Ruleset overrides and tag overrides apply to both existing and future rules in the managed ruleset. If you want to override existing rules only, you must use rule overrides.

## Overriding workflow
{: #override-workflow}

To apply an override for a managed ruleset, take the following steps.

1. List the rulesets available by using the list rulesets operation.
1. List the rules for that ruleset by using the get ruleset operation.
1. Call the update ruleset operation on your phase entry point.
1. Specify the overrides in the `action_parameters` of the rule that executes your managed ruleset.

   ```sh
   "action_parameters": {
     "id": "<RULESET_ID>",
     "overrides": {
       // ruleset overrides
       "property-to-modify": "value",
       "property-to-modify": "value",
       // tag overrides
       "categories": [
         {
           "category": "<TAG_NAME>",
           "property-to-modify": "value",
           "property-to-modify": "value"
         }
       ],
       // rule overrides
       "rules": [
         {
           "id": "<RULE_ID>",
           "property-to-modify": "value",
           "property-to-modify": "value"
         }
       ]
     }
   }
   ```
   {: codeblock}

You can override the following rule properties.

* "action"
* "enabled"

Some managed rulesets can have extra override requirements, or they might override other rule properties.

It is not effective to enable all the rules in a managed ruleset at the instance level by using an override. This change can affect all the zones in your instance. Some rules are disabled by default because they eventually affect legitimate traffic. Do not enable these rules across zones without previous consideration.

## Overriding managed rulesets from the CLI
{: #cli-override-rule-sets}
{: cli}

You can override rulesets from the CLI.

### Listing managed rulesets from the CLI
{: #cli-override-list-rule-sets}

To list all zone rulesets from the CLI, run the following command:

```sh
ibmcloud cis managed-waf rulesets DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #command-options-listing-rules}

`DNS_DOMAIN_ID`
:   The ID of the domain.

`-i, --instance value`
:   The instance name or ID.

`--output value`
:   Specifies the output format; only JSON is supported.

### Listing rules under a zone ruleset from the CLI
{: #cli-override-list-rule-sets-rules}

To list the rules under a zone ruleset from the CLI, run the following command:

```sh
ibmcloud cis managed-waf ruleset DNS_DOMAIN_ID RULESET_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **`DNS_DOMAIN_ID`** is the ID of the domain.
* **`RULESET_ID`** is the ID of the ruleset for the rules to be listed.
* **`-i, --instance value`** is the instance name or ID.
* **`--output value`** specifies the output format; only JSON is supported.

### Overriding managed rulesets from the CLI
{: #cli-override-entry-point-rule-set}

To override a managed WAF ruleset from the CLI, run the following command:

```sh
ibmcloud cis managed-waf deployment-add-ruleset DNS_DOMAIN_ID RULESET_ID [--match EXPRESSION] [--enabled true|false] [--override-action ACTION] [--override-status STATUS] [--paranoia-level LEVEL] [--override-rules RULE] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **`DNS_DOMAIN_ID`** is the ID of the domain.
* **`--match value`** is the conditions that must be matched for the rule to run. See [Using fields, functions, and expressions](https://cloud.ibm.com/docs/cis?topic=cis-fields-and-expressions) for a list of values to match.
* **`--enabled value`** indicates whether the rule is active. Defaults to "true".
* **`--override-action value`** is the ruleset action of any overrides. Valid values are "managed_challenge", "block", "js_challenge", "log", "challenge".
* **`--paranoia-level value`** is the OWASP paranoia level. Valid values are "PL1", "PL2", "PL3", "PL4" and it's only available for `CIS OWASP Core Ruleset`.
* **`--override-rules value`** is the rules options of the overrides. For example, `--override-rules rule=RULE_ID,action=ACTION,enabled=STATUS`.
* **`-i, --instance value`** is the instance name or ID.
* **`--output value`** specifies the output format; only JSON is supported.


## Overriding managed rulesets with the API
{: #api-override-rule-sets}
{: api}

You can override rulesets from the API.

### Listing zone rulesets from the API
{: #api-override-list-zone-rule-sets}

To list all zone rulesets from the API, run the following command:

```sh
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/$CRN/zones/$ZONE_ID/rulesets \
  -H 'content-type: application/json' \
  -H 'accept: application/json' \
  -H 'x-auth-user-token: Bearer xxxxxx'
```
{: codeblock}

### Listing all rules for a ruleset from the API
{: #api-override-list-rule-sets-rules}

To list all rules for a specific ruleset, run the following command:

```sh
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/$CRN/zones/$ZONE_ID/rulesets/$RULESET_ID \
  -H 'content-type: application/json' \
  -H 'accept: application/json' \
  -H 'x-auth-user-token: Bearer xxxxxx'
```
{: codeblock}

Where:

* **`$RULESET_ID`** is the ID of the managed ruleset which the rules are listed for.

### Overriding an entry point ruleset from the API
{: #api-override-entry-point-rule-set}

To update the entry point ruleset from the API with an override, run the following command:

```sh
curl -X PUT \
  https://api.cis.cloud.ibm.com/v1/$CRN/zones/$ZONE_ID/rulesets/phases/$RULESET_PHASE/entrypoint \
  -H 'content-type: application/json' \
  -H 'accept: application/json' \
  -H 'x-auth-user-token: Bearer xxxxxx' \
  -d '{"description":"Deploy managed ruleset, enabling a specific rule with log action","rules":[{"action":"execute","expression":"true","action_parameters":{"id":"<MANAGED_RULESET_ID>","overrides":{"rules":[{"id":"<RULE_ID>","enabled":true,"action":"log"}]}}}]}'
```
{: codeblock}

Where:
* **`$RULESET_PHASE`** is the ruleset phase that is deployed to. Use `http_request_firewall_managed` to override managed WAF rulesets.
* **`-d`** is the object of attributes that are required to create the ruleset.
    * **`description`** defines your own summary of what a ruleset is accomplishing.
    * **`rules`** is the array of rules to deploy with the ruleset.
      * **`action`** is the action for the rule to take. See [WAF ruleset actions](/docs/cis?topic=cis-waf-actions) for a description of available actions.
      * **`action_parameters`** is the object for defining what the action operates on.
        * **`id`** is the ID of the ruleset to execute. This ID is retrieved from the list zone rulesets operation.
        * **`overrides`** is the object of overrides to set upon the selected ruleset.
          * **`rules`** is the list of rules that are overridden with the selected properties.
            * **`id`** is the ID of the rule to override. This ID is retrieved from the list zone ruleset rules operation.
            * **`enabled`** overwrites even when the rule is enabled.
            * **`action`** specifies the overridden action that the rule takes.
      * **`expression`** is the condition under which the rule runs. Using "true" means that this rule always runs.
      * **`description`** defines your own summary of what the rule is accomplishing.

## Overriding managed rulesets with Terraform
{: #override-rule-sets-terraform}
{: terraform}

You can override rulesets using Terraform.

### Listing managed rulesets with Terraform
{: #terraform-override-list-rule-sets}

The following example lists all managed rulesets using Terraform:

```sh
data "ibm_cis_rulesets" "tests" {
    cis_id    = ibm_cis.instance.id
    domain_id = data.ibm_cis_domain.cis_domain.domain_id
}
```
{: pre}

For more information about the arguments and attributes, see [`ibm_cis_rulesets`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_rulesets){: external} in the Terraform registry.

### Listing all rules of a managed ruleset with Terraform
{: #terraform-override-list-rule-sets-rules}

The following example lists all rules of a managed ruleset using Terraform:

```sh
resource "ibm_cis_ruleset" "config" {
    cis_id    = ibm_cis.instance.id
    domain_id = data.ibm_cis_domain.cis_domain.domain_id
    ruleset_id = "943c5da120114ea5831dc1edf8b6f769"
}
```
{: pre}

For more information about the arguments and attributes, see [`ibm_cis_ruleset`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_ruleset){: external} in the Terraform registry.

### Overriding a rule with Terraform
{: #terraform-override-entry-point-rule-set}

This example shows how to deploy the CIS managed ruleset with various overrides. First, it enables and blocks traffic for all rules. Then, it enables and blocks traffic for a specific rule. Finally, it enables and blocks traffic for all rules in the `wordpress` category. Essentially, this example illustrates the different methods for overriding deployed rules (global, specific, by category).

```sh
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
{: pre}

For more information about the arguments and attributes, see [`ibm_cis_ruleset_entrypoint_version`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_ruleset_entrypoint_version){: external} in the Terraform registry.
