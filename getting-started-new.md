---

copyright:
  years: 2018, 2025
lastupdated: "2025-12-08"

keywords: IBM Cloud Internet Services, IBM CIS application, CIS

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with {{site.data.keyword.cis_full_notm}}
{: #getting-started}

{{site.data.keyword.cis_full}} ({{site.data.keyword.cis_short_notm}}) is a cloud-native solution that helps protect and optimize your internet-facing applications. Powered by Cloudflare’s global network, CIS acts as a reverse proxy to help secure traffic, improve performance, and maintain availability.
{: shortdesc}

CIS delivers three essential benefits:
* Security – Safeguards your applications from DDoS attacks, malicious bots, and other web threats using features like a Web Application Firewall (WAF), rate limiting, and SSL/TLS encryption.
* Reliability – Ensures uptime and resilience through global load balancing, automatic failover, and robust DNS services.
* Performance – Accelerates content delivery with a global Content Delivery Network (CDN), intelligent caching, and optimized protocols.

After you provision a CIS instance on IBM Cloud, you can access and configure these features.

## Before you begin
{: #before-you-begin-new}

Before you begin using {{site.data.keyword.cis_short_notm}}, ensure that you have met the following requirements:

* You need an IBMid to sign in to IBM Cloud and manage CIS. If you don’t have one, you can [create an account](https://www.ibm.com/account/reg/us-en/signup?formid=urx-19776){: external} to access trials, demos, and services.
* You must have a domain registered with a domain registrar. CIS protects and accelerates traffic for this domain. 
* Decide whether you want to protect your entire domain ([full setup](/docs/cis?topic=cis-convert-partial-cname-full&interface=cli)) or specific subdomains ([partial setup](/docs/cis?topic=cis-cname-setup&interface=cli)). This decision affects how you’ll configure DNS and what level of protection and optimization you get from CIS.
* [Compare and select a CIS plan](/docs/cis?topic=cis-cis-plan-comparison) that best meets your needs (Lite, Standard, or Enterprise). Each plan offers different levels of security, performance, and feature access.
* Understand the basics. Take time to familiarize yourself with the [core concepts](/docs/cis?group=concepts) of CIS so that you can configure it effectively. 

It is recommended that you use Google Chrome when working with {{site.data.keyword.cis_short_notm}}.
{: tip}

## Getting started process
{: #process-overview-new}

CIS provides cloud-native tools to secure, optimize, and ensure the reliability of your internet-facing applications. Key capabilities include DDoS protection, a Web Application Firewall (WAF), DNS management, traffic analytics, and performance acceleration.

Follow these high-level steps to get started with CIS:

1. [Create a CIS instance](/docs/cis?topic=cis-create-cis-instance) in your IBM Cloud account. The CIS instance acts as the central place to manage your domain's security, DNS, and performance settings.
1. Add your domain to your CIS instance. CIS supports multiple ways to onboard a domain, depending on your DNS setup needs. Choose the method that best fits your setup:

   * [Configure a full setup (authoritative DNS)](/docs/cis?topic=cis-domains): CIS becomes your domain’s DNS provider. You update your domain registrar’s name servers to point to CIS. This gives you full control and access to all CIS features.
   * [Configure a partial setup (CNAME-based)](/docs/cis?topic=cis-cname-setup): You keep your current DNS provider and only route specific subdomains (for example, `www.techcorp.com`) through CIS by configuring CNAME records. Ideal if you can’t or prefer not to change your domain’s name servers.
   
1. After adding your domain, optionally [import or set up your DNS records](/docs/cis?topic=cis-set-up-your-dns-for-cis) before activating traffic through CIS. 

1. [Configure your name servers with the registrar or existing DNS provider](/docs/cis?topic=cis-name-servers). 

   * If you're using a full setup, update your domain registrar's name servers to the ones provided by CIS. This change routes all DNS queries through CIS so that its security and performance features can take effect.

   * If you're using a partial setup, configure the necessary CNAME records at your DNS provider to proxy specific subdomains through CIS.

   After updating your name servers or CNAME records, it can take up to 24–48 hours for DNS changes to propagate across the internet.
   {: note}

1. Ensure that CIS is resolving the domain information for your application, hostname, or website.

   To proceed, select **Reliability > DNS**. Be sure to add the appropriate DNS records. Add the A Record and any AAAA or MX entries that are populated. If you forget to add these records before the registrar's delegation is complete, CIS can't resolve the domain information for your internet-facing applications.
 
1. [Explore the CIS console](/docs/cis?topic=cis-manage-your-cis-deployment). Familiarize yourself with CIS, including areas for domain management, DNS configuration, traffic analytics, and security settings.
1. [Review best practices](/docs/cis?group=best-practices) for CIS setup, security, reliability, and performance.
1. Enable and configure additional features. After your domain is active, [explore the full range of CIS capabilities](/docs/cis?topic=cis-about-ibm-cloud-internet-services-cis), such as DDoS protection, Web Application Firewall (WAF), rate limiting and bot management, SSL/TLS settings, page rules, and real-time traffic analytics.

To navigate to your CIS instance:

   1. Go to **Navigation Menu** icon![Navigation Menu icon](../icons/icon_hamburger.svg) and click **Resource list**, then expand **Security**. 
   1. Expand **Security** and click the name of your CIS instance.

[QUESTION]{: tag-red} WHERE SHOULD WE TALK ABOUT DELEGATING DOMAIN MANAGEMENT AFTER ADDING DNS RECORDS? ALSO, WE HAVE TOPIC ON USING SERVICE ENDPOINTS TO PRIVATELY CONNECT TO CIS. SHOULD THIS BE PART OF THE GETTING STARTED STEPS LIKE ADDING DNS RECORDS?
