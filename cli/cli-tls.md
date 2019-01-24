---

copyright:
  years: 2018
lastupdated: "2018-12-14"

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
* List origin certificates
* Create origin certificate
* Show a origin certificate
* Delete origin certificate

## Show TLS setting
**NAME**

  `tls-settings` - Get TLS settings for a given domain.

**USAGE**

 `ibmcloud cis tls-settings DNS_DOMAIN_ID [-i, --instance INSTANCE_NAME] [--output FORMAT]`

**OPTIONS**

  `-i, --instance INSTANCE_NAME`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

  `--output FORMAT`              Specify output format, only JSON is supported now.




## Update TLS Settings

**NAME**

  `tls-settings-update` - Update tls settings for a given DNS domain.

**USAGE**

  `ibmcloud cis tls-settings-update DNS_DOMAIN_ID [--mode MODE] [--universal (true|false)] [--tls-1-2-only (on|off)] [--tls-1-3 (on|off|zrt)] [-i, --instance INSTANCE_NAME][--output FORMAT]`

**OPTIONS**

   `--mode value` Specify whether visitors can browse your website over a secure connection, and when they do, how CIS will connect to your origin server.
                Valid values: `off`, `client-to-edge`, `end-to-end-flexible`, `end-to-end-ca-signed`, `https-only-origin-pull`.
                See below documentation link for detailed TLS mode description.
                    https://console.bluemix.net/docs/infrastructure/cis/ssl-options.html#tls-options

   `--universal value` Specify whether universal ssl is enabled for you domain. Valid values are `true` and
                                       `false`.

   `--tls-1-2-only value`  Specify whether Crypto TLS 1.2 feature is enable for your domain. Enabling this
                                       feature prevents use of previous versions. Valid values are `on` and `off`.

   `--tls-1-3 value`  Specify whether Crypto TLS 1.3 feature is enabled for your domain. Valid values are `on` and
                               `off`.

   `--min-tls-version value`     Only accept HTTPS requests that use at least the TLS protocol version specified.  Valid values: `1.0`, `1.1`, `1.2`, `1.3`.

   `-i, --instance INSTANCE_NAME`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `--output FORMAT`              Specify output format, only JSON is supported now.


## List Certificates

**NAME**

  `certificates` - List all certificates for a given DNS domain, including shared, dedicated and custom certificates.

**USAGE**

   `ibmcloud cis certificates DNS_DOMAIN_ID [-i, --instance INSTANCE_NAME] [--output FORMAT]`

**OPTIONS**

   `-i, --instance INSTANCE_NAME`  (Optional) Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `--output FORMAT`  (Optional) Specify output format, only JSON is supported now.

## Show a certificate

**NAME**

  `certificate` - Get details of a given shared, dedicated, custom certificate.

**USAGE**

 `ibmcloud cis certificate DNS_DOMAIN_ID (--cert-id CERT_ID | --universal) [-i, --instance INSTANCE_NAME] [--output FORMAT]`

**OPTIONS**

   `-i, --instance INSTANCE_NAME ` (Optional) Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `--cert-id value:` ID of dedicated or custom certificate.

   `--universal:` Show universal certificate details.

   `--output FORMAT`  (Optional) Specify output format, only JSON is supported now.


## Order dedicated certificate

**NAME**

  `certificate-order` - Order a certificate pack with an optional list of hostnames for a given DNS domain.

**USAGE**

  `ibmcloud cis certificate-order DNS_DOMAIN_ID [--hostnames host1 --hostnames host2 ...] [-i, --instance INSTANCE_NAME] [--output FORMAT]`

**OPTIONS**

   `--hostnames HOSTNAME`  (Optional) valid host names for the certificate packs. Add up to 50 custom hostnames - May
affect price.

   `-i, --instance INSTANCE_NAME`  (Optional) Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `--output FORMAT` (Optional) Specify output format, only JSON is supported now.

## Upload certificate

**NAME**

 `certificate-upload` - Upload a custom certificate for a DNS domain

**USAGE**

  `ibmcloud cis certificate-upload DNS_DOMAIN_ID [-i, --instance INSTANCE_NAME] [-s, --json-str JSON_STR] [-j, --json-file JSON_FILE] [--output FORMAT]`

**OPTIONS**

   `-i, --instance INSTANCE_NAME`  (Optional) Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `-s, --json-str JSON_STR`  The JSON data used to upload a custom certificate.
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

   `--output FORMAT`  (Optional) Specify output format, only JSON is supported now.


## Update certificate

**NAME**

 `update-certificate` Update a custom certificate for a DNS domain.

**USAGE**

  `ibmcloud cis certificate-update DNS_DOMAIN_ID CERT_ID [-i, --instance INSTANCE_NAME] [-s, --json-str JSON_STR] [-j, --json-file JSON_FILE] [--output FORMAT]`

**OPTIONS**

