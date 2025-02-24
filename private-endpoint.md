---

copyright:
  years: 2021, 2025
lastupdated: "2025-02-24"

keywords: isolation for cis, service endpoints for cis, private network for cis, network isolation in cis, non-public routes for cis, private connection for cis, private connectivity for cis

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Using service endpoints to privately connect to {{site.data.keyword.cis_short_notm}}
{: #service-endpoints}

To help ensure that you have enhanced control and security over your configuration when you use {{site.data.keyword.cis_full}}, you can use private routes to {{site.data.keyword.cloud}} service endpoints. Private routes are not accessible or reachable over the internet. By using the {{site.data.keyword.cloud_notm}} private service endpoints feature, you can protect your configuration from threats from the public network and logically extend your private network.
{: shortdesc}

When you use the {{site.data.keyword.cis_short_notm}} private endpoint, any DNS records or global load balancers can be reached on the public network.
{: note}

## Before you begin
{: #prereq-service-endpoint}

To get started, enable [virtual routing and forwarding (VRF) and service endpoints](/docs/account?topic=account-vrf-service-endpoint){: external} for your infrastructure account. After you enable VRF for your account, you can connect to {{site.data.keyword.cis_short_notm}} by using a private IP that is accessible only through the {{site.data.keyword.cloud_notm}} private network.

To learn more about private connections on {{site.data.keyword.cloud_notm}}, see [Service endpoints for private connections](/docs/account?topic=account-service-endpoints-overview){: external}.

## Setting up service endpoints for {{site.data.keyword.cis_short_notm}}
{: #endpoint-setup}

These service endpoints are only for managing the configuration of an instance with the API or CLI, the control plane. Using the IBM Cloud private service endpoints feature does not affect the data plane, and the public endpoints remain available. For information on the control plane and data plane, see [Learning about CIS architecture and workload isolation](/docs/cis?topic=cis-compute-isolation).
{: note}

## Targeting private endpoints
{: #private-network-prereqs}

Before you target a private endpoint for {{site.data.keyword.cis_short_notm}}:

1. Make sure that your {{site.data.keyword.cloud_notm}} infrastructure account is enabled for [virtual routing and forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint&interface=ui#vrf){: external}.

    When you enable VRF, a separate routing table is created for your account, and connections to and from your account's resources are routed separately
    on the {{site.data.keyword.cloud_notm}} network. To learn more about VRF technology, see [Virtual routing and forwarding on {{site.data.keyword.cloud_notm}}](/docs/dl?topic=dl-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud){: external}.

    Enabling VRF permanently alters the networking for your account. Be sure that you understand the impact to your account and resources. After you enable
    VRF, it can't be disabled.
    {: important}

2. Make sure that your {{site.data.keyword.cloud_notm}} infrastructure account is enabled for [service endpoints](/docs/account?topic=account-vrf-service-endpoint#service-endpoint){: external}.

    After you enable VRF and service endpoints for your account, all existing and future {{site.data.keyword.cis_short_notm}} resources and instances become available from both the public and private endpoints.
    {: note}

## Using the CLI
{: #vpe-setup-cli}
{: cli}

### Step 1. Configure the {{site.data.keyword.cloud_notm}} private network on your virtual server
{: #configure-private-network}

Prepare your virtual server instance or test server by configuring your routing table for the {{site.data.keyword.cloud_notm}} private network.

1. To route traffic to the {{site.data.keyword.cloud_notm}} private network, run the following command on your virtual server instance:

    ```sh
    route add -net 166.9.0.0/16 gw <gateway> dev <gateway_interface>
    ```
    {: pre}

    Replace `<gateway>` (for example, `10.x.x.x`) and `<gateway_interface>` (for example, `eth10`) with the appropriate values.

2. Optional: Verify that the route was added successfully by displaying your new routing table.

    ```sh
    route -n
    ```
    {: pre}

### Step 2. Target the {{site.data.keyword.cis_short_notm}} private endpoint
{: #target-private-endpoint}

After you configure your virtual server instance to accept {{site.data.keyword.cloud_notm}} private network traffic, you can target the private endpoint for
{{site.data.keyword.cis_short_notm}} by using the {{site.data.keyword.cis_short_notm}} API or {{site.data.keyword.cis_short_notm}} CLI plug-in.

1. Log in to the {{site.data.keyword.cloud_notm}} console.

    ```sh
    ibmcloud login
    ```
    {: pre}

    If the login fails, run the `ibmcloud login --sso` command to try again. The `--sso` parameter is required when you log in with a federated ID. If you use this
    option, go to the link listed in the CLI output to generate a one-time passcode.
    {: note}

2. Optional: Make sure that your account is enabled for VRF and service endpoints.

    ```sh
    ibmcloud account show
    ```
    {: pre}

    The following CLI output shows the account details of a VRF and service endpoint-enabled account.

    ```plaintext
    Retrieving account John Doe's Account of john.doe@email.com...
    OK

    Account ID:                   d154dfbd0bc2edefthyufffc9b5ca318
    Currently Targeted Account:   true
    Linked Softlayer Account:     1008967
    VRF Enabled:                  true
    Service Endpoint Enabled:     true
    ```
    {: screen}

    To learn how to set up your account for connecting to a private network, see [Enabling VRF and service endpoints](/docs/account?topic=account-vrf-service-endpoint){: external}.
    {: tip}

### Step 3. Create a {{site.data.keyword.cis_short_notm}} resource on the private network
{: #create-key-private-network}

Test your private network connection by using the [{{site.data.keyword.cis_short_notm}} CLI plug-in](/docs/cis-cli-plugin?topic=cis-cli-plugin-cis-cli).

1. Log in to a {{site.data.keyword.cis_short_notm}} private endpoint instance.

    ```sh
    ibmcloud login -a private.cloud.ibm.com
    ```
    {: pre}

## Using the API
{: #vpe-setup-api}
{: api}

Use the service endpoint's FQDN `api.private.cis.cloud.ibm.com` in the URL to access the service, as shown in the following example.

```sh
curl https://api.private.cis.cloud.ibm.com/v1/:crn/zones -H 'content-type: application/json' -H 'accept: application/json' -H 'x-auth-user-token: Bearer xxxxxx'
```
{: pre}
