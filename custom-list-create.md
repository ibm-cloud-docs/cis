---

copyright:
  years: 2025
lastupdated: "2025-07-01"

keywords: custom lists

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Creating custom lists   
{: #create-custom-lists}

You can create,update, and delete the custom list in the console, from the CLI, with the API and terraform.
{: shortdesc}

### Creating a custom list in the console
{: #create-custom-list-console}
{: ui}

NEED UI TO BE IMPLEMENTED

[Create a list in the dashboard](https://developers.cloudflare.com/waf/tools/lists/create-dashboard/) [WAITING UI]{: tag-red}

### Creating a custom list from the CLI
{: #create-custom-list-cli}
{: cli}

You can list, create, update, and delete the custom list from the CLI.

#### Listing the custom lists for the instance
{: #list-custom-lists-instance}

To list the custom lists for your instance, run the following command:
```sh
ibmcloud cis custom-lists lists [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

##### Command options
{: #custom-list-instance}

`-i, --instance`
:   Instance name or ID. If not set, the context instance specified by 'cis instance-set INSTANCE' is used.

`--output`
:   Specify the output format. Currently, only JSON is supported.

##### Command example
{: #example-lists-cli}

```sh
ibmcloud cis custom-lists lists -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

#### Getting a custom list for your instance
{: #get-custom-list-instance}

To get a custom list for your instance, run the following command:
```sh
ibmcloud cis custom-lists list LIST_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

##### Command options
{: #command-options-to-get-custom-list}

`LIST_ID`
:   The ID of the custom list.

`-i, --instance`
:   Instance name or ID. If not set, the context instance specified by 'cis instance-set INSTANCE' is used.

`--output`
:   Specify the output format. Currently, only JSON is supported.

##### Command example
{: #example-to-get-custom-list}

```sh
ibmcloud cis custom-lists list f93d11a87c4945a0a6bd12820776a66d -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9:: -o json
```
{: pre}

#### Creating a custom list for your instance
{: #create-custom-list-instance}

To create a custom list for your instance enter the following command:

```sh
ibmcloud cis custom-lists list-create (--kind KIND) (--name NAME) [--description DESCRIPTION] [-i, --instance INSTANCE]
```
{: pre}

You can also accept JSON input (from a file or directly as a string):

```sh
ibmcloud cis custom-lists list-create (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE]
```
{: pre}

##### Command options
{: #command-option-create-cli}

`--kind`
:   Custom list kind. Valid values: `ip`, `asn`, and `hostname`.

`--name`
:   The list name.

`--description`
:   Description of the list. 

`-i, --instance`
:   Instance name or ID. If not set, the context instance specified by 'cis instance-set INSTANCE' is used.

`--json`
:   The JSON file or JSON string used to describe a custom list.

:   The required fields in JSON data are:
:   `"kind"`: Custom list kind. Valid values are `ip`, `asn`, and `hostname`.
:   `"name"`: The list name.

:   The optional field is:
:   `"description"`: To briefly describe the list.

    Sample JSON data:

    ```sh
    {
      "kind": "ip",
      "name": "string",
      "description": "string"
    }
    ```
    {: codeblock}

##### Command examples
{: #example-1-create-custom-list}

```sh
ibmcloud cis custom-lists list-create --kind ip --name iplistone -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

```sh
ibmcloud cis custom-lists list-create —-json @example.json -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

#### Updating the description of a custom list
{: #updating-description-custom}

To update the description of a custom list, run the following commands:

```sh
ibmcloud cis custom-lists list-update LIST_ID (--description DESCRIPTION) [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

```sh
ibmcloud cis custom-lists list-update LIST_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

##### Command options
{: #command-options-update-description-custom}

`LIST_ID`
:   The ID of the custom list.

`--description`
:   Briefly describe the list.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance specified by `cis instance-set INSTANCE` will be used.

`--output`
:   Specify output format, only JSON is supported now.

`json`
:   The JSON file or JSON string used to describe a custom list.
:   The optional field is:
:   **"description"**: To briefly describe the list.

    Sample JSON data:
    ```sh
      {
        "description": "string"
      }
    ```
    {: codeblock}

##### Command examples
{: #example--update-description-custom}
 
```sh
ibmcloud cis custom-lists list-update a46c54444a97431e810c975bf2db4f83 --description "description example" -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}
 
```sh
ibmcloud cis custom-lists list-update a46c54444a97431e810c975bf2db4f83 —-json @example.json -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

#### Deleting a custom list
{: #delete-custom-list}

To delete a custom list for your instance, run the following command:

```sh
ibmcloud cis custom-lists list-delete LIST_ID [-f, --force] [-i, --instance INSTANCE]
```
{: pre}

##### Command options
{: #command-delete-custom-list}

`LIST_ID`
:   The ID of the custom list.

`-f, --force`
:   Attempt to delete custom list without prompting for confirmation.

`-i, --instance`
:   Instance name or ID. If not set, the context instance specified by `cis instance-set INSTANCE` will be used.

##### Command example
{: #example-delete-custom-list}

```sh
custom-lists list-delete 78277700444f4f69aefef78ea2bef013 -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

#### Getting the list items for a custom list
{: #getting-list-items-custom}

```sh
ibmcloud cis custom-lists items LIST_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

##### Command options
{: #command-get-list-items}

`LIST_ID`
:   The ID of the custom list.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance specified by `cis instance-set INSTANCE` will be used.

`--output`
:   Specify output format, only JSON is supported now.

##### Command example
{: #example-get-list-items}

```sh
ibmcloud cis custom-lists items f93d11a87c4945a0a6bd12820776a66d -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

#### Viewing a specific item in a custom list from the CLI
{: #view-specific-item-in-list}

To view a specific item in a custom list, run the following command:
```sh
ibmcloud cis custom-lists item LIST_ID ITEM_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

##### Command options
{: #command-options-custom-list-cli}

`LIST_ID`
:   The ID of the custom list.

`ITEM_ID`
:   The ID of the custom list item.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance specified by `cis instance-set INSTANCE` will be used.

`--output`
:   Specify output format, only JSON is supported now.

##### Example
{: #create-custom-list-cli}

```sh
ibmcloud cis custom-lists item f93d11a87c4945a0a6bd12820776a66d f550e1d3ede74455bf225a06800bd1be -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

#### Creating a new item in a custom list
{: #create-item-in-custom-list}

To create a new item in a custom list from the CLI, run the following command:

Using command 1:
```sh
ibmcloud cis custom-lists item-create LIST_ID (--asn ASN | --ip IP | --hostname HOSTNAME) [--comment COMMENT] [-i, --instance INSTANCE]
```
{: pre}

Using command 2:
```sh
ibmcloud cis custom-lists item-create LIST_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE]
```
{: pre}

##### Command options
{: #command-create-new-item}

`LIST_ID`
:   The ID of the custom list.

`--asn`
:   The ASN value.

`--ip`
:   The Ipv4 address.

`--hostname`
:   The hostname.

`--comment`
:   To provide a brief comment on the item.

`-i, --instance`
:   Instance name or ID. If instance or ID is not set, the context instance specified by `cis instance-set INSTANCE` will be used.

`--json`
:   The JSON file or JSON string used to describe a custom list.

:   The required fields in JSON data are:
:   **"items"**: List of custom list items to create.
:   **"asn"**: The ASN.
:   **"hostname"**: The hostname.
:   **"ip"**: The Ipv4 address.
:   **"comment"**: To provide a brief comment on the item.

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

##### Examples
{: #example-create-new-item}

Example using command 1:
```sh
ibmcloud cis custom-lists item-create f93d11a87c4945a0a6bd12820776a66d --ip 192.0.0.3  -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

Example using command 2:
```sh
ibmcloud cis custom-lists item-create f93d11a87c4945a0a6bd12820776a66d --json @example.json -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

#### Updating all list items for custom list
{: #update-all-list-items}

This step removes existing items from the list. This operation is asynchronous. To get current the operation status, use the operation command. To update all list items for your custom list, run the following command:

```sh
ibmcloud cis custom-lists item-update LIST_ID (--json @JSON_FILE | JSON_STRING) [-f, --force] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

##### Command options
{: #command-updating-all-list-items}

`LIST_ID`
:   The ID of the custom list.

`--json`
:   The JSON file or JSON string used to describe a custom list.
:   The required fields in JSON data are:
:   **"items"**: List of custom list items to create.
:   **"asn"**: The ASN value.
:   **"hostname"**: The hostname.
:   **"ip"**: The Ipv4 address.
:   **"comment"**: To provide a brief comment on the item.

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

`-f, --force`
:   Attempt to delete custom list without prompting for confirmation.

`--output value`
:   Specify output format, only JSON is supported now.

`-i, --instance`
:   Instance name or ID. If instance value or ID is not set, the context instance specified by `cis instance-set INSTANCE` will be used.

##### Example
{: #example-updating-all-list-items}

```sh
ibmcloud cis custom-lists item-update f93d11a87c4945a0a6bd12820776a66d —json @example.json -f -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

#### Deleting an item from a custom list
{: #delete-an-item-list}

To delete an item from a custom list, run the following commands:

Using command 1:
```sh
ibmcloud cis custom-lists item-delete LIST_ID (--item-id CUSTOM_LIST_ITEM_ID) [-f, --force] [-i, --instance INSTANCE]
```
{: pre}

Using command 2:
```sh
ibmcloud cis custom-lists item-delete LIST_ID (--json @JSON_FILE | JSON_STRING) [-f, --force] [-i, --instance INSTANCE]
```
{: pre}

##### Command options
{: #command-delete-an-item-list}

`LIST_ID`
:   The ID of the custom list.

`--item-id`
:   `CUSTOM_LIST_ITEM_ID` is the ID of the custom list item.

`-f, --force`
:   Attempt to delete custom list without prompting for confirmation.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance specified by `cis instance-set INSTANCE` will be used.

`--json`
:   The JSON file or JSON string used to describe a custom list.
:   The required fields in JSON data are:
:   **"items"**: List of custom list items to delete by ID.
:   **"id"**: Unique ID of the custom list item.

    Sample JSON data:
    ```sh
      {
        "items": [
          {
            "id": "70c2009751b24ffc9ed1ab462ba957b4"
          }
        ]
      }
    ```
    {: codeblock}

##### Examples
{: #example-delete-an-item-list}

Example using command 1:
```sh
ibmcloud cis custom-lists item-delete f93d11a87c4945a0a6bd12820776a66d --item-id —force 42851cc4589746229552ec5a54f9d623 -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

Example using command 2:
```sh
ibmcloud cis custom-lists item-delete f93d11a87c4945a0a6bd12820776a66d —json @example.json —-force -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

#### Getting the status for a custom list operation
{: #getting-status-custom}

To get the status for the custome list operation, run the following command:
```sh
ibmcloud cis custom-lists operation OPERATION_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

##### Command options
{: #command-getting-status-custom}

`OPERATION_ID`
:   The ID of the custom list operation.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance specified by `cis instance-set INSTANCE` will be used.

`--output`
:   Specify output format, only JSON is supported now.

##### Example
{: #example-getting-status-custom}

```sh
ibmcloud cis custom-lists operation 04cdb3b267a44ceb895e766fc2affe72 -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9:: -o json
```
{: pre}

### Creating a custom list with the API
{: #create-custom-list-api}
{: api}

Follow these steps to create a custom list with the API:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded Cloud Resource Name (CRN) of the service instance.

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

### Adding items to a custom list with the API
{: #add-items-custom-list-api}
{: api}

Follow these steps to add items to a custom list with the API:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded Cloud Resource Name (CRN) of the service instance.

   `LIST_ID`: The custom list id.

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

   `CRN`: The full URL-encoded Cloud Resource Name (CRN) of the service instance.

   `OPERATION_ID`: The list operation id returned during the list item operation.

1. When all variables are initiated, get the list operation status:

```sh
curl -X POST "https://api.cis.cloud.ibm.com/v1/$CRN/rules/lists/bulk_operations/$OPERATION_ID" \
--header "X-Auth-User-Token: Bearer <API_TOKEN>" \
--header "Content-Type: application/json"
```
{: pre}

For more information, see [Lists API](/apidocs/cis#create-custom-lists).
