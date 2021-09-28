---

copyright:
  years: 2018, 2020
lastupdated: "2020-02-20"

keywords: IBM Cloud Internet Services, IBM CIS application, CIS

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

# Getting started with {{site.data.keyword.cis_full_notm}}
{: #getting-started}

{{site.data.keyword.cis_full}} ({{site.data.keyword.cis_short_notm}}), powered with Cloudflare, offers three main capabilities to enhance your workflow: [security](/docs/cis?topic=cis-managing-cis-for-optimal-security), [reliability](/docs/cis?topic=cis-managing-your-cis-deployment-for-optimal-reliability), and [performance](/docs/cis?topic=cis-managing-your-cis-deployment-for-best-performance). You can navigate to features for each of these capabilities after you open the {{site.data.keyword.cis_short_notm}} UI.
{: shortdesc}

For each capability, {{site.data.keyword.cis_short_notm}} helps you tune its features to suit your specific needs. These features are detailed in the [About {{site.data.keyword.cis_full_notm}}](/docs/cis?topic=cis-about-ibm-cloud-internet-services) section.

## Before you begin
{: #before-you-begin}

Before you begin using {{site.data.keyword.cis_short_notm}}:

* You'll need an [IBMid](https://www.ibm.com/account/reg/us-en/signup?formid=urx-19776). 
* Then, you can order your services through the [{{site.data.keyword.cis_full_notm}} console](https://{DomainName}/catalog/services/internet-services).

It is recommended that you use the Chrome browser for {{site.data.keyword.cis_short_notm}}.
{: tip}

## Process overview
{: #process-overview}

You can start using {{site.data.keyword.cis_short_notm}} for your internet traffic with just a few steps.

1. Open the {{site.data.keyword.cis_short_notm}} application from your IBM Cloud dashboard.
1. Add the domain that you want to manage.
1. Set up your DNS records (optional).
1. Configure your DNS information with the name servers provided.
1. Continue getting started with {{site.data.keyword.cis_short_notm}} by following a tutorial, or by setting up other features.

### Step 1: Open the IBM {{site.data.keyword.cis_short_notm}} application
{: #open-cis-application}

Open the [{{site.data.keyword.cloud_notm}} catalog](https://{DomainName}/catalog/). Then, select the **Networking** category in the navigation pane. Click the **Internet Services** tile to open the {{site.data.keyword.cis_full_notm}} application.

**The Overview screen**

After the {{site.data.keyword.cis_short_notm}} application starts up, you'll see the {{site.data.keyword.cis_short_notm}} **Overview** screen, and you'll find the tabs for **Security**, **Reliability**, and **Performance**.

**Which plan do I choose?**

There are several plans to choose from:

* **Enterprise Usage**
* **Enterprise Package**
* **Enterprise GLB**
* **Enterprise Security**
* **Standard Plan**
* **Free Trial**

The **Free Trial** expires after 30 days, at which point you can upgrade to the **Standard Plan** or an **Enterprise Plan**. A single **Standard** instance can manage one domain. You can create as many **Standard** service instances as you want within a single account, each managing a single domain. The **Enterprise Plans** allow you to manage multiple domains in a single service instance.

Select **Create** on the **Overview** screen to begin provisioning your account.

The **Free Trial** is limited to one instance per account.
{: note}

**Begin provisioning**

You'll see the first screen of the {{site.data.keyword.cis_short_notm}} application, where you select **Add Domain** to begin.

Select **Let's get started** from the welcome page to begin setting up {{site.data.keyword.cis_short_notm}}.

### Step 2. Add and configure your domain
{: #add-configure-your-domain}

Next, begin protecting and improving the performance of your web service by entering your domain or a subdomain.

Specify DNS zones. You can configure the name servers for these domains or subdomains at the domain's registrar or DNS provider. Do not use CNAMEs.
{: note}

The Overview screen shows your domain in `Pending` status and remains `Pending` until you complete configuring your name servers with the registrar or existing DNS provider, which is covered in Step 4.

You cannot delete the {{site.data.keyword.cis_short_notm}} instance after you add a domain. To delete the instance, delete the domain from the instance first.
{: tip}

### Step 3. Set up your DNS records (optional)
{: #setup-your-dns-records}

Before transitioning the traffic for your domain to {{site.data.keyword.cis_short_notm}}, it is recommended that you import or recreate your DNS records in {{site.data.keyword.cis_short_notm}}. You can choose to skip this step, but if your DNS records are not configured properly in {{site.data.keyword.cis_short_notm}}, it might leave parts of your website inaccessible.

Import records by uploading your exported records from your current DNS, or manually create your DNS records. To import records, select **Import records**.

When you are finished, or to skip this step, select **Next step**.

### Step 4. Configure your name servers with the registrar or existing DNS provider
{: #configure-your-name-servers-with-the-registrar-or-existing-dns-provider}

To begin receiving the benefits of {{site.data.keyword.cis_short_notm}}, you must delegate your domain to {{site.data.keyword.cis_short_notm}}. To delegate a domain, create an NS record with the name servers provided by {{site.data.keyword.cis_short_notm}} at your domain's registrar or existing DNS provider. If you are unsure of who the registrar is for your domain, you can look it up at [whois.icann.org](https://whois.icann.org/){: external}.

If you delegate a subdomain (for instance, `subdomain.example.com`) from another DNS provider, you must replace the existing name server (NS) records and replace them with a name server record for each of the name servers that are provided by {{site.data.keyword.cis_short_notm}}. See [Managing DNS records in Cloudflare](https://support.cloudflare.com/hc/en-us/articles/360019093151-Managing-DNS-records-in-Cloudflare){: external} for detailed instructions by provider.

After you configure your registrar or DNS provider, it can take up to 24 hours for the changes to take effect. When we verify that the specified name servers were configured correctly for your domain or subdomain, the domain's status changes from `Pending` to `Active`. 

Your domain must move to `Active` state within 60 days or your domain and any configuration data is removed.
{: important}

### Step 5. Ensure that {{site.data.keyword.cis_short_notm}} is resolving the domain information for your application, hostname, or website
{: #ensure-cis-is-resolving-domain-info}

To proceed, select **Reliability > DNS**. Be sure to add the appropriate DNS records. Add the **A Record** and any **AAAA** or **MX** entries that are populated. If you forget to add these records before the registrar's delegation is complete, {{site.data.keyword.cis_full_notm}} cannot resolve the domain information for your internet-facing applications.

## Next steps

To begin managing {{site.data.keyword.cis_short_notm}} functions and features, see [Managing your IBM Cloud Internet Services deployment](/docs/cis?topic=cis-managing-your-cis-deployment).
