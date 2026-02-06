---

copyright:
  years: 2026
lastupdated: "2026-02-06"

keywords: domains

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Adding and delegating your domain
{: #add-delegate-domain}

Adding your domain to CIS allows you to protect, accelerate, and manage traffic for your applications. Delegating your domain ensures that DNS queries for your domain are correctly routed to CIS or your designated DNS provider.
{: shortdesc} 

Follow these steps to add your domain to CIS, optionally configure DNS records, delegate your domain, and verify that it is properly set up.

1. Log in to IBM Cloud and navigate to your CIS instance.  

1. Click **Add a Domain** and enter your domain name (for example, `example.com`).  

1. Choose your setup type:  
   - Partial setup (CNAME-based): Only specific subdomains (like `www.example.com`) are proxied through CIS. You keep your existing DNS provider.  
   - Full setup (authoritative DNS): CIS becomes the authoritative DNS provider for your domain, routing all DNS queries through CIS.  

1. Optionally import or set up your DNS records before activating traffic through CIS. Ensure all required records (A, AAAA, MX, and CNAME) are present. You can [import existing DNS records or add new ones](/docs/cis?topic=cis-set-up-your-dns-for-cis).  

1. Delegate your domain:  
   1. Sign in to your domain registrar or DNS host and locate the **Name Server (NS) settings**.  
   1. Update the NS records to point to CIS name servers (for full setup) or your existing DNS provider (for partial setup with CNAMEs).  
   1. Save your changes. 
   
   DNS delegation changes can take up to 24–48 hours to propagate globally.  
   {: note}

1. To verify delegation and DNS record, use a DNS lookup tool, such as `dig` or `nslookup` to confirm your domain points to the correct authoritative name servers. Example:  

   ```bash
   dig NS example.com
   ```
   {: pre}
