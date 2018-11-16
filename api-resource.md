---

copyright:
  years: 2018
lastupdated: "2018-11-16"

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

1. To view the CIS APIs, navigate to the [API Docs](../../bluemix.net/apidocs/) page. 

2. From the left navigation menu, check the Networking box to filter the APIs.

3. Choose from the list of available Cloud Internet Services APIs.


## Notes

1. API endpoint: `https://api.cis.cloud.ibm.com`.

2. The **X-Auth-User-Token** header is required for each API call. This header is the bearer token for the user, which can be retrieved from IAM (for example, using the `ibmcloud iam oauth-tokens` command).

3. The **crn** field is also required in the path for each API call. This field contains the full Cloud Resource Name (CRN) for a CIS resource instance that is being configured. (For example, the CRN for a resource instance can be retrieved from its name using the command `ibmcloud resource service-instance <instance-name>`). The CRN must be URL encoded in the API call.

4. API calls are rate limited. A total of 100 API calls can be made in 1 minute. If this rate is exceeded, subsequent calls are blocked for a period of time.
