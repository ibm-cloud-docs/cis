---

copyright:
  years: 2018
lastupdated: "2018-09-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Firewall

The following `firewall` commands are available:

* Create
* Update
* List
* Detail
* Delete

## Create Firewall

**NAME**

   `firewall-create` - Create a new firewall rule.

**USAGE**

   `ibmcloud cis firewall-create (-t, --type Type) (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-d --domain DNS_DOMAIN_ID] [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]`

**OPTIONS**

`-t value, --type value`  Type of firewall rule to create. Valid values: `access-rules`, `ua-rules`, `lockdowns`.
  
  * `access-rules`: Access Rules are a way to allow, challenge, or block requests to your website. You can apply access rules to one domain only or all domains in the same service instance.
  * `ua-rules`: Perform access control when matching the exact UserAgent reported by the client. The access control mechanisms can be defined within a rule to help manage traffic from particular clients. This enables you to customize the access to your site.
  * `lockdowns`: Lock access to URLs in this domain to only permitted addresses or address ranges.
    
`-d value, --domain value`    DNS Domain ID.
   
`-s value, --json-str value`  The JSON data describing a firewall rule. Enter `ibmcloud cis help firewall-create -t [type]` for details JSON data format.
   
`-j value, --json-file value`  A file contains input JSON data.
   
`-i value, --instance value`   Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
   
`-o value, --output value`     Specify output format, only JSON is supported now.

### Create Firewall with access rules

**NAME**

   `firewall-create -t access-rules` - Create a new firewall access rule for a given service instance.

**USAGE**

   `ibmcloud cis firewall-create -t access-rules [-d --domain DNS_DOMAIN_ID] (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]`

**OPTIONS**
   
  `-d value, --domain value`    DNS Domain ID. If not set, this is an instance level firewall access rule.
  
  `-s value, --json-str value`  The JSON data describing a firewall access rule.

The required fields in JSON data are `mode`, `notes`.

 * `mode`: The type of action to perform. Valid values: `block`, `challenge`, `whitelist`, `js_challenge`.
 * `notes`: Some useful information about this rule to help identify the purpose of it.

The optional field is `configuration`.

 * `configuration`: Target/Value pair to use for this rule.
   * `target`: The request property to target. Valid values: "ip", "ip_range", "asn", "country".
   * `value`: The value for the selected target.
     * For `ip` the value is a valid IP address.
     * For `ip_range` the value specifies IP range limited to /16 and /24.
     * For `asn` the value is an AS number.
     * For `country` the value is a country code for the country.

**Sample JSON data:**

```
                   {
                       "mode": "block",
                       "notes": "This rule is added because of event X that occurred on date xyz",
                       "configuration": {
                           "target": "ip",
                           "value": "127.0.0.1"
                       }
                   }
 ```  
   
   `-j value, --json-file value`  A file contains input JSON data.
   
   `-i value, --instance value`   Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
   
   `-o value, --output value`     Specify output format, only JSON is supported now.


### Create Firewall with user agent rules

**NAME**

   `firewall-create -t ua-rules` - Create a new user-agent rule for a given domain under a service instance.

**USAGE**

   `ibmcloud cis firewall-create -t ua-rules (-d --domain DNS_DOMAIN_ID) (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]`

**OPTIONS**

   `-d value, --domain value`    DNS Domain ID.
   
   `-s value, --json-str value`  The JSON data describing a user-agent rule.

The required field in JSON data is `mode`.

  * `mode`: The type of action to perform. Valid values: `block`, `challenge`, `js_challenge`.

The optional fields are `paused`, `description`, `configuration`.

  * `paused`: Whether this rule is currently disabled.
  * `description`: Some useful information about this rule to help identify the purpose of it.
  * `configuration`: Target/Value pair to use for this rule.
     * `target`: The request property to target. Valid values: `ua`.
     * `value`: The exact UserAgent string to match with this rule.

**Sample JSON data:**
```
                   {
                       "mode": "block",
                       "configuration": {
                           "target": "ua",
                           "value": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/603.2.4 (KHTML, like Gecko) Version/10.1.1 Safari/603.2.4"
                       }
                   }
  ```                 
                   
   `-j value, --json-file value`  A file contains input JSON data.
   
   `-i value, --instance value`  Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' will be used.
   
   `-o value, --output value`     Specify output format, only JSON is supported now.


### Create Firewall with lockdowns
**NAME**

   `firewall-create -t lockdowns` - Create a new lockdown rule for a given zone under a service instance.

**USAGE**

   `ibmcloud cis firewall-create -t lockdowns (-d --domain DNS_DOMAIN_ID) (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]`

**OPTIONS**

   `-d value, --domain value`   DNS Domain ID.
   
   `-s value, --json-str value`  The JSON data describing a user-agent rule.

