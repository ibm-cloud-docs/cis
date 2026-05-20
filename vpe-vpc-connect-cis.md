---

copyright:
  years: 2026
lastupdated: "2026-05-20"

keywords: vpe, virtual private endpoints

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Using virtual private endpoints for VPC to privately connect to {{site.data.keyword.cis_short_notm}}
{: #vpe-connection-cis}

{{site.data.keyword.cloud}} Virtual Private Endpoints (VPE) for VPC enables private connectivity from your VPC network to {{site.data.keyword.cis_short_notm}} by using the IP addresses of your choosing that are allocated from a subnet within your VPC.
{: shortdesc}

VPEs are virtual IP interfaces that are bound to an endpoint gateway created on a per service, or service instance, basis (depending on the service operation model). VPEs are virtual IP interfaces that are bound to an endpoint gateway created on a per service, or service instance, basis (depending on the service operation model). The endpoint gateway is a virtualized component that scales horizontally, is redundant, highly available, and spans all availability zones in your VPC. VPE gateways enable communication between virtual server instances in your VPC and cloud services. VPE for VPC gives you the experience of controlling all the private addressing within your cloud. For more information, see [About virtual private endpoint gateways](/docs/vpc?topic=vpc-about-vpe).

## Before you begin
{: #prereq-service-endpoint-cis}

Before you target a VPE for {{site.data.keyword.cis_short_notm}}, you must complete the following tasks.

* Ensure that a [Virtual Private Cloud is created](/docs/vpc?topic=vpc-getting-started).
* Make a plan for your [virtual private endpoints](/docs/vpc?topic=vpc-planning-considerations).
* Ensure that [correct access controls](/docs/vpc?topic=vpc-configure-acls-sgs-endpoint-gateways&interface=ui#vpe-configuring-acls) are set for your VPE.
* Review VPE [limitations](/docs/vpc?topic=vpc-limitations-vpe).

## Setting up a VPE for {{site.data.keyword.cis_short_notm}}
{: #endpoint-setup-cis}

When you create a VPE by using the CLI or API, use the following CRN information.

| Location | Region | Cloud Resource Name (CRN) |
| --------- | ------- | ---------------- |
| Global | `global` | `crn:v1:bluemix:public:internet-svcs:global::::` |
{: caption="Region availability and Cloud Resource Names (CRNs) for connecting {{site.data.keyword.cis_short_notm}} over {{site.data.keyword.cloud_notm}} private networks" caption-side="bottom"}

### Configuring an endpoint gateway
{: #endpoint-gateway-cis}

To configure a VPE gateway, follow these steps:

1. List the available services, including IBM Cloud infrastructure services that are available by default to all VPC users.
1. [Create an endpoint gateway](/docs/vpc?topic=vpc-ordering-endpoint-gateway) for {{site.data.keyword.cis_short_notm}} that you want to be privately available to the VPC.
1. [Bind a reserved IP address](/docs/vpc?topic=vpc-bind-unbind-reserved-ip) to the endpoint gateway.
1. View the created VPE gateways associated with the {{site.data.keyword.cis_short_notm}} instance. For more information, see [Viewing details of an endpoint gateway](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway).

Now your virtual server instances in the VPC can privately access your {{site.data.keyword.cis_short_notm}} instance through the VPE gateway.

## Using an endpoint gateway for {{site.data.keyword.cis_short_notm}}
{: #using-cis-vpe}

After you create a VPE for {{site.data.keyword.cis_short_notm}}, follow these steps:

### Using an endpoint gateway from the CLI
{: #vpe-cis-cli}
{: cli}

To update to the latest version of the CLI and the {{site.data.keyword.cis_short_notm}} plug-in, follow these steps:

1. Update the {{site.data.keyword.cloud_notm}} CLI to the latest version:

   ```sh
   ibmcloud update
   ```
   {: pre}

1. Update the {{site.data.keyword.cis_short_notm}} CLI plug-in:

   ```sh
   ibmcloud plugin update cloud-internet-services
   ```
   {: pre}

1. Log in by using the private IBM Cloud endpoint at `private.cloud.ibm.com`. For more information about logging into the private cloud, see [Securing your connection when using the IBM Cloud CLI](/docs/cli?topic=cli-service-connection).

### Using an endpoint gateway with the VPC API
{: #vpe-cis-api}
{: api}

After you create a VPE for {{site.data.keyword.cis_short_notm}}, use the service endpoint FQDN `api.private.cis.cloud.ibm.com` in the URL to access the service. For example:

```sh
curl https://api.private.cis.cloud.ibm.com/v1/internet-svcs -H "Authorization: Bearer $iam_token"
```
{: pre}

### Using an endpoint gateway with the SDK
{: #vpe-sdk}
{: api}

After you create a VPE for {{site.data.keyword.cis_short_notm}}, you must use the private endpoint FQDN when you set the service endpoint during construction of the {{site.data.keyword.cis_short_notm}} gateway service object.

```sh
api.private.cis.cloud.ibm.com
```
{: pre}

For examples of setting the service's FQDN for the specific SDK language, see [SDK API examples](/apidocs/cis?code=go).

### Using an endpoint gateway with Terraform
{: #vpe-terraform}
{: terraform}

If you plan to access {{site.data.keyword.cis_short_notm}} with Terraform, make sure to set the `IBMCLOUD_PRIVATE_CIS_API_ENDPOINT` environment variable to `api.private.cis.cloud.ibm.com`. For example:

```sh
export IBMCLOUD_PRIVATE_CIS_API_ENDPOINT=api.private.cis.cloud.ibm.com
```
{: pre}

For more information, see [Getting started with Terraform on IBM Cloud](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started).
