---

copyright:
  years: 2018
lastupdated: "2018-12-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Routing

The following `routing` commands are available:

* Show routing
* Update routing settings
* Show routing analytics

## Show Routing Setting

**NAME**

  `routing` - Get details of Routing settings. (enterprise plan only)

**USAGE**

  `ibmcloud cis routing DNS_DOMAIN_ID (--smart-routing | --tiered-caching) [-i, --instance INSTANCE_NAME]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.
   
**OPTIONS**

   `--smart-routing`  One of Routing features.

   `--tiered-caching` One of Routing features.

   `-i, --instance`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

**Output Message**

* routing feature ID
* routing feature value
* routing feature modified time


## Update Routing Setting

**NAME**

  `routing-update` - Update Routing setting. (enterprise plan only)

**USAGE**

  `ibmcloud cis routing-update DNS_DOMAIN_ID  (--smart-routing (on | off) | --tiered-caching (on | off)) [-i, --instance INSTANCE_NAME]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.
   
**OPTIONS**

   `--smart-routing value`       One of Routing features. Valid values: "on", "off".

   `--tiered-caching value`      One of Routing features. Valid values: "on", "off".
   
   `-i, --instance`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

**Output Message**

* routing feature id
* routing feature value
* routing feature modified time

## Display routing analytics

**NAME**

   `routing-analytics` - Get analytics of smart-routing latency. (enterprise plan only)

**USAGE**

   `ibmcloud cis routing-analytics DNS_DOMAIN_ID [--colos] [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the id of DNS domain.

**OPTIONS**

   `--colos`                      Analytics of smart-routing latency colos.
   
   `-i value, --instance value`   Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `-o value, --output value`     Specify output format, only JSON is supported now.


**Output Message**
  * Analytics Data