The optional fields are `paused`, `description`, `urls`, `configurations`.

   * `paused`: Whether this rule is currently disabled.
   * `description`: Some useful information about this rule to help identify the purpose of it.
   * `urls`: URLs included in this rule definition. Wildcards are permitted. The URL pattern entered here is escaped before use. This limits the URL to just simple wildcard patterns.
   * `configurations`: List of IP addresses or CIDR ranges to use for this rule. This can include any number of `ip` or `ip_range` configurations that can access the provided URLs.
     * `target`: The request property to target. Valid values: `ip`, `ip_range`.
     * `value`: IP addresses or CIDR. If target is `ip`, then value is an IP addresses, otherwise CIDR.

**Sample JSON data:**
```
                  {
                       "urls": [
                           "api.mysite.com/some/endpoint*"
                       ],
                       "configurations": [
                           {
                               "target": "ip",
                               "value": "127.0.0.1"
                           },
                           {
                               "target": "ip_range",
                               "value": " 2.2.2.0/24"
                           }
                       ]
                   }
```                   
   `-j value, --json-file value`  A file contains input JSON data.
   
   `-i value, --instance value`   Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
   
   `-o value, --output value`     Specify output format, only JSON is supported now.


## Update Firewall rule

**NAME**

   `firewall-update` - Update a firewall rule.

**USAGE**

   `ibmcloud cis firewall-update FIREWALL_RULE_ID (-t, --type Type) (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-d --domain DNS_DOMAIN_ID] [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]`

**ARGUMENTS**

   `FIREWALL_RULE_ID` is the ID of firewall rule.

**OPTIONS**

`-t value, --type value`  Type of firewall rule to update. Valid values: `access-rules`, `ua-rules`, `lockdowns`.
   
  * `access-rules`: Access Rules are a way to allow, challenge, or block requests to your website. You can apply access rules to one domain only or all domains in the same service instance.
  * `ua-rules`: Perform access control when matching the exact UserAgent reported by the client. The access control mechanisms can be defined within a rule to help manage traffic from particular clients. This enables you to customize the access to your site.
  * `lockdowns`: Lock access to URLs in this domain to only permitted addresses or address ranges.
   
`-d value, --domain value`    DNS Domain ID.
   
`-s value, --json-str value`  The JSON data describing a firewall rule. Enter `ibmcloud cis help firewall-update -t [type]` for details JSON data format.
   
`-j value, --json-file value`  A file contains input JSON data.
   
`-i value, --instance value`   Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
   
`-o value, --output value`     Specify output format, only JSON is supported now.

### Update Firewalls with access rules

**NAME**

   `firewall-update -t access-rules` - Update a new firewall access rule for a given service instance.

**USAGE**

   `ibmcloud cis firewall-update -t access-rules [-d --domain DNS_DOMAIN_ID] (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]`

**OPTIONS**

   `-d value, --domain value`    DNS Domain ID. If not set, this is an instance level firewall access rule.
   
   `-s value, --json-str value`  The JSON data describing a firewall access rule.

The required fields in JSON data are `mode`, `notes`.

  * `mode`: The type of action to perform. Valid values: `block`, `challenge`, `whitelist`, `js_challenge`.
  * `notes`: Some useful information about this rule to help identify the purpose of it.

The optional field is `configuration`.

  * `configuration`: Target/Value pair to use for this rule.
    * `target`: The request property to target. Valid values: `ip`, `ip_range`, `asn`, `country`.
    * `value`: The value for the selected target.
      *  For ip the value is a valid ip address.
      *  For ip_range the value specifies ip range limited to /16 and /24.
      *  For asn the value is an AS number.
      *  For country the value is a country code for the country.

**Sample JSON data:**

```
                   {
                       "mode": "challenge",
                       "notes": "This rule is added because of event X that occurred on date xyz",
                   }
```   
   `-j value, --json-file value`  A file contains input JSON data.
   
   `-i value, --instance value`   Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
   
   `-o value, --output value`     Specify output format, only JSON is supported now.

### Update Firewalls with user agent rules
**NAME**

   `firewall-update -t ua-rules` - Update a new user-agent rule for a given domain under a service instance.

**USAGE**

   `ibmcloud cis firewall-update -t ua-rules (-d --domain DNS_DOMAIN_ID) (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]`

**OPTIONS**

   `-d value, --domain value`    DNS Domain ID.
   
   `-s value, --json-str value`  The JSON data describing a user-agent rule.

The required field in JSON data is `mode`.

  * `mode`: The type of action to perform. Valid values: `block`, `challenge`, `js_challenge`.

The optional fields are `paused`, `description`, `configuration`.

  * `paused`: Whether this rule is currently disabled.
  * `description`: Some useful information about this rule to help identify the purpose of it.
  * `configuration`: Target/Value pair to use for this rule.
    * `target`: The request property to target. Valid values: `ua`.
    * `value`: The exact UserAgent string to match with this rule.
    
**Sample JSON data:**

```
                   {
                       "mode": "block",
                       "configuration": {
                           "target": "ua",
                           "value": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/603.2.4 (KHTML, like Gecko) Version/10.1.1 Safari/603.2.4"
                       }
                   }
```

   `-j value, --json-file value`  A file contains input JSON data.
   
   `-i value, --instance value`   Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
   
   `-o value, --output value`    Specify output format, only JSON is supported now.


