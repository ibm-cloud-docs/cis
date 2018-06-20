---

copyright:
  years: 2018
lastupdated: "2018-06-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# TLS

The following `tls` commands are available:

* Show TLS setting
* Update TLS settings
* List certificates
* Show a certificate
* Order dedicated certificate
* Upload certificate
* Update certificate
* Change the priority of custom certificate
* Delete certificate

## Show TLS setting
**NAME**

  `tls-settings` - Get TLS settings for a given domain.

**USAGE**

 `ibmcloud cis tls-settings DNS_DOMAIN_ID [-i, --instance INSTANCE_NAME]`

**OPTIONS**

  `-i, --instance INSTANCE_NAME`  (Optional) Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

**Output Message**
   * TLS Mode
   * Universal SSL
   * TLS 1.2 only
   * TLS 1.3



## Update TLS Settings

**NAME**

  `tls-settings-update` - Update tls settings for a given DNS domain.

**USAGE**

  `ibmcloud cis tls-settings-update DNS_DOMAIN_ID [--mode MODE] [--universal (true | false)]
                              [--tls-1-2-only (on | off)] [--tls-1-3 (on | off)] [-i, --instance INSTANCE_NAME]`

**OPTIONS**

   `-i, --instance INSTANCE_NAME`  (Optional) Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `--mode value:` Specify whether visitors can browse your website over a secure connection, and when they
                do, how CIS connect to your origin server.
                Valid values are: `off`, `client-to-edge`, `end-to-end-flexible`, `end-to-end-ca-signed`.
                See documentation link for detailed TLS mode description.
                https://console.bluemix.net/docs/infrastructure/cis/ssl-options.html#tls-options

   `--universal-ssl value:` Specify whether universal ssl is enabled for you domain. Valid values are `true` and
                                       `false`.

   `--tls-1-2-only value:`  Specify whether Crypto TLS 1.2 feature is enable for your domain. Enabling this
                                       feature prevents use of previous versions. Valid values are `on` and `off`.

   `--tls-1-3 value:`  Specify whether Crypto TLS 1.3 feature is enabled for your domain. Valid values are `on` and
                               `off`.

**Output Message**

  Result of updating tls settings


## List Certificates

**NAME**

  `certificates` - List all certificates for a given DNS domain, including shared, dedicated and custom certificates.

**USAGE**

   `ibmcloud cis certificates DNS_DOMAIN_ID [-i, --instance INSTANCE_NAME] [-o, --output OUTPUT_FILE]`

**OPTIONS**

   `-i, --instance INSTANCE_NAME`  (Optional) Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `-o, --output OUTPUT_FILE`  (Optional) Output the result as JSON style to a file. If not set, outputs the result to terminal.

**Output Table Columns**
   * Type
   * ID: for dedicated certificate only
   * Hosts:  not applicable for custom uploaded certificate
   * Primary certificate: not applicable for custom uploaded certificate
   * Certificates: not applicable for custom uploaded certificate
     * ID:  not applicable for universal certificate
     * Hosts: not applicable for universal certificate
     * Issuer: not applicable for universal certificate
     * Status: not applicable for universal certificate
     * Uploaded On: not applicable for universal certificate
     * Modified On:  not applicable for universal certificate
     * Expires On: not applicable for universal certificate
     * Signature: not applicable for universal certificate
     * Bundle method:  for custom uploaded certificate only
     * Domain ID: for custom uploaded certificate only
     * Priority: for custom uploaded certificate only

## Show a certificate

**NAME**

  `certificate` - Get details of a given shared, dedicated, custom certificate.

**USAGE**

 `ibmcloud cis certificate DNS_DOMAIN_ID (--cert-id CERT_ID | --universal) [-i, --instance INSTANCE_NAME] [-o, --output OUTPUT_FILE]`

**OPTIONS**

   `-i, --instance INSTANCE_NAME ` (Optional) Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `--cert-id value:` ID of dedicated or custom certificate.

   `--universal:` Show universal certificate details.

   `-o, --output OUTPUT_FILE`  (Optional) Output the result as JSON style to a file. If not set, outputs the result to terminal.


**Output message**

   * Type
   * ID: for dedicated certificate only
   * Hosts:  not applicable for custom uploaded certificate
   * Primary certificate: not applicable for custom uploaded certificate
   * Certificates: not applicable for custom uploaded certificate
     * ID:  not applicable for universal certificate
     * Hosts: not applicable for universal certificate
     * Issuer: not applicable for universal certificate
     * Status: not applicable for universal certificate
     * Uploaded On: not applicable for universal certificate
     * Modified On:  not applicable for universal certificate
     * Expires On: not applicable for universal certificate
     * Signature: not applicable for universal certificate
     * Bundle method:  for custom uploaded certificate only
     * Domain ID: for custom uploaded certificate only
     * Priority: for custom uploaded certificate only

## Order dedicated certificate

**NAME**

  `certificate-order` - Order a certificate pack with an optional list of hostnames for a given DNS domain.

**USAGE**

  `ibmcloud cis certificate-order DNS_DOMAIN_ID [--hostnames host1 --hostnames host2 ...] [-i, --instance INSTANCE_NAME] [-o, --output OUTPUT_FILE]`

