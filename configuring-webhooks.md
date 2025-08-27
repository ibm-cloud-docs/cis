---

copyright:
  years: 2021, 2025
lastupdated: "2025-08-27"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Configuring webhooks
{: #configuring-webhooks}

{{site.data.keyword.cis_full}} has alerts that you can configure through the UI, CLI, and API to warn you when events occur. Use webhooks to notify an external service when events occur in your account.
{: shortdesc}

Alerts are available only to Enterprise plans.
{: note}

## Configuring webhooks in the console
{: #configure-webhooks-ui}
{: ui}

To configure webhooks in the console, navigate to your **Account** page and select the **Alerts** tab. In the Alerts section, select the **webhooks** tab.

### Creating a webhook in the console
{: #create-webhooks-ui}

1. Click **Create**.
1. Enter a name for your webhook.
1. Enter the webhook URL. This URL can't be updated; if you want to change it, you must delete and re-create the webhook.
1. Enter the webhook secret. The secret can't be updated; if you want to change it, you must delete and re-create the webhook.

### Editing a webhook in the console
{: #update-webhooks-ui}

To edit a webhook in the console, click the pencil icon next to the name of the webhook you want to update. You can edit only the name of the webhook. If you need to modify a webhook, it is recommended that you delete and re-create the webhook instead of editing it.

### Deleting a webhook in the console
{: #delete-webhooks-ui}

To delete a webhook in the console, click the Actions menu ![overflow icon](/images/horizontal-overflow-icon.png) of the webhook you want to delete, and select **Delete**. Select **Delete** in the confirmation box to confirm, or **Cancel** to close the confirmation box without completing the delete operation.


## Configuring webhooks from the CLI
{: #configure-webhooks-cli}
{: cli}

### Creating a webhook from the CLI
{: #create-webhooks-cli}

To create a webhook from the CLI, run the following command.

```sh
ibmcloud cis alert-webhook-create --name NAME --url URL [--secret SECRET] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **--name value** is the name of the webhook.
* **--url value** is the POST endpoint to call when an alert is dispatched.
* **--secret value** is the secret that is passed in the webhook auth header when a webhook alert is dispatched.
* **-i, --instance value** is the instance name or ID. If not set, the context instance that is specified by 'cis instance-set INSTANCE' is used.
* **--output value** specifies the output format; only JSON is supported.

### Listing all webhooks from the CLI
{: #list-webhooks-cli}


To list a webhook from the CLI, run the following command.

```sh
ibmcloud cis alert-webhooks [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **-i, --instance value** is the instance name or ID. If not set, the context instance that is specified by 'cis instance-set INSTANCE' is used.
* **--output value** specifies the output format; only JSON is supported.

### Getting details for a webhook from the CLI
{: #get-webhooks-cli}

To get a webhook from the CLI, run the following command.

```sh
ibmcloud cis alert-webhook WEBHOOK_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **WEBHOOK_ID** is the ID of webhook.
* **-i, --instance value** is the instance name or ID. If not set, the context instance that is specified by 'cis instance-set INSTANCE' is used.
* **--output value** specifies the output format; only JSON is supported.

### Updating a webhook from the CLI
{: #update-webhooks-cli}

To update a webhook from the CLI, run the following command.

```sh
ibmcloud cis alert-webhook-update WEBHOOK_ID [--name NAME] [--url URL] [--secret SECRET] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **WEBHOOK_ID** is the ID of webhook.
* **--name value** is the name of the webhook.
* **--url value** is the POST endpoint to call when an alert is dispatched.
* **--secret value** is the secret that is passed in the webhook auth header when a webhook alert is dispatched.
* **-i, --instance value** is the instance name or ID. If not set, the context instance that is specified by 'cis instance-set INSTANCE' is used.
* **--output value** specifies the output format; only JSON is supported.

### Deleting a webhook from the CLI
{: #delete-webhooks-cli}

To delete a webhook from the CLI, run the following command.

```sh
ibmcloud cis alert-webhook-delete WEBHOOK_ID [-i, --instance INSTANCE] [-f, --force]
```
{: pre}

Where:

* **WEBHOOK_ID** is the ID of webhook.
* **i, --instance value** is the instance name or ID. If not set, the context instance that is specified by 'cis instance-set INSTANCE' is used.
* **-f, --force** attempts to delete webhook without prompting for confirmation.

## Configuring webhooks with the API
{: #api-configure-webhooks}
{: api}

To call these methods, you must be assigned one or more IAM access roles.

* `internet-svcs.zones.read`
* `internet-svcs.zones.update`

You can check your access by going to **Users > _name_ > Access policies**.
{: tip}


### Creating a webhook with the API
{: #api-create-webhooks}

Creating a webhook alert is a two-step process. First, create the webhook, then use the ID in the response that you receive to create the alert.

To create a webhook by with the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following variable to be used in the API command:
    * `crn`: the full url-encoded CRN of the service instance.
    * `name`: the name of the webhook.
    * `url`: the URL of the webhook.
    * `secret`: the optional secret or API key that is needed to use the webhook.
1. When all variables are initiated, run the following command to create the webhook:

```sh
curl -X POST https://api.cis.cloud.ibm.com/v1/:crn/alerting/destinations/webhooks
-H 'content-type: application/json'
-H 'x-auth-user-token: Bearer xxxxxx'
-d '{"name":"Example Webhook","url":"https://hooks.slack.com/services/Ds3fdBFbV/456464Gdd"}'
```
{: codeblock}

The following response is returned:

```sh
{
    "result": {
        "id": "6d16fcab3e8044b3b59ba3716237832e"
    },
    "success": true,
    "errors": [],
    "messages": []
}
```
{: codeblock}

Use the ID in the response that you receive to create the alert:
```sh
    curl -X POST \
        https://api.cis.cloud.ibm.com/v1/:crn/alerting/policies \
        -H 'content-type: application/json' \
        -H 'x-auth-user-token: Bearer xxxxxx' \
        -d '{"name":"Example Policy","enabled":true,"alert_type":"dos_attack_l7","mechanisms":{"email":[{"id":"cistestemail@ibm.com"}],"webhooks": [{"id": "6d16fcab3e8044b3b59ba3716237832e"}]}}'
```
{: codeblock}

### Listing all webhooks with the API
{: #api-list-webhooks}

To list all webhooks by with the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following variable to be used in the API command:
    * `crn`: the full url-encoded CRN of the service instance.
1. When all variables are initiated, get the list of webhooks:

```sh
curl -X GET https://api.cis.cloud.ibm.com/v1/:crn/alerting/destinations/webhooks
-H 'content-type: application/json'
-H 'accept: application/json'
-H 'x-auth-user-token: Bearer xxxxxx'
```
{: codeblock}


### Getting details for a webhook with the API
{: #api-get-webhooks}

To get the details of a webhook by with the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following variable to be used in the API command:
    * `crn`: the full url-encoded CRN of the service instance.
    * `webhook_id`: alert webhook identifier.
1. When all variables are initiated, get the webhook details:

```sh
curl -X GET https://api.cis.cloud.ibm.com/v1/:crn/alerting/destinations/webhooks/:webhook_id
-H 'content-type: application/json'
-H 'accept: application/json'
-H 'x-auth-user-token: Bearer xxxxxx'
```
{: codeblock}

### Updating a webhook with the API
{: #api-update-webhooks}

To update a webhook by with the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following variable to be used in the API command:
    * `crn`: the full url-encoded CRN of the service instance.
    * `webhook_id`: alert webhook identifier.
    * `name`: the name of the webhook.
    * `url`: the URL of the webhook.
    * `secret`: the optional secret or API key that is needed to use the webhook.
1. When all variables are initiated, update the webhook:

```sh
curl -X PUT https://api.cis.cloud.ibm.com/v1/:crn/alerting/destinations/webhooks/:webhook_id
-H 'content-type: application/json'
-H 'x-auth-user-token: Bearer xxxxxx'
-d '{"name":"Example Webhook","url":"https://hooks.slack.com/services/Ds3fdBFbV/456464Gdd"}'
```
{: codeblock}

### Deleting a webhook with the API
{: #api-delete-webhooks}

To delete a webhook by with the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following variable to be used in the API command:
    * `crn`: the full url-encoded CRN of the service instance.
    * `webhook_id`: alert webhook identifier.
1. When all variables are initiated, delete the webhook:

```sh
curl -X DELETE https://api.cis.cloud.ibm.com/v1/:crn/alerting/destinations/webhooks/:webhook_id
-H 'content-type: application/json'
-H 'accept: application/json'
-H 'x-auth-user-token: Bearer xxxxxx'
```
{: codeblock}