`-i, --instance INSTANCE_NAME`  (Optional) Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
`-s, --json-str JSON_STR`  The JSON data used to update a custom certificate.
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

`--output FORMAT`  (Optional) Specify output format, only JSON is supported now.


## Change the priority of custom certificate

**NAME**

  `certificate-priority-change` - Change custom certificates' priority for a given DNS domain.

**USAGE**

  `ibmcloud cis certificate-priority-change DNS_DOMAIN_ID [-i, --instance INSTANCE_NAME] [-s, --json-str JSON_STR] [-j, --json-file JSON_FILE] [--output FORMAT]`

**OPTIONS**

   `-i, --instance INSTANCE_NAME`  (Optional) Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `-s, --json-str JSON_STR`  The JSON data used to change the custom certificates' priority.
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

   `--output FORMAT`  (Optional) Specify output format, only JSON is supported now.

## Delete certificate

**NAME**

  `certificate-delete` - Delete a dedicated or custom certificate.

**USAGE**

  `ibmcloud cis certificate-delete DNS_DOMAIN_ID CERT_ID [-i, --instance INSTANCE_NAME]`

**OPTIONS**

   `-i, --instance INSTANCE_NAME`  (Optional) Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.


##  List origin certificates

**NAME**

  `origin-certificates` - List all origin certificates for a given DNS domain.

**USAGE**

  `ibmcloud cis origin-certificates DNS_DOMAIN_ID [--instance INSTANCE_NAME] [--output FORMAT]`

**ARGUMENTS**

  `DNS_DOMAIN_ID`  The id of DNS domain.

**OPTIONS**
   `-i, --instance INSTANCE_NAME`  Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' is used.
   
   `--output FORMAT`    Specify output format, only JSON is supported now.


##  Create origin certificate

**NAME**

  `origin-certificate-create` - Create a CIS-signed certificate.

**USAGE**

  `ibmcloud cis origin-certificate-create DNS_DOMAIN_ID [--request-type REQUEST_TYPE] [--hostnames HOST_NAME1] [--hostnames HOST_NAME2] [--requested-validity DAYS] [--csr CSR] [--json-str JSON_STR | --json-file JSON_FILE] [--instance INSTANCE_NAME] [--output FORMAT]`

**ARGUMENTS**

  `DNS_DOMAIN_ID`  The id of DNS domain.

**OPTIONS**
   `--request-type REQUEST_TYPE`        Signature type desired on certificate. Valid values: "origin-rsa", "origin-ecc".

   `--hostnames HOSTNAME`           hostname or wildcard name bound to the certificate.
   
   `--requested-validity DAYS`  The number of days for which the certificate should be valid. (default: 5475)
   
   `--csr CSR`                 The Certificate Signing Request (CSR). If not set, CIS will generate one.
   
   `-s, --json-str JSON_STR`  The JSON data describing an origin certificate.

                   The required fields in JSON data are "request_type", "hostnames".
                       
                       "request_type": Signature type desired on certificate. Valid values: "origin-rsa", "origin-ecc".
                       "hostnames": Array of hostnames or wildcard names bound to the certificate.

                   The optional fields are "requested_validity", "csr".
                       
                       "requested_validity": The number of days for which the certificate should be valid. Valid values: "0", "7", "30", "90", "365", "730", "1095", "5475".
                       "csr": The Certificate Signing Request (CSR). If not set, CIS will generate one.

                   Sample JSON data:
                   
                   {
                       "request_type": "origin-rsa",
                       "hostnames": [
                           "*.example.com",
                           "example.com",
                     ],
                       "requested_validity": 5475,
                       "csr": "your_csr"
                   }
   `-j, --json-file JSON_FILE`  A file contains input JSON data.


   `-i, --instance INSTANCE_NAME`  Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' is used.
   
   `--output FORMAT`    Specify output format, only JSON is supported now.


##  Show a origin certificate

**NAME**

  `origin-certificate` - Get details of a given origin certificate.

**USAGE**

  `ibmcloud cis origin-certificate DNS_DOMAIN_ID CERT_ID [--instance INSTANCE_NAME] [--output FORMAT]`

**ARGUMENTS**

  `DNS_DOMAIN_ID`  The id of DNS domain.

  `CERT_ID` The id of Origin Certificate.


**OPTIONS**
   `-i, --instance INSTANCE_NAME`  Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' is used.
   
   `--output FORMAT`    Specify output format, only JSON is supported now.

##  Delete origin certificate

**NAME**

  `origin-certificate-delete` - Delete an origin certificate.

**USAGE**

  `ibmcloud cis  origin-certificate-delete DNS_DOMAIN_ID CERT_ID [--instance INSTANCE_NAME]`

**ARGUMENTS**

  `DNS_DOMAIN_ID`  The id of DNS domain.

  `CERT_ID` The id of Origin Certificate.


**OPTIONS**
   `-i, --instance INSTANCE_NAME`  Instance name. If not set, the context instance specified by 'ibmcloud cis instance-set' is used.
