---

copyright:
  years: 2026
lastupdated: "2026-10-19"

keywords: endpoint management, create operation, API gateway operations, cf-llm label, label endpoints

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Creating and labeling endpoint operations
{: #endpoint-management-creating}

Save API endpoints to {{site.data.keyword.cis_full_notm}} (CIS) endpoint management and apply labels to control AI Security for Apps scanning. Applying the `cf-llm` managed label to a saved operation is the final step that enables AI Security for Apps to inspect traffic for prompt injection, personally identifiable information (PII), and unsafe topics.
{: shortdesc}

[Endpoint Management (all plans) and AI Security for Apps](/docs/cis?topic=cis-release-notes#cis-october-1926) and its mitigation features (Enterprise plans only) are available for evaluation and testing. These features are provided at no additional charge during the beta period. To provide feedback or report issues, open a support case in the [IBM Cloud Support Center](/docs/support?topic=support-open-case&interface=ui). For IBM internal users, post in [#ibmcloud-cis](https://ibm.enterprise.slack.com/archives/C8XKQ9FPB).
{: beta}

Before you create and label operations, you must enable AI Security for Apps on your zone. For more information, see [Managing AI Security for Apps settings](/docs/cis?topic=cis-ai-security-settings).
{: important}

## Creating and labeling endpoint operations in the console
{: #endpoint-management-creating-ui}
{: ui}

### Creating operations in the console
{: #endpoint-management-creating-bulk-ui}

1. In the {{site.data.keyword.cloud_notm}} console, go to your {{site.data.keyword.cis_short_notm}} instance.
1. Go to **Security** > **Endpoint management**.
1. On the **Manage endpoints** tab, select **Add endpoints**.
1. In the **Add endpoints** panel, select the **Method**, and enter the **Hostname** and **Path** for the endpoint. To add more endpoints, select **Add**.
1. Select **Save**. **Save** is enabled only after all rows are valid.

### Applying the cf-llm label in the console
{: #endpoint-management-creating-labels-ui}

Before applying the `cf-llm` label, AI Security for Apps must be enabled on your zone. For more information, see [Managing AI Security for Apps settings](/docs/cis?topic=cis-ai-security-settings).
{: important}

1. In the {{site.data.keyword.cloud_notm}} console, go to your {{site.data.keyword.cis_short_notm}} instance.
1. Go to **Security** > **Endpoint management**.
1. On the **Manage endpoints** tab, find the endpoint that you want to protect.
1. In the **Action** column, select **Protect**.

{{site.data.keyword.cis_short_notm}} applies the `cf-llm` managed label to the endpoint. The protection status changes from **Pending** to **Protected**.

## Creating and labeling endpoint operations from the CLI
{: #endpoint-management-creating-cli}
{: cli}

### Creating operations in bulk from the CLI
{: #endpoint-management-creating-bulk-cli}

To create API gateway operations in bulk from the CLI, follow these steps:

1. [Set up your CLI environment](/docs/cis?topic=cis-cis-cli#-cli-prereqs).
1. Log in to your account from the CLI. After you enter the password, the system prompts for the account and region that you want to use:

   ```sh
   ibmcloud login --sso
   ```
   {: pre}

1. Run the following command to create operations in bulk (1–100 at a time):

   ```sh
   ibmcloud cis api-gateway operations-create DNS_DOMAIN_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE]
   ```
   {: pre}

#### Command options
{: #endpoint-management-creating-bulk-cli-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--json`
:   The JSON file or JSON string that describes the operations to create. The format is an array of operation objects.

   - The required fields in each operation object are `method`, `host`, and `endpoint`:
      - `method`: The HTTP method. Valid values are `GET`, `POST`, `PUT`, `PATCH`, `DELETE`, `HEAD`, and `OPTIONS`.
      - `host`: The RFC 3986-compliant hostname. Minimum length is 1, maximum is 253.
      - `endpoint`: The path pattern. Must start with `/`.

   Sample JSON data:

   ```json
   [
     {
       "method": "POST",
       "host": "api.example.com",
       "endpoint": "/v1/messages"
     }
   ]
   ```
   {: codeblock}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

### Creating a single operation from the CLI
{: #endpoint-management-creating-single-cli}

To create a single API gateway operation from the CLI, follow these steps:

1. [Set up your CLI environment](/docs/cis?topic=cis-cis-cli#-cli-prereqs).
1. Log in to your account from the CLI. After you enter the password, the system prompts for the account and region that you want to use:

   ```sh
   ibmcloud login --sso
   ```
   {: pre}

1. Run the following command to create a single operation:

   ```sh
   ibmcloud cis api-gateway operation-create DNS_DOMAIN_ID (--method METHOD --host HOST --endpoint ENDPOINT) [-i, --instance INSTANCE]
   ```
   {: pre}

   You can also create an operation by providing a JSON file or a JSON string directly:

   ```sh
   ibmcloud cis api-gateway operation-create DNS_DOMAIN_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE]
   ```
   {: pre}

#### Command options
{: #endpoint-management-creating-single-cli-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--method`
:   The HTTP method. Valid values are `GET`, `POST`, `PUT`, `PATCH`, `DELETE`, `HEAD`, and `OPTIONS`. Required unless `--json` is used.

`--host`
:   The RFC 3986-compliant hostname. Minimum length is 1, maximum is 253. Required unless `--json` is used.

`--endpoint`
:   The path pattern. Must start with `/`. Required unless `--json` is used.

`--json`
:   The JSON file or JSON string that describes the operation to create. The required fields are `method`, `host`, and `endpoint`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

### Attaching labels to a single operation from the CLI
{: #endpoint-management-attaching-labels-single-cli}

To attach labels to a single saved operation from the CLI, follow these steps:

1. [Set up your CLI environment](/docs/cis?topic=cis-cis-cli#-cli-prereqs).
1. Log in to your account from the CLI. After you enter the password, the system prompts for the account and region that you want to use:

   ```sh
   ibmcloud login --sso
   ```
   {: pre}

1. Run the following command to attach labels:

   ```sh
   ibmcloud cis api-gateway operation-labels-create DNS_DOMAIN_ID OPERATION_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE]
   ```
   {: pre}

#### Command options
{: #endpoint-management-attaching-labels-single-cli-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`OPERATION_ID`
:   The UUID of the API gateway operation. Required.

`--json`
:   The JSON file or JSON string that specifies labels to attach. The format is a map of label type to array of label strings.

   Sample JSON data:

   ```json
   {
     "managed": ["cf-llm"],
     "user": ["my-label"]
   }
   ```
   {: codeblock}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

### Replacing labels on a single operation from the CLI
{: #endpoint-management-replacing-labels-single-cli}

To replace all labels on a single saved operation from the CLI, follow these steps:

1. [Set up your CLI environment](/docs/cis?topic=cis-cis-cli#-cli-prereqs).
1. Log in to your account from the CLI. After you enter the password, the system prompts for the account and region that you want to use:

   ```sh
   ibmcloud login --sso
   ```
   {: pre}

1. Run the following command to replace labels:

   ```sh
   ibmcloud cis api-gateway operation-labels-replace DNS_DOMAIN_ID OPERATION_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE]
   ```
   {: pre}

#### Command options
{: #endpoint-management-replacing-labels-single-cli-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`OPERATION_ID`
:   The UUID of the API gateway operation. Required.

`--json`
:   The JSON file or JSON string that specifies the replacement labels. Pass an empty array for a label type to clear those labels.

   Sample JSON data:

   ```json
   {
     "managed": ["cf-llm"],
     "user": []
   }
   ```
   {: codeblock}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

### Removing labels from a single operation from the CLI
{: #endpoint-management-removing-labels-single-cli}

To remove labels from a single saved operation from the CLI, follow these steps:

1. [Set up your CLI environment](/docs/cis?topic=cis-cis-cli#-cli-prereqs).
1. Log in to your account from the CLI. After you enter the password, the system prompts for the account and region that you want to use:

   ```sh
   ibmcloud login --sso
   ```
   {: pre}

1. Run the following command to remove labels:

   ```sh
   ibmcloud cis api-gateway operation-labels-delete DNS_DOMAIN_ID OPERATION_ID [(--json @JSON_FILE | JSON_STRING)] [-f, --force] [-i, --instance INSTANCE]
   ```
   {: pre}

#### Command options
{: #endpoint-management-removing-labels-single-cli-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`OPERATION_ID`
:   The UUID of the API gateway operation. Required.

`--json`
:   Optional. The JSON file or JSON string that specifies which labels to remove. Omit to remove all labels from the operation.

   Sample JSON data:

   ```json
   {
     "managed": ["cf-llm"]
   }
   ```
   {: codeblock}

`-f, --force`
:   Attempt to remove labels from the operation without prompting for confirmation.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

### Adding or removing labels on operations in bulk from the CLI
{: #endpoint-management-add-remove-labels-bulk-cli}

Before applying the `cf-llm` label, AI Security for Apps must be enabled on your zone. For more information, see [Managing AI Security for Apps settings](/docs/cis?topic=cis-ai-security-settings).
{: important}

To apply the `cf-llm` label to one or more saved operations from the CLI, follow these steps:

1. [Set up your CLI environment](/docs/cis?topic=cis-cis-cli#-cli-prereqs).
1. Log in to your account from the CLI. After you enter the password, the system prompts for the account and region that you want to use:

   ```sh
   ibmcloud login --sso
   ```
   {: pre}

1. Run the following command to apply labels:

   ```sh
   ibmcloud cis api-gateway operations-labels-update DNS_DOMAIN_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE]
   ```
   {: pre}

#### Command options
{: #endpoint-management-add-remove-labels-bulk-cli-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--json`
:   The JSON file or JSON string that describes the label update. The required field is `selector.include.operation_ids`.

   - The required fields in JSON data are under `selector`:
      - `selector.include.operation_ids`: Array of operation UUIDs to label. Minimum one item required.
   - The optional fields are `managed` and `user`:
      - `managed.labels`: Managed label strings such as `cf-llm`.
      - `user.labels`: User-defined label strings.

   Sample JSON data:

   ```json
   {
     "selector": {
       "include": {
         "operation_ids": ["f174e90a-fafe-4643-bbbc-4a0ed4fc8415"]
       }
     },
     "managed": {
       "labels": ["cf-llm"]
     }
   }
   ```
   {: codeblock}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

### Replacing labels on operations in bulk from the CLI
{: #endpoint-management-replacing-labels-bulk-cli}

To replace labels on one or more saved operations in bulk from the CLI, follow these steps:

1. [Set up your CLI environment](/docs/cis?topic=cis-cis-cli#-cli-prereqs).
1. Log in to your account from the CLI. After you enter the password, the system prompts for the account and region that you want to use:

   ```sh
   ibmcloud login --sso
   ```
   {: pre}

1. Run the following command to replace labels in bulk:

   ```sh
   ibmcloud cis api-gateway operations-labels-replace DNS_DOMAIN_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE]
   ```
   {: pre}

#### Command options
{: #endpoint-management-replacing-labels-bulk-cli-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--json`
:   The JSON file or JSON string that describes the label replacement. The required field is `selector.include.operation_ids`.

   - The required fields in JSON data are under `selector`:
      - `selector.include.operation_ids`: Array of operation UUIDs to target. Minimum one item required.
   - The optional fields are `managed` and `user`:
      - `managed.labels`: Replacement managed label strings.
      - `user.labels`: Replacement user-defined label strings.

   Sample JSON data:

   ```json
   {
     "managed": { "labels": ["cf-llm"] },
     "user": { "labels": [] },
     "selector": {
       "include": {
         "operation_ids": ["f174e90a-fafe-4643-bbbc-4a0ed4fc8415"]
       }
     }
   }
   ```
   {: codeblock}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

### Removing labels from operations in bulk from the CLI
{: #endpoint-management-removing-labels-bulk-cli}

To remove labels from one or more saved operations in bulk from the CLI, follow these steps:

1. [Set up your CLI environment](/docs/cis?topic=cis-cis-cli#-cli-prereqs).
1. Log in to your account from the CLI. After you enter the password, the system prompts for the account and region that you want to use:

   ```sh
   ibmcloud login --sso
   ```
   {: pre}

1. Run the following command to remove labels in bulk:

   ```sh
   ibmcloud cis api-gateway operations-labels-delete-all DNS_DOMAIN_ID [(--json @JSON_FILE | JSON_STRING)] [-f, --force] [-i, --instance INSTANCE]
   ```
   {: pre}

#### Command options
{: #endpoint-management-removing-labels-bulk-cli-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--json`
:   Optional. The JSON file or JSON string that specifies which operations and labels to target. Omit to remove all labels from all operations.

   Sample JSON data:

   ```json
   {
     "managed": { "labels": ["cf-llm"] },
     "selector": {
       "include": {
         "operation_ids": ["f174e90a-fafe-4643-bbbc-4a0ed4fc8415"]
       }
     }
   }
   ```
   {: codeblock}

`-f, --force`
:   Attempt to remove all labels from operations without prompting for confirmation.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

## Creating and labeling endpoint operations with the API
{: #endpoint-management-creating-api}
{: api}

To call these methods, you must be assigned one or more IAM access roles:

* `internet-svcs.security.read` — Required for all GET operations
* `internet-svcs.security.update` — Required for all POST and PATCH operations

You can check your access by going to **Manage** > **Access (IAM)** > **Users** > **_User name_** > **Access**.
{: tip}

{{site.data.keyword.cis_short_notm}} uses coarse IAM actions for authorization and fine-grained Activity Tracker (AT) events for auditing. For example, the IAM action `internet-svcs.security.update` governs access to the bulk operations endpoint, while the AT event `internet-svcs.api_gateway_operations.create` records that specific action in the audit log. For a full mapping of IAM actions to AT events for every CIS operation, see [IAM and Activity Tracker actions by API](/docs/cis?topic=cis-at_iam_CIS).
{: note}

### Creating operations in bulk with the API
{: #endpoint-management-creating-bulk-api}

To create API gateway operations in bulk with the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following variables to be used in the API command:

   * `crn`: The full URL-encoded CRN of the service instance.
   * `zone_identifier`: The zone identifier.

1. When all variables are initiated, run the following command to create the operations:

   ```sh
   curl -X POST \
     https://api.cis.cloud.ibm.com/v1/:crn/zones/:zone_identifier/api_gateway/operations \
     -H 'content-type: application/json' \
     -H 'x-auth-user-token: Bearer xxxxxx' \
     -d '[{"method": "POST", "host": "api.example.com", "endpoint": "/v1/messages"}]'
   ```
   {: pre}

   The following response is returned:

   ```json
   {
     "result": [
       {
         "operation_id": "f174e90a-fafe-4643-bbbc-4a0ed4fc8415",
         "method": "POST",
         "host": "api.example.com",
         "endpoint": "/v1/messages"
       }
     ],
     "success": true,
     "errors": [],
     "messages": []
   }
   ```
   {: screen}

Save the `operation_id` values. You need them to apply labels in the next step.

### Creating a single operation with the API
{: #endpoint-management-creating-single-api}

To create a single API gateway operation with the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following variables to be used in the API command:

   * `crn`: The full URL-encoded CRN of the service instance.
   * `zone_identifier`: The zone identifier.
   * `method`: The HTTP method. Valid values are `GET`, `POST`, `PUT`, `PATCH`, `DELETE`, `HEAD`, and `OPTIONS`.
   * `host`: The RFC 3986-compliant hostname.
   * `endpoint`: The path pattern. Must start with `/`.

1. When all variables are initiated, run the following command to create the operation:

   ```sh
   curl -X POST \
     https://api.cis.cloud.ibm.com/v1/:crn/zones/:zone_identifier/api_gateway/operations/item \
     -H 'content-type: application/json' \
     -H 'x-auth-user-token: Bearer xxxxxx' \
     -d '{"method": "POST", "host": "api.example.com", "endpoint": "/v1/messages"}'
   ```
   {: pre}

   The following response is returned:

   ```json
   {
     "result": {
       "operation_id": "f174e90a-fafe-4643-bbbc-4a0ed4fc8415",
       "method": "POST",
       "host": "api.example.com",
       "endpoint": "/v1/messages"
     },
     "success": true,
     "errors": [],
     "messages": []
   }
   ```
   {: screen}

### Applying the cf-llm label with the API
{: #endpoint-management-creating-labels-api}

Before applying the `cf-llm` label, AI Security for Apps must be enabled on your zone. For more information, see [Managing AI Security for Apps settings](/docs/cis?topic=cis-ai-security-settings).
{: important}

To apply the `cf-llm` label to one or more saved operations with the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following variables to be used in the API command:

   * `crn`: The full URL-encoded CRN of the service instance.
   * `zone_identifier`: The zone identifier.
   * `operation_ids`: An array of operation UUIDs to label.

1. When all variables are initiated, run the following command to apply the label:

   ```sh
   curl -X POST \
     https://api.cis.cloud.ibm.com/v1/:crn/zones/:zone_identifier/api_gateway/operations/labels \
     -H 'content-type: application/json' \
     -H 'x-auth-user-token: Bearer xxxxxx' \
     -d '{"managed": {"labels": ["cf-llm"]}, "selector": {"include": {"operation_ids": ["f174e90a-fafe-4643-bbbc-4a0ed4fc8415"]}}}'
   ```
   {: pre}

   The following response is returned:

   ```json
   {
     "result": [
       {
         "operation_id": "f174e90a-fafe-4643-bbbc-4a0ed4fc8415",
         "labels": [
           "cf-llm"
         ]
       }
     ],
     "success": true,
     "errors": [],
     "messages": []
   }
   ```
   {: screen}

## Creating and labeling endpoint operations with Terraform
{: #endpoint-management-creating-terraform}
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

### Creating operations in bulk with Terraform
{: #endpoint-management-creating-bulk-terraform}

To create multiple API gateway operations in a single resource with Terraform, follow these steps:

1. Add the `ibm_cis_api_gateway_operations` resource to your configuration. Define one `operations` block for each operation:

   ```terraform
   resource "ibm_cis_api_gateway_operations" "bulk_ops" {
     cis_id    = data.ibm_cis.cis.id
     domain_id = data.ibm_cis_domain.cis_domain.domain_id

     operations {
       method   = "GET"
       host     = "api.example.com"
       endpoint = "/api/v1/models"
     }

     operations {
       method   = "DELETE"
       host     = "api.example.com"
       endpoint = "/api/v1/sessions"
     }

     operations {
       method   = "POST"
       host     = "api.example.com"
       endpoint = "/api/v1/embeddings"
     }
   }

   output "bulk_op_ids" {
     value = [for op in ibm_cis_api_gateway_operations.bulk_ops.operations : op.operation_id]
   }
   ```
   {: codeblock}

1. Run `terraform apply`. The resource creates all operations in a single API call. The `operations` attribute returns each operation with its server-assigned `operation_id`.

The `method` argument accepts `GET`, `POST`, `PUT`, `DELETE`, `PATCH`, `HEAD`, and `OPTIONS`. The `endpoint` value must start with `/`.
{: note}

If you import the `ibm_cis_api_gateway_operations` resource, the state contains all operations that are currently registered in the zone, including operations that were created outside of Terraform. After you import, run `terraform plan` to review the differences before you run `terraform apply`.
{: tip}

For more information about the arguments and attributes, see [`ibm_cis_api_gateway_operations`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_api_gateway_operations){: external} in the Terraform registry.

### Creating a single operation with Terraform
{: #endpoint-management-creating-single-terraform}

To create a single API gateway operation with Terraform, follow these steps:

1. Add the `ibm_cis_api_gateway_operation` resource to your configuration:

   ```terraform
   resource "ibm_cis_api_gateway_operation" "single_op" {
     cis_id    = data.ibm_cis.cis.id
     domain_id = data.ibm_cis_domain.cis_domain.domain_id
     method    = "POST"
     host      = "api.example.com"
     endpoint  = "/api/v1/chat/completions"
   }

   output "single_op_id" {
     value = ibm_cis_api_gateway_operation.single_op.operation_id
   }
   ```
   {: codeblock}

1. Run `terraform apply`. The `operation_id` attribute contains the UUID of the created operation.

Changing the `method`, `host`, or `endpoint` argument forces Terraform to create a new operation.
{: note}

To create multiple single operations that you manage independently in Terraform state, use `for_each` on the `ibm_cis_api_gateway_operation` resource:

```terraform
locals {
  llm_endpoints = {
    chat        = { method = "POST", host = "api.example.com", endpoint = "/v1/messages" }
    completions = { method = "POST", host = "api.example.com", endpoint = "/v1/completions" }
  }
}

resource "ibm_cis_api_gateway_operation" "llm" {
  for_each  = local.llm_endpoints
  cis_id    = data.ibm_cis.cis.id
  domain_id = data.ibm_cis_domain.cis_domain.domain_id
  method    = each.value.method
  host      = each.value.host
  endpoint  = each.value.endpoint
}
```
{: codeblock}

For more information about the arguments and attributes, see [`ibm_cis_api_gateway_operation`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_api_gateway_operation){: external} in the Terraform registry.

### Reading saved operations with Terraform
{: #endpoint-management-creating-read-terraform}

To read operations that are saved to endpoint management with Terraform, follow these steps:

1. To list saved operations, add the `ibm_cis_api_gateway_operations` data source to your configuration. You can use the optional `host`, `method`, `endpoint`, `user_labels`, `order`, `direction`, `page`, and `per_page` arguments to filter, sort, and paginate the results:

   ```terraform
   data "ibm_cis_api_gateway_operations" "all_ops" {
     cis_id    = data.ibm_cis.cis.id
     domain_id = data.ibm_cis_domain.cis_domain.domain_id
     order     = "method"
     direction = "asc"

     depends_on = [
       ibm_cis_api_gateway_operation.single_op,
       ibm_cis_api_gateway_operations.bulk_ops,
     ]
   }

   output "total_saved_ops" {
     value = data.ibm_cis_api_gateway_operations.all_ops.total_count
   }
   ```
   {: codeblock}

1. To read a single operation by UUID, add the `ibm_cis_api_gateway_operation` data source to your configuration:

   ```terraform
   data "ibm_cis_api_gateway_operation" "single_op_read" {
     cis_id       = data.ibm_cis.cis.id
     domain_id    = data.ibm_cis_domain.cis_domain.domain_id
     operation_id = ibm_cis_api_gateway_operation.single_op.operation_id
   }
   ```
   {: codeblock}

For more information about the arguments and attributes, see [`ibm_cis_api_gateway_operations`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_api_gateway_operations){: external} and [`ibm_cis_api_gateway_operation`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_api_gateway_operation){: external} in the Terraform registry.

### Applying the cf-llm label with Terraform
{: #endpoint-management-creating-labels-terraform}

Before applying the `cf-llm` label, AI Security for Apps must be enabled on your zone. For more information, see [Managing AI Security for Apps settings](/docs/cis?topic=cis-ai-security-settings).
{: important}

To apply the `cf-llm` label to saved operations with Terraform, follow these steps:

1. Add the `ibm_cis_api_gateway_operation_labels` resource to your configuration. The following example applies the label to the single operation and to all of the bulk operations:

   ```terraform
   resource "ibm_cis_api_gateway_operation_labels" "llm_labels" {
     cis_id    = data.ibm_cis.cis.id
     domain_id = data.ibm_cis_domain.cis_domain.domain_id

     operation_ids = concat(
       [ibm_cis_api_gateway_operation.single_op.operation_id],
       [for op in ibm_cis_api_gateway_operations.bulk_ops.operations : op.operation_id]
     )
     managed_labels = ["cf-llm"]
   }

   output "label_result" {
     value = ibm_cis_api_gateway_operation_labels.llm_labels.result
   }
   ```
   {: codeblock}

1. Run `terraform apply`. The `result` attribute lists the labels that are assigned to each operation.

You can also use the `user_labels` argument to apply your own labels to the selected operations. Running `terraform destroy` removes the labels that are managed by the resource. The operations are not deleted.
{: note}

For more information about the arguments and attributes, see [`ibm_cis_api_gateway_operation_labels`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_api_gateway_operation_labels){: external} in the Terraform registry.

### Example: Protecting an LLM endpoint
{: #endpoint-management-creating-e2e-terraform}

To protect an LLM endpoint with Terraform, configure your resources in the following workflow:

1. Enable AI Security for Apps on the zone with the `ibm_cis_ai_security_settings` resource.
1. Save your endpoints as individual operations (`ibm_cis_api_gateway_operation`) or in bulk (`ibm_cis_api_gateway_operations`).
1. Apply the `cf-llm` managed label to the operations with the `ibm_cis_api_gateway_operation_labels` resource.

```terraform
resource "ibm_cis_ai_security_settings" "ai_sec" {
  cis_id    = data.ibm_cis.cis.id
  domain_id = data.ibm_cis_domain.cis_domain.domain_id
  enabled   = true
}

resource "ibm_cis_api_gateway_operation" "single_op" {
  cis_id    = data.ibm_cis.cis.id
  domain_id = data.ibm_cis_domain.cis_domain.domain_id
  method    = "POST"
  host      = "api.example.com"
  endpoint  = "/api/v1/chat/completions"

  depends_on = [ibm_cis_ai_security_settings.ai_sec]
}

resource "ibm_cis_api_gateway_operations" "bulk_ops" {
  cis_id    = data.ibm_cis.cis.id
  domain_id = data.ibm_cis_domain.cis_domain.domain_id

  operations {
    method   = "POST"
    host     = "api.example.com"
    endpoint = "/api/v1/embeddings"
  }
}

resource "ibm_cis_api_gateway_operation_labels" "protect" {
  cis_id    = data.ibm_cis.cis.id
  domain_id = data.ibm_cis_domain.cis_domain.domain_id

  operation_ids = concat(
    [ibm_cis_api_gateway_operation.single_op.operation_id],
    [for op in ibm_cis_api_gateway_operations.bulk_ops.operations : op.operation_id]
  )
  managed_labels = ["cf-llm"]
}
```
{: codeblock}

After you apply this configuration, AI Security for Apps scans incoming requests to `POST api.example.com/api/v1/chat/completions` and `POST api.example.com/api/v1/embeddings` for prompt injection, PII, and unsafe topics.

## Related resources
{: #endpoint-management-creating-related}

- [About AI Security for Apps](/docs/cis?topic=cis-ai-security-overview)
- [Managing AI Security for Apps settings](/docs/cis?topic=cis-ai-security-settings)
- [Labeling endpoints](/docs/cis?topic=cis-endpoint-management-labeling)
- [Endpoint discovery](/docs/cis?topic=cis-endpoint-management-discovery)
- [AI Security for Apps fields](/docs/cis?topic=cis-ai-security-fields)
