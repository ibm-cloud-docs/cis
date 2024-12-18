---

copyright:
  years: 2021, 2024
lastupdated: "2024-12-18"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Configuring alert policies
{: #configuring-policies}

{{site.data.keyword.cis_full}} has alerts that you can configure through the API to warn you when events occur.
{: shortdesc}

See [Configuring webhooks](/docs/cis?topic=cis-configuring-webhooks) for detailed instructions on using webhooks.

Alerts are available only to Enterprise plans.
{: note}

## Types of alerts
{: #notification-types}

{{site.data.keyword.cis_short_notm}} offers the following alert types:

* **DDoS attack layer 7 alerts** are intended for WAF and CDN customers who want to receive a notification when an attack is mitigated.

   No action is necessary if you receive a DDoS attack layer 7 alert. Each alert includes a short description, the time the attack was detected and mitigated, the attack type, its maximum rate of attack, and the target.

* **Certificate alerts** include alerts that pertain to TLS certificates. The following alert types specify the renewal aspect you need.
    * **Dedicated/Advanced** receive notification for validation, issuance renewal, and expiration of Dedicated/Advanced certificates.
    * **Universal SSL** certificates are automatically refreshed and no user action is required.
    * **Mutual TLS** alert you when the mTLS certificate is expiring.
* **Logpush job alerts** alerts when the job is disabled due to consistent failures, not when a failure occurs the first time. Any impacted job destinations are included in the alert.
* **Web metrics report** is a weekly summary with reports from your account's web metrics.
* **Cloudflare maintenance report** shows scheduled, changed, or canceled Cloudflare maintenance windows.
* **Cloudflare incident report** shows ongoing Cloudflare incidents.
* **Security alerts** include WAF alerts and Advanced WAF alerts.
    * **WAF alerts** look for spikes across all services that generate log entries in firewall events. The mean time to detection is 2 hours.
    * **Advanced WAF alerts**. You can select the services to monitor, and each selected service is monitored separately. The mean time to detection is 5 minutes.
* **Load balancing health check alerts** are sent when a change occurs in the health status of a load balancing health check.
* **Pool toggle alerts** notify when the pool is enabled or disabled manually.

   No action is necessary if you receive a pool toggle alert. Each alert includes the state that the pool was toggled to, the time it occurred, and which user made the change.


## Configuring alert policies in the UI
{: #ui-configure-alert-policies}
{: ui}

Use the UI to create, update, and delete alerting policies.

To configure alert policies in the UI, navigate to your **Account** page and select the **Alerts** tab. In the Alerts section, select the **Alerting policies** tab.

### Creating a security alert policy in the UI
{: #ui-create-alert}

1. Click **Create**.
1. Select the type of alert policy that you want to create:
    * HTTP DDoS attack alert, which detects and mitigates an HTTP DDoS attack against one of your domains.
    * Dedicated/Advanced alerts, which alert you when dedicated certificates are expired, and when they are renewed.
    * Universal SSL alert, which alerts you when Universal certificates are automatically refreshed.
    * Mutual TLS alert, which alerts you when a Mutual TLS certificate is expiring.
    * Logpush job alert, which alerts you when any configured Logpush job fails.
    * Web metrics report, which is a weekly report that helps identify changes in your application's traffic and performance over time.
    * Cloudflare maintenance report, which reports on scheduled, changed or canceled Cloudflare maintenance windows.
    * Cloudflare incident report, which reports on ongoing Cloudflare incidents.
    * Security events alert, which alerts you within 2 hours of detecting a spike in all security events.
    * Advanced security events alert, which alerts you within 5 minutes of detecting a spike in security events with optional service filter.
    * Load balancing health check alerts, which alerts you when the health status changes for a pool health check, or pool origin.
    * Pool enablement alert, which are alert based on the pool's enabled or disabled toggle status.
1. Enter a name for your alerting policy, and optionally enter a description.
1. Choose an alerting method. You can select a webhook, enter an email address to send alerts to, or both. Only one notification is required to complete configuration.
    * Enter an email address to which {{site.data.keyword.cis_short}} sends alerts. Click the `+` to add the address to the alert. Repeat for all email addresses.
    * Click **Add webhook** and select an available webhook. If no webhooks are present, this option is unavailable.
1. Click **Create**

By default, alert policies are enabled when created. You can disable alerts that you created by switching the toggle in the **Enabled** column.

### Creating an advanced security alert policy in the UI
{: #ui-create-advanced-security-alert}

To create an advanced security alert in the UI, take the following steps:

1. Click **Create**.
1. Select Advanced security events alert.
1. Enter a name for your alerting policy, and optionally enter a description.
1. Choose an alerting method. You can either select a webhook, or enter an email address to send alerts to, or both. Only one notification is required to complete configuration.
    * Enter an email address to which {{site.data.keyword.cis_short}} sends alerts. Click the `+` to add the address to the alert. Repeat for all email addresses.
    * Click **Add webhook** and select an available webhook. If no webhooks are present, this option is unavailable.
1. Click **Next**.
1. Select which domains the alert policy monitors.
1. Select which services the alert policy monitors.
1. Click **Create**.

### Editing an alert policy in the UI
{: #ui-edit-alert}

To edit an alert policy:
1. Click the overflow menu of the alert in the **Alerts** section and select **Edit**.
1. Make the changes that you want to the name and description, add or delete email addresses, and add, remove, or edit webhooks.
1. Click **Edit** to save your changes.

### Deleting an alert policy in the UI
{: #ui-delete-alert}

To delete an alert policy:

1. Click the overflow menu of the alert in the **Alerts** section and select **Delete**.
1. Click **Delete** in the confirmation message.

You can delete only alerts that you created.
{: note}

## Configuring alert policies from the CLI
{: #cli-configure-alert}
{: cli}

Configure alert policies from the CLI.

### Listing all alert policies from the CLI
{: #cli-list-alerts}

To list all alert policies from the CLI, run the following command:

```sh
ibmcloud cis alert-policy list [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **-i, --instance value** is the instance name or ID.
* **--output value** specifies the output format; only JSON is supported.

### Getting the details of an alert policy from the CLI
{: #cli-get-details-alert}

To get the details of an alert policy from the CLI, run the following command:

```sh
ibmcloud cis alert-policy get POLICY_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **POLICY_ID** is the ID of alert policy.
* **-i, --instance value** is the instance name or ID.
* **--output value** specifies the output format; only JSON is supported.

### Creating a DDoS Attack Alert from the CLI
{: #cli-create-ddos-alert}

To create a DDoS attack alert policy from the CLI, run the following command:

```sh
ibmcloud cis alert-policy ddos-attack-l7-alert-create --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **--name value** is the name of the alert policy.
* **--description value** is the description for the alert policy.
* **--emails value** is the email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`.
* **--webhooks value** is the webhook IDs for dispatching an alert notification. For example, `--webhooks webhookID1,webhookID2`.
* **--enabled value** determines whether the alert policy is enabled.
* **-i, --instance value** is the instance name or ID.
* **--output value** specifies the output format; only JSON is supported.

### Creating a pool toggle alert from the CLI
{: #cli-create-pool-toggle-alert}

To create a pool toggle alert from the CLI, run the following command:

```sh
ibmcloud cis alert-policy pool-toggle-alert-create --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) --pools POOLS --trigger-condition (enabled | disabled | either) [--include-future-pools (true | false)] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **--name value** is the name of the alert policy.
* **--description value** is the description for the alert policy.
* **--emails value** is the email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`.
* **--webhooks value** is the webhook IDs for dispatching an alert notification. For example, `--webhooks webhookID1,webhookID2`.
* **--enabled value** determines whether the alert policy is enabled.
* **--pools value** is the IDs of origin pool. If set to all, all pool IDs are used.
* **--trigger-condition value** is the condition of pool toggle status.
* **--include-future-pools value** determines whether to include the future pools.
* **-i, --instance value** is the instance name or ID.
* **--output value** specifies the output format; only JSON is supported.

### Creating a security alert from the CLI
{: #cli-create-security-alert}

To create a security alert from the CLI, run the following command:

```sh
ibmcloud cis alert-policy firewall-events-alert-create --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) --domains DOMAINS [--services SERVICES] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **--name value** is the name of the alert policy.
* **--description value** is the description for the alert policy.
* **--emails value** is the email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`.
* **--webhooks value** is the webhook IDs for dispatching an alert notification. For example, `--webhooks webhookID1,webhookID2`.
* **--domains value** is the domain IDs for the alert policy. For example, `--domains domainID1,domainID2`.
* **--services value** specifies which services the alert monitors (for advanced security alerts). Valid services: `country-access-rules`, `waf`, `firewall-rules`, `ratelimit`, `securitylevel`, `ip-access-rules`, `browser-integrity-check`, `ua-rules`,`lockdowns`, `iprange-access-rules`, `asn-access-rules`, `managed-firewall`, `hotlink`, `ssl-validation`. (Enterprise plan only.)
* **--enabled value** determines whether the alert policy is enabled.
* **-i, --instance value** is the instance name or ID.
* **--output value** specifies the output format; only JSON is supported.

Security alerts and advanced security alerts use the same command. When you create an advanced security events alert command in the CLI, specify the services for the alert. If you do not specify the services for the alert, the mean detection time changes from 5 minutes to 2 hours.
{: important}

### Updating a DDoS Attack Alert Policy from the CLI
{: #cli-update-ddos-alert}

To update a DDoS attack alert policy from the CLI, run the following command:

```sh
ibmcloud cis alert-policy ddos-attack-l7-alert-update POLICY_ID [--name NAME] [--emails EMAILS] [--webhooks WEBHOOKS] [--enabled (true | false)] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **POLICY_ID** is the ID of alert policy.
* **--name value** is the name of the alert policy.
* **--description value** is the description for the alert policy.
* **--emails value** is the email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`.
* **--webhooks value** is the webhook IDs for dispatching an alert notification. For example, `--webhooks webhookID1,webhookID2`.
* **--enabled value** determines whether the alert policy is enabled.
* **-i, --instance value** is the instance name or ID.
* **--output value** specifies the output format; only JSON is supported.

### Updating a pool toggle alert policy from the CLI
{: #cli-update-pool-toggle-alert}

To update a pool toggle alert policy from the CLI, run the following command:

```sh
ibmcloud cis alert-policy pool-toggle-alert-update POLICY_ID [--name NAME] [--emails EMAILS] [--webhooks WEBHOOKS] [--enabled (true | false)] [--pools POOLS] [--trigger-condition (enabled | disabled | either)] [--include-future-pools (true | false)] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **--name value** is the name of the alert policy.
* **--description value** is the description for the alert policy.
* **--emails value** is the email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`.
* **--webhooks value** is the webhook IDs for dispatching an alert notification. For example, `--webhooks webhookID1,webhookID2`.
* **--enabled value** determines whether the alert policy is enabled.
* **--pools value** is the IDs of origin pool. If set to all, all pool IDs are used.
* **--trigger-condition value** is the condition of pool toggle status.
* **--include-future-pools value** determines whether to include the future pools.
* **-i, --instance value** is the instance name or ID.
* **--output value** specifies the output format; only JSON is supported.

### Updating a security alert policy from the CLI
{: #cli-update-security-alert}

To update a security alert policy from the CLI, run the following command:

```sh
ibmcloud cis alert-policy firewall-events-alert-update POLICY_ID [--name NAME] [--emails EMAILS] [--webhooks WEBHOOKS] [--enabled (true | false)] [--domains DOMAINS] [--services SERVICES] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

Where:

* **--name value** is the name of the alert policy.
* **--description value** is the description for the alert policy.
* **--emails value** is the email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`.
* **--webhooks value** is the webhook IDs for dispatching an alert notification. For example, `--webhooks webhookID1,webhookID2`.
* **--domains value** is the domain IDs for the alert policy. For example, `--domains domainID1,domainID2`.
* **--services value** specifies which services the alert monitors (Enterprise plan only). Valid services: `country-access-rules`, `waf`, `firewall-rules`, `ratelimit`, `securitylevel`, `ip-access-rules`, `browser-integrity-check`, `ua-rules`, `lockdowns`, `iprange-access-rules`, `asn-access-rules`, `managed-firewall`, `hotlink`, `ssl-validation`.
* **--enabled value** determines whether the alert policy is enabled.
* **-i, --instance value** is the instance name or ID.
* **--output value** specifies the output format; only JSON is supported.

### Deleting an alert policy from the CLI
{: #cli-delete-alert}

To delete an alert policy from the CLI, run the following command:

```sh
ibmcloud cis alert-policy delete POLICY_ID [-i, --instance INSTANCE] [-f, --force]
```
{: pre}

Where:

* **POLICY_ID** is the id of alert policy.
* **-f, --force** attempts to delete alert policy without prompting for confirmation.
* **-i, --instance value** is the instance name or ID.

## Creating an alert policy with the API
{: #api-create-email-notification}
{: api}

To create an email alert, take the following steps:

1. Log in to your {{site.data.keyword.cloud_notm}} account.
2. Get a token.
3. Using that token, run one of the following commands:
    * DDoS attack layer 7
    * Pool toggle alert
    * Security (WAF) alert
    * Advanced security (WAF) alert

### Alert commands
{: #api-alerting-commands}

#### DDoS attack layer 7 command
{: #api-ddos-attack-alert-cmd}

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
    - **alert_type** is the type of the alert (one of `dos_attack_l7`, `load_balancing_pool_enablement_alert`, `clickhouse_alert_fw_anomaly`, `clickhouse_alert_fw_ent_anomaly`, `dedicated_ssl_certificate_event_type`, `universal_ssl_event_type`, `load_balancing_health_alert`, or `web_analytics_metrics_update`).
    - **mechanisms** are at least one of `email`, `webhooks`.
    - **description** (optional) is the description of the alert.

#### Pool toggle alert command
{: #api-pool-toggle-alert-cmd}

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
       },
       "conditions": {
       }}'
```
{: codeblock}

Where:

- **-d** is the array of attributes that are required to create the alert.
    - **name** is the name of the alert.
    - **enabled** is the state of the alert (one of `true`, `false`).
    - **alert_type** is the type of the alert (one of `dos_attack_l7`, `load_balancing_pool_enablement_alert`, `clickhouse_alert_fw_anomaly`, `clickhouse_alert_fw_ent_anomaly`, `dedicated_ssl_certificate_event_type`, `universal_ssl_event_type`, or `load_balancing_health_alert`).
    - **mechanisms** are at least one of `email`, `webhooks`.
    - **description** (optional) is the description of the alert.
    - **filter** is the list of all enablement statuses and pool IDs for the pool toggle alert.
    - **conditions** describe for all pools whether the pool is being enabled, disabled, or both. Content is generated automatically if the field is empty.

#### Security (WAF) alert command
{: #api-waf-alert-command}

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
    - **mechanisms** are at least one of `email`, `webhooks`.
    - **filters** are the list of all zones for the WAF alert.

#### Advanced security (WAF) alert command
{: #api-advanced-waf-command}

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
    - **mechanisms** are at least one of `email`, `webhooks`.
    - **filters** are the list of all services to monitor for security events and zones for the Advanced WAF alert.

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
{: caption="Services that can be monitored by Advanced WAF alerts" caption-side="bottom"}

### Editing alert policies with the API
{: #api-edit-alert}

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

### Deleting alert policies with the API
{: #api-delete-alert}

To delete an email alert, run the following command:

```sh
curl -X DELETE \
  https://api.cis.cloud.ibm.com/v1/:crn/alerting/policies/:policy_id \
  -H 'content-type: application/json' \
  -H 'accept: application/json' \
  -H 'x-auth-user-token: Bearer xxxxxx'
```
{: codeblock}
