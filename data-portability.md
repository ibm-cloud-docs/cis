---

copyright:
  years: 2024, 2025
lastupdated: "2025-01-24"

keywords: CIS

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Understanding data portability for CIS
{: #data-portability}

[Data portability](#x2113280){: term} involves a set of tools and procedures that enable customers to export the digital artifacts that are needed to implement similar workload and data processing on different service providers or on-premises software. It includes procedures for copying and storing the service customer content, including the related configuration that is used by the service to store and process the data, on the customer's own location.
{: shortdesc}

## Responsibilities
{: #data-portability-responsibilities}

{{site.data.keyword.cloud_notm}} services provide interfaces and instructions to guide the customer to copy and store the service customer content, including the related configuration, on their own selected location.

The customer is responsible for the use of the exported data and configuration for data portability to other infrastructures, which includes:

- The planning and execution for setting up alternative infrastructure on different cloud providers or on-premises software that provide similar capabilities to the {{site.data.keyword.IBM_notm}} services.
- The planning and execution for the porting of the required application code on the alternative infrastructure, including the adaptation of customer's application code, deployment automation, and so on.
- The conversion of the exported data and configuration to the format that's required by the alternative infrastructure and adapted applications.

For more information about your responsibilities for CIS, see [Understanding your responsibilities when using CIS](/docs/cis?topic=cis-responsibilities-cis).

## Data export procedures
{: #data-portability-procedures}

CIS provides the mechanisms to export your content that's uploaded, stored, and processed when you use the service.

You can use the CLI and API to export settings and configurations that are used to process the customer's content. For example, you can export global load balancers, DNS records, advanced settings in zones, and page and firewall rules.

You cannot export custom certificates, advanced certificates, or universal certificates that Cloudflare manages for you.

### Exporting CIS data with the CLI and API
{: #cis-export-cli-api}

The following table provides mechanisms to export the settings and configurations that are used to process configuration content through the means of the CIS [CLI](/docs/cis?topic=cis-cis-cli) and [API](/apidocs/cis). The procedures given in the linked documentation should be followed and the output stored to ensure all necessary configuration data is available.

| CLI  | API |
|--------------------|-------------------------|
| [ibmcloud cis access-apps](/docs/cis?topic=cis-cis-cli#access-apps) \n [ibmcloud cis access-certificates](/docs/cis?topic=cis-cis-cli#access-certificates) \n [ibmcloud cis access-policies](/docs/cis?topic=cis-cis-cli#access-policies) \n [ibmcloud cis alert-webhooks](/docs/cis?topic=cis-cis-cli#list-alert-webhooks) \n  [ibmcloud cis authenticated-origin-pull-certificates](/docs/cis?topic=cis-cis-cli#show-authenticated-origin-pull-certificates) \n [ibmcloud cis certificates](/docs/cis?topic=cis-cis-cli#list-cert) \n [ibmcloud cis dns-records](/docs/cis?topic=cis-cis-cli#list-dns-records) \n [ibmcloud cis domains](/docs/cis?topic=cis-cis-cli#list-domain) \n [ibmcloud cis edge-functions-actions](/docs/cis?topic=cis-cis-cli#list-edge-functions-actions) \n [ibmcloud cis edge-functions-triggers](/docs/cis?topic=cis-cis-cli#list-edge-functions-triggers) \n [ibmcloud cis firewalls](/docs/cis?topic=cis-cis-cli#list-firewall) \n [ibmcloud cis glb-events](/docs/cis?topic=cis-cis-cli#get-glb-events) \n  [ibmcloud cis glb-monitors](/docs/cis?topic=cis-cis-cli#list-glb-monitors) \n [ibmcloud cis glb-pools](/docs/cis?topic=cis-cis-cli#list-glb-pools) \n [ibmcloud cis glbs](/docs/cis?topic=cis-cis-cli#list-glb) \n [ibmcloud cis instances](/docs/cis?topic=cis-cis-cli#list-cis-service-instances) \n [ibmcloud cis origin-certificates](/docs/cis?topic=cis-cis-cli#origin-certificates) \n [ibmcloud cis page-rules](/docs/cis?topic=cis-cis-cli#page-rules) \n [ibmcloud cis ratelimit-rules](/docs/cis?topic=cis-cis-cli#list-ratelimit-rules) \n [ibmcloud cis waf-groups](/docs/cis?topic=cis-cis-cli#list-waf-groups) \n [ibmcloud cis cis waf-overrides](/docs/cis?topic=cis-cis-cli#list-waf-overrides) \n [ibmcloud cis waf-packages](/docs/cis?topic=cis-cis-cli#list-waf-packages) \n [ibmcloud cis waf-rules](/docs/cis?topic=cis-cis-cli#list-waf-rules) \n [ibmcloud cis alert-policy list](/docs/cis?topic=cis-cis-cli#list-alert-policies) \n [ibmcloud cis advanced-rate-limiting rules](/docs/cis?topic=cis-cis-cli#list-rules) \n [ibmcloud cis managed-waf rulesets](/docs/cis?topic=cis-cis-cli#list-rulesets) \n [ibmcloud cis managed-waf deployments](/docs/cis?topic=cis-cis-cli#list-deployments) | [list access apps](/apidocs/cis#list-access-applications) \n [list access certificates](/apidocs/cis#list-access-certificates) \n [list access policies](/apidocs/cis#list-access-policies) \n   \n [list alert webhooks](/apidocs/cis?code=python#list-alert-webhooks) \n list authenticated origin pull certificates \n [list certificates](/apidocs/cis#list-certificates) \n [list dns records](/apidocs/cis#list-all-dns-records) \n [list zones](/apidocs/cis#list-zones) \n [get edge functions actions](/apidocs/cis#list-edge-functions-actions) \n [list edge functions triggers](/apidocs/cis#list-edge-functions-triggers) \n [list firewall rules](/apidocs/cis#listallfirewallrules) \n  [list glb events](/apidocs/cis#get-load-balancer-events) \n [list glb monitors](/apidocs/cis#list-all-load-balancer-monitors) \n [list glb pools](/apidocs/cis#list-all-load-balancer-pools) \n [list glbs](/apidocs/cis#list-all-load-balancers) \n [list instance rulesets](/apidocs/cis#get-instance-rulesets) \n [list origin certificates](/apidocs/cis#list-origin-certificates) \n [list page rules](/apidocs/cis#list-page-rules) \n [list zone rate limits](/apidocs/cis#list-all-zone-rate-limits) \n [list waf rule groups](/apidocs/cis#list-waf-rule-groups) \n list waf overrides \n [list waf rule packages](/apidocs/cis#list-waf-packages) \n [list waf rules](/apidocs/cis#list-waf-rules) \n [list alert policies](/apidocs/cis?code=python#list-alert-policies) \n list advanced rate limiting rules \n [list waf rules](/apidocs/cis#list-waf-rules) \n list waf deployments |
{: caption="Exporting CIS data with the CLI and API" caption-side="bottom"}

## Exported data formats
{: #data-portability-data-formats}

CIS supports the following data format and schema of the exported data, configuration, and application:

* Export in JSON format only

   * Example CLI using the [ibmcloud cis glbs](/docs/cis?topic=cis-cis-cli#list-glb) command:

   ```sh
   ibmcloud cis glbs DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
   ```
   {: pre}

   * Example API request using the [list-all-load-balancers](/apidocs/cis#list-all-load-balancers) API:

      ```curl
      curl -X GET https://api.cis.cloud.ibm.com/v1/:crn/zones/:zone_id/load_balancers \
      -H 'content-type: application/json' \
      -H 'x-auth-user-token: Bearer xxxxxx'
      ```
      {: codeblock}

CIS doesn't support the export of other data formats and other schema of the exported data, configuration, and application, including the following:

* Exporting [zone files](https://en.wikipedia.org/wiki/Zone_file){: external}

## Data ownership
{: #data-portability-ownership}

All exported data is classified as customer content. Apply the full customer ownership and licensing rights, as stated in the [IBM Cloud Service Agreement](https://www.ibm.com/support/customer/csol/terms/?id=Z126-6304_WS){: external}.
