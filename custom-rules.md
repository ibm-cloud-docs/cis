---

copyright:
  years: 2024, 2025
lastupdated: "2025-02-28"

keywords: custom rules, rulesets, waf, firewall rules

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# About WAF custom rules
{: #custom-rules-overview}

The WAF custom rules feature allows you to control incoming traffic by filtering requests to a domain. You can perform actions such as **Block** or **Managed challenge** on incoming requests according to the rules you define.
{: shortdesc}

Like other rules evaluated by the Ruleset Engine, WAF custom rules require the following basic parameters:
- An expression that specifies the criteria you are matching traffic on using the rules language.
- An action that specifies what to perform when there is a match for the rule.

Custom rules are evaluated in the order they are set, from first to last position, in the custom rules table. You can view the table by navigating to **Security > Custom Rules**. Some actions like **Block** will stop the evaluation of other rules. For more details on actions and their behavior, see [Ruleset Engine rules actions]([/docs/cis?topic=cis-cis-ruleset-engine](/docs/cis?topic=cis-cis-ruleset-engine#ruleset-engine-actions)).
{: important}

Refer to [Migrating to custom rules](/docs/cis?topic=cis-migrating-to-custom-rules) to learn more about the differences between firewall rules and WAF custom rules. 
{: note}

## Common use cases
{: #custom-rules-use-cases}

The following sections detail examples of common use cases for WAF custom rules.

### Only allow traffic from specified countries
{: #cis-cr-allow-countries}

Using the **Block** action, this example blocks requests based on their country code using the `ip.src.country` field, only allowing requests from two countries: the United States and Mexico: 

```sh
(not ip.src.country in {"US" "MX"})
```

### Block requests by IP reputation
{: #cis-cr-block-requests-ip}

IP reputation is a score from 0 (zero risk) to 100 (high risk), classifying the IP reputation of a visitor.

IP reputation is calculated based on Project Honeypot, external public IP information, as well as internal threat intelligence from managed rules and DDoS.
{: note}

Using the **Block** action, this example blocks requests based on country codes (ISO 3166-1 Alpha 2 ↗ format), from IP addresses that score greater than 0:

```sh
(ip.src.country in {"CN" "TW" "US" "GB"} and cf.threat_score gt 0)
```

### Configuring a rule to skip other CIS features
{: #cis-cr-skip-features}

The skip action supports different skip options, according to the security features or products that you want to skip.

This section contains examples of different skip rule scenarios for WAF custom rules. You should take the following considerations into account: 

* The `{zone_id}` value is the ID of the zone where you want to add the rule.
* The `{ruleset_id}` value is the ID of the entry point ruleset of the `http_request_firewall_custom` phase. For details on obtaining this ruleset ID, see [List and view rulesets](/apidocs/cis#get-zone-rulesets). The following API examples add a skip rule to an existing ruleset using the [Create a zone ruleset](/apidocs/cis#create-zone-ruleset-rule) rule operation.

   However, the entry point ruleset may not exist yet. In this case, invoke the [Update entrypoint ruleset](/apidocs/cis#update-zone-entrypoint-ruleset) operation to create the entry point ruleset with a skip rule.

* Although each example only includes one action parameter, you can use several skip options in the same rule by specifying the ruleset, phases, and products action parameters simultaneously.

#### Skip the remaining rules in the current ruleset
{: #cis-skip-remaining-rules}

This example invokes the [Create a zone ruleset](/apidocs/cis#create-zone-ruleset-rule) rule operation to add a skip rule to the existing `http_request_firewall_custom` phase entry point ruleset with ID `{ruleset_id}`. The rule skips all remaining rules in the current ruleset for requests matching the rule expression:

```sh
curl -X POST "https://api.cis.cloud.ibm.com/v1/$CRN/zones/$ZONE_ID/rulesets/$RULESET_ID/rules" \
--header "X-Auth-User-Token: Bearer <API_TOKEN>" \
--header "Content-Type: application/json" \
--data '{
  "action": "skip",
  "action_parameters": {
    "ruleset": "current"
  },
  "expression": "http.request.uri.path contains \"/skip-current-ruleset/\"",
  "description": ""
}'
```

#### Skip a phase 
{: #cis-skip-phase}

This example invokes the Create a zone ruleset rule operation to add a rule to the existing `http_request_firewall_custom` phase entry point ruleset with ID `{ruleset_id}`. The rule will skip the `http_ratelimit` phase for requests matching the rule expression:

```sh
url -X POST "https://api.cis.cloud.ibm.com/v1/$CRN/zones/$ZONE_ID/rulesets/$RULESET_ID/rules" \
--header "X-Auth-User-Token: Bearer <API_TOKEN>" \
--header "Content-Type: application/json" \
--data '{
  "action": "skip",
  "action_parameters": {
    "phases": [
      "http_ratelimit"
    ]
  },
  "expression": "http.request.uri.path contains \"/skip-phase/\"",
  "description": ""
}'
```

#### Skip a phase and do not log matching requests
{: #cis-skip-phase-no-matching}

This example invokes the [Create a zone ruleset](/apidocs/cis#create-zone-ruleset-rule) rule operation to add a rule that both skips the `http_ratelimit` phase and disables event logging for the current rule:

```sh
curl -X POST "https://api.cis.cloud.ibm.com/v1/$CRN/zones/$ZONE_ID/rulesets/$RULESET_ID/rules" \
--header "X-Auth-User-Token: Bearer <API_TOKEN>" \
--header "Content-Type: application/json" \
--data '{
  "action": "skip",
  "action_parameters": {
    "phases": [
      "http_ratelimit"
    ]
  },
  "logging": {
    "enabled": false
  },
  "expression": "http.request.uri.path contains \"/disable-logging/\"",
  "description": ""
}'
```

#### Skip security products
{: #cis-skip-security-products}

This example uses the [Create a zone ruleset](/apidocs/cis#create-zone-ruleset-rule) rule operation to add a rule that skips the Zone Lockdown and User Agent Blocking products for requests matching the rule expression:

```sh
url -X POST "https://api.cis.cloud.ibm.com/v1/$CRN/zones/$ZONE_ID/rulesets/$RULESET_ID/rules" \
--header "X-Auth-User-Token: Bearer <API_TOKEN>" \
--header "Content-Type: application/json" \
--data '{
  "action": "skip",
  "action_parameters": {
    "products": [
      "zoneLockdown",
      "uaBlock"
    ]
  },
  "expression": "http.request.uri.path contains \"/skip-products/\"",
  "description": ""
}'
```
