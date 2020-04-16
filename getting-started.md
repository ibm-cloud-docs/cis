---

copyright:
  years: 2018, 2020
lastupdated: "2020-02-20"

keywords: IBM Cloud Internet Services, IBM CIS application, Authoritative DNS servers, CIS

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

{{site.data.keyword.cis_full}} ({{site.data.keyword.cis_short_notm}}), powered with Cloudflare, offers three main capabilities to enhance your workflow: [security](/docs/cis?topic=cis-manage-your-ibm-cis-for-optimal-security), [reliability](/docs/cis?topic=cis-manage-your-ibm-cloud-internet-services-deployment-for-optimal-reliability), and [performance](/docs/cis?topic=cis-manage-your-cis-deployment-for-best-performance). You can navigate to features for each of these capabilities after you open the {{site.data.keyword.cis_short_notm}} UI.
{:shortdesc}

 For each capability, {{site.data.keyword.cis_short_notm}} helps you tune its features to suit your specific needs, including:

 * Authoritative DNS servers
 * Global and Local Load Balancing
 * Web Application Firewall (WAF)
 * DDoS Protection
 * Caching and page rules


## Before you begin
{:#before-you-begin}

Before you begin using {{site.data.keyword.cis_short_notm}}:

* You'll need an [IBMid](https://www.ibm.com/account/reg/us-en/signup?formid=urx-19776). Then, you can order your services through your IBM Cloud Account, or through the new [{{site.data.keyword.cis_full_notm}} console](https://{DomainName}/catalog/services/internet-services), depending on your preference.

* If you need assistance in obtaining an account to use {{site.data.keyword.cis_short_notm}}, [contact your IBM Sales representative](https://{DomainName}/cloud/support) for more guidance on getting started.

* If you have an existing SoftLayer account, you can [link your account](/docs/account?topic=account-unifyingaccounts) with your IBMid.

## Process overview
{:#process-overview}

You can start using {{site.data.keyword.cis_short_notm}} for your internet traffic with just a few steps.

 1. Open the {{site.data.keyword.cis_short_notm}} application from your IBM Cloud dashboard.
 2. Add the domain that you want to manage.
 3. Configure your DNS information with the name servers provided.
 4. Continue getting started with {{site.data.keyword.cis_short_notm}}, by following a tutorial or by setting up other features.

### Step 1: Open the IBM {{site.data.keyword.cis_short_notm}} application
{:#open-cis-application}

Open the [{{site.data.keyword.cloud_notm}} catalog](https://{DomainName}/catalog/). Then, select the **Networking** category in the navigation pane. Click the **Internet Services** tile to open the {{site.data.keyword.cis_full_notm}} application.

**The Overview Screen**

After the {{site.data.keyword.cis_short_notm}} application starts up, you'll see the {{site.data.keyword.cis_short_notm}} **Overview** screen, and you'll find the tabs for **Security**, **Reliability**, and **Performance**.

**Which plan do I choose?**

There are several plans to choose from:
* **Enterprise Usage**
* **Enterprise Package**
* **Enterprise GLB**
* **Enterprise Security**
* **Standard Plan**
* **Free Trial**.

The **Free Trial** expires after 30 days, at which point you can upgrade to the **Standard Plan** or an **Enterprise Plan**. A single **Standard** instance can manage one domain. You can create as many **Standard** service instances as you want within a single account, each managing a single domain.

The **Enterprise Plans** allow you to manage multiple domains in a single service instance. Select **Create** on the **Overview** screen to begin provisioning your account.

The **Free Trial** is limited to one instance per account.
{:note}

**Begin Provisioning**

You'll see the first screen of the {{site.data.keyword.cis_short_notm}} application, where you select **Add Domain** to begin.

Select **Let's get started** from the welcome page to begin setting up {{site.data.keyword.cis_short_notm}}.

![Getting Started](images/overview-setup-step1.png)

### Step 2. Add and configure your domain.
{:#add-configure-your-domain}

Next, begin protecting and improving the performance of your web service by entering your domain or a subdomain.

Specify DNS zones. You can configure the name servers for these domains or subdomains at the domain's registrar or DNS provider. Do not use CNAMEs.
{:note}

![Getting Started](images/overview-setup-step2.png)

The Overview screen shows your domain in `Pending` status and remains `Pending` until you complete configuring your name servers with the registrar or existing DNS provider, which is covered in Step 4.

You cannot delete the {{site.data.keyword.cis_short_notm}} instance after you add a domain. To delete the instance, delete the domain from the instance first.
{:note}

### Step 3. Set up your DNS records (optional).
{:#setup-your-dns-records}

Before transitioning the traffic for your domain to {{site.data.keyword.cis_short_notm}}, it is recommended that you import or re-create your DNS records in {{site.data.keyword.cis_short_notm}}. You can choose to skip this step, but if your DNS records are not configured properly in {{site.data.keyword.cis_short_notm}}, it might leave parts of your website inaccessible.

Import records by uploading your exported records from your current DNS or manually create your DNS records. To import records, select **Import records**.

![Getting Started](images/overview-setup-step3.png)

When you are finished, or to skip this step, select **Next step**.

### Step 4. Configure your name servers with the registrar or existing DNS provider.
{:#configure-your-name-servers-with-the-registrar-or-existing-dns-provider}

To begin receiving the benefits of {{site.data.keyword.cis_short_notm}}, configure your registrar or domain name provider to use the name servers listed. If you're delegating a domain (something like `example.com`), configure the listed name servers in your domain's settings, where they are managed by your registrar (for example, on the registrar's web portal). If you are unsure of who the registrar is for your domain, you can look it up at [whois.icann.org](https://whois.icann.org/){:external}. If you delegate a subdomain (for instance, `subdomain.example.com`) from another DNS provider, you must replace the existing name server (NS) records and replace them with a name server record for each of the name servers that are provided by {{site.data.keyword.cis_short_notm}}. See [Managing DNS Records](https://support.cloudflare.com/hc/en-us/articles/360019093151-Managing-DNS-records-in-Cloudflare){:external}, written by our partners at Cloudflare, for detailed instructions by provider.

After you configure your registrar or DNS provider, it can take up to 24 hours for the changes to take effect. When we verify that the specified name servers were configured correctly for your domain or subdomain, the domain's status changes from `Pending` to `Active`. After configuring the name servers, you can click the "Recheck name servers" link in the `Overview` page to potentially accelerate the activation of your domain. You can submit this check only one time an hour.

Your domain must move to `Active` state within 60 days or your domain and any configuration data is removed.
{:note}

![Getting Started](images/overview-setup-step4.png)

### Step 5. Ensure that {{site.data.keyword.cis_full_notm}} is resolving the domain information for your application, hostname, or website.
{:#ensure-cis-is-resolving-domain-info}

To proceed, select **Reliability > DNS**. Be sure to add the appropriate _DNS Records_. Add the **A Record** and any **AAAA** or **MX** entries that are populated. If you forget to add these records before the registrar's delegation is complete, {{site.data.keyword.cis_full_notm}} cannot resolve the domain information for your internet-facing applications.

![Getting Started](images/dns-records.png)

### Step 6. In the meantime, you can begin managing other {{site.data.keyword.cis_short_notm}} functions and features.
{:#manage-other-cis-functions}

For information about managing other functions and features, see [step-by-step instructions](/docs/cis?topic=cis-manage-your-cis-deployment#manage-your-cis-deployment).
