---

copyright:
  years: 2021, 2025
lastupdated: "2025-08-29"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Configuring alert policies
{: #configuring-policies}

{{site.data.keyword.cis_full}} has alerts that you can configure through the API to warn you when events occur.
{: shortdesc}

See [Configuring webhooks](/docs/cis?topic=cis-configuring-webhooks) for instructions on using webhooks.

Alerts are available only to Enterprise plans.
{: note}

## Configuring alert policies in the console
{: #ui-configure-alert-policies}
{: ui}

Use the UI to create, update, and delete alerting policies.

### Creating a security alert policy in the console
{: #ui-create-alert}

To create a security alert policy, follow these steps:

1. In the CIS console, navigate to the **Account** page.
1. Select the **Alerts** tab.
1. Select the **Alerting policies** and then click **Create**
1. Select the type of alert policy that you want to create. For more information, see [Alert types](/docs/cis?topic=cis-types-alerts) to select alert policies.
1. Enter a name for your alerting policy, and optionally enter a description.
1. Choose an alerting method. You can select a webhook, enter an email address to send alerts to, or both. Only one notification is required to complete configuration.
    * Enter an email address to which {{site.data.keyword.cis_short}} sends alerts. Click the `+` to add the address to the alert. Repeat for all email addresses.
    * Click **Add webhook** and select an available webhook. If no webhooks are present, this option is unavailable.
1. Click **Create**.

By default, alert policies are enabled when created. You can disable alerts that you created by switching the toggle in the **Enabled** column.

### Creating an advanced security alert policy in the console
{: #ui-create-advanced-security-alert}

To create an advanced security alert, take these steps:

1. In the CIS console, navigate to the **Account** page.
1. Select the **Alerts** tab.
1. Select the **Alerting policies** and then click **Create**
1. Select **Advanced security events alert** and then click **Next**.
1. Enter a name for your alerting policy, and optionally enter a description.
1. Choose an alerting method. You can either select a webhook, or enter an email address to send alerts to, or both. Only one notification is required to complete configuration.
    * Enter an email address to which {{site.data.keyword.cis_short}} sends alerts. Click the `+` to add the address to the alert. Repeat for all email addresses.
    * Click **Add webhook** and select an available webhook. If no webhooks are present, this option is unavailable.
1. Click **Next**.
1. Select which domains the alert policy monitors.
1. Select which services the alert policy monitors.
1. Click **Create**.

### Editing an alert policy in the console
{: #ui-edit-alert}

To edit an alert policy, follow these steps:
1. In the CIS console, navigate to the **Account** page.
1. Select the **Alerts** tab.
1. In the **Alerting policies**, locate the alert policy that you want to edit, then click the Actions menu on the right of the row.
1. Click **Edit** to save your changes.
1. Make the change that you want to the name and description, add or delete email addresses, and add, remove, or edit webhooks.
1. Click **Save**.

### Deleting an alert policy in the console
{: #ui-delete-alert}

To delete an alert policy, follow these steps:

1. In the CIS console, navigate to the **Account** page.
1. Select the **Alerts** tab.
1. In the **Alerting policies**, locate the alert policy that you want to delete, then click the Actions menu on the right of the row.
1. Click **Delete** in the confirmation message.

You can delete only alerts that you created.
{: note}

## Configuring alert policies from the CLI
{: #cli-configure-alert}
{: cli}

You can create email alerts for each alert type by using the CLI.

### Listing all alert policies from the CLI
{: #cli-list-alerts}

To list all alert policies from the CLI, run the following command:

```sh
ibmcloud cis alert-policy list [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #command-options-listing}

`-i, --instance`
:   The instance name or ID.

`--output`
:   Specifies the output format; only JSON is supported.

### Getting the details of an alert policy from the CLI
{: #cli-get-details-alert}

To get the details of an alert policy from the CLI, run the following command:

```sh
ibmcloud cis alert-policy get POLICY_ID [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #command-options-getting}

`POLICY_ID`
:   The ID of alert policy.

`-i, --instance`
:   The instance name or ID.

`--output`
:   Specifies the output format; only JSON is supported.

### Creating a DDoS Attack Alert from the CLI
{: #cli-create-ddos-alert}

To create a DDoS attack alert policy from the CLI, run the following command:

```sh
ibmcloud cis alert-policy ddos-attack-l7-alert-create --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #command-options-ddos-attack}

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`.

`--webhooks`
:   The webhook IDs for dispatching an alert notification. For example, `--webhooks webhookID1,webhookID2`.

`--enabled`
:   Determines whether the alert policy is enabled.

`-i, --instance`
:   The instance name or ID.

`--output`
:   Specifies the output format; only JSON is supported.

### Creating a pool toggle alert from the CLI
{: #cli-create-pool-toggle-alert}

To create a pool toggle alert from the CLI, run the following command:

```sh
ibmcloud cis alert-policy pool-toggle-alert-create --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) --pools POOLS --trigger-condition (enabled | disabled | either) [--include-future-pools (true | false)] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #command-options-pool-toggle}

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`.

`--webhooks value`
:   The webhook IDs for dispatching an alert notification. For example, `--webhooks webhookID1,webhookID2`.

`--enabled`
:   Determines whether the alert policy is enabled.

`--pools`
:   The IDs of origin pool. If set to all, all pool IDs are used.

`--trigger-condition`
:   The condition of the pool toggle status.

`--include-future-pools`
:   Determines whether to include the future pools.

`-i, --instance`
:   The instance name or ID.

`--output`
Specifies the output format; only JSON is supported.

### Creating a security alert from the CLI
{: #cli-create-security-alert}

Create an alert policy about spikes in firewall events. Firewall events alerts use a z-score calculation over the last six hours and five-minute buckets of events. An alert is triggered whenever the z-score is more than 3.5 (the threshold). Duplicate alerts are not recieved within the same two-hour time frame.

To create a security alert from the CLI, run the following command:

```sh
ibmcloud cis alert-policy firewall-events-alert-create --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) --domains DOMAINS [--services SERVICES] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #command-options-alert-security}

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`.

`--webhooks`
:   The webhook IDs for dispatching an alert notification. For example, `--webhooks webhookID1,webhookID2`.

`--domains`
:   The domain IDs for the alert policy. For example, `--domains domainID1,domainID2`.

`--services`
:   Specifies which services the alert monitors (for advanced security alerts). Valid services: `country-access-rules`, `waf`, `firewall-rules`, `ratelimit`, `securitylevel`, `ip-access-rules`, `browser-integrity-check`, `ua-rules`,`lockdowns`, `iprange-access-rules`, `asn-access-rules`, `managed-firewall`, `hotlink`, `ssl-validation`. (Enterprise plan only.)

`--enabled`
:   Determines whether the alert policy is enabled.

`-i, --instance`
:   The instance name or ID.

`--output`
:   Specifies the output format; only JSON is supported.

Security alerts and advanced security alerts use the same command. When you create an advanced security events alert command in the CLI, specify the services for the alert. If you do not specify the services for the alert, the mean detection time changes from 5 minutes to 2 hours.
{: important}

### Creating Universal SSL alert command
{: #cli-universal-ssl-alert-cmd}

To create an alert policy for certificate events, run the following command:

```sh
ibmcloud cis alert-policy certificate-alert-create --type (universal | dedicated) --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #command-options-ssl-alert}

`--type`
:   The type of the certificate.

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`.

`--webhooks`
:   The webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`.

`--enabled`
:   Sets whether the alert policy is enabled.

`-i, --instance`
:   The instance name or ID. If not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   Specifies the output format; only JSON is supported.

### Load balancing health check alert command
{: #cli-lb-health-check-alert-cmd}

To create an alert policy for changes in health status for global load balancer, pools, and origins, run the following command:

```sh
ibmcloud cis alert-policy glb-healthcheck-alert-create --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) --pools POOLS [--include-future-pools (true | false)] [--health-status-trigger (healthy | unhealthy | either)] [--event-source-trigger (pool | origin | either)] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #command-load-balancing}

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`.

`--webhooks`
:   The webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`.

`--enabled`
:   Sets whether the alert policy is enabled.

`--pools`
:   The IDs of origin pool. If set to `all`, all the pool IDs are used.

`--include-future-pools`
:   Sets whether include the future pools (default "false").

`--health-status-trigger`
:   The trigger condition to fire the notification. Valid values: "healthy", "unhealthy", "either" (default "either").

`--event-source-trigger`
:   The event source of trigger to fire the notification. Valid values: "pool", "origin", "either" (default "either").

`-i, --instance`
:   The instance name or ID. If not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   Specifies the output format; only JSON is supported.

### Updating a DDoS Attack Alert Policy from the CLI
{: #cli-update-ddos-alert}

To update a DDoS attack alert policy from the CLI, run the following command:

```sh
ibmcloud cis alert-policy ddos-attack-l7-alert-update POLICY_ID [--name NAME] [--emails EMAILS] [--webhooks WEBHOOKS] [--enabled (true | false)] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #command-options-updating-ddos}

`POLICY_ID`
:   The ID of alert policy.

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`.

`--webhooks`
:   The webhook IDs for dispatching an alert notification. For example, `--webhooks webhookID1,webhookID2`.

`--enabled`
:   Determines whether the alert policy is enabled.

`-i, --instance`
:   The instance name or ID.

`--output`
:   Specifies the output format; only JSON is supported.

### Updating a pool toggle alert policy from the CLI
{: #cli-update-pool-toggle-alert}

To update a pool toggle alert policy from the CLI, run the following command:

```sh
ibmcloud cis alert-policy pool-toggle-alert-update POLICY_ID [--name NAME] [--emails EMAILS] [--webhooks WEBHOOKS] [--enabled (true | false)] [--pools POOLS] [--trigger-condition (enabled | disabled | either)] [--include-future-pools (true | false)] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #command-options-update-pool}

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`.

`--webhooks`
:   The webhook IDs for dispatching an alert notification. For example, `--webhooks webhookID1,webhookID2`.

`--enabled`
:   Determines whether the alert policy is enabled.

`--pools`
:   The IDs of origin pool. If set to all, all pool IDs are used.

`--trigger-condition`
:   The condition of pool toggle status.

`--include-future-pools`
:   Determines whether to include the future pools.

`-i, --instance`
:   The instance name or ID.

`--output`
:   Specifies the output format; only JSON is supported.

### Updating a security alert policy from the CLI
{: #cli-update-security-alert}

To update a security alert policy from the CLI, run the following command:

```sh
ibmcloud cis alert-policy firewall-events-alert-update POLICY_ID [--name NAME] [--emails EMAILS] [--webhooks WEBHOOKS] [--enabled (true | false)] [--domains DOMAINS] [--services SERVICES] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

#### Command options
{: #command-options-update-security}

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`.

`--webhooks`
:   The webhook IDs for dispatching an alert notification. For example, `--webhooks webhookID1,webhookID2`.

`--domains`
:   The domain IDs for the alert policy. For example, `--domains domainID1,domainID2`.

`--services`
:   Specifies which services the alert monitors (Enterprise plan only). Valid services: `country-access-rules`, `waf`, `firewall-rules`, `ratelimit`, `securitylevel`, `ip-access-rules`, `browser-integrity-check`, `ua-rules`, `lockdowns`, `iprange-access-rules`, `asn-access-rules`, `managed-firewall`, `hotlink`, `ssl-validation`.

`--enabled`
:   Determines whether the alert policy is enabled.

`-i, --instance`
:   The instance name or ID.

`--output`
:   Specifies the output format; only JSON is supported.

### Deleting an alert policy from the CLI
{: #cli-delete-alert}

To delete an alert policy from the CLI, run the following command:

```sh
ibmcloud cis alert-policy delete POLICY_ID [-i, --instance INSTANCE] [-f, --force]
```
{: pre}

#### Command options
{: #command-options-delete-alert}

`POLICY_ID`
:   The id of alert policy.

`-f, --force`
:   Attempts to delete alert policy without prompting for confirmation.

`-i, --instance`
:   The instance name or ID.

## Creating an alert policy with the API
{: #api-create-email-notification}
{: api}

To create an email alert, follow these steps:

1. Log in to your {{site.data.keyword.cloud_notm}} account.
2. Get a token.
3. Using that token, run one of the following commands:
    * DDoS attack layer 7
    * Pool toggle alert
    * Security (WAF) alert
    * Advanced security (WAF) alert

### Creating DDoS attack layer 7 command with the API
{: #api-ddos-attack-alert-cmd}

To create the DDoS attack layer 7, run the following command:

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

### Creating pool toggle alert command with API
{: #api-pool-toggle-alert-cmd}

To create the pool toggle alert, run the following command:

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

### Creating security (WAF) alert command with the API
{: #api-waf-alert-command}

To create a WAF alert, run the following command:

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

#### Creating advanced security (WAF) alert command with the API
{: #api-advanced-waf-command}

To create an Advanced WAF alert, run the following command:

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

### Creating universal SSL alert command
{: #api-universal-ssl-alert-cmd}

To create a Universal SSL alert, run the following command:

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

### Creating load balancing health check alert command
{: #api-lb-health-check-alert-cmd}

To create a load balancing health check alert, run the following command:

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
