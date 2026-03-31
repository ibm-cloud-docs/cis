---

copyright:
  years: 2018, 2026
lastupdated: "2026-03-31"

keywords: security, best practices, waf, owasp

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Managing {{site.data.keyword.cis_short_notm}} for optimal security
{: #manage-your-ibm-cis-for-optimal-security}

The {{site.data.keyword.cis_full}} ({{site.data.keyword.cis_short_notm}}) security settings include safe defaults that are designed to avoid false positives and negative influence on your traffic. However, these safe default settings do not provide the best security posture for every customer. Follow these steps to make sure that your {{site.data.keyword.cis_short_notm}} account is configured in a safe and secure way.
{: shortdesc}

## Best practice 1: Secure your origin IP addresses
{: #best-practice-secure-origin-ip-address}

When a subdomain uses {{site.data.keyword.cis_short_notm}} for proxying, all traffic is protected because {{site.data.keyword.cis_short_notm}} returns IP addresses that are associated with its proxy network. This ensures that connections are routed through CIS proxies first, which hides the origin IP addresses.

### Use {{site.data.keyword.cis_short_notm}} proxies for all DNS records for HTTP traffic from your origin
{: #use-cis-proxies-for-dns-records}

To improve the security of your origin IP address, you must proxy all HTTP and HTTPS traffic.

See the difference by querying a non-proxied and a proxied record:

```sh
dig nonproxied.theburritobot.com +short
1.2.3.4 (The origin IP address)

$ dig proxied.theburritobot.com +short
104.16.22.6 , 104.16.23.6 (CIS IP addresses)
```
{: pre}

### Obscure non-proxied origin records with non-standard names
{: #obscure-non-proxied-origin-records-with-non-standard-names}

Any records that can't be proxied through {{site.data.keyword.cis_short_notm}}, and that still use your origin IP, such as FTP, can be secured by creating additional obfuscation.

If you require a record for your origin that can't be proxied by {{site.data.keyword.cis_short_notm}}, use a non-standard name. For example, instead of `ftp.example.com` use `[random word or-random characters].example.com.` This obfuscation makes dictionary scans of your DNS records less likely to expose your origin IP addresses.

### Use separate IP ranges for HTTP and non-HTTP traffic if possible
{: #use-separate-ipranges-for-traffic}

Some customers use separate IP ranges for HTTP and non-HTTP traffic. This approach helps them proxy all records for their HTTP IP range, and hide all non-HTTP traffic with a different IP subnet.

## Best practice 2: Activate your Web Application Firewall safely
{: #best-practice-activate-waf-safely}

Your WAF is available in the **Security** section. These steps walk through the settings in reverse order to ensure that your WAF is configured as safely as possible before you enable it for your entire domain.

These initial settings can reduce false positives by populating **Security Events** for further tuning. Your WAF is updated automatically to handle new vulnerabilities as they are identified. For more information, see [Using Security events capability](/docs/cis?topic=cis-using-the-cis-security-events-capability).

The following are some examples of the types of attacks that WAF can protect against:

* SQL injection attack
* Cross-site scripting
* Cross-site forgery

CIS provides several preconfigured rulesets within WAF for Layer 7 protection. Each ruleset includes protections to mitigate the most common web application attacks. You can enable or disable these rulesets and override individual rules to meet your security requirements. For optimal protection, enable the CIS Managed Ruleset at the highest priority. You can use the OWASP ruleset for additional coverage, but place it after the CIS Managed Ruleset in your rule execution order. 

The OWASP ruleset is prone to false positives and offers only marginal benefits when placed before the CIS Managed Ruleset and WAF attack score. If you enable the OWASP ruleset, monitor traffic and adjust rule settings as needed to prevent false positives. For more information, see [WAF actions](/docs/cis?topic=cis-waf-actions) for details about the ruleset and the behavior of each rule.
{: note}

For more information, see [Web Application Firewall (WAF) concepts](/docs/cis?topic=cis-waf-q-and-a).

## Best practice 3: Configure WAF Attack Score safely
{: #waf-attack-score-rule}

WAF Attack Score strengthens your security posture by detecting variations of known attacks by using machine learning. It complements WAF managed rules by identifying malicious requests that do not match existing rule signatures.

To configure WAF Attack Score safely, begin with monitoring traffic before you enforce blocking actions. This approach allows you to review scored traffic in Security Events and adjust thresholds to minimize false positives.

For more information, see [using WAF Attack Score](/docs/cis?topic=cis-waf-attack-score#using-waf-score) to cofigure WAF Attack Score in a custom rule.

CIS recommends using WAF managed rules along with WAF Attack Score. Managed rules protect against known attack patterns, while WAF Attack Score detects modified or obfuscated attacks, providing layered and adaptive protection for your domain. For more information, see [About WAF Attack Score](/docs/cis?topic=cis-waf-attack-score).

## Best practice 4: Configure your TLS settings
{: #best-practice-configure-tls-settings}

Protect your site and control your Transport Layer Security (TLS) settings. Manage the certificates used to secure traffic to your site. IBM {{site.data.keyword.cis_short_notm}} functions as a reverse proxy and provides multiple options for encrypting your traffic. As a reverse proxy, TLS connections terminate at CIS data centers, and a new TLS connection is opened to your origin server.

TLS offers six modes of operations that are listed from most secure to least secure:

1. [Authenticated origin pull](/docs/cis?topic=cis-cis-tls-options#tls-encryption-modes-authenticated-origin): (Enterprise only)
1. [HTTPS only origin pull](/docs/cis?topic=cis-cis-tls-options#tls-encryption-modes-origin-only-pull) (Enterprise only)
1. [End-to-end CA signed](/docs/cis?topic=cis-cis-tls-options#tls-encryption-modes-end-to-end-ca-signed) (default and recommended)
1. [End-to-end flexible](/docs/cis?topic=cis-cis-tls-options#tls-encryption-modes-end-to-end-flexible) (edge-to-origin certificates can be self-signed)
1. [Client-to-edge](/docs/cis?topic=cis-cis-tls-options#tls-encryption-modes-client-to-edge) (edge-to-origin not encrypted, self-signed certificates are not supported)
1. [Off](/docs/cis?topic=cis-cis-tls-options#tls-encryption-modes-off) (not recommended)

See [TLS options](/docs/cis?topic=cis-cis-tls-options) for details on the different modes.

With IBM {{site.data.keyword.cis_short_notm}}, you can use custom certificates or a wildcard certificate that is provisioned for you by {{site.data.keyword.cis_short_notm}}.

### Upload custom certificates
{: #upload-custom-certs}

You can upload your custom certificate by clicking **Add Certificate** and entering your certificate, private key, and bundle method. After you upload a custom certificate, you gain immediate compatibility with encrypted traffic and maintain control over your certificate (for example, an Extended Validation (EV) certificate).

{{site.data.keyword.cis_short_notm}} does not support certificate pinning with ordered or Universal certificates. If you want to use certificate pinning, it is recommended that you upload and maintain your own custom certificate.

You are responsible for managing your certificate if you upload a custom certificate. For example, {{site.data.keyword.cis_short_notm}} doesn't track the certificate expiration date.
{: important}

### Order dedicated certificates
{: #order-dedicated-certs}

{{site.data.keyword.cis_short_notm}} simplifies certificate management by offering dedicated certificates. You no longer need to generate private keys, create certificate signing requests (CSR), or remember to renew certificates. You can order a dedicated certificate by clicking **Add Certificate** and ordering a wildcard certificate or entering hostnames to order a dedicated custom certificate. Available certificate types include:

* SHA-2/ECDSA signed certificate that uses a P-256 key,
* SHA-2/RSA signed certificate that uses an RSA 2048-bit key, and
* SHA-1/RSA signed certificate that uses an RSA 2048-bit key.

{{site.data.keyword.cis_short_notm}} can issue certificates for all top-level domains (TLDs) except the following:

 * `.cu` (Cuba)
 * `.iq` (Iraq)
 * `.ir` (Iran)
 * `.kp` (North Korea)
 * `.sd` (Sudan)
 * `.ss` (South Sudan)
 * `.ye` (Yemen)

{{site.data.keyword.cis_short_notm}} manages the certificate expiration date for dedicated certificates.

To edit the hostnames on a dedicated custom certificate, you must reorder the certificate and then delete the original one. For example, suppose that you order a dedicated custom certificate with the hostname `alpha.yourdomain.com`. To add the hostname `beta.yourdomain.com` to your dedicated custom certificate, order another dedicated custom certificate with the hostnames `alpha.yourdomain.com` and `beta.yourdomain.com`. Afterward, you must delete the original dedicated custom certificate.

The first time that you order a dedicated certificate, the Domain Control Validation (DCV) process runs and generates a corresponding TXT record. If you delete the TXT record, the DCV process runs again when you order another dedicated certificate. If you delete a dedicated certificate, the TXT record corresponding to the DCV process is not deleted.
{: note}

The following are common errors that might occur when you order dedicated certificates:

   * `Error connecting to certificate service.`
   * `Error while requesting from certificate service.`

If you receive an error when you order certificates, refresh the page and try again.

### Use a provisioned certificate
{: #use-provisioned-certificate}

IBM has partnered with several certificate authorities (CAs) to provide wildcard certificates for customer domains. Manual verification might be required during he setup process. Your support team can help you complete these additional steps.

### Certificate priority at our edge
{: #certificate-priority-at-our-edge}

Certificates are served at the edge in the following priority order:

1. Uploaded custom
1. Dedicated custom
1. Dedicated wildcard
1. Universal

### Minimum TLS version
{: #security-minimum-tls-version}

Higher TLS versions provide stronger security but might prevent some customers from connecting to your site. For more information, see [Minimum TLS version](/docs/cis?topic=cis-cis-tls-options#minimum-tls-version).

## Best practice 5: Configure rate limiting
{: #best-practice-rate-limiting}

Use rate-limiting rules to protect your site or API from malicious traffic by blocking client IP addresses that match a URL pattern or exceed a defined threshold.

Common use cases for rate limiting include:

* Enforcing granular access control to resources. This process includes access control based on criteria, such as user agent, IP address, referrer, host, country, and world region.
    * Limit by user agent: A common use case is to limit the rate of requests performed by individual user agents.
    * Allow specific IP addresses or ASNs: Another use case when you control access to resources is to exclude or include IP addresses or Autonomous System Numbers (ASNs) from a rate-limiting rule.
    * Limit by referrer: Some applications receive requests that are originated by other sources (for example, used by advertisements that link to third-party pages). You can limit the number of requests that are generated by individual referrer pages to manage quotas or avoid indirect DDoS attacks.
    * Limit by destination host: Create a rate-limiting rule that uses the host as a counting characteristic.
* Protecting against credential stuffing and account takeover attacks.
* Limiting the number of operations performed by individual clients. This action includes preventing scraping by bots, accessing sensitive data, bulk creation of new accounts, and programmatic buying in e-commerce platforms.
    * Prevent content scraping (through query string)
    * Prevent content scraping (through body)
    * Limit requests from bots
* Protecting REST APIs from resource exhaustion (targeted DDoS attacks) and resources from abuse in general.
    * Prevent volumetric attacks
    * Protect resources
* Protecting GraphQL APIs by preventing server overload and limiting the number of operations.
    * Limit the number of operations
    * Prevent server overload
