---

copyright:
  years: 2026
lastupdated: "2026-02-09"

keywords: domains

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Configuring a full (authoritative) zone
{: #full-authoritative-zone}

A "full setup" delegates DNS authority to CIS. You update your domain’s name servers at your registrar so CIS becomes the authoritative DNS provider for your domain. This can be applied to a root domain (`example.com`) or a subdomain (`sub.example.com`) if needed.

To configure a full (authoritiative) zone, follow these steps:

1. Prepare your domain:

   1. Ensure you own the domain or subdomain.  
   1. Identify your current DNS provider or registrar.  
   1. Gather all existing DNS records (A, AAAA, MX, TXT, CNAME, DKIM, SPF, CAA, etc.) that must be preserved.  
   1. Disable DNSSEC at your registrar if it is currently enabled.  
   1. Remove or resolve any conflicting records at the registrar that could prevent delegation.

1. Add your domain to CIS:

   1. Log in to the **IBM Cloud Console** and open your CIS instance.  
   1. Navigate to **Domains > Add domain**.  
   1. Enter your domain or subdomain name and select **Full setup (authoritative DNS)**.  
   1. Proceed to add the domain.  

1. Import or recreate DNS records in CIS:

   1. Go to **DNS > Records** in the CIS dashboard.  
   1. Import existing DNS records from your previous provider if available.  
   1. If import is not available, manually add all necessary records, including:  
      - A and AAAA records  
      - MX and TXT records (including SPF, DKIM)  
      - CAA and other service-specific records  
   1. Verify that all records are correct before updating name servers.  

   Missing or incorrect records cause service interruptions once CIS becomes authoritative.  
   {: note}

1. Update name servers at your registrar:

   1. In the CIS console, note the **assigned name servers** (for example, `ns004.name.cloud.ibm.com`, `ns005.name.cloud.ibm.com`).  
   1. Log in to your domain registrar.  
   1. Locate your domain’s **DNS / Nameserver settings**.  
   1. Replace the existing name servers with the CIS name servers exactly as provided.  
   1. Save the changes.

   Ensure name servers are entered accurately. Typos or omissions break DNS resolution.
   {: note}

1. Wait for propagation and verify:

   * DNS changes can take **24–48 hours**, or in rare cases up to **72 hours**, to propagate globally.  
   * Use `dig` or `nslookup` to confirm that the domain now resolves with CIS name servers.  
   * The CIS console automatically detects when delegation is complete, and the domain status changes from **Pending** to **Active**. 

1. Optionally, after propagation, re-enable DNSSEC at your registrar if required. Use the DS records provided by CIS to complete DNSSEC setup.  

1. Confirm DNS functionality:

   1. Test your domain’s website, email, and any other services.  
   1. Ensure all DNS records (for example, A, MX, TXT, CAA) are resolving correctly.  
   1. Troubleshoot any issues by checking records in CIS or verifying name server settings at your registrar.  
 
