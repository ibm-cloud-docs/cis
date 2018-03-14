---
copyright:
  years: 2018
lastupdated: "2018-03-05"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Getting Started with IBM Cloud Internet Services (CIS)

IBM Cloud Internet Services (CIS) offers three main capabilities to enhance your workflow: [security](managing-for-security.html), [reliability](managing-for-reliability.html), and [performance](managing-for-performance.html).

For each capability, IBM CIS helps you tune its features to suit your specific needs, including:

 * Authoritative DNS servers
 * Global and Local Load Balancing
 * Web Application Firewall (WAF)
 * Caching and page rules
 * DDoS Protection

## Process overview

You can start using IBM Cloud Internet Services (CIS) for your internet traffic with just a few steps.

 * Open the IBM CIS application from your IBM Cloud dashboard.
 * Add the domain you want to manage.
 * Configure your DNS information with the name servers we've provided.
 * Continue getting started with IBM CIS, by following a tutorial or by setting up other features.

**Step 1: Open the IBM CIS application**

To begin, open your IBM Cloud dashboard and find the IBM CIS application icon under the **Platform -> Network** category.

![Catalog](images/catalog-cis-tile.png)

For the Early Access release, there is only one plan and it is free. Click the "Create" button to begin provisioning your account.

You'll see the first screen of the IBM CIS application, where you'll select the "Add Domain" button to begin.

**Step 2. Add and configure your Domain.**

Begin protecting and improving the performance of your web service by entering your domain or a subdomain.

![Getting Started](images/overview-add-domain.png)

The Overview screen will show your domain in "Pending" status.
Note: The IBM CIS instance will not be able to be deleted when a domain has been added. To delete the instance, please delete the domain from the instance first.

**Step 3. Configure your Name Servers with the Registrar or existing DNS Provider.**

To begin receiving the benefits of IBM CIS, configure your registrar or domain name provider to use the name servers listed. If you're delegating a domain (something like `example.com`), configure the listed name servers in your domain's settings, where they are managed by your registrar (for example, on the registrar's web portal). If you delegate a subdomain (for instance, `subdomain.example.com`) from another DNS provider, you must add a Name Server (NS) record for each of the listed name servers.

After you've configured your registrar or DNS provider, it may require up to 24 hours for the changes to take effect.

**Step 4. In the meantime, you can begin managing other IBM CIS functions and features.**

For more details about managing other functions and features, please see the [step-by-step instructions](how-to.html).
