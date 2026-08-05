---

copyright:
  years: 2026
lastupdated: "2026-08-05"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Creating a configuration rules
{: #create-config-rules}

Create a configuration rule by adding it to the `http_config_settings` phase ruleset for a zone.

## Before you begin
{: #before-begin-api}

When creating a configuration rule via API, make sure you:

* Set the rule action to `set_config`.
* Define the parameters in the `action_parameters` field according to the settings you wish to override for matching requests.
* Deploy the rule to the `http_config_settings` phase at the zone level.

## Creatin a configuration rule via API
{: #procedure-create-config-api-rules}

Complete the following steps to create a configuration rule for a given zone via API:

1. Check whether a ruleset exists for the `http_config_settings` phase by using the [List zone rulesets](/docs/apis/cis#get-zone-rulesets) API.
1. If a ruleset for the `http_config_settings` phase doesn't exist, create one by using the Create a zone ruleset API as shown in the following example.

   Set the following values in the request body:

   * kind: `zone`
   * phase: `http_config_settings`

   ```sh
   curl -X POST \
    "https://api.cis.cloud.ibm.com/v1/crn:v1:bluemix:public:internet-svcs:global:a/361583ba4e52947c3e111ba9d29702e3:78345201-a3a7-4de3-abe4-7115e6b0e2f1::/zones/2ce4a192bf5978e6b65a09ed2d36d4c2/rulesets" \
    --header "X-Auth-User-Token: Bearer xxxx" \
    --header "Content-Type: application/json" \
    --data '{
   "name": "Zone-level phase entrypoint",
   "kind": "zone",
   "description": "Config settings ruleset",
   "phase": "http_config_settings"
   }'

   {"result": {"description": "Config settings ruleset", "id": "b19bf5e7c3bd40b890a0302390e86e0c", "kind": "zone", "last_updated": "2026-06-13T14:52:37.636034Z", "name": "Zone-level phase entrypoint", "phase": "http_config_settings", "version": "1"}, "success": true, "errors": [], "messages": []}%
   ```
   {: pre}

1. Add a configuration rule to the ruleset by using the [Update a zone ruleset](/docs/apis/cis#update-zone-ruleset) API. Alternatively, include the rule in the Create a zone ruleset request mentioned in the previous step.
   ```sh
   curl -X PUT \
   "https://api.cis.cloud.ibm.com/v1/crn:v1:bluemix:public:internet-svcs:global:a/361583ba4e52947c3e111ba9d29702e3:78345201-a3a7-4de3-abe4-7115e6b0e2f1::/zones/2ce4a192bf5978e6b65a09ed2d36d4c2/rulesets/b19bf5e7c3bd40b890a0302390e86e0c" \
   "Content-Type: application/json" \
   -H "Accept: application/json" \
   -H "X-Auth-User-Token: Bearer xxxxx" \
   -d '{
     "description": "My http_config_settings ruleset to execute managed rulesets",
     "kind": "root",
     "phase": "http_config_settings",
     "rules": [
       {
         "action": "set_config",
          "expression": "starts_with(http.request.uri.path, \"/upload/\")",
          "description": "Disable request buffering for file uploads",
         "action_parameters": {
           "request_body_buffering": "none"
         }
       }
     ]
   }'
   {"result": {"description": "My http_config_settings ruleset to execute managed rulesets", "id": "b19bf5e7c3bd40b890a0302390e86e0c", "kind": "zone", "last_updated": "2026-06-13T15:12:56.987507Z", "name": "Zone-level phase entrypoint", "phase": "http_config_settings", "rules": [{"action": "set_config", "action_parameters": {"request_body_buffering": "none"}, "description": "Disable request buffering for file uploads", "enabled": true, "expression": "starts_with(http.request.uri.path, \"/upload/\")", "id": "f2a88e88081c4a7e9ead5134de0a61c9", "last_updated": "2026-06-13T15:12:56.987507Z", "ref": "f2a88e88081c4a7e9ead5134de0a61c9", "version": "1"}], "version": "2"}, "success": true, "errors": [], "messages": []}%
   ```
   {: pre}

## Configuration rule examples
{: #config-rule-examples}

The following examples show how to use configuration rules to control request and response body buffering for incoming traffic.

### Adding a rule that disables request body buffering for file uploads
{: #add-rule-disable-request-body}

Use this rule to stream file upload requests directly to the origin server instead of buffering the request body.
```sh
curl -X PUT \
"https://api.cis.cloud.ibm.com/v1/{crn}/zones/{zone_id}/rulesets/{ruleset_id}" \
-H "Content-Type: application/json" \
-H "Accept: application/json" \
-H "X-Auth-User-Token: Bearer {IAM_TOKEN}" \
-d '{
  "phase": "http_config_settings",
  "rules": [
    {
      "action": "set_config",
      "expression": "starts_with(http.request.uri.path, \"/upload/\")",
      "description": "Disable request buffering for file uploads",
      "action_parameters": {
        "request_body_buffering": "none"
      }
    }
  ]
}'
```
{: pre}

This rule applies only to requests whose URL path starts with `/upload/`.
{: note}

### Adding a rule that disables request body buffering for a specific hostname
{: #add-rule-request-for-spec-hostname}

Use this rule to disable request body buffering only for requests sent to a specific hostname.
```sh
curl -X PUT \
  "https://api.cis.cloud.ibm.com/v1/{crn}/zones/{zone_id}/rulesets/{ruleset_id}" \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -H "X-Auth-User-Token: Bearer {IAM_TOKEN}" \
  -d '{
    "phase": "http_config_settings",
    "rules": [
      {
        "action": "set_config",
        "expression": "http.host eq \"uploads.example.com\"",
        "description": "Unbuffered uploads for specific hostname",
        "action_parameters": {
          "request_body_buffering": "none"
        }
      }
    ]
  }'
```
{: pre}

Only requests to `uploads.example.com` use unbuffered request handling.
{: note}

### Adding a rule that enables full request body buffering for all requests
{: #add-rule-enable-full-request-buffer}

Use this rule to buffer the entire request body before forwarding requests to the origin server.
```sh
curl -X PUT \
  "https://api.cis.cloud.ibm.com/v1/{crn}/zones/{zone_id}/rulesets/{ruleset_id}" \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -H "X-Auth-User-Token: Bearer {IAM_TOKEN}" \
  -d '{
    "phase": "http_config_settings",
    "rules": [
      {
        "action": "set_config",
        "expression": "true",
        "description": "Buffer entire request body",
        "action_parameters": {
          "request_body_buffering": "full"
        }
      }
    ]
  }'
```
{: pre}

Because the rule expression is `true`, the configuration applies to all incoming requests.
{: note}

### Adding a rule that disables request and response body buffering for a specific hostname
{: #add-rule-disable-request-response}

Use this rule to stream both request and response bodies for requests sent to a specific hostname.
```sh
{
  "result": {
    "id": "b19bf5e7c3bd40b890a0302390e86e0c",
    "phase": "http_config_settings",
    "rules": [
      {
        "action": "set_config",
        "action_parameters": {
          "request_body_buffering": "none"
        },
        "description": "Disable request buffering for file uploads",
        "enabled": true,
        "expression": "starts_with(http.request.uri.path, \"/upload/\")",
        "id": "f2a88e88081c4a7e9ead5134de0a61c9"
      }
    ]
  },
  "success": true
}
```
{: pre}

Only requests to `uploads.example.com` are streamed directly between the customer and the origin server without request or response body buffering.
{: note}
