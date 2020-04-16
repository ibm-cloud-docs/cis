---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

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

1. Click **Overview** on the left side of the Getting Started screen. Input your Domain Name (or Sub-domain Name) and click **Add domain**.

    ![IMAGE](images/reliability3.png)

    The IBM Cloud Internet Service is not a DNS registrar, so this domain (or sub-domain) must have been previously created.
    {:note}

    Under the Service Details section, you’ll notice that the newly-added domain will initially show up in a Pending state.

    ![IMAGE](images/reliability4.png)    

2. Navigate to the administration page for your domain with your respective DNS registrar, and delegate your domain/sub-domain to IBM name servers by defining NS records.

You may have to wait up to 24 hours for your information to replicate in the DNS database. Once it does, your domain state will change to Active.

![IMAGE](images/reliability5.png)
