---

copyright:
  years: 2018, 2026
lastupdated: "2026-06-18"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Configuring rate limiting
{: #cis-rate-limiting}

The _previous_ version of rate-limiting rules is deprecated. Active rules from the previous version will no longer function.
{: deprecated}

Rate limiting (Enterprise plan only) protects against denial-of-service attacks, brute-force login attempts, and other types of abusive behavior targeting the application layer.
{: shortdesc}

Select the type of rate-limiting rule, either a **Custom rule** or **Protect login**.

## Creating a custom rate limiting rule in the console
{: #create-a-custom-rate-limiting-rule-ui}
{: ui}

To create a custom rate limiting rule, complete the following steps:

1. In the {{site.data.keyword.cis_short}} console, navigate to the **Security** > **Rate limiting**, and then click **Create rule**.
1. Enter a name for the rule.
1. Define the match condition for the rule:
   1. Select a request field (for example, URI path, HTTP method, or header).
   1. Select an operator (for example, equals, contains, or matches).
   1. Enter or select a value.
   1. Optional: Use the Expression Builder to create a custom expression for more complex matching logic.
   1. Optional: Combine multiple conditions by using **And** and **Or** operators to create compound rules.
   1. Optional: Disable **Cache status** if you want the rate-limiting rule to consider only requests that reach the origin server. By default, cached requests are included in the rate calculation.
1. In **With the same characteristics**, select the characteristic that {{site.data.keyword.cis_short}} uses to identify matching requests. Common options include IP address, IP with NAT support, session, headers, cookie, query string, or JA3 fingerprint.
1. Optional: To define a custom counting expression:
   1. Enable **Use custom counting expression**.
   1. Enter the counting expression. By default, the counting expression matches the rule expression. A custom counting expression allows you to count requests differently from how they are matched.
1. In **When rate exceeds**, configure the request threshold:
   1. Enter the maximum number of requests allowed.
   1. Select the time period that {{site.data.keyword.cis_short}} uses to evaluate the request rate (for example, 10 seconds, 1 minute, or 1 hour).
1. In **Then take action**, select the action to apply when the threshold is exceeded. Options include **Block** (reject requests), **Challenge** (present a CAPTCHA), **JS Challenge** (present a JavaScript challenge), **Log** (log without action), or **Managed Challenge** (present an appropriate challenge based on client characteristics). For example, selecting **Block** causes {{site.data.keyword.cis_short}} to reject requests that exceed the configured rate limit.
1. In **With the following behavior**, select the mitigation behavior:
   1. Select a mitigation timeout to block requests for a specified duration after the threshold is exceeded (for example, 1 minute, 10 minutes, or 1 hour).
   1. Enterprise customers with the rate limiting add-on can select **Throttle requests over the maximum configured rate** to limit requests instead of applying the configured action.
1. In **Place at**, select the rule order. Rules are evaluated in order, so place more specific rules before general rules.
1. Click **Deploy**.

The rate limiting rule is created and deployed. The rule takes effect immediately and begins monitoring traffic according to your configuration.

## Updating a rate limiting rule in the console
{: #rate-limit-ui-update}

To update a rate-limiting rule, complete the following steps:

1. In the {{site.data.keyword.cis_short}} console, navigate to **Security** > **Rate limiting**.
1. In the rate limiting ruleset table, locate the rule that you want to modify.
1. Click Actions menu on the right of the row and then select **Edit**.
1. Modify the rule settings as needed.
1. Click **Save** to update the rule.

## Deleting a rate limiting rule in the console
{: #rate-limit-ui-delete}

To delete a rate limiting rule in the console, follow these steps:

1. In the {{site.data.keyword.cis_short}} console, navigate to **Security** > **Rate limiting**.
1. In the rate limiting rules table, locate the rule that you want to delete.
1. Click the Actions menu for the rule, and then select **Delete**.
1. Review the confirmation message and click **Delete** to confirm.

## Configuring the response
{: #rate-limiting-configure-response}
{: ui}

Select from the actions listed, and specify the timeout period. In this case, the timeout refers to the ban period that the action takes place. A 60-second timeout means that the action is applied for 60 seconds.

| Action | Description |
| ------ | ------------ |
| Block | Issues a 429 error when the threshold is exceeded |
| Challenge | User must pass a Google re-Captcha Challenge before proceeding. If successful, the request is accepted. Otherwise, the request gets blocked. |
| JS Challenge | The user must pass a JavaScript Challenge before proceeding. If successful, the request is accepted. Otherwise, the request gets blocked. |
| Simulate | You can use this option to test your rule before applying any of the other options in your live environment.
{: caption="Actions for rate limiting" caption-side="bottom"}

## Getting the rate-limiting rule entrypoint for the API
{: #get-ratelimit-rule-entry-point-api}
{: api}

All rate-limiting rule API operations require a `RULESET_ID` of the entrypoint ruleset for the rate-limiting rules phase. This entrypoint ruleset might exist or might need to be created if it does not exist.

Follow these steps to get the rate-limiting rule entrypoint ruleset:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded Cloud Resource Name (CRN) of the service instance.

   `ZONE_ID`: The domain ID.

1. When all variables are initiated, get the entrypoint ruleset:

   ```sh
   curl -X GET "https://api.cis.cloud.ibm.com/v1/$CRN/zones/$ZONE_ID/rulesets/phases/http_ratelimit/entrypoint" \
   --header "X-Auth-User-Token: Bearer <API_TOKEN>" \
   --header "Content-Type: application/json"
   ```
   {: pre}

   The ruleset ID is in the response of the successful request. If the preceding call returns a 404 Not Found response, use the following API to create the entrypoint ruleset for the rate-limiting rule phase:

   ```sh
   curl -x POST https://api.cis.cloud.ibm.com/v1/$CRN/zones/$ZONE_ID/rulesets \
   --header "X-Auth-User-Token: Bearer <API_TOKEN>" \
   --header "Content-Type: application/json" \
   --data '{
     "name": "Zone-level phase entrypoint",
     "kind": "zone",
     "description": "Rate-limting rule entrypoint ruleset.",
     "phase": "http_ratelimit"
   }'
   ```
   {: pre}

### Creating a rate-limiting rule with the API
{: #create-rate-limiting-rule-api}
{: api}

Follow these steps to create a rate-limiting rule with the API:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded Cloud Resource Name (CRN) of the service instance.

   `ZONE_ID`: The domain ID.

   `RULESET_ID`: The ID of the rate-limiting rule entrypoint ruleset.

1. When all variables are initiated, create the rate-limiting rule:

   ```sh
   curl -X POST "https://api.cis.cloud.ibm.com/v1/$CRN/zones/$ZONE_ID/rulesets/$RULESET_ID/rules" \
   --header "X-Auth-User-Token: Bearer <API_TOKEN>" \
   --header "Content-Type: application/json" \
   --data '{
     "description": "My rate limiting rule",
     "expression": "(http.request.uri.path matches \"^/api/\")",
     "action": "block",
     "ratelimit": {
       "characteristics": [
         "cf.colo.id",
         "ip.src"
       ],
       "period": 60,
       "requests_per_period": 100,
       "mitigation_timeout": 600
     }
   }'
   ```
   {: pre}

### Updating a rate-limiting rule with the API
{: #update-rate-limiting-rule-api}
{: api}

Follow these steps to update an existing rate-limiting rule with the API:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded Cloud Resource Name (CRN) of the service instance.

   `ZONE_ID`: The domain ID.

   `RULESET_ID`: The ID of the rate-limiting rule entrypoint ruleset.

   `RULE_ID`: The ID of the rate-limiting rule to be modified.

1. When all variables are initiated, update the rate-limiting rule:

   ```sh
   curl -X PATCH "https://api.cis.cloud.ibm.com/v1/$CRN/zones/$ZONE_ID/rulesets/$RULESET_ID/rules/$RULE_ID" \
   --header "X-Auth-User-Token: Bearer <API_TOKEN>" \
   --header "Content-Type: application/json" \
   --data '{
     "enabled": true,
     "description": "rate limit IPs for API"
   }'
   ```
   {: pre}

### Deleting a rate-limiting rule with the API
{: #delete-rate-limiting-rule-api}
{: api}

Follow these steps to delete an existing rate-limiting rule with the API:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded Cloud Resource Name (CRN) of the service instance.

   `ZONE_ID`: The domain ID.

   `RULESET_ID`: The ID of the rate-limiting rule entrypoint ruleset.

   `RULE_ID`: The ID of the rate-limiting rule to be modified.

1. When all variables are initiated, delete the rate-limiting rule:

   ```sh
   curl -X DELETE "https://api.cis.cloud.ibm.com/v1/$CRN/zones/$ZONE_ID/rulesets/$RULESET_ID/rules/$RULE_ID" \
   --header "X-Auth-User-Token: Bearer <API_TOKEN>" \
   --header "Content-Type: application/json"
   ```
   {: pre}

### Verifying the rate-limiting rules and response consistency by using HTTP status
{: #verify-rate-limiting-response}
{: api}

When you apply rate-limiting rules to a web address or service, it’s important to confirm that the rules are enforced correctly. A simple test confirms that the system responds with the following appropriate HTTP status codes:

* `200 OK` or `404 Not Found` for allowed requests
* `429 Too Many Requests` when rate limits are exceeded.

To verify the rate-limiting rules and response consistency, run the following command:

```sh
for i in {1..N}; do curl -s -o /dev/null -w "%{http_code}\n" <your-target-url>; done
```
{: pre}

#### Command options
{: #rate-command-options}

`N`
:   Number of requests you want to send.

`your-target-url`
:   URL of the service or endpoint you want to test.

This command provides output to the HTTP status code for each request and allows you to observe when the rate limit threshold is reached.

## Creating a rate limiting rule from the CLI
{: #create-rate-limit-cli}
{: cli}

To create a rate limiting rule from the CLI, follow these steps:
1. [Set up your CLI environment](/docs/cis?topic=cis-cis-cli#-cli-prereqs).
1. Log in to your account from the CLI. After you enter the password, the system prompts for the account and region that you want to use:

   ```sh
   ibmcloud login --sso
   ```
   {: pre}

1. Run the following command to create a rate-limiting rule:
   ```sh
   ibmcloud cis ratelimit-rule-create DNS_DOMAIN_ID --url URL [--description DESCRIPTION] [--threshold NUM] [--period SECONDS] [...]
   ```
   {: pre}

   You can also create a rate-limiting rule by providing a JSON file or a JSON string directly:
   ```sh
   ibmcloud cis ratelimit-rule-create DNS_DOMAIN_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
   ```
   {: pre}

### Command options
{: #create-commands-options-cli}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--json`
:   The JSON file or JSON string that is used to describe a rate limiting rule.
    - The required fields in JSON data are `match`, `threshold`, `period` and `action` :
        - `match` : Determines which traffic the rate limiting rule counts toward the threshold.
            - `request` : Matches HTTP requests.
                - `methods` :  HTTP Methods, can be a subset `[POST,PUT]` or all `[_ALL_]`. This field is not required to create a rate limit rule. Valid values are `GET`, `POST`, `PUT`, `DELETE`, `PATCH`, `HEAD`, `_ALL_`.
                - `schemes` :  HTTP Schemes, can be one `[HTTPS]`, both `[HTTP`,`HTTPS]` or all `[_ALL_]`. This field is not required.
                - `url` : The URL pattern to match composed of the host and path, for instance, `example.org/path`. Wildcards are expanded to match applicable traffic, query strings are not matched. Use `*` for all traffic to your zone. The max length is `1024`.
            - `response` : Matches HTTP responses before they are returned to the client. If this is defined, then the entire counting of traffic occurs at this stage.
                - `status` : HTTP Status codes, can be one `[403]`, many `[401,403]` or indicate all by not providing this value. This field is not required. The min value is `100`and the max value is `999`.
                - `headers` : Array of response headers to match. If a response does not meet the header criteria, then the request is not counted towards the rate limiting rule. The header matching criteria includes the following properties.
                    - `name` : The name of the response header to match.
                    - `op` : The operator when matching, eq means equals, ne means not equals. Valid values are `eq` and `ne`.
                    - `value` : The value of the header, which is exactly matched.
        - `threshold` : The threshold that triggers the rate limit mitigations, which are combined with a period. For example, the threshold per period. The min value is `2`and the max value is`1000000`.
        - `period` : The time, in seconds, to count matching traffic. If the count exceeds the threshold within this period, the action is performed. The min value is `10` and the max value is `86400`.
        - `action` : The action performed when the threshold of matched traffic within the period defined is exceeded.
            - `mode` : The type of action performed. Valid values are: `simulate`, `ban`, `challenge`, `js_challenge`.
            - `timeout` : The time in seconds, as an integer to perform the mitigation action. The timeout can be the same or greater than the period. This field is valid only when the mode is `simulate` or `ban`. The min value is `10` and the max value is `86400`.
            - `response` : Custom content-type and body to return. This overrides the custom error for the zone. This field is not required. Omission results in the default HTML error page. This field is valid only when mode is `simulate` or `ban`.
                - `content_type` : The content-type of the body, which must be one of the following: `text/plain`, `text/xml`, `application/json`.
                - `body` : The body to return. The content here must conform to the `content_type`. The max length is `10240`.
    - The optional fields are `id`, `disabled`, `description`, `correlate` and `bypass`:
        - `id` : Identifier of the rate limiting rule.
        - `disabled` : Whether this rate limiting rule is currently disabled.
        - `description` : A note that you can use to describe the reason for a rate limiting rule.
        - `correlate` : Whether to enable NAT-based rate limiting.
            - `by` : Valid value is `nat`.
        - `bypass` : Criteria that allow the rate limit to be bypassed. For example, to express that you shouldn’t apply a rate limit to a set of URLs.
            - `name` : Valid value is `url`.
            - `value` : The url to bypass.

Sample JSON data:

```json
{
   "id": "92f17202ed8bd63d69a66b86a49a8f6b",
   "disabled": false,
   "description": "Prevent multiple login failures to mitigate brute force attacks",
   "bypass": [
      {
         "name": "url",
         "value": "api.example.com/*"
      }
   ],
   "threshold": 60,
   "period": 900,
   "correlate": {
      "by": "nat"
   },
   "action": [
      {
         "mode": "simulate",
         "timeout": 86400,
         "response": {
            "content_type": "text/plain",
            "body": "<error>This request has been rate-limited.</error>"
         }
      }
   ],
   "match": {
      "request": {
               "methods": [
                  "GET"
               ],
               "schemes": [
                  "HTTP",
                  "HTTPS"
               ],
               "url": "*.example.org/path*"
      },
      "response": {
         "status": [
               403, 401
         ],
         "headers": [
            {
               "name": "Cf-Cache-Status",
               "op": "eq",
               "value": "HIT"
            }
         ]
      }
   }
}
```
{: codeblock}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

## Updating a rate limiting rule from the CLI
{: #updating-rate-limit-cli}
{: cli}

Run the following command to update a rate limiting rule from the CLI:
```sh
ibmcloud cis ratelimit-rule-update DNS_DOMAIN_ID RATELIMIT_RULE_ID [--url URL] [--description DESCRIPTION] [--threshold NUM] [--period SECONDS] [...]
```
{: pre}

You can also update a rate-limiting rule by providing a JSON file or a JSON string directly:
```sh
ibmcloud cis ratelimit-rule-update DNS_DOMAIN_ID RATELIMIT_RULE_ID  (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

### Command options
{: #command-options-update-cli}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`RATELIMIT_RULE_ID`
:   The ID of rate limiting rule. Required.

`--json`
:   The JSON file or JSON strinthat is used to describe a rate limiting rule.
    - The required fields in JSON data are `match`, `threshold`, `period` and `action` :
        - `match` : Determines which traffic the rate limiting rule counts towards the threshold.
            - `request` : Matches HTTP requests.
                - `methods` :  HTTP Methods, can be a subset `[POST,PUT]` or all `[ALL]`. This field is not required to create a rate limit rule. Valid values are `GET`, `POST`, `PUT`, `DELETE`, `PATCH`, `HEAD`, `ALL`.
                - `schemes` :  HTTP Schemes, can be one `[HTTPS]`, both `[HTTP,HTTPS]` or all `[_ALL_]`. This field is not required.
                - `url` : The URL pattern to match consisted of the host and path, for instance, `example.org/path`. Wildcards are expanded to match applicable traffic, query strings are not matched. Use `*` for all traffic to your zone. The max length is `1024`.
            - `response` : Matches HTTP responses before they are returned to the client. If this field is defined, then the entire counting of traffic occurs at this stage.
                - `status` : HTTP Status codes, can be one `[403]`, many `[401,403]` or indicate all by not providing this value. This field is not required. The min value is `100` and the max value is `999`.
                - `headers` : Array of response headers to match. If a response does not meet the header criteria, then the request is not counted towards the rate limiting rule. An array of header matching criteria includes the following properties.
                    - `name` : The name of the response header to match.
                    - `op` : The operator when matching, eq means equals, ne means not equals. Valid values are `eq` and `ne`.
                    - `value` : The value of the header, which is exactly matched.
        - `threshold` : The threshold that triggers the rate limit mitigations, which are combined with period. For example, the threshold per period. The min value is `2` and the max value is `1000000`.
        - `period` : The time, in seconds, to count matching traffic. If the count exceeds the threshold within this period the action is performed. The min value is `1` and the max value is `3600`.
        - `action` : The action is performed when the threshold of matched traffic within the defined period is exceeded.
            - `mode` : The type of action performed. Valid values are `simulate`, `ban`, `challenge`, `js_challenge`.
            - `timeout` : The time, in seconds, as an integer to perform the mitigation action. Timeout is the same or greater than the period. This field is valid only when mode is `simulate` or `ban`. The min value is `10` and the max value is `86400`.
            - `response` : Custom content-type and body to return. This overrides the custom error for the zone. This field is not required. Omission results in the default HTML error page. This field is valid only when mode is `simulate` or `ban`.
                - `content_type` : The content-type of the body, which must be one of the following: `text/plain`, `text/xml`, `application/json`.
                - `body` : The body to return. The content here must conform to the `content_type`. The max length is `10240`.
    - The optional fields are `disabled`, `description`, `correlate` and `bypass`:
        - `disabled` : Whether this rate limiting rule is currently disabled.
        - `description` : A note that you can use to describe the reason for a rate limiting rule.
        - `correlate` : Whether to enable NAT-based rate limiting.
            - `by` : Valid value is `nat`.
        - `bypass` : Criteria that allow the rate limit to be bypassed. For example, to express that you shouldn’t apply a rate limit to a set of URLs.
            - `name` : Valid value is `url`.
            - `value` : The url to bypass.

Sample JSON data:

```json
{
   "disabled": false,
   "description": "Prevent multiple login failures to mitigate brute force attacks",
   "bypass": [
      {
         "name": "url",
         "value": "api.example.com/*"
      }
   ],
   "threshold": 60,
   "period": 900,
   "correlate": {
      "by": "nat"
   },
   "action": [
      {
         "mode": "simulate",
         "timeout": 86400,
         "response": {
            "content_type": "text/plain",
            "body": "<error>This request has been rate-limited.</error>"
         }
      }
   ],
   "match": {
      "request": {
               "methods": [
                  "GET"
               ],
               "schemes": [
                  "HTTP",
                  "HTTPS"
               ],
               "url": "*.example.org/path*"
      },
      "response": {
         "status": [
               403, 401
         ],
         "headers": [
            {
               "name": "Cf-Cache-Status",
               "op": "eq",
               "value": "HIT"
            }
         ]
      }
   }
}
```
{: codeblock}

`-i, --instance`
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   Specify output format, only `JSON` is supported.

## Deleting a rate limiting rule from the CLI
{: #rate-limite-delete-cli}
{: cli}

Run the following command to delete a rate limiting rule from the CLI:
```sh
ibmcloud cis ratelimit-rule-delete DNS_DOMAIN_ID RATELIMIT_RULE_ID [--instance INSTANCE]
```
{: pre}

### Command options
{: #commands-options-delete-cli}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`RATELIMIT_RULE_ID`
:   The ID of rate limit rule. Required.

`-i, --instance`
:   Instance name or ID. If not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

For more information, see [CLI rate-limiting](/docs/cis?topic=cis-cis-cli#ratelimit).

## Creating a custom rate-limiting rule with Terraform
{: #create-a-custom-rate-limiting-rule-tf}
{: terraform}

To create a rate-limiting ruleset, you must create an entrypoint first, then create the rate-limiting ruleset. To do so, follow these steps:

1. To create an entrypoint ruleset, run the following command:

   ```terraform
   resource "ibm_cis_ruleset_entrypoint_version" "config" {
     cis_id    = data.ibm_cis.cis_instance.id
     domain_id = data.ibm_cis_domain.cis_domain.domain_id
     phase     = "http_ratelimit"

     rulesets {
       description = "Zone rate limit entrypoint"
     }
     lifecycle {
       ignore_changes = [
         rulesets
       ]
     }
   }
   ```
   {: pre}

   Use a `lifecycle` block to prevent Terraform from updating the entrypoint ruleset. Some entrypoint parameters are updated during every `terraform apply`, which can introduce unintended configuration changes. The `lifecycle` block helps you ignore these updates and maintain resource stability.
   {: important}

1. To create a rate-limiting ruleset, run the following command:

   ```terraform
   resource "ibm_cis_ruleset_rule" "config" {
     cis_id     = data.ibm_cis.cis_instance.id
     domain_id  = data.ibm_cis_domain.cis_domain.domain_id
     ruleset_id = "data.ibm_cis_ruleset_entrypoint_versions.ruleset_id"
     rule {
       action      = "block"
       enabled     = true
       description = "Block IPs making over 100 requests/minute to /api/"
       expression  = "(http.request.uri.path matches \"^/api/\")"
       ratelimit {
         characteristics     = ["cf.colo.id", "ip.src"]
         period              = 60
         requests_per_period = 100
         mitigation_timeout  = 300
       }
     }
   }
   ```
   {: codeblock}

The following example shows how to create an entrypoint and rate-limiting rule with Terraform:

```terraform
resource ibm_cis_ruleset_entrypoint_version test {
  cis_id    = ibm_cis.instance.id
  domain_id = data.ibm_cis_domain.cis_domain.domain_id
  phase = "http_ratelimit"
  rulesets {
      description = "Entrypoint ruleset for ratelimit ruleset"
    }
    lifecycle {
      ignore_changes = [
        rulesets
      ]
  }
}

data ibm_cis_ruleset_entrypoint_versions test {
  cis_id    = ibm_cis.instance.id
  domain_id = data.ibm_cis_domain.cis_domain.domain_id
  phase = "http_ratelimit"
   depends_on = [
    ibm_cis_ruleset_entrypoint_version.ratelimit_ep
  ]
}

resource "ibm_cis_ruleset_rule" "ratelimit_rule_1" {
  cis_id    = ibm_cis.instance.id
  domain_id = data.ibm_cis_domain.cis_domain.domain_id
  ruleset_id = data.ibm_cis_ruleset_entrypoint_versions.ratelimit_data.rulesets[0].ruleset_id

    rule {
      action      = "block"
      description = "Block IPs making over 100 requests/minute to /api/"
      enabled     = true
      expression  = "(http.request.uri.path matches \"^/api/\")"

      rate_limit {
      characteristics     = ["cf.colo.id","ip.src"]
      mitigation_timeout  = 300
      period              = 120
      requests_per_period = 100
      }
    }
  }
```
{: codeblock}
