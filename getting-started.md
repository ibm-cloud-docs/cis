---

copyright:
  years: 2018, 2025
lastupdated: "2025-07-05"

keywords: IBM Cloud Internet Services, IBM CIS application, CIS

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with {{site.data.keyword.cis_full_notm}}
{: #getting-started}

{{site.data.keyword.cis_full}} ({{site.data.keyword.cis_short_notm}}), powered with Cloudflare, offers three main capabilities to enhance your workflow: [security](/docs/cis?topic=cis-manage-your-ibm-cis-for-optimal-security), [reliability](/docs/cis?topic=cis-manage-your-ibm-cloud-internet-services-deployment-for-optimal-reliability), and [performance](/docs/cis?topic=cis-manage-your-cis-deployment-for-best-performance). You can navigate to features for each of these capabilities after you open the {{site.data.keyword.cis_short_notm}} UI.
{: shortdesc}

For each capability, {{site.data.keyword.cis_short_notm}} helps you tune its features to suit your specific needs. These features are detailed in the [About {{site.data.keyword.cis_full_notm}}](/docs/cis?topic=cis-about-ibm-cloud-internet-services-cis) section.

## Before you begin
{: #before-you-begin}

Before you begin using {{site.data.keyword.cis_short_notm}}:

* You'll need an [IBMid](https://www.ibm.com/account/reg/us-en/signup?formid=urx-19776).
* Then, you can order your services through the [{{site.data.keyword.cis_full_notm}} console](/catalog/services/internet-services).

It is recommended that you use the Chrome browser for {{site.data.keyword.cis_short_notm}}.
{: tip}

## Process overview
{: #process-overview}

You can start using {{site.data.keyword.cis_short_notm}} for your internet traffic with just a few steps.

1. Provision an instance of [IBM Cloud Internet Services](/catalog/services/internet-services){: external}.
1. Add the domain that you want to manage.
1. Set up your DNS records (optional).
1. Configure your DNS information with the name servers provided.
1. Continue getting started with {{site.data.keyword.cis_short_notm}} by following a tutorial, or by setting up other features.

### Step 1: Open the IBM {{site.data.keyword.cis_short_notm}} application
{: #open-cis-application}

Open the [{{site.data.keyword.cloud_notm}} catalog](/catalog). Then, select the **Networking** category in the navigation pane. Click the **Internet Services** tile to open the {{site.data.keyword.cis_full_notm}} application.

#### The Overview page
{: #the-overview-page}

After the {{site.data.keyword.cis_short_notm}} application starts up, you'll see the {{site.data.keyword.cis_short_notm}} **Overview** page, and you'll find the tabs for **Security**, **Reliability**, and **Performance**.

#### Which plan do I choose?
{: #which-plan}

There are several plans to choose from:

* **Enterprise Usage**
* **Enterprise Package**
* **Enterprise GLB**
* **Enterprise Security**
* **Standard Next**
* **No-cost Trial**

The **No-cost Trial** expires after 30 days, at which point you can upgrade to a plan that best suits your needs. The trial plan instance will have the same features available as a **Standard Next** plan instance would. Both the **Standard Next** and **Enterprise Plans** (except for **Enterprise Usage** plan) have a single domain included, but will allow you to onboard multiple domains under a single service instance for a cost.

Select **Create** on the **Overview** page to begin provisioning your account.

The **No-cost Trial** is limited to one instance per account.
{: note}

#### Begin provisioning
{: #begin-provisioning}

You'll see the first page of the {{site.data.keyword.cis_short_notm}} application, where you select **Add Domain** to begin.

Select **Let's get started** from the welcome page to begin setting up {{site.data.keyword.cis_short_notm}}.

### Step 2. Add and configure your domain
{: #add-configure-your-domain}

Next, begin protecting and improving the performance of your web service by entering your domain or a subdomain.

Specify DNS zones. You can configure the name servers for these domains or subdomains at the domain's registrar or DNS provider. Do not use CNAMEs.
{: note}

The Overview page shows your domain in `Pending` status and remains `Pending` until you complete configuring your name servers with the registrar or existing DNS provider, which is covered in Step 4.

You can't delete the {{site.data.keyword.cis_short_notm}} instance after you add a domain. To delete the instance, delete the domain from the instance first.
{: tip}

### Step 3. Set up your DNS records (optional)
{: #setup-your-dns-records}

Before transitioning the traffic for your domain to {{site.data.keyword.cis_short_notm}}, it is recommended that you import or recreate your DNS records in {{site.data.keyword.cis_short_notm}}. You can choose to skip this step, but if your DNS records are not configured properly in {{site.data.keyword.cis_short_notm}}, it might leave parts of your website inaccessible.

Import records by uploading your exported records from your current DNS, or manually create your DNS records. To import records, select **Import records**.

When you are finished, or to skip this step, select **Next step**.

### Step 4. Configure your name servers with the registrar or existing DNS provider
{: #configure-your-name-servers-with-the-registrar-or-existing-dns-provider}

To begin receiving the benefits of {{site.data.keyword.cis_short_notm}}, you must delegate your domain to {{site.data.keyword.cis_short_notm}}. To delegate a domain, create an NS record with the name servers provided by {{site.data.keyword.cis_short_notm}} at your domain's registrar or existing DNS provider. If you are unsure of who the registrar is for your domain, you can look it up at [lookup.icann.org](https://lookup.icann.org/en){: external}.

If you delegate a subdomain (for instance, `subdomain.example.com`) from another DNS provider, you must replace the existing name server (NS) records and replace them with a name server record for each of the name servers that are provided by {{site.data.keyword.cis_short_notm}}. See [Managing DNS records in Cloudflare](https://developers.cloudflare.com/dns/manage-dns-records/how-to/create-dns-records/){: external} for instructions by provider.

After you configure your registrar or DNS provider, it can take up to 24 hours for the changes to take effect. When we verify that the specified name servers were configured correctly for your domain or subdomain, the domain's status changes from `Pending` to `Active`.

Your domain must move to `Active` state within 60 days or your domain and any configuration data is removed.
{: important}

### Step 5. Ensure that {{site.data.keyword.cis_short_notm}} is resolving the domain information for your application, hostname, or website
{: #ensure-cis-is-resolving-domain-info}

To proceed, select **Reliability > DNS**. Be sure to add the appropriate DNS records. Add the **A Record** and any **AAAA** or **MX** entries that are populated. If you forget to add these records before the registrar's delegation is complete, {{site.data.keyword.cis_full_notm}} can't resolve the domain information for your internet-facing applications.

## Next steps
{: #get-started-next-steps}

To begin managing {{site.data.keyword.cis_short_notm}} functions and features, see [Managing your IBM Cloud Internet Services deployment](/docs/cis?topic=cis-manage-your-cis-deployment).
