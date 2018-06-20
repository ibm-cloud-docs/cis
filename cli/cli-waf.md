---

copyright:
  years: 2018
lastupdated: "2018-06-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Web Application Firewall (WAF)

The following `waf` commands are available:

* Show WAF setting
* Update WAF settings
* List WAF packages
* Show a WAF package
* Update WAF OWASP package
* List WAF groups
* Show a WAF group
* Update a WAF group
* List WAF rules
* Show a WAF rule
* Update a WAF rule


## Show WAF setting

**NAME**

  `waf-setting` - Show WAF setting.

**USAGE**

  `ibmcloud cis waf-setting DNS_DOMAIN_ID`
  
**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.

**OPTIONS**

   `-i, --instance`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

**Output Message**

   * waf setting ID
   * waf mode



## Update WAF Setting

**NAME**

  `waf-setting-update` - Update WAF setting.

**USAGE**

  `ibmcloud cis waf-setting-update DNS_DOMAIN_ID WAF_MODE`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.
   
   `WAF_MODE` is the mode of WAF setting. Valid values are:  `waf-enable` , `waf-disable`.

**OPTIONS**

   `-i, --instance`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

**Output Message**

   * waf setting ID
   * waf mode

## List WAF packages

**NAME**

  `waf-packages` - List all WAF packages.

**USAGE**

  `ibmcloud cis waf-packages DNS_DOMAIN_ID`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.

**OPTIONS**

   `-i, --instance`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

**Output Message**

   * package ID
   * package name
   * package mode



## Show a WAF package

**NAME**

  `waf-package` - Get detail of a package.

**USAGE**

  `ibmcloud cis waf-package DNS_DOMAIN_ID WAF_PACKAGE_ID`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.
   
   `WAF_PACKAGE_ID` is the ID of WAF package.

**OPTIONS**

   `-i, --instance`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

**Output Message**
   * Package ID
   * Package Name
   * Package Description
   * Package Mode



## Update WAF OWASP package

**NAME**

  `waf-package-set` - Set config of the OWASP package.

**USAGE**

  `ibmcloud cis waf-package-set DNS_DOMAIN_ID OWASP_PACKAGE_ID SENSITIVITY ACTION_MODE`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.
   
   `OWASP_PACKAGE_ID` is the package ID of OWASP.
   
   `SENSITIVITY` is the sensitivity of the package. Valid values are: `high`, `low`, `off`.
   
   `ACTION_MODE` is the action that is taken for rules under the package. Valid values are: `simulate`, `block`, `challenge`.

**OPTIONS**

   `-i, --instance`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

**Output Message**

   * Package ID
   * Package Name
   * Package Description
   * Package Detection Mode
   * Domain ID
   * Package Status
   * Package Sensitivity
   * Package Action Mode


## List WAF groups

**NAME**

  `waf-groups` - List WAF groups in a given WAF package.

**USAGE**

  `ibmcloud cis waf-groups DNS_DOMAIN_ID WAF_PACKAGE_ID`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.
   
   `WAF_PACKAGE_ID` is the ID of WAF package.

**OPTIONS**

   `-i, --instance`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

**Output Message**
   * Group ID
   * Group Name
   * Group Description
   * Group Mode


## Show a WAF group

**NAME**

  `waf-group` - Get detail of a WAF group.

**USAGE**

  `ibmcloud cis waf-group DNS_DOMAIN_ID WAF_PACKAGE_ID WAF_GROUP_ID`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.
   
   `WAF_PACKAGE_ID` is the ID of WAF package.
   
   `WAF_GROUP_ID` is the ID of WAF group.
   
**OPTIONS**

   `-i, --instance`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

**Output Message**
   * Group Name
   * Group ID
   * Group mode
   * Group Description
   * Rules Count
   * Modified Rules Count


## Update a WAF group

**NAME**

  `waf-group-mode-set` - Set mode of a WAF group.

**USAGE**

  `ibmcloud cis waf-group-mode-set DNS_DOMAIN_ID WAF_PACKAGE_ID WAF_GROUP_ID WAF_GROUP_MODE`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.
   
   `WAF_PACKAGE_ID` is the ID of WAF package.
   
   `WAF_GROUP_ID` is the ID of WAF group.
   
   `WAF_GROUP_MODE` is the mode of WAF group. Valid values are: `on`, `off`.

**OPTIONS**

   `-i, --instance`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

**Output Message**
   * Group ID
   * Group Mode


## List WAF rules

**NAME**

  `waf-rules` - List all WAF rules of a given WAF package.

**USAGE**

  `ibmcloud cis waf-rules DNS_DOMAIN_ID WAF_PACKAGE_ID`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.
   
   `WAF_PACKAGE_ID` is the ID of WAF package.

**OPTIONS**

   `-i, --instance`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
   
   `-p, --page-no` Page num
   
   `-n, --number-per-page`  Number of rules per page. Min value is `5` and max value is `1000`.

**Output Message**

   * Rule ID
   * Rule Description
   * Rule Current Mode



## Show a WAF rule

**NAME**

  `waf-rule` - Get detail of a WAF rule.

**USAGE**

  `ibmcloud cis waf-rule DNS_DOMAIN_ID WAF_PACKAGE_ID WAF_RULE_ID`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.
   
   `WAF_PACKAGE_ID` is the ID of WAF package.
   
   `WAF_RULE_ID` is the ID of WAF rule.

**OPTIONS**

   `-i, --instance`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

**Output Message**
   * Rule ID
   * Rule Description
   * Rule Current Mode
   * Rule Default Mode
   * Rule Allowed Mode
   * Rule Priority
   * Group ID of the rule belonging to
   * Group Name of the rule belonging to


## Update a WAF rule

**NAME**

  `waf-rule-mode-set` - Set mode of a WAF rule.

**USAGE**

  `ibmcloud cis waf-rule-mode-set DNS_DOMAIN_ID WAF_PACKAGE_ID WAF_RULE_ID WAF_RULE_MODE`  

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.
   
   `WAF_PACKAGE_ID` is the ID of WAF package.
   
   `WAF_RULE_ID` is the ID of WAF rule.
   
   `WAF_RULE_MODE` is the mode of WAF rule. Valid values are: `on`, `off`, `default`, `disable`, `simulate`, `block`,  `challenge`.

**OPTIONS**

   `-i, --instance`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

**Output Message**
   * Rule ID
   * Rule Current Mode
