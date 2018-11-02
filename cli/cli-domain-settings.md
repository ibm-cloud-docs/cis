---

copyright:
  years: 2018
lastupdated: "2018-10-29"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Domain

The following `domain-settings` commands are available:

* Display domain-settings
* Update domain-settings

## Display domain-settings
**NAME**

   `domain-settings` - Display a domain settings.

**USAGE**

   `ibmcloud cis domain-settings DNS_DOMAIN_ID (-t, --type Type) [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the id of DNS domain.

**OPTIONS**

   `-t value, --type value`      Type of domain settings to check. Valid values: "automatic_https_rewrites", "browser_check", "cname_flattening", "opportunistic_encryption". 
   
                               "automatic_https_rewrites": 
                                   Help fix mixed content by changing "http" to "https" for all resources or links on your web site that can be served with HTTPS.
                                   
                               "browser_check": 
                                   Evaluate HTTP headers from your visitors browser for threats. If a threat is found a block page will be delivered.
                                   
                               "cname_flattening": 
                                   Follow a CNAME to where it points and return that IP address instead of the CNAME record.
                                   By default, only flatten the CNAME at the root of your domain.
                                   
                               "opportunistic_encryption": 
                                   Opportunistic Encryption allows browsers to benefit from the improved performance of HTTP/2 
                                   by letting them know that your site is available over an encrypted connection.
                                   
   `-i value, --instance value`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `-o value, --output value`    Specify output format, only JSON is supported now.

**Output**
  * ID                     
  * Value         
  * Modified On  
  * Editable      

## Update domain-settings

**NAME**

   `domain-settings-update` - Update a feature for the domain.

**USAGE**

   `ibmcloud cis domain-settings-update DNS_DOMAIN_ID (-t, --type Type) (-v, --value VALUE) [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the id of DNS domain.

**OPTIONS**

   `-t value, --type value`      Type of domain settings to check. Valid values: "automatic_https_rewrites", "browser_check", "cname_flattening", "opportunistic_encryption". 
   
                               "automatic_https_rewrites": 
                                   Help fix mixed content by changing "http" to "https" for all resources or links on your web site that can be served with HTTPS.
                                   
                               "browser_check": 
                                   Evaluate HTTP headers from your visitors browser for threats. If a threat is found a block page will be delivered.
                                   
                               "cname_flattening": 
                                   Follow a CNAME to where it points and return that IP address instead of the CNAME record.
                                   By default, only flatten the CNAME at the root of your domain.
                                   
                               "opportunistic_encryption": 
                                   Opportunistic Encryption allows browsers to benefit from the improved performance of HTTP/2 
                                   by letting them know that your site is available over an encrypted connection.

   `-v value, --type value`      The value set to the feature for domain.
 
                              Valid values for "cname_flattening" are "flatten_at_root", "flatten_all", "flatten_none".
                                  "flatten_at_root": Flatten CNAME at root domain. This is the default value.
                                  "flatten_all": Flatten all CNAME records under your domain.
                                  "flatten_none": Disable cname flattening.
                              Valid values for "opportunistic_encryption" are "on", "off".
                              Valid values for "automatic_https_rewrites" are "on", "off".
                              Valid values for "browser_check" are "on", "off".
   
   `-i value, --instance value`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `-o value, --output value`    Specify output format, only JSON is supported now.


**Output**
  * ID                     
  * Value         
  * Modified On  
  * Editable       
