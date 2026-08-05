---

copyright:
  years: 2026
lastupdated: "2026-08-05"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Creating a origin rules
{: #create-origin-rules}

Create a origin rule by adding it to the `http_request_origin` phase ruleset for a zone.

## Before you begin
{: #before-begin-api}

When creating a configuration rule with the API, make sure you:

* Set the rule action to `set_config`.
* Define the parameters in the `action_parameters` field according to the settings you wish to override for matching requests.
* Deploy the rule to the `http_request_origin` phase at the zone level.

## Creatin a configuration rule with the API
{: #procedure-create-config-api-rules}

Complete the following steps to create a orgin rule for a given zone via API:

1. Check whether a ruleset exists for the `http_request_origin` phase by using the [List zone rulesets](/docs/apis/cis#get-zone-rulesets) API.
1. If a ruleset for the `http_request_origin` phase doesn't exist, create one by using the **Create a zone ruleset** as shown in the following example.

   Set the following values in the request body:

   * kind: `zone`
   * phase: `http_request_origin`

   ```sh
   curl -X POST \
    "https://api.cis.cloud.ibm.com/v1/crn:v1:bluemix:public:internet-svcs:global:a/361583ba4e52947c3e111ba9d29702e3:78345201-a3a7-4de3-abe4-7115e6b0e2f1::/zones/2ce4a192bf5978e6b65a09ed2d36d4c2/rulesets" \
    --header "X-Auth-User-Token: Bearer xxxx" \
    --header "Content-Type: application/json" \
    --data '{
   "name": "Zone-level phase entrypoint",
   "kind": "zone",
   "description": "Config settings ruleset",
   "phase": "http_request_origin"
   }'

   {"result": {"description": "Config settings ruleset", "id": "b19bf5e7c3bd40b890a0302390e86e0c", "kind": "zone", "last_updated": "2026-06-13T14:52:37.636034Z", "name": "Zone-level phase entrypoint", "phase": "http_request_origin", "version": "1"}, "success": true, "errors": [], "messages": []}%
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
     "description": "My http_request_origin ruleset to execute managed rulesets",
     "kind": "root",
     "phase": "http_request_origin",
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
   {"result": {"description": "My http_request_origin ruleset to execute managed rulesets", "id": "b19bf5e7c3bd40b890a0302390e86e0c", "kind": "zone", "last_updated": "2026-06-13T15:12:56.987507Z", "name": "Zone-level phase entrypoint", "phase": "http_request_origin", "rules": [{"action": "set_config", "action_parameters": {"request_body_buffering": "none"}, "description": "Disable request buffering for file uploads", "enabled": true, "expression": "starts_with(http.request.uri.path, \"/upload/\")", "id": "f2a88e88081c4a7e9ead5134de0a61c9", "last_updated": "2026-06-13T15:12:56.987507Z", "ref": "f2a88e88081c4a7e9ead5134de0a61c9", "version": "1"}], "version": "2"}, "success": true, "errors": [], "messages": []}%
   ```
   {: pre}
