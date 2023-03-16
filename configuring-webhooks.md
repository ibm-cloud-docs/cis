---

copyright:
  years: 2021, 2022
lastupdated: "2022-03-23"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Configuring webhooks
{: #configuring-webhooks}

{{site.data.keyword.cis_full}} has alerts that you can configure through the API to warn you when events occur. Use webhooks to notify an external service when events occur in your account.
{: shortdesc}

Alerts are available only to Enterprise plans.
{: note}

## Configuring webhooks using the console
{: #configure-webhooks-ui}
{: ui}

To configure webhooks using the console, navigate to your **Account** page and select the **Alerts** tab. In the Alerts section, select the **webhooks** tab.

### Creating a webhook using the console
{: #create-webhooks-ui}

1. Click **Create**.
1. Enter a name for your webhook.
1. Enter the webhook URL. This URL cannot be updated; if you want to change it, you must delete and recreate the webhook.
1. Enter the webhook secret. The secret cannot be updated; if you want to change it, you must delete and recreate the webhook.

### Editing a webhook using the console
{: #update-webhooks-ui}

To edit a webhook using the console, click the pencil icon next to the name of the webhook you want to update. You can only edit the name of the webhook. If you need to modify a webhook, it is recommended that you delete and recreate the webhook instead of editing it.

### Deleting a webhook using the console
{: #delete-webhooks-ui}

To delete a webhook using the console, click the overflow menu ![overflow icon](/images/horizontal-overflow-icon.svg) of the webhook you want to delete, and select **Delete**. Select **Delete** in the confirmation box to confirm, or **Cancel** to close the confirmation box without completing the delete operation.


## Configuring webhooks using the CLI
{: #configure-webhooks-cli}
{: cli}

### Creating a webhook using the CLI
{: #create-webhooks-cli}

To create a webhook using the CLI, run the following command.

```sh
ibmcloud cis alert-webhook-create --name NAME --url URL [--secret SECRET] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **--name value**is the name of the webhook.
* **--url value** is the POST endpoint to call when dispatching an alert.
* **--secret value** is the secret that will be passed in the webhook auth header when dispatching a webhook alert.
* **-i, --instance value** is the instance name or ID. If not set, the context instance specified by 'cis instance-set INSTANCE' is used.
* **--output value** specifies output format; only JSON is supported.

### Listing all webhooks using the CLI
{: #list-webhooks-cli}


To list a webhook using the CLI, run the following command.

```sh
ibmcloud cis alert-webhooks [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **-i, --instance value** is the instance name or ID. If not set, the context instance specified by 'cis instance-set INSTANCE' is used.
* **--output value** specifies output format; only JSON is supported.

### Getting details for a webhook using the CLI
{: #get-webhooks-cli}

To get a webhook using the CLI, run the following command.

```sh
ibmcloud cis alert-webhook WEBHOOK_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **WEBHOOK_ID** is the ID of webhook.
* **-i, --instance value** is the instance name or ID. If not set, the context instance specified by 'cis instance-set INSTANCE' is used.
* **--output value** specifies output format; only JSON is supported.

### Updating a webhook using the CLI
{: #update-webhooks-cli}

To update a webhook using the CLI, run the following command.

```sh
ibmcloud cis alert-webhook-update WEBHOOK_ID [--name NAME] [--url URL] [--secret SECRET] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **WEBHOOK_ID** is the ID of webhook.
* **--name value** is the name of the webhook.
* **--url value** is the POST endpoint to call when dispatching an alert.
* **--secret value** is the secret that is passed in the webhook auth header when dispatching a webhook alert.
* **-i, --instance value** is the instance name or ID. If not set, the context instance specified by 'cis instance-set INSTANCE' is used.
* **--output value** specifies output format; only JSON is supported.

### Deleting a webhook using the CLI
{: #delete-webhooks-cli}

To delete a webhook using the CLI, run the following command.

```sh
ibmcloud cis alert-webhook-delete WEBHOOK_ID [-i, --instance INSTANCE] [-f, --force]
```
{: pre}

Where:

* **WEBHOOK_ID** is the ID of webhook.
* **i, --instance value** is the instance name or ID. If not set, the context instance specified by 'cis instance-set INSTANCE' is used.
* **-f, --force** attempts to delete webhook without prompting for confirmation.

## Configuring webhooks using the API
{: #api-configure-webhooks}
{: api}

To call these methods, you must be assigned one or more IAM access roles.

* `internet-svcs.zones.read`
* `internet-svcs.zones.update`

You can check your access by going to **Users > _name_ > Access policies**.
{: tip}


### Creating a webhook using the API
{: #api-create-webhooks}

Creating a webhook alert is a two step process. First, create the webhook, then use the ID in the response that you receive to create the alert.

To create a webhook by using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store your the following variable to be used in the API command:
    * `crn`: the full url-encoded CRN of the service instance.
    * `name`: the name of the webhook.
    * `url`: the URL of the webhook.
    * `secret`: the optional secret or API key needed to use the webhook.
1. When all variables are initiated, create the webhook:

```sh
curl -X POST https://api.cis.cloud.ibm.com/v1/:crn/alerting/destinations/webhooks 
-H 'content-type: application/json' 
-H 'x-auth-user-token: Bearer xxxxxx' 
-d '{"name":"Example Webhook","url":"https://hooks.slack.com/services/Ds3fdBFbV/456464Gdd"}'
```
{: codeblock}

### Listing all webhooks using the API
{: #api-list-webhooks}

To list all webhooks by using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store your the following variable to be used in the API command:
    * `crn`: the full url-encoded CRN of the service instance.
1. When all variables are initiated, get the list of webhooks:

```sh
curl -X GET https://api.cis.cloud.ibm.com/v1/:crn/alerting/destinations/webhooks 
-H 'content-type: application/json' 
-H 'accept: application/json' 
-H 'x-auth-user-token: Bearer xxxxxx'
```
{: codeblock}


### Getting details for a webhook using the API
{: #api-get-webhooks}

To get the details of a webhook by using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store your the following variable to be used in the API command:
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

### Updating a webhook using the API
{: #api-update-webhooks}

To update a webhook by using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store your the following variable to be used in the API command:
    * `crn`: the full url-encoded CRN of the service instance.
    * `webhook_id`: alert webhook identifier.
    * `name`: the name of the webhook.
    * `url`: the URL of the webhook.
    * `secret`: the optional secret or API key needed to use the webhook.
1. When all variables are initiated, update the webhook:

```sh
curl -X PUT https://api.cis.cloud.ibm.com/v1/:crn/alerting/destinations/webhooks/:webhook_id 
-H 'content-type: application/json' 
-H 'x-auth-user-token: Bearer xxxxxx' 
-d '{"name":"Example Webhook","url":"https://hooks.slack.com/services/Ds3fdBFbV/456464Gdd"}'
```
{: codeblock}

### Deleting a webhook using the API
{: #api-delete-webhooks}

To delete a webhook by using the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store your the following variable to be used in the API command:
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
