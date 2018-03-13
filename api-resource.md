---

copyright:
  years: 2018
lastupdated: "2018-02-26"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# API Specs

Here's how to view the CIS API specifications: 

1. To view CIS APIs, navigate to the [CIS API Spec](https://pages.github.ibm.com/NetworkTribe/cis-api-spec/#/) page. 

2. Select an API category from the dropdown list near the top right corner of this page to view the details.


## Notes

1. API endpoints: https://api.cis.cloud.ibm.com (Production), https://api.stage.cis.cloud.ibm.com (Staging).

2. **X-Auth-User-Token** header is required for each API call. This is the bearer token for the user that can be retrieved from IAM (for example, using the "bx iam oauth-tokens" command).

3. The **crn** field is also required in the path for each API call. This is the full Cloud Resource Name (CRN) for a CIS resource instance that is being configured (for example, the CRN for a resource instance can be retrieved from its name using the command "bx resource service-instance <instance-name>"). The CRN must be URL encoded in the API call.

4. API calls are rate limited. A total of 100 API calls can be made in 1 minute. If this rate is exceeded, subsequent calls will be blocked for a period of time.

## Available APIs

Here is the list of CIS API specs available to view.

* CIS_Frontend_API_Spec-Cache.yaml
* CIS_Frontend_API_Spec-DNSRecords.yaml
* CIS_Frontend_API_Spec-Firewall.yaml
* CIS_Frontend_API_Spec-FirewallEvents.yaml
* CIS_Frontend_API_Spec-GLB.yaml
* CIS_Frontend_API_Spec-GLB_Monitor.yaml
* CIS_Frontend_API_Spec-GLB_Pool.yaml
* CIS_Frontend_API_Spec-Metric.yaml
* CIS_Frontend_API_Spec-Overview.yaml
* CIS_Frontend_API_Spec-Page_Rules.yaml
* CIS_Frontend_API_Spec-SSL.yaml
* CIS_Frontend_API_Spec-WAF.yaml
* CIS_Frontend_API_Spec-ZoneSettings.yaml
* CIS_Frontend_API_Spec-Zones.yaml
