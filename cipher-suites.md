---

copyright:
  years: 2024, 2025
lastupdated: "2025-02-24"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Setting up cipher suites
{: #set-up-cipher-suites}

Cipher suites are a combination of algorithms and protocols that help to secure network connections during the TLS handshake. {{site.data.keyword.cis_full}} secures network connections by using edge and origin cipher suites.
{: shortdesc}

## Edge cipher suites
{: #edge-cipher-suites}

The following ciphers are supported at the cloud edge. You can restrict the ciphers that are used for your domain through the CIS CLI plugin to the IBM Cloud CLI. See the `ciphers` option on the [domain settings command](/docs/cis?topic=cis-cis-cli#domain-settings).

|OpenSSL Name| TLS 1.0 | TLS 1.1 | TLS 1.2 | TLS 1.3|
|:--------|:---:|:---:|:---:|:---|
|ECDHE-ECDSA-AES128-GCM-SHA256 | | |![Available](../icons/checkmark-icon.svg)| |
|ECDHE-ECDSA-CHACHA20-POLY1305 | | |![Available](../icons/checkmark-icon.svg)| |
|ECDHE-RSA-AES128-GCM-SHA256   | | |![Available](../icons/checkmark-icon.svg)| |
|ECDHE-RSA-CHACHA20-POLY1305   | | |![Available](../icons/checkmark-icon.svg)| |
|ECDHE-ECDSA-AES128-SHA256     | | |![Available](../icons/checkmark-icon.svg)| |
|ECDHE-ECDSA-AES128-SHA        |![Available](../icons/checkmark-icon.svg)|![Available](../icons/checkmark-icon.svg)|![Available](../icons/checkmark-icon.svg)| |
|ECDHE-RSA-AES128-SHA256       | | |![Available](../icons/checkmark-icon.svg) | |
|ECDHE-RSA-AES128-SHA          |![Available](../icons/checkmark-icon.svg)|![Available](../icons/checkmark-icon.svg)|![Available](../icons/checkmark-icon.svg)| |
|AES128-GCM-SHA256             | | |![Available](../icons/checkmark-icon.svg)| |
|AES128-SHA256                 | | |![Available](../icons/checkmark-icon.svg)| |
|AES128-SHA                    |![Available](../icons/checkmark-icon.svg)|![Available](../icons/checkmark-icon.svg)|![Available](../icons/checkmark-icon.svg) | |
|ECDHE-ECDSA-AES256-GCM-SHA384 | | |![Available](../icons/checkmark-icon.svg)| |
|ECDHE-ECDSA-AES256-SHA384     | | |![Available](../icons/checkmark-icon.svg)| |
|ECDHE-RSA-AES256-GCM-SHA384   | | |![Available](../icons/checkmark-icon.svg)| |
|ECDHE-RSA-AES256-SHA384       | | |![Available](../icons/checkmark-icon.svg)| |
|ECDHE-RSA-AES256-SHA          |![Available](../icons/checkmark-icon.svg)|![Available](../icons/checkmark-icon.svg)|![Available](../icons/checkmark-icon.svg)| |
|AES256-GCM-SHA384             | | |![Available](../icons/checkmark-icon.svg)| |
|AES256-SHA256                 | | |![Available](../icons/checkmark-icon.svg)| |
|AES256-SHA                    |![Available](../icons/checkmark-icon.svg)|![Available](../icons/checkmark-icon.svg)|![Available](../icons/checkmark-icon.svg)| |
|DES-CBC3-SHA                  |![Available](../icons/checkmark-icon.svg)| | | |
|AEAD-AES128-GCM-SHA256        | | | |![Available](../icons/checkmark-icon.svg)|
|AEAD-AES256-GCM-SHA384        | | | |![Available](../icons/checkmark-icon.svg)|
|AEAD-CHACHA20-POLY1305-SHA256 | | | |![Available](../icons/checkmark-icon.svg)|
{: caption="Edge cipher suites" caption-side="bottom"}

## Origin cipher suites
{: #origin-cipher-suites}

The following ciphers are supported at the origin. You can restrict the ciphers that are used for your domain through the CIS CLI plugin to the IBM Cloud CLI. See the `ciphers` option on the [domain settings command](/docs/cis?topic=cis-cis-cli#domain-settings).

|OpenSSL Name| TLS 1.0 | TLS 1.1 | TLS 1.2 | TLS 1.3|
|:--------|:---:|:---:|:---:|:---|
| AEAD-AES128-GCM-SHA256 [^A]| | | | ![Available](../icons/checkmark-icon.svg) |
| AEAD-AES256-GCM-SHA384 [^B] | | | |![Available](../icons/checkmark-icon.svg) |
| AEAD-CHACHA20-POLY1305-SHA256 [^C] | | | | ![Available](../icons/checkmark-icon.svg) |
| ECDHE-ECDSA-AES128-GCM-SHA256 | | |![Available](../icons/checkmark-icon.svg) | |
| ECDHE-RSA-AES128-GCM-SHA256 | | |![Available](../icons/checkmark-icon.svg) | |
| ECDHE-RSA-AES128-SHA |![Available](../icons/checkmark-icon.svg) |![Available](../icons/checkmark-icon.svg) |![Available](../icons/checkmark-icon.svg) | |
| AES128-GCM-SHA256 | | |![Available](../icons/checkmark-icon.svg) | |
| AES128-SHA |![Available](../icons/checkmark-icon.svg) |![Available](../icons/checkmark-icon.svg) |![Available](../icons/checkmark-icon.svg) | |
| ECDHE-ECDSA-AES256-GCM-SHA384 | | |![Available](../icons/checkmark-icon.svg) | |
| ECDHE-RSA-AES256-SHA384 | | |![Available](../icons/checkmark-icon.svg) | |
| AES256-SHA |![Available](../icons/checkmark-icon.svg) |![Available](../icons/checkmark-icon.svg) |![Available](../icons/checkmark-icon.svg) | |
| DES-CBC3-SHA |![Available](../icons/checkmark-icon.svg) | | | |
{: caption="Origin cipher suites" caption-side="bottom"}

[^A]: Although TLS 1.3 uses the same cipher suite space as previous versions of TLS, TLS 1.3 cipher suites are defined differently, specifying only the symmetric ciphers, and can't be used for TLS 1.2. Similarly, TLS 1.2 and lower cipher suites can't be used with TLS 1.3 (IETF TLS 1.3 draft 21). BoringSSL also hardcodes cipher preferences in this order for TLS 1.3.

[^B]: Although TLS 1.3 uses the same cipher suite space as previous versions of TLS, TLS 1.3 cipher suites are defined differently, specifying only the symmetric ciphers, and can't be used for TLS 1.2. Similarly, TLS 1.2 and lower cipher suites can't be used with TLS 1.3 (IETF TLS 1.3 draft 21). BoringSSL also hardcodes cipher preferences in this order for TLS 1.3.

[^C]: Although TLS 1.3 uses the same cipher suite space as previous versions of TLS, TLS 1.3 cipher suites are defined differently, specifying only the symmetric ciphers, and can't be used for TLS 1.2. Similarly, TLS 1.2 and lower cipher suites can't be used with TLS 1.3 (IETF TLS 1.3 draft 21). BoringSSL also hardcodes cipher preferences in this order for TLS 1.3.

## Managing cipher suites from the CLI
{: #cli-manage-cipher-suites}
{: cli}

You can manage cipher suites by from the CLI.

### Working with edge cipher suites from the CLI
{: #cli-edge-cipher}

* Within the `ibmcloud cis domain-settings` CLI, set the following variable:

    `ciphers`: An allowlist of ciphers for TLS termination in the `BoringSSL` format. This command lists only ciphers that are allowlisted by customers. If no ciphers are allowlisted, the list is empty and the default ciphers are used. See [Edge cipher suites](#edge-cipher-suites) for the list of default ciphers.

* Within the `ibmcloud cis domain-settings-update` CLI, set the following variable:

    `ciphers`: An allowlist of ciphers for TLS termination. These ciphers must be in the `BoringSSL` format.

## Managing cipher suites with the API
{: #api-manage-cipher-suites}
{: api}

You can manage cipher suites with the API.

### Getting ciphers with the API
{: #api-get-cipher}

To get ciphers with the API, take the following steps.

1. Set up your environment with the right variables.
1. Store any variables to be used in the API commands. For example,
    * `crn` (string): The full URL-encoded cloud resource name (CRN) of the resource instance.
    * `zone_identifier` (string): The zone identifier.
1. When all variables are initiated, get the ciphers:

```curl
curl -X GET https://api.cis.cloud.ibm.com/v1/:crn/zones/:zone_id/settings/ciphers -H 'content-type: application/json' -H 'accept: application/json' -H 'x-auth-user-token: Bearer xxxxxx'
```
{: pre}

### Updating ciphers with the API
{: #api-update-cipher}

To update ciphers with the API, take the following steps.

1. Set up your environment with the right variables.
1. Store any variables to be used in the API commands. For example,
    * `crn` (string): The full URL-encoded cloud resource name (CRN) of the resource instance.
    * `zone_identifier` (string): The zone identifier.
    * `value`(string): The cipher suites that you want to include.
1. When all variables are initiated, get the ciphers:

```curl
curl -X PATCH https://api.cis.cloud.ibm.com/v1/:crn/zones/:zone_id/settings/ciphers -H 'content-type: application/json' -H 'x-auth-user-token: Bearer xxxxxx' -d '{"value": ["AES256-GCM-SHA384", "AES256-SHA256"]}'

```
{: pre}
