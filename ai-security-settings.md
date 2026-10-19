---

copyright:
  years: 2026
lastupdated: "2026-10-19"

keywords: AI security settings, enable AI security, disable AI security, cf-llm, ibmcloud cis ai-security, ibm_cis_ai_security_settings

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}



# Managing AI security for apps settings
{: #ai-security-settings}

Enable AI security for apps on your zone to allow {{site.data.keyword.cis_full_notm}} (CIS) to scan traffic to endpoints that carry the `cf-llm` label. You can also disable it at any time.
{: shortdesc}

[Endpoint Management (all plans) and AI Security for Apps](/docs/cis?topic=cis-release-notes#cis-october-1926) and its mitigation features (Enterprise plans only) are available for evaluation and testing. These features are provided at no additional charge during the beta period. To provide feedback or report issues, open a support case in the [IBM Cloud Support Center](/docs/support?topic=support-open-case&interface=ui). For IBM internal users, post in [#ibmcloud-cis](https://ibm.enterprise.slack.com/archives/C8XKQ9FPB).
{: beta}

AI security for apps is available only on Enterprise {{site.data.keyword.cis_short_notm}} plans.
{: important}

## Managing AI security for apps settings in the console
{: #ai-security-settings-ui}
{: ui}

### Viewing the current setting in the console
{: #ai-security-settings-get-ui}

1. In the {{site.data.keyword.cloud_notm}} console, go to your {{site.data.keyword.cis_short_notm}} instance.
1. Go to **Security** > **Endpoint management**.
1. Check the **AI Security for Apps** tile to view the current enabled or disabled state.

### Enabling or disabling AI security for apps in the console
{: #ai-security-settings-update-ui}

1. In the {{site.data.keyword.cloud_notm}} console, go to your {{site.data.keyword.cis_short_notm}} instance.
1. Go to **Security** > **Endpoint management**.
1. Set the **AI Security for Apps** toggle to **Enabled** or **Disabled**.

## Managing AI security for apps settings from the CLI
{: #ai-security-settings-cli}
{: cli}

### Viewing the current setting from the CLI
{: #ai-security-settings-get-cli}

To view the current AI security for apps setting from the CLI, follow these steps:

1. [Set up your CLI environment](/docs/cis?topic=cis-cis-cli#-cli-prereqs).
1. Log in to your account from the CLI. After you enter the password, the system prompts for the account and region that you want to use:

   ```sh
   ibmcloud login --sso
   ```
   {: pre}

1. Run the following command to view the current setting:

   ```sh
   ibmcloud cis ai-security settings DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
   ```
   {: pre}

#### Command options
{: #ai-security-settings-get-cli-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

### Enabling or disabling AI security for apps from the CLI
{: #ai-security-settings-update-cli}

To enable or disable AI security for apps from the CLI, follow these steps:

1. [Set up your CLI environment](/docs/cis?topic=cis-cis-cli#-cli-prereqs).
1. Log in to your account from the CLI. After you enter the password, the system prompts for the account and region that you want to use:

   ```sh
   ibmcloud login --sso
   ```
   {: pre}

1. Run the following command to update the setting:

   ```sh
   ibmcloud cis ai-security settings-update DNS_DOMAIN_ID (--enabled true|false) [-i, --instance INSTANCE]
   ```
   {: pre}

#### Command options
{: #ai-security-settings-update-cli-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--enabled`
:   Set to `true` to enable AI security for apps on the zone, or `false` to disable it. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

## Managing AI security for apps settings with the API
{: #ai-security-settings-api}
{: api}

To call these methods, you must be assigned one or more IAM access roles:

* `internet-svcs.zones.read`
* `internet-svcs.zones.update`

You can check your access by going to **Manage** > **Access (IAM)** > **Users** > **_User name_** > **Access**.
{: tip}

### Viewing the current setting with the API
{: #ai-security-settings-get-api}

To view the current AI security for apps setting with the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following variables to be used in the API command:

   * `crn`: The full URL-encoded CRN of the service instance.
   * `zone_identifier`: The zone identifier.

1. When all variables are set, run the following command to get the current setting:

   ```sh
   curl -X GET \
     https://api.cis.cloud.ibm.com/v1/:crn/zones/:zone_identifier/ai-security/settings \
     -H 'content-type: application/json' \
     -H 'accept: application/json' \
     -H 'x-auth-user-token: Bearer xxxxxx'
   ```
   {: pre}

   The following response is returned:

   ```json
   {
     "result": {
       "enabled": false
     },
     "success": true,
     "errors": [],
     "messages": []
   }
   ```
   {: screen}

### Enabling or disabling AI security for apps with the API
{: #ai-security-settings-update-api}

To enable or disable AI security for apps with the API, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following variables to be used in the API command:

   * `crn`: The full URL-encoded CRN of the service instance.
   * `zone_identifier`: The zone identifier.
   * `enabled`: Set to `true` to enable AI security for apps, or `false` to disable it.

1. When all variables are set, run the following command to update the setting:

   ```sh
   curl -X PUT \
     https://api.cis.cloud.ibm.com/v1/:crn/zones/:zone_identifier/ai-security/settings \
     -H 'content-type: application/json' \
     -H 'accept: application/json' \
     -H 'x-auth-user-token: Bearer xxxxxx' \
     -d '{"enabled": true}'
   ```
   {: pre}

   The following response is returned:

   ```json
   {
     "result": {
       "enabled": true
     },
     "success": true,
     "errors": [],
     "messages": []
   }
   ```
   {: screen}

## Managing AI security for apps settings with Terraform
{: #ai-security-settings-terraform}
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

### Viewing the current setting with Terraform
{: #ai-security-settings-get-terraform}

To view the current AI security for apps setting with Terraform, follow these steps:

1. Add the `ibm_cis_ai_security_settings` data source to your configuration:

   ```terraform
   data "ibm_cis_ai_security_settings" "ai_sec_read" {
     cis_id    = data.ibm_cis.cis.id
     domain_id = data.ibm_cis_domain.cis_domain.domain_id
   }

   output "ai_security_enabled" {
     value = data.ibm_cis_ai_security_settings.ai_sec_read.enabled
   }
   ```
   {: codeblock}

1. Run `terraform apply`. The `enabled` attribute returns `true` when AI security for apps is enabled on the zone.

For more information about the arguments and attributes, see [`ibm_cis_ai_security_settings`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/data-sources/cis_ai_security_settings){: external} in the Terraform registry.

### Enabling or disabling AI security for apps with Terraform
{: #ai-security-settings-update-terraform}

To enable or disable AI security for apps with Terraform, follow these steps:

1. Add the `ibm_cis_ai_security_settings` resource to your configuration. Set `enabled` to `true` to enable AI security for apps, or `false` to disable it:

   ```terraform
   resource "ibm_cis_ai_security_settings" "ai_sec" {
     cis_id    = data.ibm_cis.cis.id
     domain_id = data.ibm_cis_domain.cis_domain.domain_id
     enabled   = true
   }
   ```
   {: codeblock}

1. Run `terraform apply`.

If you do not set the `enabled` argument, it defaults to `false`.
{: note}

Running `terraform destroy` disables AI security for apps on the zone by setting `enabled` to `false`.
{: note}

To read the setting after the resource is created, add `depends_on` to the data source so that Terraform reads the setting only after the resource is applied:

```terraform
data "ibm_cis_ai_security_settings" "ai_sec_read" {
  cis_id    = data.ibm_cis.cis.id
  domain_id = data.ibm_cis_domain.cis_domain.domain_id

  depends_on = [ibm_cis_ai_security_settings.ai_sec]
}
```
{: codeblock}

For more information about the arguments and attributes, see [`ibm_cis_ai_security_settings`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_ai_security_settings){: external} in the Terraform registry.

### Importing the AI security for apps setting with Terraform
{: #ai-security-settings-import-terraform}

To import an existing AI security for apps setting into Terraform state, run the following command, where `<domain_id>` is the 32-character zone ID and `<crn>` is the CRN of the service instance:

```sh
terraform import ibm_cis_ai_security_settings.ai_sec <domain_id>:<crn>
```
{: pre}

## Related resources
{: #ai-security-settings-related}

- [About AI security for apps](/docs/cis?topic=cis-ai-security-overview)
- [Getting started with AI security for apps](/docs/cis?topic=cis-ai-security-getting-started)
- [Labeling endpoints](/docs/cis?topic=cis-endpoint-management-labeling)
- [About endpoint management](/docs/cis?topic=cis-endpoint-management-overview)


