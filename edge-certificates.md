---

copyright:
  years: 2024
lastupdated: "2024-09-06"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Managing edge certificates
{: #managing-edge-certs}

{{site.data.keyword.cis_full}} offers three types of edge certificates: Universal, Advanced, and Custom.
{: shortdesc}

## Universal certificates
{: #universal-certificate-type}

By default, {{site.data.keyword.cis_short_notm}} issues free, unshared, publicly trusted SSL certificates to all domains added on {{site.data.keyword.cis_short_notm}}. For these Universal certificates, {{site.data.keyword.cis_short_notm}} controls the validity periods and certificate authorities (CAs), making sure that renewals always occur. Universal certificates issued by Let’s Encrypt or Google Trust Services have a 90 day validity period.

## Advanced certificates
{: #advanced-certificate-type}

Advanced certificates offer a flexible and customizable way to issue and manage certificates. Use advanced certificates when you want something more customizable than Universal SSL but still want the convenience of SSL certificate issuance and renewal.

Advanced certificates are ordered directly through {{site.data.keyword.cis_short_notm}}.

## Certificate validity and renewal periods for Universal and Advanced certificates
{: #cert-validity-renewal-periods}

Universal certificates are always valid for 90 days and are renewed automatically 30 days before expiration.

By using Advanced certificates, you can select the validity and auto-renewal dates as shown in the following table.

|Certificate validity period|Auto renewal period|Details|
|------|-------|-----|
|3 months|30 days| |
|1 month|7 days|Not supported by Let's Encrypt|
|2 weeks|3 days|Not supported by Let's Encrypt|
{: caption="Table 1. {{site.data.keyword.cis_short_notm}} certificate validity periods" caption-side="bottom"}

Renewal periods are automated on the back end, and are not customizable.
{: note}

## Certificate Authorities
{: #certificate-authorities}

For publicly trusted certificates, Cloudflare partners with different certificate authorities (CAs). The following CAs are available for selection in {{site.data.keyword.cis_short_notm}}:

- Let's Encrypt
   - Supports validity periods of 90 days
   - DCV tokens are valid for 7 days
   - [Compatibility documentation](https://letsencrypt.org/docs/certificate-compatibility/)
- Google Trust Services
   - Supports validity periods of 14, 30, and 90 days
   - DCV tokens are valid for 14 days
   - [Compatibility documentation](https://pki.goog/faq/)
- DigiCert [deprecated]{: tag-deprecated}
   - Supports validity periods of 14, 30, and 90 days
   - DCV tokens are valid for 30 days
   - [Compatibility documentation](https://www.digicert.com/faq/public-trust-and-certificates/are-digicert-tls-ssl-certificates-compatible-with-my-browser)
- Sectigo
   - Used only for backup certificates when {{site.data.keyword.cis_short_notm}} is providing authoritative DNS for your domain
   - Supports validity periods of 90 days
   - [Compatibility documentation](https://www.sectigo.com/knowledge-base/detail/SSL-Browser-Compatibility-1527076085062/kA01N000000zFJt)

## Custom certificates
{: #custom-certificate-type}

Custom certificates are for customers who want to use their own SSL certificates. You upload these certificates to {{site.data.keyword.cis_short_notm}}.

Unlike Universal or advanced certificates, {{site.data.keyword.cis_short_notm}} does not manage the issuance or renewal for custom certificates. You are responsible for uploading, updating, and tracking the expiration dates of your custom certificates.

## Failure to renew and certificate replacement
{: #failure-to-renew-replace}

For certificates managed by {{site.data.keyword.cis_short_notm}}, renewal attempts begin at the auto renewal period and continue until 24 hours before the expiration. If a certificate fails to renew and another valid certificate exists for the hostname, {{site.data.keyword.cis_short_notm}} deploys the valid certificate within these last 24 hours.

## CAA records
{: #caa-records}

A [Certificate Authority Authorization (CAA) DNS record](https://cloud.ibm.com/docs/cis?topic=cis-set-up-your-dns-for-cis#caa-type-record) specifies which certificate authorities (CAs) are allowed to issue certificates for a domain. This record reduces the chance of unauthorized certificate issuance and promotes standardization across your organization.

The following table lists the CAA record content for each CA:

|Certificate authority|CAA record content|
|---|---|
|Let’s Encrypt|`letsencrypt.org`|
|Google Trust Services|`pki.goog; cansignhttpexchanges=yes`|
|DigiCert|`digicert.com; cansignhttpexchanges=yes`|
|Sectigo|`sectigo.com`|
{: caption="Table 2. CAA record content for each CA" caption-side="bottom"}

## Limitations
{: #edge-certificate-limitations}

* **Certificate pinning:** Certificate pinning is not supported natively in {{site.data.keyword.cis_short_notm}}. If you want to use certificate pinning, you must use custom certificates.
* **Full setup:** Universal SSL certificates only support SSL for the root or first-level subdomains such as `example.com` and `www.example.com`. To enable SSL support on second, third, and fourth-level subdomains such as `dev.www.example.com` or `app3.dev.www.example.com` use either an advanced certificate or a custom certificate.
* **CNAME (partial) setup:** On a CNAME setup zone, each subdomain has its own Universal SSL certificate and does not require additional features or purchases.
* **Range:** Universal SSL is not compatible with {{site.data.keyword.cis_short_notm}} Range application. If you are trying to use Range, use either an advanced certificate or a custom certificate.
