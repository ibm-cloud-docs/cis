---

copyright:
  years: 2024, 2025
lastupdated: "2025-02-28"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Deploying managed rulesets
{: #deploying-rule-sets}

You can deploy managed rulesets at the zone or instance level by using the CLI or API.
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

## Deploying managed rulesets from the CLI
{: #cli-deploy-rule-sets}
{: cli}

You can deploy managed rulesets from the CLI.

### Listing managed rulesets from the CLI
{: #cli-list-rule-sets}

To list all zone-managed rulesets from the CLI, run the following command:

```sh
ibmcloud cis managed-waf rulesets DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **DNS_DOMAIN_ID** is the ID of the domain.
* **-i, --instance value** is the instance name or ID.
* **--output value** specifies the output format; only JSON is supported.

### Updating deployed ruleset from the CLI
{: #cli-update-entry-point-rule-set}

To update a managed ruleset that was deployed by using the CLI, run the following command:

```sh
ibmcloud cis managed-waf deployment-add-ruleset DNS_DOMAIN_ID RULESET_ID [--match EXPRESSION] [--enabled true|false] [--override-action ACTION] [--override-status STATUS] [--paranoia-level LEVEL] [--override-rules RULE] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **DNS_DOMAIN_ID** is the ID of the domain.
* **--match value** is the conditions that must be matched for the rule to run. See [Using fields, functions, and expressions](https://cloud.ibm.com/docs/cis?topic=cis-fields-and-expressions) for a list of values to match.
* **--enabled value** indicates whether the rule is active. The default is `true`.
* **--overide-action value** is the ruleset action of any overrides. Valid values are `managed_challenge`, `block`, `js_challenge`, `log`, `challenge`.
* **--paranoia-level value** is the OWASP paranoia level. Valid values are `PL1`, `PL2`, `PL3`, `PL4`. This is only available for the `CIS OWASP Core Ruleset`.
* **--override-rules value** is the rules options of the overrides. For example `--override-rules rule=RULE_ID,action=ACTION,enabled=STATUS`.
* **-i, --instance value** is the instance name or ID.
* **--output value** specifies the output format; only JSON is supported.

## Deploying managed rulesets with the API
{: #api-deploy-rule-sets}
{: api}

You can deploy managed rulesets from the API.

### Listing managed rulesets from the API
{: #api-list-rule-sets}

To list all zone-managed rulesets from the API, run the following command:

```sh
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/$CRN/zones/$ZONE_ID/rulesets \
  -H 'content-type: application/json' \
  -H 'accept: application/json' \
  -H 'x-auth-user-token: Bearer xxxxxx'
```
{: codeblock}

### Updating entry point ruleset from the API
{: #api-update-entry-point-rule-set}

To update the entry point ruleset from the API, run the following command:

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
