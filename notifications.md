---

copyright:
  years: 2021, 2022
lastupdated: "2022-03-09"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Configuring alerts
{: #configuring-notifications}

{{site.data.keyword.cis_full}} has alerts that you can configure through the API to warn you when events occur. Use email or webhooks to receive alerts.
{: shortdesc}

Alerts are available only to Enterprise plans.
{: note}

## Types of alerts
{: #notification-types}

{{site.data.keyword.cis_short_notm}} offers three alert types:

* **DDoS attack layer 7 alerts** are intended for WAF and CDN customers who want to receive a notification when an attack is mitigated.

   No action is necessary if you receive a DDoS attack layer 7 alert. Each alert includes a short description, the time the attack was detected and mitigated, the attack type, its maximum rate of attack, and the target.

* **Pool toggle alerts** tell you when the pool is enabled or disabled manually.

   No action is necessary if you receive a pool toggle alert. Each alert includes the state the pool was toggled to, the time it occurred, and which user made the change.
   
* **Security alerts** include WAF alerts and Advanced WAF alerts. 
    * **WAF alerts** look for spikes across all services that generate log entries in firewall events. The mean time to detection is two hours.
    * **Advanced WAF alerts**. You can select the services to monitor, and each selected service is monitored separately. The mean time to detection is five minutes.

## Creating an email alert using the API
{: #create-email-notification-api}
{: api}

To create an email alert, take the following steps:

1. Log in to your {{site.data.keyword.cloud_notm}} account.
2. Get a token.
3. Using that token, run one of the following commands:

### DDoS attack layer 7 command
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
    - **alert_type** is the type of the alert (one of `dos_attack_l7`, `g6_pool_toggle_alert`, `clickhouse_alert_fw_anomaly`, or `clickhouse_alert_fw_ent_anomaly`).
    - **mechanisms** is at least one of `email`, `webhooks`.
    - **description** (optional) is the description of the alert.
    
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
       }}'
```
{: codeblock}

Where:

- **-d** is the array of attributes required to create the alert.
    - **name** is the name of the alert.
    - **enabled** is the state of the alert (one of `true`, `false`).
    - **alert_type** is the type of the alert (one of `dos_attack_l7`, `g6_pool_toggle_alert`, `clickhouse_alert_fw_anomaly`, or `clickhouse_alert_fw_ent_anomaly`).
    - **mechanisms** is at least one of `email`, `webhooks`.
    - **description** (optional) is the description of the alert.
    - **filter** is the list of all enablement statuses and pool IDs for the pool toggle alert.
    - **conditions** describe for all pools whether the pool is being enabled, disabled, or both. Content is generated automatically if the field is empty.
    
### WAF alert command
{: #waf-alert-command}

To configure a WAF alert, use the following command:

```sh
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/:crn/alerting/policies \
  -H 'Content-Type: application/json' \
  -H 'X-Auth-User-Token: Bearer xxxxxx' \
  -d '{
  "name": "WAF Alerter",
  "description": "Send an email on spike in firewall events for any service",
  "enabled": true,
  "alert_type": "clickhouse_alert_fw_anomaly",
  "mechanisms": {
    "email": [
      {
        "id": "sreteam@techcompany.com"
      }
    ]
  },
  "filters": {
    "zones": [
      "123456ab7d8e9f0g12h2j34l5mn6op78"
    ]
  }
}'
```
{: codeblock}

Where:

- **-d** is the array of attributes required to create the alert.
    - **name** is the name of the alert.
    - **description** (optional) is the description of the alert.
    - **enabled** is the state of the alert (one of `true`, `false`).
    - **alert_type** is the type of the alert (one of `dos_attack_l7`, `g6_pool_toggle_alert`, `clickhouse_alert_fw_anomaly`, or `clickhouse_alert_fw_ent_anomaly`).
    - **mechanisms** is at least one of `email`, `webhooks`.
    - **filters** is the list of all zones for the WAF alert.
   
### Advanced WAF alert command
{: #advanced-waf-command}

To configure an Advanced WAF alert, use the following command:

```sh
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/:crn/alerting/policies \
  -H 'Content-Type: application/json' \
  -H 'X-Auth-User-Token: Bearer xxxxxx' \
  -d '{
  "name": "WAF Alerter",
  "description": "Send an email on spike in firewall events for WAF or browser integrity check",
  "enabled": true,
  "alert_type": "clickhouse_alert_fw_ent_anomaly",
  "mechanisms": {
    "email": [
      {
        "id": "sreteam@techcompany.com"
      }
    ]
  },
  "filters": {
    "services": [
      "waf",
      "bic"
    ],
    "zones": [
      "123456ab7d8e9f0g12h2j34l5mn6op78"
    ]
  }
}'
```
{: codeblock}

Where:

- **-d** is the array of attributes required to create the alert.
    - **name** is the name of the alert.
    - **description** (optional) is the description of the alert.
    - **enabled** is the state of the alert (one of `true`, `false`).
    - **alert_type** is the type of the alert (one of `dos_attack_l7`, `g6_pool_toggle_alert`, `clickhouse_alert_fw_anomaly`, or `clickhouse_alert_fw_ent_anomaly`).
    - **mechanisms** is at least one of `email`, `webhooks`.
    - **filters** is the list of all services to monitor for security events and zones for the Advanced WAF alert.
    
You can monitor the following services:

|Services|Log value|
|--------|---------|
|Country IP access rules|`country`|
|WAF|`waf`|
|Firewall rules|`firewallrules`|
|Rate limiting|`ratelimit`|
|Security level|`securitylevel`|
|IP access rules|`ip`|
|Validation|`validation`|
|Browser integrity check|`bic`|
|Hot link protection|`hot`|
|User agent block|`uablock`|
|Zone lockdown|`zonelockdown`|
|IP range access rules|`iprange`|
|ASN IP access rules|`asn`|
|Custom firewall|`firewallCustom`|
|Managed firewall|`firewallManaged`|
|Data loss prevention|`dlp`|
{: caption="Table 1. Services that can be monitored by Advanced WAF alerts" caption-side="bottom"}

## Creating webhook alerts using the API
{: #configuring-webhooks-api}

Creating a webhook alert is a two step process.

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
    {: screen}

2. Use the ID in the response that you receive to create the alert:

    ```sh
        curl -X POST \
          https://api.cis.cloud.ibm.com/v1/:crn/alerting/policies \
          -H 'content-type: application/json' \
          -H 'x-auth-user-token: Bearer xxxxxx' \
          -d '{"name":"Example Policy","enabled":true,"alert_type":"dos_attack_l7","mechanisms":{"email":[{"id":"cistestemail@ibm.com"}],"webhooks": [{"id": "6d16fcab3e8044b3b59ba3716237832e"}]}}'
    ```
    {: codeblock}

## Editing alerts using the API
{: #edit-notification-api}

To edit an email alert, run the following command:

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

## Deleting alerts using the API
{: #delete-notification-api}

To delete an email alert, run the following command:

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
