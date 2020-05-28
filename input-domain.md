---

copyright:
  years: 2018, 2020
lastupdated: "2020-05-21"

keywords: domain Input information, IBM Cloud Internet Service, Domain Name

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
{:table: .aria-labeledby="caption"}

# Input information about your domain
{:#input-information-about-your-domain}

Input information about the domain you wish to protect and provide global load balancing for.
{: shortdesc}

1. Click **Overview** on the left side navigation menu of the Getting Started screen, and then click **Let's get started**. 
1. Input your Domain Name (or Sub-domain Name) and click **Connect and continue**.
   The IBM Cloud Internet Service is not a DNS registrar, so this domain (or sub-domain) must have been previously created.
   {:note}

   In the **Domain** section, notice that the newly-added domain initially shows as a **Pending** state.    

1. Navigate to the administration page for your domain with your respective DNS registrar, and delegate your domain/sub-domain to IBM name servers by defining NS records.

You may have to wait up to 24 hours for your information to replicate in the DNS database. After it does, your domain state changes to **Active**.
