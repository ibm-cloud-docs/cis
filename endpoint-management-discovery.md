---

copyright:
  years: 2026
lastupdated: "2026-10-19"

keywords: endpoint discovery, API discovery, API gateway discovery, API operations, discovered operations

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Endpoint discovery
{: #endpoint-management-discovery}

{{site.data.keyword.cis_full_notm}} (CIS) automatically discovers your API endpoints by analyzing traffic to your zone. Endpoint discovery helps you map your API attack surface, which is the full set of endpoints that could be targeted.
{: shortdesc}

[Endpoint Management (all plans) and AI Security for Apps](/docs/cis?topic=cis-release-notes#cis-october-1926) and its mitigation features (Enterprise plans only) are available for evaluation and testing. These features are provided at no additional charge during the beta period. To provide feedback or report issues, open a support case in the [IBM Cloud Support Center](/docs/support?topic=support-open-case&interface=ui). For IBM internal users, post in [#ibmcloud-cis](https://ibm.enterprise.slack.com/archives/C8XKQ9FPB).
{: beta}



## How endpoint discovery works
{: #endpoint-management-discovery-how}

{{site.data.keyword.cis_short_notm}} produces a map of API endpoints by grouping similar request paths together through path normalization.

For example, if your zone receives thousands of requests that follow similar patterns, such as:

```text
api.example.com/profile/238
api.example.com/profile/392
```
{: screen}

{{site.data.keyword.cis_short_notm}} normalizes these to a single endpoint:

```text
api.example.com/profile/{var1}
```
{: screen}

Similarly, if multiple subdomains share the same set of endpoints, {{site.data.keyword.cis_short_notm}} consolidates them:

```text
us-api.example.com/api/v1/users/{var1}
de-api.example.com/api/v1/users/{var1}
```
{: screen}

These consolidate to:

```text
{hostVar1}.example.com/api/v1/users/{var1}
```
{: screen}

For an endpoint to appear in discovery results, each request must meet the following conditions:

* The request must return a 2xx response code from the {{site.data.keyword.cis_short_notm}} edge.
* The request must not originate directly from a {{site.data.keyword.cis_short_notm}} edge function. Traffic that is sent through the CIS traffic simulator or other Edge Functions-based test harnesses is not counted toward discovery thresholds.
* The endpoint must receive at least 500 requests within a continuous 10-day period.

## Discovery methods
{: #endpoint-management-discovery-methods}

{{site.data.keyword.cis_short_notm}} uses two discovery methods:

Session identifier-based discovery
:   Discovers API endpoints based on session identifiers in your traffic. If all of your zone's API traffic contains the configured session identifier, results might overlap with machine learning-based discovery.

Machine learning-based discovery
:   Identifies API traffic regardless of whether your API uses a session identifier. This method can discover endpoints that session identifier-based discovery might miss.

## Discovering endpoints in the console
{: #endpoint-management-discovery-ui}
{: ui}

### Viewing discovered endpoints in the console
{: #endpoint-management-discovery-schema-ui}

1. In the {{site.data.keyword.cloud_notm}} console, go to your {{site.data.keyword.cis_short_notm}} instance.
1. Go to **Security** > **Endpoint management**.
1. Select the **Discover endpoints** tab.
1. Filter by **Candidate** to view discovered endpoints that have not yet been promoted.

### Listing discovered operations in the console
{: #endpoint-management-discovery-list-ui}

1. In the {{site.data.keyword.cloud_notm}} console, go to your {{site.data.keyword.cis_short_notm}} instance.
1. Go to **Security** > **Endpoint management**.
1. Select the **Discover endpoints** tab.
1. Use the filter controls to narrow results by status or other criteria.

### Updating a discovered operation state in the console
{: #endpoint-management-discovery-update-ui}

1. In the {{site.data.keyword.cloud_notm}} console, go to your {{site.data.keyword.cis_short_notm}} instance.
1. Go to **Security** > **Endpoint management**.
1. Select the **Discover endpoints** tab.
1. Open the row actions for the endpoint that you want to update.
1. Select **Ignore** to dismiss it or **Review** to requeue it.

### Viewing API gateway schemas in the console
{: #endpoint-management-discovery-schemas-ui}

Saved endpoints and their schemas are visible on the **Manage endpoints** tab under **Security** > **Endpoint management**.

## Discovering endpoints from the CLI
{: #endpoint-management-discovery-cli}
{: cli}

### Retrieving discovered endpoints as an OpenAPI schema from the CLI
{: #endpoint-management-discovery-schema-cli}

To retrieve discovered endpoints as an OpenAPI schema from the CLI, follow these steps:

1. [Set up your CLI environment](/docs/cis?topic=cis-cis-cli#-cli-prereqs).
1. Log in to your account from the CLI. After you enter the password, the system prompts for the account and region that you want to use:

   ```sh
   ibmcloud login --sso
   ```
   {: pre}

1. Run the following command to retrieve the schema:

   ```sh
   ibmcloud cis api-gateway discovery DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
   ```
   {: pre}

#### Command options
{: #endpoint-management-discovery-schema-cli-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

### Listing discovered operations from the CLI
{: #endpoint-management-discovery-list-cli}

To list discovered operations from the CLI, follow these steps:

1. [Set up your CLI environment](/docs/cis?topic=cis-cis-cli#-cli-prereqs).
1. Log in to your account from the CLI. After you enter the password, the system prompts for the account and region that you want to use:

   ```sh
   ibmcloud login --sso
   ```
   {: pre}

1. Run the following command to list discovered operations:

   ```sh
   ibmcloud cis api-gateway discovery-operations DNS_DOMAIN_ID [--diff] [--direction asc|desc] [--endpoint ENDPOINT] [--host HOST] [--method METHOD] [--order FIELD] [--origin ML|SessionIdentifier|LabelDiscovery] [--state review|saved|ignored] [--page PAGE] [--per-page PER_PAGE] [-i, --instance INSTANCE] [--output FORMAT]
   ```
   {: pre}

#### Command options
{: #endpoint-management-discovery-list-cli-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--diff`
:   When set, returns only operations that are not yet saved to endpoint management.

`--direction`
:   Sort direction. Valid values are `asc` and `desc`.

`--endpoint`
:   Filters results to only include endpoints that contain this pattern.

`--host`
:   Filters results to only include the specified hostname. This option is repeatable.

`--method`
:   Filters results to only include the specified HTTP method. This option is repeatable.

`--order`
:   Field to order results by. Valid values are `host`, `method`, `endpoint`, `traffic_stats.requests`, and `traffic_stats.last_updated`.

`--origin`
:   Filters results by discovery engine. Valid values are `ML`, `SessionIdentifier`, and `LabelDiscovery`.

`--state`
:   Filters results by state. Valid values are `review`, `saved`, and `ignored`.

`--page`
:   Page number of paginated results. Minimum value is `1`.

`--per-page`
:   Maximum number of results per page. Minimum value is `1`, maximum is `100`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

### Updating discovered operation states from the CLI
{: #endpoint-management-discovery-update-cli}

To update the state of one or more discovered operations from the CLI, follow these steps. Use this command to dismiss false positives (`ignored`) or requeue them (`review`). To promote an operation to endpoint management, use `operations-create` instead.

1. [Set up your CLI environment](/docs/cis?topic=cis-cis-cli#-cli-prereqs).
1. Log in to your account from the CLI. After you enter the password, the system prompts for the account and region that you want to use:

   ```sh
   ibmcloud login --sso
   ```
   {: pre}

1. Run the following command to update operation states:

   ```sh
   ibmcloud cis api-gateway discovery-operations-update DNS_DOMAIN_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE]
   ```
   {: pre}

#### Command options
{: #endpoint-management-discovery-update-cli-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--json`
:   The JSON file or JSON string that describes the state updates. The format is a map of operation UUID to the new state object.

   - Valid state values are `ignored` and `review`.

   Sample JSON data:

   ```json
   {
     "f174e90a-fafe-4643-bbbc-4a0ed4fc8415": { "state": "ignored" }
   }
   ```
   {: codeblock}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

### Retrieving API gateway schemas from the CLI
{: #endpoint-management-discovery-schemas-cli}

To retrieve OpenAPI schemas for operations that are already saved to endpoint management from the CLI, follow these steps:

1. [Set up your CLI environment](/docs/cis?topic=cis-cis-cli#-cli-prereqs).
1. Log in to your account from the CLI. After you enter the password, the system prompts for the account and region that you want to use:

   ```sh
   ibmcloud login --sso
   ```
   {: pre}

1. Run the following command to retrieve schemas:

   ```sh
   ibmcloud cis api-gateway schemas DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
   ```
   {: pre}

#### Command options
{: #endpoint-management-discovery-schemas-cli-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

## Discovering endpoints with the API
{: #endpoint-management-discovery-api}
{: api}

To call these methods, you must be assigned one or more IAM access roles:

* `internet-svcs.security.read` — Required for all GET operations
* `internet-svcs.security.update` — Required for all PATCH operations

You can check your access by going to **Manage** > **Access (IAM)** > **Users** > **_User name_** > **Access**.
{: tip}

### Retrieving discovered endpoints as an OpenAPI schema with the API
{: #endpoint-management-discovery-schema-api}

To retrieve discovered endpoints as an OpenAPI schema with the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following variables to be used in the API command:

   * `crn`: The full URL-encoded CRN of the service instance.
   * `zone_identifier`: The zone identifier.

1. When all variables are initiated, run the following command to retrieve the schema:

   ```sh
   curl -X GET \
     https://api.cis.cloud.ibm.com/v1/:crn/zones/:zone_identifier/api_gateway/discovery \
     -H 'content-type: application/json' \
     -H 'accept: application/json' \
     -H 'x-auth-user-token: Bearer xxxxxx'
   ```
   {: pre}

   The following response is returned:

   ```json
   {
     "errors": [],
     "messages": [],
     "result": {
       "schemas": [
         {
           "info": {
             "title": "OpenAPI JSON schema for www.example.com",
             "version": "1.0"
           },
           "openapi": "3.0.0",
           "paths": {
             "... Further paths ...": {},
             "/api/v1/users/{var1}": {
               "get": {
                 "parameters": [
                   {
                     "name": "var1",
                     "in": "path",
                     "required": true,
                     "schema": {
                       "type": "string"
                     }
                   }
                 ]
               }
             }
           },
           "servers": [
             {
               "url": "www.example.com"
             }
           ]
         }
       ],
       "timestamp": "2014-01-01T05:20:00.12345Z"
     },
     "success": true
   }
   ```
   {: screen}

### Listing discovered operations with the API
{: #endpoint-management-discovery-list-api}

To list discovered operations with the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following variables to be used in the API command:

   * `crn`: The full URL-encoded CRN of the service instance.
   * `zone_identifier`: The zone identifier.

1. When all variables are initiated, run the following command to list the operations:

   ```sh
   curl -X GET \
     https://api.cis.cloud.ibm.com/v1/:crn/zones/:zone_identifier/api_gateway/discovery/operations \
     -H 'content-type: application/json' \
     -H 'accept: application/json' \
     -H 'x-auth-user-token: Bearer xxxxxx'
   ```
   {: pre}

   The following response is returned:

   ```json
   {
     "result": [
       {
         "id": "f174e90a-fafe-4643-bbbc-4a0ed4fc8415",
         "method": "POST",
         "host": "api.example.com",
         "endpoint": "/v1/messages",
         "state": "review",
         "origin": [
           "ML"
         ],
         "last_updated": "2024-01-01T00:00:00Z"
       }
     ],
     "result_info": {
       "page": 1,
       "per_page": 20,
       "count": 1,
       "total_count": 1
     },
     "success": true,
     "errors": [],
     "messages": []
   }
   ```
   {: screen}

### Updating discovered operation states with the API
{: #endpoint-management-discovery-update-api}

To promote a discovered operation to the saved state, use the `operations-create` endpoint instead. For more information, see the [CIS API reference](https://{DomainName}/apidocs/cis){: external}.
{: note}

To update the state of one or more discovered operations with the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following variables to be used in the API command:

   * `crn`: The full URL-encoded CRN of the service instance.
   * `zone_identifier`: The zone identifier.
   * `operation_uuid`: The UUID of the discovered operation to update.
   * `state`: The new state. Valid values are `ignored` and `review`.

1. When all variables are initiated, run the following command to update the state:

   ```sh
   curl -X PATCH \
     https://api.cis.cloud.ibm.com/v1/:crn/zones/:zone_identifier/api_gateway/discovery/operations \
     -H 'content-type: application/json' \
     -H 'x-auth-user-token: Bearer xxxxxx' \
     -d '{"f174e90a-fafe-4643-bbbc-4a0ed4fc8415": {"state": "ignored"}}'
   ```
   {: pre}

   Replace `f174e90a-fafe-4643-bbbc-4a0ed4fc8415` with the UUID of the discovered operation.

   The following response is returned:

   ```json
   {
     "result": [
       {
         "id": "f174e90a-fafe-4643-bbbc-4a0ed4fc8415",
         "method": "POST",
         "host": "api.example.com",
         "endpoint": "/v1/messages",
         "state": "ignored",
         "origin": [
           "ML"
         ],
         "last_updated": "2024-01-01T00:00:00Z"
       }
     ],
     "success": true,
     "errors": [],
     "messages": []
   }
   ```
   {: screen}

### Retrieving API gateway schemas with the API
{: #endpoint-management-discovery-schemas-api}

To retrieve API gateway schemas with the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following variables to be used in the API command:

   * `crn`: The full URL-encoded CRN of the service instance.
   * `zone_identifier`: The zone identifier.

1. When all variables are initiated, run the following command to retrieve the schemas:

   ```sh
   curl -X GET \
     https://api.cis.cloud.ibm.com/v1/:crn/zones/:zone_identifier/api_gateway/schemas \
     -H 'content-type: application/json' \
     -H 'accept: application/json' \
     -H 'x-auth-user-token: Bearer xxxxxx'
   ```
   {: pre}

   The following response is returned:

   ```json
   {
     "result": {},
     "success": true,
     "errors": [],
     "messages": []
   }
   ```
   {: screen}

## Discovering endpoints with Terraform
{: #endpoint-management-discovery-terraform}
{: terraform}

Before you begin, make sure that you complete the steps to [set up Terraform for {{site.data.keyword.cis_short_notm}}](/docs/cis?topic=cis-terraform-setup-cis).

The examples in this section reference the following data sources for the {{site.data.keyword.cis_short_notm}} instance and domain. Add them to your Terraform configuration, replacing the values with your own.

```terraform
data "ibm_cis" "cis" {
  name = "<cis_instance_name>"
}

data "ibm_cis_domain" "cis_domain" {
  cis_id = data.ibm_cis.cis.id
  domain = "example.com"
}
```
{: codeblock}

### Retrieving discovered endpoints as an OpenAPI schema with Terraform
{: #endpoint-management-discovery-schema-terraform}

To retrieve discovered endpoints as an OpenAPI schema with Terraform, follow these steps:

1. Add the `ibm_cis_api_gateway_discovery` data source to your configuration:

   ```terraform
   data "ibm_cis_api_gateway_discovery" "openapi_doc" {
     cis_id    = data.ibm_cis.cis.id
     domain_id = data.ibm_cis_domain.cis_domain.domain_id
   }

   output "discovery_doc" {
     value = data.ibm_cis_api_gateway_discovery.openapi_doc.result
   }
   ```
   {: codeblock}

1. Run `terraform apply`. The `result` attribute contains the discovered operations rendered as a JSON-encoded OpenAPI schema document.

For more information about the arguments and attributes, see [`ibm_cis_api_gateway_discovery`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_api_gateway_discovery){: external} in the Terraform registry.

### Listing discovered operations with Terraform
{: #endpoint-management-discovery-list-terraform}

To list discovered operations with Terraform, follow these steps:

1. Add the `ibm_cis_api_gateway_discovery_operations` data source to your configuration. The following example lists operations that are in the `review` state:

   ```terraform
   data "ibm_cis_api_gateway_discovery_operations" "discovered" {
     cis_id    = data.ibm_cis.cis.id
     domain_id = data.ibm_cis_domain.cis_domain.domain_id
     state     = "review"
     per_page  = 25
   }

   output "discovered_ops_count" {
     value = length(data.ibm_cis_api_gateway_discovery_operations.discovered.operations)
   }

   output "discovered_operations" {
     value = data.ibm_cis_api_gateway_discovery_operations.discovered.operations
   }
   ```
   {: codeblock}

1. Run `terraform apply`. Each item in the `operations` list includes the `id`, `method`, `host`, `endpoint`, `state`, `origin`, and `last_updated` attributes. The `total_count` attribute contains the total number of matching operations.

You can use the following optional arguments to filter and paginate the results:

`diff`
:   When `true`, returns only operations that are not yet saved to endpoint management.

`state`
:   Filters results by discovery state. Valid values are `review`, `saved`, and `ignored`.

`origin`
:   Filters results by discovery engine source. Valid values are `ML`, `LabelDiscovery`, and `SessionIdentifier`.

`host`, `method`
:   Filters results to only the specified hosts or HTTP methods. Both arguments accept a list of strings.

`endpoint`
:   Filters results to endpoints that contain the specified pattern.

`order`, `direction`
:   Orders results by `endpoint`, `host`, `method`, `traffic_stats.last_updated`, or `traffic_stats.requests`, in `asc` or `desc` direction.

`page`, `per_page`
:   The page number and the maximum number of results per page.

For more information about the arguments and attributes, see [`ibm_cis_api_gateway_discovery_operations`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_api_gateway_discovery_operations){: external} in the Terraform registry.

### Updating discovered operation states with Terraform
{: #endpoint-management-discovery-update-terraform}

To promote a discovered operation to the saved state, create the operation by using the `ibm_cis_api_gateway_operation` resource. For more information, see [Creating and labeling endpoint operations](/docs/cis?topic=cis-endpoint-management-creating).
{: note}

To update the state of one or more discovered operations with Terraform, follow these steps:

1. Get the UUIDs of the discovered operations by listing them with the `ibm_cis_api_gateway_discovery_operations` data source. For more information, see [Listing discovered operations with Terraform](#endpoint-management-discovery-list-terraform).
1. Add the `ibm_cis_api_gateway_discovery_operations` resource to your configuration. The `operation_states` argument is a map of discovered operation UUIDs to their desired state:

   ```terraform
   resource "ibm_cis_api_gateway_discovery_operations" "update_states" {
     cis_id    = data.ibm_cis.cis.id
     domain_id = data.ibm_cis_domain.cis_domain.domain_id

     operation_states = {
       "f174e90a-fafe-4643-bbbc-4a0ed4fc8415" = "ignored"
       "a1b2c3d4-0000-1111-2222-333344445555" = "review"
     }
   }

   output "updated_operations" {
     value = ibm_cis_api_gateway_discovery_operations.update_states.result
   }
   ```
   {: codeblock}

1. Run `terraform apply`. The `result` attribute lists the updated operations that the API returns.

To import an existing configuration into Terraform state, run the following command, where `<domain_id>` is the zone ID and `<crn>` is the CRN of the service instance:

```sh
terraform import ibm_cis_api_gateway_discovery_operations.update_states <domain_id>:<crn>
```
{: pre}

For more information about the arguments and attributes, see [`ibm_cis_api_gateway_discovery_operations`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_api_gateway_discovery_operations){: external} in the Terraform registry.

### Retrieving API gateway schemas with Terraform
{: #endpoint-management-discovery-schemas-terraform}

To retrieve API gateway schemas with Terraform, follow these steps:

1. Add the `ibm_cis_api_gateway_schemas` data source to your configuration to retrieve the OpenAPI schemas for operations already saved to endpoint management:

   ```terraform
   data "ibm_cis_api_gateway_schemas" "schemas" {
     cis_id    = data.ibm_cis.cis.id
     domain_id = data.ibm_cis_domain.cis_domain.domain_id
   }

   output "api_gateway_schemas" {
     value = data.ibm_cis_api_gateway_schemas.schemas.schemas
   }
   ```
   {: codeblock}

1. Run `terraform apply`. The `schemas` attribute contains the API gateway schemas rendered as a JSON-encoded OpenAPI schema document.

For more information about the arguments and attributes, see [`ibm_cis_api_gateway_schemas`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_api_gateway_schemas){: external} in the Terraform registry.

### Example: Reviewing discovered endpoints
{: #endpoint-management-discovery-e2e-terraform}

The following example reads the OpenAPI discovery document, lists operations that are in review, dismisses a discovered operation by setting its state to `ignored`, and reads saved endpoint schemas:

```terraform
data "ibm_cis_api_gateway_discovery" "openapi_doc" {
  cis_id    = data.ibm_cis.cis.id
  domain_id = data.ibm_cis_domain.cis_domain.domain_id
}

data "ibm_cis_api_gateway_discovery_operations" "discovered" {
  cis_id    = data.ibm_cis.cis.id
  domain_id = data.ibm_cis_domain.cis_domain.domain_id
  state     = "review"
}

resource "ibm_cis_api_gateway_discovery_operations" "dismiss" {
  cis_id    = data.ibm_cis.cis.id
  domain_id = data.ibm_cis_domain.cis_domain.domain_id

  operation_states = {
    "<discovered_operation_uuid>" = "ignored"
  }
}

data "ibm_cis_api_gateway_schemas" "schemas" {
  cis_id    = data.ibm_cis.cis.id
  domain_id = data.ibm_cis_domain.cis_domain.domain_id
}

output "discovered_ops_count" {
  value = length(data.ibm_cis_api_gateway_discovery_operations.discovered.operations)
}
```
{: codeblock}

When no operations require updates or no discovered operations exist yet, set `operation_states = {}` to avoid errors during `terraform plan` or `terraform apply`.
{: tip}

## Related resources
{: #endpoint-management-discovery-related}

- [About endpoint management](/docs/cis?topic=cis-endpoint-management-overview)
- [Creating and labeling endpoint operations](/docs/cis?topic=cis-endpoint-management-creating)
- [Labeling endpoints](/docs/cis?topic=cis-endpoint-management-labeling)
- [About AI Security for Apps](/docs/cis?topic=cis-ai-security-overview)