### Update Firewalls with lockdowns

**NAME**

   `firewall-update -t lockdowns` - Update a new lockdown rule for a given zone under a service instance.

**USAGE**

   `ibmcloud cis firewall-update -t lockdowns (-d --domain DNS_DOMAIN_ID) (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]`

**OPTIONS**

   `-d value, --domain value`    DNS Domain ID.
   
   `-s value, --json-str value`  The JSON data describing a lockdown rule.

The optional fields are `paused`, `description`, `urls`, `configurations`.

  * `paused`: Whether this rule is currently disabled.
  * `description`: Some useful information about this rule to help identify the purpose of it.
  * `urls`: URLs to be included in this rule definition. Wildcards are permitted. The URL pattern entered here will be escaped before use. This limits the URL to just simple wildcard patterns.
  * `configurations`: List of IP addresses or CIDR ranges to use for this rule. This can include any number of ip or ip_range configurations that can access the provided URLs.
    * `target`: The request property to target. Valid values: `ip`, `ip_range`.
    * `value`: IP addresses or CIDR. If target is `ip`, then value should be an IP addresses, otherwise CIDR.

**Sample JSON data:**
```
                   {
                       "urls": [
                           "api.mysite.com/some/endpoint*"
                       ],
                       "configurations": [
                           {
                               "target": "ip",
                               "value": "127.0.0.1"
                           },
                           {
                               "target": "ip_range",
                               "value": " 2.2.2.0/24"
                           }
                       ]
                   }
```

   `-j value, --json-file value`  A file contains input JSON data.
   
   `-i value, --instance value`   Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
   
   `-o value, --output value`     Specify output format, only JSON is supported now.

## List Firewall rules

**NAME**

   `firewalls` - List firewall rules.

**USAGE**

   `ibmcloud cis firewalls (-t, --type Type) [-d --domain DNS_DOMAIN_ID] [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]`

**OPTIONS**

`-t value, --type value`  Type of firewall rule to list. Valid values: `access-rules`, `ua-rules`, `lockdowns`.
  
  * `access-rules`: Access Rules are a way to allow, challenge, or block requests to your website. You can apply access rules to one domain only or all domains in the same service instance.
  * `ua-rules`: Perform access control when matching the exact UserAgent reported by the client. The access control mechanisms can be defined within a rule to help manage traffic from particular clients. This will enable you to customize the access to your site.
  * `lockdowns`: Lock access to URLs in this domain to only permitted addresses or address ranges.
    
`-d value, --domain value`    DNS Domain ID.
   
`--page value`                Page number of paginated results. (default: 0)
   
`--per-page value`            Maximum number of access rules per page. The minimum value is 5. (default: 20)
   
`-i value, --instance value`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
   
`-o value, --output value`    Specify output format, only JSON is supported now.


## Detail Firewall rule

**NAME**

   `firewall` - Get details of a firewall rule settings.

**USAGE**

   `ibmcloud cis firewall FIREWALL_RULE_ID (-t, --type Type) [-d --domain DNS_DOMAIN_ID] [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]`

**ARGUMENTS**

   `FIREWALL_RULE_ID` is the ID of firewall rule.

**OPTIONS**

`-t value, --type value`  Type of firewall settings to check. Valid values: `access-rules`, `ua-rules`, `lockdowns`.
      
  * `access-rules`: Access Rules are a way to allow, challenge, or block requests to your website. You can apply access rules to one domain only or all domains in the same service instance.
  * `ua-rules`: Perform access control when matching the exact UserAgent reported by the client. The access control mechanisms can be defined within a rule to help manage traffic from particular clients. This will enable you to customize the access to your site.
  * `lockdowns`: Lock access to URLs in this domain to only permitted addresses or address ranges.
   
`-d value, --domain value`    DNS Domain ID.
   
`-i value, --instance value`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
   
`-o value, --output value`    Specify output format, only JSON is supported now.

## Delete Firewall

**NAME**

   `firewall-delete` - Delete  a firewall rule by ID.

**USAGE**

   `ibmcloud cis firewall-delete FIREWALL_RULE_ID (-t, --type Type) [-d --domain DNS_DOMAIN_ID] [-i, --instance INSTANCE_NAME]`

**ARGUMENTS**

   `FIREWALL_RULE_ID` is the ID of firewall rule.

**OPTIONS**

`-t value, --type value`  Type of firewall rule to delete. Valid values: `access-rules`, `ua-rules`, `lockdowns`.

  * `access-rules`: Access Rules are a way to allow, challenge, or block requests to your website. You can apply access rules to one domain only or all domains in the same service instance.
  * `ua-rules`: Perform access control when matching the exact UserAgent reported by the client. The access control mechanisms can be defined within a rule to help manage traffic from particular clients. This will enable you to customize the access to your site.
  * `lockdowns`: Lock access to URLs in this domain to only permitted addresses or address ranges.
  
   
`-d value, --domain value`    DNS Domain ID.
   
`-i value, --instance value`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
