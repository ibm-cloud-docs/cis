---

copyright:
  years: 2018, 2025
lastupdated: "2025-09-09"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Configuring rate limiting
{: #cis-rate-limiting}

The _previous_ version of rate-limiting rules is now deprecated. The rate-limiting rules interface for the previous version will remain available until 30 July 2025. After this date, any active rules from the previous version will no longer function.
{: deprecated}

Rate limiting (Enterprise plan only) protects against denial-of-service attacks, brute-force login attempts, and other types of abusive behavior targeting the application layer.
{: shortdesc}

Select the type of rate-limiting rule, either a **Custom rule** or **Protect login**.

## Creating a custom rate-limiting rule in the console
{: #create-a-custom-rate-limiting-rule-ui}
{: ui}

Enter a rule name that helps you remember what the rule does. This field is an optional field.

In the **Traffic matching criteria** section, enter the following information.

1. Select the criteria type.
1. Enter the URL that you are rate limiting.
1. Select the number of requests to allow before triggering rate limiting.
1. Select the time period (in seconds) over which the requests can occur before triggering rate limiting.

    The range is from 10 to 86,400 seconds.
    {: note}

The **Advanced Criteria** option allows you to specify which HTTP methods, header responses, and origin response codes to further restrict the matching criteria.

Select a value form the **Method** list menu (ANY is the default).

Update the **HTTP response header**. You can also **Add response header** to include headers returned by your origin web server.

If you have more than one header under the **HTTP response header**, an _AND_ Boolean logic applies. To exclude a header from being matched, use the _Not Equal_ option. Also, each header must be an exact match. However, case sensitivity doesn't apply.
{: note}

Under **Origin response code**, type the valid numerical value of each HTTP response code to match. To include two or more response codes, separate each value with a comma. For example, you can enter `401, 403` if you only want those two error codes to count.

## Configuring the response
{: #rate-limiting-configure-response}

Select from the actions listed, and specify the timeout period. In this case, the timeout refers to the ban period that the action takes place. A 60-second timeout means that the action is applied for 60 seconds.

|Action| Description|
|------|------------|
|Block | Issues a 429 error when the threshold is exceeded|
|Challenge | User must pass a Google re-Captcha Challenge before proceeding. If successful, the request is accepted. Otherwise, the request gets blocked.|
|JS Challenge | The user must pass a JavaScript Challenge before proceeding. If successful, the request is accepted. Otherwise, the request gets blocked.
|Simulate| You can use this option to test your rule before applying any of the other options in your live environment.
{: caption="Actions for rate limiting" caption-side="bottom"}

In the **Advanced response** section, specify the response type when a rule's threshold is exceeded.

### Verifying the rate-limiting rules and response consistency by using HTTP status
{: #verify-rate-limiting-response}

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

## Bypassing URLs
{: #rate-limiting-bypass}

Bypass helps you to create the equivalent of an allowlist or exception for a set of URLs. No actions trigger for those URLs, even if the rate-limiting rule is matched.

## Login protection
{: #rate-limiting-protect-login}

Protect login is a predefined rate-limiting rule designed to prevent brute-force attacks on your login endpoint. Clients (by IP address) that attempt to log in more than 5 times within 5 minutes
are blocked from accessing the login URL for 15 minutes.

To configure this rule:

1. Enter a name for the rule.
1. Specify the login URL path (for example, `/login`, `/admin/login`).
 
CIS automatically enforces the rate limits to protect your login page.

## Getting the rate-limiting rule entry point for the API
{: #get-ratelimit-rule-entry-point-api}
{: api}

All rate-limiting rule API operations require a `RULESET_ID` of the entry point ruleset for the rate-limiting rules phase. This entry point ruleset might exist or needs to be created if it does not exist.

Follow these steps to get the rate-limiting rule entry point ruleset:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded Cloud Resource Name (CRN) of the service instance.

   `ZONE_ID`: The domain ID.

1. When all variables are initiated, get the entry point ruleset:

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
     "name": "Zone-level phase entry point",
     "kind": "zone",
     "description": "Rate-limting rule entry point ruleset.",
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

## Creating a custom rate-limiting rule with Terraform
{: #create-a-custom-rate-limiting-rule-tf}
{: terraform}

The following example shows how to create an entry point and rate-limiting rule with Terraform:

```sh
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
