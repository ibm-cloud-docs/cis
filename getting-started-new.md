---

copyright:
  years: 2018, 2026
lastupdated: "2026-02-09"

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
* Reliability – Helps ensure uptime and resilience through global load balancing, automatic failover, and robust DNS services.
* Performance – Accelerates content delivery with a global Content Delivery Network (CDN), intelligent caching, and optimized protocols.

After you provision a CIS instance on IBM Cloud, you can access and configure these features.

## Before you begin
{: #before-you-begin-new}

Before you begin using {{site.data.keyword.cis_short_notm}}, make sure that you have met the following requirements:

* You need an IBMid to sign in to IBM Cloud and manage CIS. If you don’t have one, you can [create an account](https://www.ibm.com/account/reg/us-en/signup?formid=urx-19776){: external} to access trials, demos, and services.
* You must have a domain registered with a domain registrar. CIS protects and accelerates traffic for this domain. 
* Decide whether you want to protect your entire domain ([full setup](/docs/cis?topic=cis-full-authoritative-zone&interface=cli)) or specific subdomains ([partial setup](/docs/cis?topic=cis-cname-setup&interface=cli)). This decision affects how you’ll configure DNS and what level of protection and optimization you get from CIS.
* [Compare and select a CIS plan](/docs/cis?topic=cis-cis-plan-comparison) that best meets your needs (Lite, Standard, or Enterprise). Each plan offers different levels of security, performance, and feature access.
* Familiarize yourself with [CIS core concepts](/docs/cis?group=concepts) and terminology to better understand the configuration steps.  

It is recommended that you use Google Chrome when working with {{site.data.keyword.cis_short_notm}}.
{: tip}

## Getting started process
{: #process-overview-new}

This section outlines high-level steps to onboard your domain and activate CIS features. 

Updates to your DNS delegation, name servers, or CNAME records can take up to 24–48 hours to propagate globally.  
{: attention}

1. [Create a CIS instance](/docs/cis?topic=cis-create-cis-instance) in your IBM Cloud account. The CIS instance acts as the central place to manage your domain's security, DNS, and performance settings.
1. Add your domain to your CIS instance. CIS supports multiple ways to onboard a domain, depending on your DNS setup needs. Choose the method that best fits your setup:

   * [Configure a full setup (authoritative DNS)](/docs/cis?topic=cis-full-authoritative-zone): CIS becomes your domain’s DNS provider. You update your domain registrar’s name servers to point to CIS. This gives you full control and access to all CIS features.

      If you already have a partial setup, see [Converting a partial (CNAME) configuration to full](/docs/cis?topic=cis-convert-partial-cname-full).
      {: note}

   * [Configure a partial setup (CNAME-based)](/docs/cis?topic=cis-cname-setup): You keep your current DNS provider and only route specific subdomains (for example, `www.techcorp.com`) through CIS by configuring CNAME records. Ideal if you can’t or prefer not to change your domain’s name servers.

1. [Import or add your DNS records](/docs/cis?topic=cis-set-up-your-dns-for-cis). Before updating DNS delegation or CNAME records, make sure that all required DNS records exist in CIS. This step ensures that CIS can immediately resolve traffic when delegation is complete.

   You can import existing DNS records or add them manually. Make sure that required records such as A, AAAA, MX, and CNAME records are present. 

1. Configure DNS delegation based on the setup type you selected. After DNS records are in place, update your registrar or DNS provider to route traffic through CIS.

   For a full setup:

   1. Sign in to your domain registrar or DNS host and locate the **Name Server (NS) settings**.  
   1. Update the NS records to point to CIS name servers (for full setup) or your existing DNS provider (for partial setup with CNAMEs).  
   1. Save your changes. 

   For a partial setup:

   1. Sign in to your DNS provider and locate the DNS record settings.
   1. Configure the required CNAME records to proxy specific subdomains through CIS.
   1. Save your changes.

1. Verify DNS delegation and domain resolution. After propagation begins, confirm that your domain is delegated correctly and that CIS is resolving traffic as expected.

   Use a DNS lookup tool, such as `dig` or `nslookup` to verify authoritativee name servers and record resolution. For example:  

      ```bash
      dig NS example.com
      ```
      {: pre}
   
1. [Configure your name servers with the registrar or existing DNS provider](/docs/cis?topic=cis-name-servers). 

   * If you're using a full setup, update your domain registrar's name servers to the ones provided by CIS. This change routes all DNS queries through CIS so that its security and performance features can take effect.
   * If you're using a partial setup, configure the necessary CNAME records at your DNS provider to proxy specific subdomains through CIS. 

1. Confirm that CIS is resolving the domain information for your application, hostname, or website.

   To proceed, select **Reliability > DNS**. Be sure to add the appropriate DNS records. Add the A Record and any AAAA or MX entries that are populated. If you forget to add these records before the registrar's delegation is complete, CIS can't resolve the domain information for your internet-facing applications.

1. [Review CIS best practices](/docs/cis?group=best-practices) and [explore the CIS console](/docs/cis?topic=cis-manage-your-cis-deployment) to familiarize yourself with domain management, DNS configuration, traffic analytics, and security settings.
1. Enable and configure additional features. After your domain is active, explore the full range of CIS capabilities, such as DDoS protection, rate limiting and bot management, SSL/TLS settings, page rules, and real-time traffic analytics.
