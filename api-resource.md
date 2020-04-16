---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: API Specs, CIS APIs

subcollection: cis

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:term: .term}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}


# API specs
{:#api-specs}

Here's how to view the {{site.data.keyword.cis_full}} API specifications:
  1. To view the {{site.data.keyword.cis_short_notm}} APIs, navigate to the [API Docs](/apidocs/) page.
  1. From the left navigation menu, check the Networking box to filter the APIs.
  1. Choose from the list of available {{site.data.keyword.cis_short_notm}} APIs.
{:shortdesc}


## Notes
{:#api-notes}

1. API endpoint: `https://api.cis.cloud.ibm.com`.

2. The **X-Auth-User-Token** header is required for each API call. This header is the bearer token for the user, which can be retrieved from IAM (for example, using the `ibmcloud iam oauth-tokens` command).

3. The **crn** field is also required in the path for each API call. This field contains the full Cloud Resource Name (CRN) for a CIS resource instance that is being configured. (For example, the CRN for a resource instance can be retrieved from its name using the command `ibmcloud resource service-instance <instance-name>`). The CRN must be URL encoded in the API call.

4. API calls are rate limited. A total of 100 API calls can be made in 1 minute. If this rate is exceeded, subsequent calls are blocked for a period of time.
