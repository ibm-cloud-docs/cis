---
copyright:
  years: 2018
lastupdated: "2018-05-30"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Getting Started with IBM Cloud Internet Services (CIS)

IBM Cloud Internet Services (CIS), powered by Cloudflare, offers three main capabilities to enhance your workflow: [security](/docs/infrastructure/cis/managing-for-security.html), [reliability](/docs/infrastructure/cis/managing-for-reliability.html), and [performance](/docs/infrastructure/cis/managing-for-performance.html). Each area of capability is represented in the left-hand navbar of your screen, once you've opened the IBM CIS application.

For each capability, IBM CIS helps you tune its features to suit your specific needs, including:

 * Authoritative DNS servers
 * Global and Local Load Balancing
 * Web Application Firewall (WAF)
 * DDoS Protection
 * Caching and page rules



## Before you begin
Before you begin using IBM CIS, you'll first need an [IBMid](https://www.ibm.com/account/us-en/signup/register.html). Then you can order your services through your IBM Cloud Account, or through the new [IBM Cloud Internet Services Portal](https://console.bluemix.net/catalog/services/internet-services), depending on your preference.

If you need assistance in obtaining an account to use IBM Cloud Internet Services, [contact your IBM sales representative](https://www.ibm.com/cloud-computing/bluemix/contact-us) for additional guidance on getting started.

If you have an existing Softlayer account, you can [link your account](https://console.bluemix.net/docs/account/softlayerlink.html#unifyingaccounts) with your IBMid. 

## Process overview

You can start using IBM CIS for your Internet traffic with just a few steps.

 * Open the IBM CIS application from your IBM Cloud dashboard.
 * Add the domain you want to manage.
 * Configure your DNS information with the name servers we've provided.
 * Continue getting started with IBM CIS, by following a tutorial or by setting up other features.

### Step 1: Open the IBM CIS application

Open your [IBM Cloud dashboard](https://console.bluemix.net/catalog/). Then navigate to the IBM CIS application icon by selecting the **Infrastructure -> Network** category in the left-hand navigation bar of the dashboard. Open the IBM Cloud Internet Services application by clicking the icon that you'll see near the middle of your screen. 

![Catalog](images/catalog-cis-tile.png)

**The Overview Screen**

Once the IBM CIS application starts up, you'll see the IBM CIS **Overview** screen, and you'll find the tabs for **Security**, **Reliability**, and **Perfomance** on the left area of the UI display.

**What plan do I choose?**

There are 2 plans to choose from, the **Standard Plan** and the **Free Trial**. The **Free Trial** expires after 30 days, at which point you would need to upgrade to the **Standard Plan**. Select the **Create** button at the lower left of your **Overview** screen to begin provisioning your account.

**Note:** The **Free Trial** is limited to one instance per account. 

**Begin Provisioning**

You'll see the first screen of the IBM CIS application, where you'll select the **Add Domain** button to begin.


### Step 2. Add and configure your Domain.
Select **Let's get started** from the welcome page to begin setting up CIS.

![Getting Started](images/overview-setup-step1.png)

Next, begin protecting and improving the performance of your web service by entering your domain or a subdomain.

**Note:** Please specify DNS zones. You can configure the nameservers for these domains or subdomains at the domain's registrar or DNS provider. Do not use CNAMEs.

![Getting Started](images/overview-setup-step2.png)

The Overview screen will show your domain in `Pending` status. Your domain will remain `Pending` until you complete Step 4.

**Note:** The IBM CIS instance cannot be deleted after a domain has been added. To delete the instance, please delete the domain from the instance first.

### Step 3. Set up your DNS records (optional).
Before transitioning the traffic for your domain to CIS, we strongly recommend that you import or re-create your DNS records in CIS. You can choose to skip this step, but if your DNS records are not configured properly in CIS, it could leave parts of your website inaccessible.

Import records by uploading your exported records from your current DNS or manually create your DNS records. To import records select **Import records**.

![Getting Started](images/overview-setup-step3.png)

When you are finished, or if you would like to skip this step, select **Next step**.

### Step 4. Configure your Name Servers with the Registrar or existing DNS Provider.

To begin receiving the benefits of IBM CIS, configure your registrar or domain name provider to use the name servers listed. If you're delegating a domain (something like `example.com`), configure the listed name servers in your domain's settings, where they are managed by your registrar (for example, on the registrar's web portal). If you are unsure of who the registrar is for your domain, you can look it up at https://whois.icann.org/. If you delegate a subdomain (for instance, `subdomain.example.com`) from another DNS provider, you must add a Name Server (NS) record for each of the listed name servers. See [Managing DNS Records (![External link icon](../../icons/launch-glyph.svg "External link icon")](https://support.cloudflare.com/hc/en-us/sections/200038106-Managing-DNS-Records){:new_window}, written by our partners at Cloudflare, for detailed instructions by provider.

After you've configured your registrar or DNS provider, it may require up to 24 hours for the changes to take effect. Once we verify that the specified nameservers have been configured corrrectly for your domain or subdomain, the domain's status changes from `Pending` to `Active`. After configuring the nameservers, you may click on the "Recheck name servers" link in the `Overview` page to potentially accelerate the activation of your domain (you can submit this check only once an hour).

![Getting Started](images/overview-setup-step4.png)

### Step 5. Ensure that IBM Cloud Internet Services is resolving the domain information for your application, hostname, or website.

To proceed, select the **Reliability** tab from your left-hand navbar, then select the **DNS** option. Be sure to add the appropriate _DNS Records_. Add the **A Record** and any **AAAA** or **MX** entries that are populated. If you forget to add these records before the registrar's delegation is complete, IBM Cloud Internet Services cannot resolve the domain information for your internet-facing applications.

![Getting Started](images/dns-records.png)

### Step 6. In the meantime, you can begin managing other IBM CIS functions and features.

For more details about managing other functions and features, please see the [step-by-step instructions](/docs/infrastructure/cis/how-to.html).
