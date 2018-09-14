---



copyright:
  years: 2017
lastupdated: "2018-06-20"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Input information about your domain
Input information about the domain you wish to protect and provide global load balancing for.

1. Click **Overview** on the left side of the Getting Started screen. Input your Domain Name (or Sub-domain Name) and click **Add domain**. 
    
    <img src="images/reliability3.png" alt="drawing" style="width: 300px;"/>
    
    **NOTE:** The IBM Cloud Internet Service is not a DNS registrar, so this domain (or sub-domain) must have been previously created.

    Under the Service Details section, you’ll notice that the newly-added domain will initially show up in a Pending state. 

    <img src="images/reliability4.png" alt="drawing" style="width: 300px;"/>    

2. Navigate to the administration page for your domain with your respective DNS registrar, and delegate your domain/sub-domain to IBM name servers by defining NS records.

You may have to wait up to 24 hours for your information to replicate in the DNS database. Once it does, your domain state will change to Active. 

<img src="images/reliability5.png" alt="drawing" style="width: 300px;"/>    
