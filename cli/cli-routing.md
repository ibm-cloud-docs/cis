---

copyright:
  years: 2018
lastupdated: "2018-09-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Routing

The following `routing` commands are available:

* Show
* Update

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
