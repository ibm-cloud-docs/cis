---

copyright:
  years: 2021
lastupdated: "2021-11-05"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Configuring notifications
{: #configuring-notifications}

{{site.data.keyword.cis_full}} has notifications that you can configure through the API to warn you when events occur. Use email or webhooks to receive notifications.
{: shortdesc}

## Types of notification
{: #notification-types}

{{site.data.keyword.cis_short_notm}} offers two notification types:

* **DDoS attack layer 7** notifications are intended for WAF and CDN customers who want to receive a notification when an attack is mitigated.

   No action is necessary if you receive a DDoS attack layer 7 notification. Each alert includes a short description, the time the attack was detected and mitigated, the attack type, its maximum rate of attack, and the target.

* **Pool toggle alert** notifications tell you when the pool is enabled or disabled manually.

   No action is necessary if you receive a pool toggle alert. Each alert includes the state the pool was toggled to, the time it occurred, and which user made the change.

## Creating an email notification using the API
{: #create-email-notification}
{: api}

To create an email notification, take the following steps:

1. Log in to your {{site.data.keyword.cloud_notm}} account.
2. Get a token.
3. Using that token, run one of the following commands:

### DDos attack layer 7 command
{: #ddos-attack-alert-cmd}

```sh
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/:crn/alerting/policies \
  -H 'content-type: application/json' \
  -H 'x-auth-user-token: Bearer xxxxxx' \
  -d '{"name":"Example Policy","enabled":true,"alert_type":"dos_attack_l7","mechanisms":{"email":[{"id":"cistestemail@ibm.com"}],"webhooks":[]}}'
```
{: codeblock}

Where:

- **-d** is the array of attributes required to create the alert.
    - **name** is the name of the alert.
    - **enabled** is the state of the alert (one of `true`, `false`).
    - **alert_type** is the type of the alert (one of `dos_attack_l7`, `g6_pool_toggle_alert`).
    - **mechanisms** is at least one of `email`, `webhooks`.
    - **description** (optional) is the description of the alert.
    - **filter** is the list of all enablement statuses and pool IDs for the pool toggle alert.

### Pool toggle alert command
{: #pool-toggle-alert-cmd}

```sh
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/:crn/alerting/policies \
  -H 'content-type: application/json' \
  -H 'x-auth-user-token: Bearer xxxxxx' \
  -d '{"name":"Example Policy","enabled":true,"alert_type":"g6_pool_toggle_alert","mechanisms":{"email":[{"id":"cistestemail@ibm.com"}],"webhooks":[]},
       “filters”: {
       “enabled”: [
         “false”,
         “true”
       ],
       “pool_id”: [
         “6e67c08e3bae7eb398101d08def8a68a”,
         “df2d9d70fcb194ea60d2e58397cb35a6”
       ]
       },
       "conditions": {
         "and": [
           {
             "or": [
               {
                 "==": [
                   {
                     "var": "pool_id"
                   },
                   "6e67c08e3bae7eb398101d08def8a68a"
                 ]
               },
               {
                 "==": [
                   {
                     "var": "pool_id"
                   },
                   "df2d9d70fcb194ea60d2e58397cb35a6"
                 ]
               }
             ]
           },
           {
             "or": [
               {
                 "==": [
                   {
                     "var": "enabled"
                   },
                   "false"
                 ]
               },
               {
                 "==": [
                   {
                     "var": "enabled"
                   },
                   "true"
                 ]
               }
             ]
           }
         ]
       }}'
```
{: codeblock}

Where:

- **-d** is the array of attributes required to create the alert.
    - **name** is the name of the alert.
    - **enabled** is the state of the alert (one of `true`, `false`).
    - **alert_type** is the type of the alert (one of `dos_attack_l7`, `g6_pool_toggle_alert`).
    - **mechanisms** is at least one of `email`, `webhooks`.
    - **description** (optional) is the description of the alert.
    - **filter** is the list of all enablement statuses and pool IDs for the pool toggle alert.
    - **conditions** describe for all pools whether the pool is being enabled, disabled, or both.

## Creating a webhook notification using the API
{: #configuring-webhooks}

Creating a webhook notification is a two step process.

1. Send the following request to create a webhook:

    ```sh
    curl -X POST \
      https://api.cis.cloud.ibm.com/v1/:crn/alerting/destinations/webhooks \
      -H 'content-type: application/json' \
      -H 'x-auth-user-token: Bearer xxxxxx' \
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

2. Use the ID in the response that you receive to create the notification:

    ```sh
        curl -X POST \
          https://api.cis.cloud.ibm.com/v1/:crn/alerting/policies \
          -H 'content-type: application/json' \
          -H 'x-auth-user-token: Bearer xxxxxx' \
          -d '{"name":"Example Policy","enabled":true,"alert_type":"dos_attack_l7","mechanisms":{"email":[{"id":"cistestemail@ibm.com"}],"webhooks": [{"id": "6d16fcab3e8044b3b59ba3716237832e"}]}}'
    ```
    {: codeblock}

Where:

- **-d** is the array of attributes required to create the alert.
    - **name** is the name of the alert.
    - **enabled** is the state of the alert (one of `true`, `false`).
    - **alert_type** is the type of the alert (one of `dos_attack_l7`, `g6_pool_toggle_alert`).
    - **mechanisms** is the method you are using to receive notifications (at least one of `email`, `webhooks`).
    - **description** (optional) is the description of the alert.
    - **filter** is the list of all enablement statuses and pool IDs for the pool toggle alert.

## Editing notifications
{: #edit-notification}

To edit an email notification, run the following command:

```sh
curl -X PUT \
  https://api.cis.cloud.ibm.com/v1/:crn/alerting/policies/:policy_id \
  -H 'content-type: application/json' \
  -H 'x-auth-user-token: Bearer xxxxxx' \
  -d '{"name":"Example Policy","enabled":true,"alert_type":"dos_attack_l7","conditions":{},"mechanisms":{"email":[{"id":"cistestemail@ibm.com"}],"webhooks":[]}}'
```
{: codeblock}

The **conditions** field is required, even though it might be empty.
{: tip}

To edit a webhook, use the following `PUT` request:

```sh
curl -X PUT \
  https://api.cis.cloud.ibm.com/v1/:crn/alerting/destinations/webhooks/:webhook_id \
  -H 'content-type: application/json' \
  -H 'x-auth-user-token: Bearer xxxxxx' \
  -d '{"name":"Example Webhook","url":"https://hooks.slack.com/services/Ds3fdBFbV/456464Gdd"}'
```
{: codeblock}

## Deleting notifications
{: #delete-notification}

To delete an email notification, run the following command:

```sh
curl -X DELETE \
  https://api.cis.cloud.ibm.com/v1/:crn/alerting/policies/:policy_id \
  -H 'content-type: application/json' \
  -H 'accept: application/json' \
  -H 'x-auth-user-token: Bearer xxxxxx'
```
{: codeblock}

To delete a webhook, use the following `DELETE` request:

```sh
curl -X DELETE \
  https://api.cis.cloud.ibm.com/v1/:crn/alerting/destinations/webhooks/:webhook_id \
  -H 'content-type: application/json' \
  -H 'accept: application/json' \
  -H 'x-auth-user-token: Bearer xxxxxx'
```
{: codeblock}
