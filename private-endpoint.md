---

copyright:
  years: 2021
lastupdated: "2021-05-04"

keywords:

subcollection: cis

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}
{:external: target="_blank" .external}
{:support: data-reuse='support'}
{:help: data-hd-content-type='help'}

# Enabling private endpoints for API
{: #private-endpoint-for-cis}

<!--{{site.data.keyword.cloud}} private endpoints enable you to connect to supported {{site.data.keyword.cloud_notm}} services by using IP addresses of your choosing.-->

<!--## Using the CLI-->
<!-- {: #cli-private-endpoint}-->

<!--After creating an endpoint gateway for {{site.data.keyword.cis_short_notm}}, follow these steps:-->

<!--1. Update the {{site.data.keyword.cloud_notm}} CLI to the latest version:-->

<!--   ```sh-->
<!--   ibmcloud update-->
<!--   ```-->
<!--{: pre}   --> 
   
<!--1. Update the {{site.data.keyword.cis_short_notm}} CLI plug-in:-->

<!--   ```sh-->
<!--   ibmcloud plugin update cis-cli-->
<!--   ```-->
<!--    {: pre}-->

<!--## Using the API-->
<!-- {: #vpe-setup-api}-->
 
Use the service endpoint's FQDN `api.private.cis.cloud.ibm.com` in the URL to access the service. For example:

```sh
curl https://api.private.cis.cloud.ibm.com/v1/:crn/zones -H 'content-type: application/json' -H 'accept: application/json' -H 'x-auth-user-token: Bearer xxxxxx'
```
{: pre}

