---

copyright:
  years: 2021, 2024
lastupdated: "2024-07-17"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Creating alerts by type
{: #create-alerts-by-type}

{{site.data.keyword.cis_full}} has alerts that you can configure to warn you when events occur. Use email or webhooks to receive alerts.
{: shortdesc}

Alerts are available only to Enterprise plans.
{: note}

For more information about each type of alert, see [Types of alerts](/docs/cis?topic=cis-configuring-policies&interface=ui#notification-types).

## Creating an email alert using the UI
{: #ui-create-email-notification}
{: ui}

You can create email alerts for each alert type by using the UI. For more information about creating email alerts using the console, see [Configuring alert policies](/docs/cis?topic=cis-configuring-policies&interface=ui#ui-configure-alert-policies).

## Creating an email alert using the CLI
{: #cli-create-email-notification}
{: cli}

You can create email alerts for each alert type by using the CLI.

### DDoS attack layer 7 command
{: #cli-ddos-attack-alert-cmd}

Create an alert policy for DDoS attack layer 7 by running the following command:

```sh
ibmcloud cis alert-policy ddos-attack-l7-alert-create --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **--name** is the name of the alert policy.
* **--description** is the description for the alert policy.
* **--emails** is the email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`
* **--webhooks** is the webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`
* **--enabled** sets whether the alert policy is enabled.
* **-i, --instance** is the instance name or ID. If not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.
* **--output** specifies the output format; only JSON is supported.

### Pool toggle alert command
{: #cli-pool-toggle-alert-cmd}

Create an alert policy for pool toggle alerts.

```sh
ibmcloud cis alert-policy pool-toggle-alert-create --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) --pools POOLS --trigger-condition (enabled | disabled | either) [--include-future-pools (true | false)] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **--name** is the name of the alert policy.
* **--description** is the description for the alert policy.
* **--emails** is the email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`
* **--webhooks** is the webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`
* **--enabled** sets whether the alert policy is enabled.
* **--pools** is the IDs of origin pool, if set to all, the all pool IDs is used.
* **--trigger-condition** is the condition of pool toggle status.
* **--include-future-pools** sets whether include the future pools.
* **-i, --instance** is the instance name or ID. If not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.
* **--output** specifies the output format; only JSON is supported.


### WAF alert command and Advanced WAF alert command
{: #cli-waf-alert-command}

Create an alert policy about spikes in firewall events. Firewall events alerts use a z-score calculation over the last six hours and five-minute buckets of events. An alert is triggered whenever the z-score is above 3.5 (the threshold). You will not receive duplicate alerts within the same two-hour time frame.

```sh
ibmcloud cis alert-policy firewall-events-alert-create --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) --domains DOMAINS [--services SERVICES] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **--name** is the name of the alert policy.
* **--description** is the description for the alert policy.
* **--emails** is the email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`
* **--webhooks** is the webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`
* **--enabled** sets whether the alert policy is enabled.
* **--domains** are the domain IDs for the alert policy. For example, `--domains domainID1,domainID2`
* **--services** (Advanced WAF) specifies which services the alert monitors. Valid values: "country-access-rules", "waf", "firewall-rules", "ratelimit", "securitylevel", "ip-access-rules", "browser-integrity-check", "ua-rules", "lockdowns", "iprange-access-rules", "asn-access-rules", "Managed-firewall".
* **-i, --instance** is the instance name or ID. If not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.
* **--output** specifies the output format; only JSON is supported.

### Universal SSL alert command
{: #cli-universal-ssl-alert-cmd}

Create an alert policy for certificate events.

```sh
ibmcloud cis alert-policy certificate-alert-create --type (universal | dedicated) --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **--type** is the type of the certificate.
* **--name** is the name of the alert policy.
* **--description** is the description for the alert policy.
* **--emails** is the email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`
* **--webhooks** is the webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`
* **--enabled** sets whether the alert policy is enabled.
* **-i, --instance** is the instance name or ID. If not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.
* **--output** specifies the output format; only JSON is supported.

### Load balancing health check alert command
{: #cli-lb-health-check-alert-cmd}

Create an alert policy for changes in health status for global load balancer, pools, and origins.

```sh
ibmcloud cis alert-policy glb-healthcheck-alert-create --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) --pools POOLS [--include-future-pools (true | false)] [--health-status-trigger (healthy | unhealthy | either)] [--event-source-trigger (pool | origin | either)] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **--name** is the name of the alert policy.
* **--description** is the description for the alert policy.
* **--emails** is the email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`
* **--webhooks** is the webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`.
* **--enabled** sets whether the alert policy is enabled.
* **--pools** are the IDs of origin pool. If set to `all`, all the pool IDs are used.
* **--include-future-pools** sets whether include the future pools (default "false").
* **--health-status-trigger** is the trigger condition to fire the notification. Valid values: "healthy", "unhealthy", "either" (default "either").
* **--event-source-trigger** is the event source of trigger to fire the notification. Valid values: "pool", "origin", "either" (default "either").
* **-i, --instance** is the instance name or ID. If not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.
* **--output** specifies the output format; only JSON is supported.


## Creating an email alert using the API
{: #create-email-notification-api}
{: api}

To create an email alert, take the following steps:

1. Log in to your {{site.data.keyword.cloud_notm}} account.
2. Get a token.
3. Using that token, run one of the following commands:

### DDoS attack layer 7 command
{: #api-config-ddos-attack-alert-cmd}

```sh
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/:crn/alerting/policies \
  -H 'content-type: application/json' \
  -H 'x-auth-user-token: Bearer xxxxxx' \
  -d '{"name":"Example Policy","enabled":true,"alert_type":"dos_attack_l7","mechanisms":{"email":[{"id":"cistestemail@ibm.com"}],"webhooks":[]}}'
```
{: codeblock}

Where:

- **-d** is the array of attributes that are required to create the alert.
    - **name** is the name of the alert.
    - **enabled** is the state of the alert (one of `true`, `false`).
    - **alert_type** is the type of the alert (one of `dos_attack_l7`, `load_balancing_pool_enablement_alert`, `clickhouse_alert_fw_anomaly`, `clickhouse_alert_fw_ent_anomaly`, `dedicated_ssl_certificate_event_type`, `universal_ssl_event_type`, or `load_balancing_health_alert`).
    - **mechanisms** is at least one of `email`, `webhooks`.
    - **description** (optional) is the description of the alert.

### Pool toggle alert command
{: #api-config-pool-toggle-alert-cmd}

```sh
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/:crn/alerting/policies \
  -H 'content-type: application/json' \
  -H 'x-auth-user-token: Bearer xxxxxx' \
  -d '{"name":"Example Policy","enabled":true,"alert_type":"load_balancing_pool_enablement_alert","mechanisms":{"email":[{"id":"cistestemail@ibm.com"}],"webhooks":[]},
       “filters”: {
       “enabled”: [
         “false”,
         “true”
       ],
       “pool_id”: [
         “6e67c08e3bae7eb398101d08def8a68a”,
         “df2d9d70fcb194ea60d2e58397cb35a6”
       ]
       }}'
```
{: codeblock}

Where:

- **-d** is the array of attributes that are required to create the alert.
    - **name** is the name of the alert.
    - **enabled** is the state of the alert (one of `true`, `false`).
    - **alert_type** is the type of the alert (one of `dos_attack_l7`, `load_balancing_pool_enablement_alert`, `clickhouse_alert_fw_anomaly`, `clickhouse_alert_fw_ent_anomaly`, `dedicated_ssl_certificate_event_type`, `universal_ssl_event_type`, or `load_balancing_health_alert`).
    - **mechanisms** is at least one of `email`, `webhooks`.
    - **description** (optional) is the description of the alert.
    - **filter** is the list of all enablement statuses and pool IDs for the pool toggle alert.

### WAF alert command
{: #api-config-waf-alert-command}

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

- **-d** is the array of attributes that are required to create the alert.
    - **name** is the name of the alert.
    - **description** (optional) is the description of the alert.
    - **enabled** is the state of the alert (one of `true`, `false`).
    - **alert_type** is the type of the alert (one of `dos_attack_l7`, `load_balancing_pool_enablement_alert`, `clickhouse_alert_fw_anomaly`, `clickhouse_alert_fw_ent_anomaly`, `dedicated_ssl_certificate_event_type`, `universal_ssl_event_type`, or `load_balancing_health_alert`).
    - **mechanisms** is at least one of `email`, `webhooks`.
    - **filters** is the list of all zones for the WAF alert.

### Advanced WAF alert command
{: #api-config-advanced-waf-command}

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

- **-d** is the array of attributes that are required to create the alert.
    - **name** is the name of the alert.
    - **description** (optional) is the description of the alert.
    - **enabled** is the state of the alert (one of `true`, `false`).
    - **alert_type** is the type of the alert (one of `dos_attack_l7`, `load_balancing_pool_enablement_alert`, `clickhouse_alert_fw_anomaly`, `clickhouse_alert_fw_ent_anomaly`, `dedicated_ssl_certificate_event_type`, `universal_ssl_event_type`, or `load_balancing_health_alert`).
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

### Universal SSL alert command
{: #api-universal-ssl-alert-cmd}

To configure a Universal SSL alert, use the following command:

```sh
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/:crn/alerting/policies \
  -H 'content-type: application/json' \
  -H 'x-auth-user-token: Bearer xxxxxx' \
  -d '{"name":"Example Policy","enabled":true,"alert_type":"universal_ssl_event_type","mechanisms":{"email":[{"id":"cistestemail@ibm.com"}],"webhooks":[]}}'
```
{: codeblock}

Where:

- **-d** is the array of attributes that are required to create the alert.
    - **name** is the name of the alert.
    - **enabled** is the state of the alert (one of `true`, `false`).
    - **alert_type** is the type of the alert (one of `dos_attack_l7`, `load_balancing_pool_enablement_alert`, `clickhouse_alert_fw_anomaly`, `clickhouse_alert_fw_ent_anomaly`, `dedicated_ssl_certificate_event_type`, `universal_ssl_event_type`, or `load_balancing_health_alert`).
    - **mechanisms** is at least one of `email`, `webhooks`.
    - **description** (optional) is the description of the alert.

### Load balancing health check alert command
{: #api-lb-health-check-alert-cmd}

To configure a load balancing health check alert, use the following command:

```sh
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/:crn/alerting/policies \
  -H 'content-type: application/json' \
  -H 'x-auth-user-token: Bearer xxxxxx' \
  -d '{"name":"Example Policy","enabled":true,"alert_type":"load_balancing_health_alert","mechanisms":{"email":[{"id":"cistestemail@ibm.com"}],"webhooks":[]},
       “filters”: {
       “event_source”: [
         “pool”,
         “origin”
       ],
       “new_health”: [
         “Healthy”,
         “Unhealthy”
       ],
       “pool_id”: [
         “6e67c08e3bae7eb398101d08def8a68a”,
         “df2d9d70fcb194ea60d2e58397cb35a6”
       ]
       }}'
```
{: codeblock}

Where:

- **-d** is the array of attributes that are required to create the alert.
    - **name** is the name of the alert.
    - **enabled** is the state of the alert (one of `true`, `false`).
    - **alert_type** is the type of the alert (one of `dos_attack_l7`, `load_balancing_pool_enablement_alert`, `clickhouse_alert_fw_anomaly`, `clickhouse_alert_fw_ent_anomaly`, `dedicated_ssl_certificate_event_type`, `universal_ssl_event_type`, or `load_balancing_health_alert`).
    - **mechanisms** is at least one of `email`, `webhooks`.
    - **description** (optional) is the description of the alert.
    - **filter** is the list of all sources, pools, health status for the load balancing health alert.

## Creating webhook alerts using the API
{: #configuring-webhooks-api}
{: api}

Creating a webhook alert is a two-step process.

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
{: api}

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
{: api}

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
