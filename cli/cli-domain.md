---

copyright:
  years: 2018
lastupdated: "2018-06-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Domain

The following `domain` commands are available:

* Add domain
* Resume domain
* Pause domain
* Display domain
* Remove domain
* List domains
* Domain activation check

## Add domain
**NAME**

   `domain-add` - Add a domain.

**USAGE**

   `ibmcloud cis domain-add DNS_DOMAIN_NAME [-i, --instance INSTANCE_NAME] [-o, --output OUTPUT_FILE]`

**ARGUMENTS**

   `DNS_DOMAIN_NAME` is the FQDN of DNS domain.

**OPTIONS**

   `-i, --instance`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `-o, --output`    Output the result as JSON style to a file. If not set, outputs the result to terminal.

**Output**
  * ID                     
  * Created On         
  * Modified On  
  * Name                   
  * Original Registrar
  * Origin DNS Host
  * Status                
  * Paused                 
  * Original Name Server
  * Name Servers         

## Resume domain

**NAME**

   `domain-resume` - Resume the given domain.

**USAGE**

   `ibmcloud cis domain-resume DNS_DOMAIN_ID [-i, --instance INSTANCE_NAME] [-o, --output OUTPUT_FILE]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.

**OPTIONS**

   `-i, --instance`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `-o, --output`    Output the result as JSON style to a file. If not set, outputs the result to terminal.


**Output**
  * ID                     
  * Created On         
  * Modified On  
  * Name                   
  * Original Registrar
  * Origin DNS Host
  * Status                
  * Paused                 
  * Original Name Server
  * Name Servers         

## Pause domain

**NAME**

   `domain-pause` - Pause the given domain.

**USAGE**

   `ibmcloud cis domain-pause DNS_DOMAIN_ID [-i, --instance INSTANCE_NAME] [-o, --output OUTPUT_FILE]`

**ARGUMENTS**

   DNS_DOMAIN_ID is the ID of DNS domain.

**OPTIONS**

   `-i, --instance`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `-o, --output`    Output the result as JSON style to a file. If not set, outputs the result to terminal.

**Output**
  * ID                     
  * Created On         
  * Modified On  
  * Name                   
  * Original Registrar
  * Origin DNS Host
  * Status                
  * Paused                 
  * Original Name Server
  * Name Servers         

## Display domain

**NAME**

   `domain` - Display the given domain details.

**USAGE**

   `ibmcloud cis domain DNS_DOMAIN_ID [-i, --instance INSTANCE_NAME] [-o, --output OUTPUT_FILE]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.

**OPTIONS**

   `-i, --instance`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `-o, --output`    Output the result as JSON style to a file. If not set, outputs the result to terminal.

**Output**
  * ID                     
  * Created On         
  * Modified On  
  * Name                   
  * Original Registrar
  * Origin DNS Host
  * Status                
  * Paused                 
  * Original Name Server
  * Name Servers         

## Remove domain

**NAME**

   `domain-remove` - Remove a domain.

**USAGE**

   `ibmcloud cis domain-remove DNS_DOMAIN_ID [-i, --instance INSTANCE_NAME]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.

**OPTIONS**

   `-i, --instance`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.


## List domains

**NAME**

   `domains` - List domains for a given service instance.

**USAGE**

   `ibmcloud cis domains [-i, --instance INSTANCE_NAME] [-o, --output OUTPUT_FILE]`

**OPTIONS**

   `-i, --instance`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `-o, --output`    Output the result as JSON style to a file. If not set, outputs the result to terminal.


**Output**
  * ID                      
  * Name                   
  * Status                
  * Paused                 


## Domain activation check

**NAME**

   `domain-activation-check` - Perform activation check on the given domain.

**USAGE**

   `ibmcloud cis domain-activation-check DNS_DOMAIN_ID [-i, --instance INSTANCE_NAME]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.

**OPTIONS**

   `-i, --instance`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
