---

copyright:
  years: 2018
lastupdated: "2018-05-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Pagerule

The following `pagerule` commmands are available:
* Create
* Update
* Delete
* List
* Show

## Create Page Rule

### NAME:
   page-rule-create - Create a page rule of the DNS domain.

### USAGE:
   ibmcloud cis page-rule-create DNS_DOMAIN_ID (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE_NAME] [-o, --output OUTPUT_FILE]

### ARGUMENTS:
   DNS_DOMAIN_ID is the id of DNS domain.

### OPTIONS:
   -s, --json-str  The JSON data describing a page rule.

                   The required fields in JSON data are targets, actions:

                       "targets":The target URL pattern to evaluate on a request.
                       "actions":An array of actions to perform if the targets of this rule match the request. Available actions are:
                           disable_security, always_use_https, ssl, browser_cache_ttl,
                           security_level, cache_level, edge_cache_ttl, bypass_cache_on_cookie,
                           browser_check, server_side_exclude, always_online, email_obfuscation,
                           automatic_https_rewrites, opportunistic_encryption, ip_geolocation,
                           explicit_cache_control, cache_deception_armor, waf and forwarding_url.

                   The optional fields are priority, status:

                       "priority":A number that indicates the preference for a page rule over another. Default is 1.
                       "status":Status of the page rule. The valid values are 'active' and 'disabled', default is 'disabled'.

                   Sample JSON data:

                   {
                       "targets": [
                           {
                               "target": "url",
                               "constraint": {
                                   "operator": "matches",
                                   "value": "*example.com/images/*"
                               }
                           }
                       ],
                       "actions": [
                           {
                               "id": "always_online",
                               "value": "on"
                           },
                           {
                               "id": "ssl",
                               "value": "flexible"
                           },
                           {
                               "id": "browser_cache_ttl",
                               "value": 14400
                           },
                           {
                               "id": "security_level",
                               "value": "medium"
                           },
                           {
                               "id": "cache_level",
                               "value": "basic"
                           },
                           {
                               "id": "edge_cache_ttl",
                               "value": 7200
                           },
                           {
                               "id": "bypass_cache_on_cookie",
                               "value": "wp-.*|wordpress.*|comment_.*"
                           }
                       ]
                   }
                   
   -j, --json-file  A file contains input JSON data.
   
   -i, --instance   Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' will be used.
   
   -o, --output     Output the result as JSON style to a file. If not set, will output the result to terminal.

#### Output Message:
   * page rule id
   * target
   * priority
   * status
   * actions table (columns as below):
       * action ID
       * action value



## Update a Page Rule

### NAME:
   page-rule-update - Update the page rule of the DNS domain.

### USAGE:
   ibmcloud cis page-rule-update DNS_DOMAIN_ID PAGE_RULE_ID (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE_NAME] [-o, --output OUTPUT_FILE]

### ARGUMENTS:
   DNS_DOMAIN_ID is the id of DNS domain.
   
   PAGE_RULE_ID is the id of page rule.

### OPTIONS:
   -s, --json-str  The JSON data describing a page rule.

                   The required fields in JSON data are targets, actions:

                       "targets":The target URL pattern to evaluate on a request.
                       "actions":An array of actions to perform if the targets of this rule match the request. Available actions are:
                           disable_security, always_use_https, ssl, browser_cache_ttl,
                           security_level, cache_level, edge_cache_ttl, bypass_cache_on_cookie,
                           browser_check, server_side_exclude, always_online, email_obfuscation,
                           automatic_https_rewrites, opportunistic_encryption, ip_geolocation,
                           explicit_cache_control, cache_deception_armor, waf and forwarding_url.

                   The optional fields are priority, status:

                       "priority":A number that indicates the preference for a page rule over another. Default is 1.
                       "status":Status of the page rule. The valid values are 'active' and 'disabled', default is 'disabled'.

                   Sample JSON data:

                   {
                       "targets": [
                           {
                               "target": "url",
                               "constraint": {
                                   "operator": "matches",
                                   "value": "*example.com/images/*"
                               }
                           }
                       ],
                       "actions": [
                           {
                               "id": "always_online",
                               "value": "on"
                           },
                           {
                               "id": "ssl",
                               "value": "flexible"
                           },
                           {
                               "id": "browser_cache_ttl",
                               "value": 14400
                           },
                           {
                               "id": "security_level",
                               "value": "medium"
                           },
                           {
                               "id": "cache_level",
                               "value": "basic"
                           },
                           {
                               "id": "edge_cache_ttl",
                               "value": 7200
                           },
                           {
                               "id": "bypass_cache_on_cookie",
                               "value": "wp-.*|wordpress.*|comment_.*"
                           }
                       ]
                   }
                   
   -j, --json-file  A file contains input JSON data.
   
   -i, --instance   Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' will be used.
   
   -o, --output     Output the result as JSON style to a file. If not set, will output the result to terminal.

#### Output Message:
   * page rule id
   * target
   * priority
   * status
   * actions table (columns as below):
       * action ID
       * action value



## Delete a Page Rule

### NAME:
   page-rule-delete - Delete a page rule of the DNS domain.

### USAGE:
   ibmcloud cis page-rule-delete DNS_DOMAIN_ID PAGE_RULE_ID [-i, --instance INSTANCE_NAME]

### ARGUMENTS:
   DNS_DOMAIN_ID is the id of DNS domain.
   
   PAGE_RULE_ID is the id of page rule.

### OPTIONS:
   -i, --instance  Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' will be used.

#### Output Message:
   * result of deleting the page rule


## List Page Rules

### NAME:
   page-rules - List page rules of the DNS domain.

### USAGE:
   ibmcloud cis page-rules DNS_DOMAIN_ID [-i, --instance INSTANCE_NAME] [-o, --output OUTPUT_FILE]

### ARGUMENTS:
   DNS_DOMAIN_ID is the id of DNS domain.

### OPTIONS:
   -i, --instance  Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' will be used.
   
   -o, --output    Output the result as JSON style to a file. If not set, will output the result to terminal.

#### Output Table Columns:
   * page rule id
   * target
   * priority
   * status


## Show a Page Rule

### NAME:
   page-rule - Get details of a page rule.

### USAGE:
   ibmcloud cis page-rule DNS_DOMAIN_ID PAGE_RULE_ID [-i, --instance INSTANCE_NAME] [-o, --output OUTPUT_FILE]

### ARGUMENTS:
   DNS_DOMAIN_ID is the id of DNS domain.
   
   PAGE_RULE_ID is the id of page rule.

### OPTIONS:
   -i, --instance  Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' will be used.
   
   -o, --output    Output the result as JSON style to a file. If not set, will output the result to terminal.


#### Output Message:
   * page rule id
   * target
   * priority
   * status
   * actions table (columns as below):
     1. action ID
     1. action value


