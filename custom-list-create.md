---

copyright:
  years: 2025
lastupdated: "2025-12-04"

keywords: custom lists

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Creating custom lists and adding items
{: #create-custom-lists-add-items}

Custom lists are a practical way to group related items, such as IP addresses, domains, or user IDs, for easier management and reuse. Custom lists help simplify rule configuration, reduce repetition, and make updates more efficient by centralizing control in one place.
{: shortdesc}

You can create and add items to a custom list using the UI, CLI, API, and Terraform.

## Creating a custom list and adding items in the console
{: #create-custom-list-console}
{: ui}

Follow these steps to create a custom list in the console:

1. In the CIS console, navigate to the **Account** page.
1. Select the **Lists** tab and then click **Create**.
1. Enter a name for your list and then select the [Type](/docs/cis?topic=cis-custom-list-types) of list.
1. Optionally, enter a description to clarify the purpose of the list.
1. Click **Create custom list**.
1. Select one of the following options:

   * To add items to the list manually:
      1. Enter the values, depending on the list type.
      1. Optionally, enter a description and then click **Add item**.

   * To add items to the list by using a CSV file:
      1. Click **Upload CSV**.

         The CSV file size is limited to 50 MB.
         {: note}

      1. Browse to the location of your CSV file, select the file, and then click **Upload**. The items displayed on the page include the items loaded from the CSV file.

         The exact CSV file format depends on the [list type](/docs/cis?topic=cis-custom-list-types).

      1. Click **Add item** to add items to the list.
1. Click **Create list items**.

##  Creating a custom list from the CLI
{: #create-custom-list-add-item-cli}
{: cli}

To create a custom list for your instance, enter the following command:

```sh
ibmcloud cis custom-lists list-create (--kind KIND) (--name NAME) [--description DESCRIPTION] [-i, --instance INSTANCE]
```
{: pre}

You can also accept JSON input (from a file or directly as a string):

```sh
ibmcloud cis custom-lists list-create (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE]
```
{: pre}

### Command options
{: #command-option-create-cli}

`--kind`
:   Custom list kind. Valid values: `ip`, `asn`, and `hostname`.

`--name`
:   The list name.

`--description`
:   Description of the list.

`-i, --instance`
:   Instance name or ID. If not set, the context instance specified by `cis instance-set INSTANCE` is used.

`--json`
:   The JSON file or JSON string used to describe a custom list.

:   `kind`: Kind of custom list. Valid values are `ip`, `asn`, and `hostname`. Required.
:   `name`: The list name. Required.
:   `description`: Description of the list. Optional.

    Sample JSON data:

    ```sh
    {
      "kind": "ip",
      "name": "string",
      "description": "string"
    }
    ```
    {: codeblock}

### Command examples
{: #example-1-create-custom-list}

```sh
ibmcloud cis custom-lists list-create --kind ip --name iplistone -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

```sh
ibmcloud cis custom-lists list-create —-json @example.json -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

## Adding items to a custom list from the CLI
{: #create-item-in-custom-list}
{: cli}

To create a new item in a custom list from the CLI, run the following command:

```sh
ibmcloud cis custom-lists item-create LIST_ID (--asn ASN | --ip IP | --hostname HOSTNAME) [--comment COMMENT] [-i, --instance INSTANCE]
```
{: pre}

You can also accept JSON input (from a file or directly as a string):

```sh
ibmcloud cis custom-lists item-create LIST_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE]
```
{: pre}

### Command options
{: #command-create-new-item}

`LIST_ID`
:   The ID of the custom list.

`--asn`
:   The ASN value.

`--ip`
:   The IPv4 address.

`--hostname`
:   The hostname.

`--comment`
:   To provide a brief comment on the item.

`-i, --instance`
:   Instance name or ID. If instance or ID is not set, the context instance specified by `cis instance-set INSTANCE` will be used.

`--json`
:   The JSON file or JSON string used to describe a custom list.

:   `items`: List of custom list items to create. Valid values are `asn`, `hostname`, and `ip`. Required.
:   `comment`: Comment on the item. Optional.

    Sample JSON data:

    ```sh
      [
        {
          "asn": 19604,
          "comment": "My list of developer IPs.",
          "hostname": "cloud.ibm.com",
          "ip": "172.64.0.0/13"
        }
      ]
    ```
    {: codeblock}

### Examples
{: #example-create-new-item}

```sh
ibmcloud cis custom-lists item-create f93d11a87c4945a0a6bd12820776a66d --ip 192.0.0.3  -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

```sh
ibmcloud cis custom-lists item-create f93d11a87c4945a0a6bd12820776a66d --json @example.json -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

## Creating a custom list with the API
{: #create-custom-list-api}
{: api}

Follow these steps to create a custom list with the API:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded CRN of the service instance.

1. When all variables are initiated, create the custom list:

   ```sh
   curl -X POST "https://api.cis.cloud.ibm.com/v1/$CRN/rules/lists" \
   --header "X-Auth-User-Token: Bearer <API_TOKEN>" \
   --header "Content-Type: application/json" \
   --data '{
     "kind": "ip",
     "name": "malicious_ips",
     "description": "IPs associated with known bad actors"
   }'
   ```
   {: pre}

## Adding items to a custom list with the API
{: #add-items-custom-list-api}
{: api}

Follow these steps to add items to a custom list with the API:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded CRN of the service instance.

   `LIST_ID`: The custom list ID.

1. When all variables are initiated, create the custom list items:

   ```sh
   curl -X POST "https://api.cis.cloud.ibm.com/v1/$CRN/rules/lists/$LIST_ID/items" \
   --header "X-Auth-User-Token: Bearer <API_TOKEN>" \
   --header "Content-Type: application/json" \
   --data '[
     {"ip":"23.87.13.199"},
     {"ip":"45.20.84.39"},
     {"ip":"72.48.188.49"},
     {"ip":"76.35.97.136"}
   ]'
   ```
   {: pre}

### Getting the list operation status with the API
{: #list-operation-status-api}
{: api}

Operations to manage list items are asynchronous. Follow these steps to get the list operation status with the API:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded CRN of the service instance.

   `OPERATION_ID`: The list operation ID returned during the list item operation.

1. When all variables are initiated, get the list operation status:

   ```sh
   curl -X POST "https://api.cis.cloud.ibm.com/v1/$CRN/rules/lists/bulk_operations/$OPERATION_ID" \
   --header "X-Auth-User-Token: Bearer <API_TOKEN>" \
   --header "Content-Type: application/json"
   ```
   {: pre}

For more information, see [Lists API](/apidocs/cis#create-custom-lists).

## Creating a custom list with Terraform
{: #create-custom-list-terraform}
{: terraform}

The following example creates a custom list:

```terraform
resource ibm_cis_custom_list custom_list {
    cis_id    = "crn:v1:staging:public:internet-svcs-ci:global:a/01652b251c3ae2787110a995d8db0135:1a9174b6-0106-417a-844b-c8eb43a72f63::"
    kind = "ip"
    name = "testip"
    description = "custom list"
}
```
{: codeblock}

## Adding items to a custom list with Terraform
{: #add-items-custom-list-terraform}
{: terraform}

The following example adds items to a custom list:

```terraform
resource ibm_cis_custom_list_items items1 {
    cis_id    = "crn:v1:staging:public:internet-svcs-ci:global:a/01652b251c3ae2787110a995d8db0135:1a9174b6-0106-417a-844b-c8eb43a72f63::"
    list_id = "ibm_cis_custom_list.custom_list.list_id"
    items {
        ip = "1.2.3.6"
    }
    items {
        ip = "2.3.4.5"
    items {
        ip = "192.168.0.1"
    }
}
```
{: codeblock}
