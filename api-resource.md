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

1. To view CIS APIs, navigate to the [CIS API Spec](https://developer.ibm.com/api/view/cis-prod:cloud-internet-services:title-Cloud_Internet_Services) page. 

2. From the left navigation menu, select **Documentation** to view available APIs.


## Notes

1. API endpoints: https://api.cis.cloud.ibm.com (Production), https://api.stage.cis.cloud.ibm.com (Staging).

2. **X-Auth-User-Token** header is required for each API call. This is the bearer token for the user that can be retrieved from IAM (for example, using the "bx iam oauth-tokens" command).

3. The **crn** field is also required in the path for each API call. This is the full Cloud Resource Name (CRN) for a CIS resource instance that is being configured (for example, the CRN for a resource instance can be retrieved from its name using the command "bx resource service-instance <instance-name>"). The CRN must be URL encoded in the API call.

4. API calls are rate limited. A total of 100 API calls can be made in 1 minute. If this rate is exceeded, subsequent calls will be blocked for a period of time.
