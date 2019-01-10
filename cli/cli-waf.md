---

copyright:
  years: 2018
lastupdated: "2018-11-07"

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

   `-i, --instance INSTANCE_NAME`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.



## Update WAF Setting

**NAME**

  `waf-setting-update` - Update WAF setting.

**USAGE**

  `ibmcloud cis waf-setting-update DNS_DOMAIN_ID WAF_MODE`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.
   
   `WAF_MODE` is the mode of WAF setting. Valid values are:  `waf-enable` , `waf-disable`.

**OPTIONS**

   `-i, --instance INSTANCE_NAME`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

## List WAF packages

**NAME**

  `waf-packages` - List all WAF packages.

**USAGE**

  `ibmcloud cis waf-packages DNS_DOMAIN_ID [-i, --instance INSTANCE_NAME] [--output FORMAT]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.

**OPTIONS**

   `-i, --instance INSTANCE_NAME`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
   
   `--output FORMAT`    Specify output format, only JSON is supported now.



## Show a WAF package

**NAME**

  `waf-package` - Get detail of a package.

**USAGE**

  `ibmcloud cis waf-package DNS_DOMAIN_ID WAF_PACKAGE_ID [-i, --instance INSTANCE_NAME] [--output FORMAT]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.
   
   `WAF_PACKAGE_ID` is the ID of WAF package.

**OPTIONS**

   `-i, --instance INSTANCE_NAME`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `--output FORMAT`    Specify output format, only JSON is supported now.



## Update WAF OWASP package

**NAME**

  `waf-package-set` - Update OWASP Package setting.

**USAGE**

  `ibmcloud cis waf-package-set DNS_DOMAIN_ID OWASP_PACKAGE_ID [--sensitivity  SENSITIVITY] [--action_mode MODE] [-i, --instance INSTANCE_NAME] [--output FORMAT]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.
   
   `OWASP_PACKAGE_ID` is the package ID of OWASP.

**OPTIONS**

   `--sensitivity SENSITIVITY`   The sensitivity of the firewall package. Valid values: `high`, `medium`, `low`, `off`.
   
   `--action-mode MODE`   The default action that will be taken for rules under the firewall package. Valid values: `simulate`, `block`, `challenge`.

   `-i, --instance INSTANCE_NAME`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `--output FORMAT`    Specify output format, only JSON is supported now.


## List WAF groups

**NAME**

  `waf-groups` - List WAF groups in a given WAF package.

**USAGE**

  `ibmcloud cis waf-groups DNS_DOMAIN_ID WAF_PACKAGE_ID [--page PAGE] [--per-page NUM] [-i, --instance INSTANCE_NAME] [--output FORMAT]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.
   
   `WAF_PACKAGE_ID` is the ID of WAF package.

**OPTIONS**

   `--page PAGE`         Page number of paginated results. (default: 1)

   `--per-page NUM`    Number of groups per page.The min value is 5 and max value is 1000. (default: 50)

   `-i, --instance INSTANCE_NAME`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `--output FORMAT`    Specify output format, only JSON is supported now.


## Show a WAF group

**NAME**

  `waf-group` - Get detail of a WAF group.

**USAGE**

  `ibmcloud cis waf-group DNS_DOMAIN_ID WAF_PACKAGE_ID WAF_GROUP_ID [-i, --instance INSTANCE_NAME] [--output FORMAT]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.
   
   `WAF_PACKAGE_ID` is the ID of WAF package.
   
   `WAF_GROUP_ID` is the ID of WAF group.
   
**OPTIONS**

   `-i, --instance INSTANCE_NAME`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `--output FORMAT`    Specify output format, only JSON is supported now.


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

   `-i, --instance INSTANCE_NAME`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

  `--output FORMAT`    Specify output format, only JSON is supported now.


## List WAF rules

**NAME**

  `waf-rules` - List all WAF rules of a given WAF package.

**USAGE**

  `ibmcloud cis waf-rules DNS_DOMAIN_ID WAF_PACKAGE_ID [--page PAGE] [--per-page NUM] [-i, --instance INSTANCE_NAME] [--output FORMAT]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.
   
   `WAF_PACKAGE_ID` is the ID of WAF package.

**OPTIONS**

   `--page PAGE`                Page number of paginated results. (default: 1)

   `--per-page NUM`         Number of rules per page. (default: 50)

   `-i, --instance INSTANCE_NAME`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
   
   `--output FORMAT`    Specify output format, only JSON is supported now.



## Show a WAF rule

**NAME**

  `waf-rule` - Get detail of a WAF rule.

**USAGE**

  `ibmcloud cis waf-rule DNS_DOMAIN_ID WAF_PACKAGE_ID WAF_RULE_ID [-i, --instance INSTANCE_NAME] [--output FORMAT]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.
   
   `WAF_PACKAGE_ID` is the ID of WAF package.
   
   `WAF_RULE_ID` is the ID of WAF rule.

**OPTIONS**

   `-i, --instance INSTANCE_NAME`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `--output FORMAT`    Specify output format, only JSON is supported now.


## Update a WAF rule

**NAME**

  `waf-rule-mode-set` - Set mode of a WAF rule.

**USAGE**

  `ibmcloud cis waf-rule-mode-set DNS_DOMAIN_ID WAF_PACKAGE_ID WAF_RULE_ID WAF_RULE_MODE [-i, --instance INSTANCE_NAME] [--output FORMAT]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.
   
   `WAF_PACKAGE_ID` is the ID of WAF package.
   
   `WAF_RULE_ID` is the ID of WAF rule.
   
   `WAF_RULE_MODE` is the mode of WAF rule. Valid values are: `on`, `off`, `default`, `disable`, `simulate`, `block`,  `challenge`.

**OPTIONS**

   `-i, --instance INSTANCE_NAME`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `--output FORMAT`    Specify output format, only JSON is supported now.
