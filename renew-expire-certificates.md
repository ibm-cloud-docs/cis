---

copyright:
  years: 2026
lastupdated: "2026-03-24"

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

Make sure that you replace or update existing custom certificates before they expire, because CIS cannot renew certificates that you upload. If certificates are not replaced in time, users might not be able to connect to your application.

CIS automatically sends email notifications 30 and 14 days before a custom certificate expires. Notifications are sent to customers with the SSL/TLS, Administrator, or Super Administrator roles.

## Expired certificates
{: #expired-certificates}

If a valid replacement certificate is already available, CIS removes the expiring custom certificate within 24 hours before expiration. No downtime is expected during this transition. If no valid replacement is available, CIS removes the custom certificate after it expires.

Affected domains and subdomains fall back to any other active certificate that covers the hostnames (for example, Universal or Advanced certificates) associated with the expiring certificate.

All certificates in a certificate pack are treated as a single object. The pack expires when the first certificate in it expires. For example, if a pack contains both an ECDSA and an RSA certificate, the entire pack is removed when either one expires.
{: note}
