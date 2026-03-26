---

copyright:
  years: 2026
lastupdated: "2026-03-26"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Renewal and expiration of certificates
{: #renewal-and-expiration}

Understand how custom certificates are renewed, how expiration is handled, and what happens to your domains when certificates expire in CIS.
{: shortdesc}

## Renewing custom certificates
{: #renew-custom-certificates}

Replace or update custom certificates before they expire, as CIS cannot renew certificates that you upload. If certificates are not replaced in time, users might not be able to connect to your application.

CIS provides certificate‑related alert policy types for TLS certificates such as certificate validation, renewal, and expiration. To receive these alerts, customers must explicitly configure the corresponding CIS alert policies, as certificate alerts are not enabled by default. For more information, see [Alert types](/docs/cis?topic=cis-types-alerts&interface=api).

## Expired certificates
{: #expired-certificates}

If a valid replacement certificate that covers some or all of the SANs in the expiring custom certificate is already available, CIS removes the expiring certificate within 24 hours before expiration. No downtime is expected during this transition.

If no valid replacement certificate is available, CIS removes the custom certificate after it expires.

Affected domains and subdomains fall back to any other active certificate that covers the hostnames that are associated with the expiring certificate (for example, Universal or Advanced certificates).

Certificates in a certificate pack are treated as a single unit. The pack expires when the first certificate reaches its **Not After** date. For example, if a pack includes both ECDSA and RSA certificates, the entire pack is removed when either certificate expires.
{: note}