**OPTIONS**

   `--hostnames`  (Optional) valid host names for the certificate packs. Add up to 50 custom hostnames - May
affect price.

   `-i, --instance INSTANCE_NAME`  (Optional) Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `-o, --output OUTPUT_FILE` (Optional) Output the result as JSON style to a file. If not set, outputs the result to terminal.

**Output Message**

   * Type
   * ID
   * Hosts
   * Primary certificate
   * Certificates
     * ID
     * Hosts
     * Issuer
     * Status
     * Uploaded On
     * Modified On
     * Expires On
     * Signature

## Upload certificate

**NAME**

 `certificate-upload` - Upload a custom certificate for a DNS domain

**USAGE**

  `ibmcloud cis certificate-upload DNS_DOMAIN_ID [-i, --instance INSTANCE_NAME] [-s, --json-str JSON_STR] [-j, --json-file JSON_FILE] [-o, --output OUTPUT_FILE]`

**OPTIONS**

   `-i, --instance INSTANCE_NAME`  (Optional) Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `-s, --json-str`  The JSON data used to upload a custom certificate.
   * The required fields in JSON data are `certificate`, `private_key`:
     * `certificate` SSL certificate or certificate and the intermediate(s) for the domain.
     * `private_key` Private key for the domain.
   * The optional fields are bundle_method:
     * `bundle_method` Bundle method, default value is `compatible`, valid values are: `compatible`, `modern` and `user-defined`.

   Sample JSON data:
   
                      {
                        "certificate": "xxx",
                        "private_key": "xxx",
                        "bundle_method": "compatible"
                      }
                      
   `-j, --json-file JSON_FILE`  (Optional) A file contains input JSON data.

   `-o, --output OUTPUT_FILE`  (Optional) Output the result as JSON style to a file. If not set, outputs the result to terminal.

**Output Message**

   * ID
   * Hosts
   * Issuer
   * Signature
   * Status
   * Bundle method
   * Domain ID
   * Uploaded On
   * Modified On
   * Expires On
   * Priority


## Update certificate

**NAME**

 `update-certificate` Update a custom certificate for a DNS domain.

**USAGE**

  `ibmcloud cis certificate-update DNS_DOMAIN_ID CERT_ID [-i, --instance INSTANCE_NAME] [-s, --json-str JSON_STR] [-j, --json-file JSON_FILE] [-o, --output OUTPUT_FILE]`

**OPTIONS**

`-i, --instance INSTANCE_NAME`  (Optional) Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
`-s, --json-str`  The JSON data used to update a custom certificate.
   * The required fields in JSON data are `certificate`, `private_key`:
     * `certificate` SSL certificate or certificate and the intermediate(s) for the domain.
     * `private_key` Private key for the domain.
   * The optional fields are bundle_method:
     * `bundle_method` Bundle method, default value is `compatible`, valid values are: `compatible`, `modern` and `user-defined`.

   Sample JSON data:
                      {
                        "certificate": "xxx",
                        "private_key": "xxx",
                        "bundle_method": "compatible"
                      }

`-j, --json-file JSON_FILE`  (Optional) A file contains input JSON data.

`-o, --output OUTPUT_FILE`  (Optional) Output the result as JSON style to a file. If not set, outputs the result to terminal.

**Output Message**

   * ID
   * Hosts
   * Issuer
   * Signature
   * Status
   * Bundle method
   * Domain ID
   * Uploaded On
   * Modified On
   * Expires On
   * Priority


## Change the priority of custom certificate

**NAME**

  `certificate-priority-change` - Change custom certificates' priority for a given DNS domain.

**USAGE**

  `ibmcloud cis certificate-priority-change DNS_DOMAIN_ID [-i, --instance INSTANCE_NAME] [-s, --json-str JSON_STR] [-j, --json-file JSON_FILE] [-o, --output OUTPUT_FILE]`

**OPTIONS**

   `-i, --instance INSTANCE_NAME`  (Optional) Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `-s, --json-str`  The JSON data used to change the custom certificates' priority.
   * The required fields in JSON data are `certificates`:
     * `certificates` An array of objects with the follow fields.
     * `id` Custom certificate identifier.
     * `priority` The order/priority in which the certificate is used in a request. Higher numbers are tried first.

   Sample JSON data:
                      {
                        "certificates":[
                          {
                            "id":"5a7805061c76ada191ed06f989cc3dac",
                            "priority":2
                          },
                          {
                            "id":"da534493b38266b17fea74f3312be21c",
                          "priority":1
                          }
                        ]
                      }

   `-j, --json-file JSON_FILE`  (Optional) A file contains input JSON data.

   `-o, --output OUTPUT_FILE`  (Optional) Output the result as JSON style to a file. If not set, outputs the result to terminal.

**Output message**

   * ID
   * Hosts
   * Issuer
   * Signature
   * Status
   * Bundle method
   * Domain ID
   * Uploaded On
   * Modified On
   * Expires On
   * Priority


## Delete certificate

**NAME**

  `certificate-delete` - Delete a dedicated or custom certificate.

**USAGE**

  `ibmcloud cis certificate-delete DNS_DOMAIN_ID CERT_ID [-i, --instance INSTANCE_NAME]`

**OPTIONS**

   `-i, --instance INSTANCE_NAME`  (Optional) Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

**Output Message**

  Result of deleting certificate
