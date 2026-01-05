---

copyright:
  years: 2024, 2026
lastupdated: "2026-01-05"

keywords: edge certificates

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Managing edge certificates
{: #managing-edge-certs}

Edge certificates are TLS certificates that are presented to users when they access your domain over HTTPS. These certificates secure the connection between the browser and the {{site.data.keyword.cis_full}} edge network. {{site.data.keyword.cis_short_notm}} offers three types of edge certificates: Universal, Advanced, and Custom.
{: shortdesc}

![Diagram of an edge certificate](images/edge-cert.svg "Diagram of an edge certificate"){: caption="A diagram of an edge certificate" caption-side="bottom"}

## Universal certificates
{: #universal-certificate-type}

By default, {{site.data.keyword.cis_short_notm}} issues free, unshared, publicly trusted SSL certificates to all domains added on {{site.data.keyword.cis_short_notm}}. For these Universal certificates, {{site.data.keyword.cis_short_notm}} controls the validity periods and certificate authorities (CAs), making sure that renewals always occur. Universal certificates that are issued by Let's Encrypt or Google Trust Services have a 90-day validity period.

CIS can change the CA of Universal certificates without prior notice, and notifies you of these changes. If you prefer to select your own issuing certificate authority, order an advanced certificate.
{: attention}

To change the universal certificate settings from the API, see [Enable or Disable Universal Certificate](/apidocs/cis#change-universal-certificate-setting). Keep in mind that this certificate is enabled by default, and it must remain enabled unless another valid certificate is already configured.

## Advanced certificates
{: #advanced-certificate-type}

Advanced certificates offer a flexible and customizable way to issue and manage certificates. Use advanced certificates when you want something more customizable than Universal SSL but still want the convenience of SSL certificate issuance and renewal.

The difference between the two is that universal certificates are automatically issued by {{site.data.keyword.cis_short_notm}} with fixed 90-day validity and auto-selected certificate authorities. However, with advanced certificates you can choose the certificate authority, select different validity periods such as 14, 30, 90, or even 365 days, and configure when renewals begin. Advanced certificates also support more control over domain validation and are better suited for environments that require compliance, tighter security policies, or integration into automated workflows.

Advanced certificates are ordered directly through {{site.data.keyword.cis_short_notm}}.

## Certificate validity and renewal periods for universal and advanced certificates
{: #cert-validity-renewal-periods}

Universal certificates are always valid for 90 days and are renewed automatically 30 days before expiration.

By using advanced certificates, you can select the validity and auto-renewal dates as shown in the following table.

|Certificate validity period|Auto renewal period|Details|
|------|-------|-----|
|3 months|30 days| |
|1 month|7 days|Not supported by Let's Encrypt|
|2 weeks|3 days|Not supported by Let's Encrypt|
{: caption="{{site.data.keyword.cis_short_notm}} certificate validity periods" caption-side="bottom"}

Renewal periods are automated on the back end, and are not customizable.
{: note}

## Backup certificates
{: #backup-certificates}

If CIS is providing authoritative DNS for your domain, CIS issues a backup Universal SSL certificate for every standard universal certificate issued.

Backup certificates are wrapped with a different private key and issued from a different certificate authority. For example, these certificates are issued from Google Trust Services, Let's Encrypt, Sectigo, or SSL.com instead of your domain’s primary Universal SSL certificate.

These backup certificates are not normally deployed, but they are deployed automatically by CIS when a certificate is revoked or when a key is compromised.

## Certificate authorities
{: #certificate-authorities}

For publicly trusted certificates, Cloudflare partners with different certificate authorities (CAs). The following CAs are available for selection in {{site.data.keyword.cis_short_notm}}:

- Let's Encrypt
   - Supports validity periods of 90 days.
   - DCV tokens are valid for 7 days.
   - [Compatibility documentation](https://letsencrypt.org/docs/certificate-compatibility/){: external}
- Google Trust Services
   - Supports validity periods of 14, 30, and 90 days.
   - DCV tokens are valid for 14 days.
   - [Compatibility documentation](https://pki.goog/faq/){: external}
- SSL.com
   - Supports validity periods of 14, 30, and 90 days.
      - 1-year validity period is available to Enterprise customers.
   - DCV tokens are valid for 14 days.
   - [Compatibility documentation](https://www.ssl.com/browser_compatibility/){: external}
- DigiCert [deprecated]{: tag-deprecated}
   - Supports validity periods of 14, 30, and 90 days.
   - DCV tokens are valid for 30 days.
   - [Compatibility documentation](https://www.digicert.com/faq/public-trust-and-certificates/are-digicert-tls-ssl-certificates-compatible-with-my-browser){: external}
- Sectigo
   - Used only for backup certificates when {{site.data.keyword.cis_short_notm}} is providing authoritative DNS for your domain.
   - Supports validity periods of 90 days.
   - [Compatibility documentation](https://www.sectigo.com/knowledge-base/detail/SSL-Browser-Compatibility-1527076085062/kA01N000000zFJt){: external}

## Custom certificates
{: #custom-certificate-type}

Custom certificates are for customers who want to use their own SSL certificates. You upload these certificates to {{site.data.keyword.cis_short_notm}}.

Unlike universal or advanced certificates, {{site.data.keyword.cis_short_notm}} doesn't manage the issuance or renewal of custom certificates. You are responsible for uploading, updating, and tracking the expiration dates of your custom certificates.

The number of certificates you can use depends on your plan. See [Comparing CIS plans](/docs/cis?topic=cis-cis-plan-comparison) for more information. If you need more, submit a support case. See [Creating support cases](/docs/account?topic=account-open-case&interface=ui)
{: note}

### Certificate priority
{: #certificate-priority}

If the hostname is the same, certain types of certificates take precedence over others as following:

|Priority|Certificate type|
|----------|------------|
|1|[Custom certificates](/docs/cis?topic=cis-managing-edge-certs#custom-certificate-type)|
|2|[Advanced certificates](/docs/cis?topic=cis-managing-edge-certs#advanced-certificate-type)|
|3|[Universal certificates](/docs/cis?topic=cis-managing-edge-certs#universal-certificate-type)|
{: caption="Priority order of certificate" caption-side="bottom"}

## Certificate renewal failure and replacement
{: #failure-to-renew-replace}

For certificates managed by {{site.data.keyword.cis_short_notm}}, renewal attempts begin at the auto renewal period and continue until 24 hours before the expiration. If a certificate fails to renew and another valid certificate exists for the hostname, {{site.data.keyword.cis_short_notm}} deploys the valid certificate within these last 24 hours.

## CAA records
{: #caa-records}

A [Certificate Authority Authorization (CAA) DNS record](/docs/cis?topic=cis-set-up-your-dns-for-cis#caa-type-record) specifies which certificate authorities (CAs) are allowed to issue certificates for a domain. This record reduces the chance of unauthorized certificate issuance and promotes standardization across your organization.

The following table lists the CAA record content for each CA:

|Certificate authority|CAA record content|
|---|---|
|Let's Encrypt|`letsencrypt.org`|
|Google Trust Services|`pki.goog; cansignhttpexchanges=yes`|
|SSL.com|`ssl.com`|
|DigiCert|`digicert.com; cansignhttpexchanges=yes`|
|Sectigo|`sectigo.com`|
{: caption="CAA record content for each CA" caption-side="bottom"}

## Certificate statuses
{: #certificate-statuses}

Each certificate status describes your current position in the issuance process, and can vary depending on the type of certificate.

### New certificate statuses
{: #new-cert-status}

When you order a new certificate, whether it's an edge certificate or one for a custom hostname, its status moves through the following stages as it progresses to the global network.

1. **Initializing**
1. **Pending Validation**
1. **Pending Issuance**
1. **Pending Deployment**
1. **Active**

After you issue a certificate, it moves to **Pending Validation**, and changes to **Active** after the validation is completed. If you see any errors, you might need to take more actions to validate the certificate.

If you deactivate a certificate, it moves to **Deactivating** and then the **Inactive** status.

### Custom certificate statuses
{: #custom-cert-status}

When you use a custom certificate and your zone status is **Pending** or **Moved**, your certificate might have a status of **Holding Deployment**.

When your zone becomes active, your custom certificate deploys automatically and changes to an **Active** status. However, if your zone is already active when you upload a custom certificate, you don't see this status.

## Related links
{: #related-links-certificates}

* [Known limitations for certificates](/docs/cis?topic=cis-known-limitations#known-limitations-certificates)
* [Introducing: Backup Certificates](https://blog.cloudflare.com/introducing-backup-certificates/){: external}
