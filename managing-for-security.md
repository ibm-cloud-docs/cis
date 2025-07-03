---

copyright:
  years: 2018, 2025
lastupdated: "2025-07-03"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Managing {{site.data.keyword.cis_short_notm}} for optimal security
{: #manage-your-ibm-cis-for-optimal-security}

The {{site.data.keyword.cis_full}} ({{site.data.keyword.cis_short_notm}}) security settings include safe defaults that are designed to avoid false positives and negative influence on your traffic. However, these safe default settings do not provide the best security posture for every customer. Follow these steps to make sure that your {{site.data.keyword.cis_short_notm}} account is configured in a safe and secure way.
{: shortdesc}

* Secure your origin IP addresses by using proxies and increasing obfuscation.
* Configure your security level selectively.
* Activate your Web Application Firewall (WAF) safely.
* Configure your TLS settings.

## Best practice 1: Secure your origin IP addresses
{: #best-practice-secure-origin-ip-address}

When a subdomain uses {{site.data.keyword.cis_short_notm}} for proxying, all traffic is protected because {{site.data.keyword.cis_short_notm}} responds with specific IP addresses that are associated with it. This process helps ensure that you connect to CIS proxies first, which hides your original IP addresses.

### Use {{site.data.keyword.cis_short_notm}} proxies for all DNS records for HTTP traffic from your origin
{: #use-cis-proxies-for-dns-records}

To improve the security of your origin IP address, you must proxy all HTTP and HTTPS traffic.

**See the difference by querying a non-proxied and a proxied record:**

```sh
dig nonproxied.theburritobot.com +short
1.2.3.4 (The origin IP address)

$ dig proxied.theburritobot.com +short
104.16.22.6 , 104.16.23.6 (CIS IP addresses)
```
{: pre}

### Obscure non-proxied origin records with non-standard names
{: #obscure-non-proxied-origin-records-with-non-standard-names}

Any records that can't be proxied through {{site.data.keyword.cis_short_notm}}, and that still use your origin IP, such as FTP, can be secured by creating additional obfuscation. In particular, if you require a record for your origin that can't be proxied by {{site.data.keyword.cis_short_notm}}, use a non-standard name. For example, instead of `ftp.example.com` use `[random word or-random characters].example.com.` This obfuscation makes dictionary scans of your DNS records less likely to expose your origin IP addresses.

### Use separate IP ranges for HTTP and non-HTTP traffic if possible
{: #use-separate-ipranges-for-traffic}

Some customers use separate IP ranges for HTTP and non-HTTP traffic. This approach helps them proxy all records for their HTTP IP range, and hide all non-HTTP traffic with a different IP subnet.

## Best practice 2: Configure your security level selectively
{: #best-practice-configure-security-level-selectively}

Your **Security Level** establishes the sensitivity of our **IP Reputation Database**. To prevent negative interactions or false positives, configure your **Security Level** by domain to heighten security where necessary, and to decrease it where appropriate.

### Increase the security level for sensitive areas to 'High'
{: #increase-security-level-for-sensitive-areas}

You can increase this level in the Advanced Security page for your domain, or by adding a **Page Rule** for admin or login pages to reduce brute-force attempts:

1. Create a **Page Rule** with the URL pattern of your API (for example, `www.example.com/wp-login`).
2. Identify the **Security Level** setting.
3. Mark the setting as **High**.
4. Select **Provision Resource**.

### Decrease the security level for non-sensitive paths or APIs to reduce false positives
{: #decrease-security-level-non-sensitive-paths-reduce-false-positives}

You can decrease this level for general pages and API traffic:

1. Create a **Page Rule** with the URL pattern of your API (for example, `www.example.com/api/*`).
2. Identify the **Security Level** setting.
3. Turn the Security Level to **Low** or **Essentially off**.
4. Select **Provision Resource**.

### What do the security level settings mean?
{: #what-do-security-level-settings-mean}

Our security level settings are aligned with threat scores that certain IP addresses acquire from malicious behavior on our network. A threat score greater than 10 is considered high.

* **High**: Threat scores greater than 0 are challenged.
* **Medium**: Threat scores greater than 14 are challenged.
* **Low**: Threat scores greater than 24 are challenged.
* **Essentially off**: Threat scores greater than 49 are challenged.
* **Off**: Enterprise only
* **Defense mode**: This level must be used only when your website is under a DDoS attack. Visitors receive an interstitial page for about five seconds while {{site.data.keyword.cis_short_notm}} analyzes the traffic and behavior to make sure that it is a legitimate visitor who is trying to access your website. Defense mode might affect some actions on your domain, such as using an API. You can set a custom security level for your API or any other part of your domain by creating a page rule for that section.

Consider reviewing your security-level settings periodically. You can find instructions in [Best practices for CIS setup](/docs/cis?topic=cis-best-practices-for-cis-setup).

## Best practice 3: Activate your Web Application Firewall (WAF) safely
{: #best-practice-activate-waf-safely}

Your WAF is available in the **Security** section. Here, we walk through these settings in reverse order to ensure that your WAF is configured as safely as possible before you turn it on for your entire domain. These initial settings can reduce false positives by populating **Security Events** for further tuning. Your WAF is updated automatically to handle new vulnerabilities as they are identified. For more information, see [Using Security events capability](/docs/cis?topic=cis-using-the-cis-security-events-capability).

The WAF protects you against the following types of attacks:
* SQL injection attack
* Cross-site scripting
* Cross-site forgery

The WAF contains a default ruleset, which includes rules to stop the most common attacks. Currently, we allow you to either enable or disable the WAF and fine-tune specific rules in the WAF rulesets. See [WAF actions](/docs/cis?topic=cis-waf-actions) document for more details on the ruleset and the behavior of each rule.

For more information, see [Web Application Firewall (WAF) concepts](/docs/cis?topic=cis-waf-q-and-a).

## Best practice 4: Configure your TLS settings
{: #best-practice-configure-tls-settings}

IBM {{site.data.keyword.cis_short_notm}} functions as a reverse proxy and provides multiple options for encrypting your traffic. As a reverse proxy, we close TLS connections at our data centers and open a new TLS connection to your origin server.

TLS offers six modes of operation listed in the order from the most secure to the least secure (Off):
1. [Authenticated origin pull](/docs/cis?topic=cis-cis-tls-options#tls-encryption-modes-authenticated-origin): (Enterprise only)
1. [HTTPS only origin pull](/docs/cis?topic=cis-cis-tls-options#tls-encryption-modes-origin-only-pull) (Enterprise only)
1. [End-to-end CA signed](/docs/cis?topic=cis-cis-tls-options#tls-encryption-modes-end-to-end-ca-signed) (default and recommended)
1. [End-to-end flexible](/docs/cis?topic=cis-cis-tls-options#tls-encryption-modes-end-to-end-flexible) (edge to origin certificates can be self-signed)
1. [Client-to-edge](/docs/cis?topic=cis-cis-tls-options#tls-encryption-modes-client-to-edge) (edge to origin not encrypted, self-signed certificates are not supported)
1. [Off](/docs/cis?topic=cis-cis-tls-options#tls-encryption-modes-off) (not recommended)

See [TLS options](/docs/cis?topic=cis-cis-tls-options) for details on the different modes of operation.

With IBM {{site.data.keyword.cis_short_notm}}, you can use custom certificates, or you can use a wildcard certificate that is provisioned for you by {{site.data.keyword.cis_short_notm}}.

### Upload custom certificates
{: #upload-custom-certs}

You can upload your custom certificate by clicking **Add Certificate** and entering your certificate, private key, and bundle method. After you upload the custom certificate, you gain immediate compatibility with encrypted traffic, and you maintain control over your certificate (for example, an Extended Validation (EV) certificate). {{site.data.keyword.cis_short_notm}} does not support certificate pinning through ordered or Universal certificates. If you want to use certificate pinning, it is recommended that you upload and maintain your own custom certificate.

You are responsible for managing your certificate if you upload a custom certificate. For example, {{site.data.keyword.cis_short_notm}} doesn't track the certificate expiration date.
{: important}

### Order dedicated certificates
{: #order-dedicated-certs}

{{site.data.keyword.cis_short_notm}} makes managing your certificates simple by offering dedicated certificates. You no longer need to generate private keys, create certificate signing requests (CSR), or remember to renew certificates. You can order a dedicated certificate by clicking **Add Certificate** and ordering a wildcard certificate or entering hostnames to order a dedicated custom certificate. The types of certificates are:

* SHA-2/ECDSA signed certificate that uses P-256 key,
* SHA-2/RSA signed certificate that uses RSA 2048-bit key, and
* SHA-1/RSA signed certificate that uses RSA 2048-bit key.

{{site.data.keyword.cis_short_notm}} can issue certificates for all top-level domains (TLDs) except for the following ones:
 * `.cu` (Cuba)
 * `.iq` (Iraq)
 * `.ir` (Iran)
 * `.kp` (North Korea)
 * `.sd` (Sudan)
 * `.ss` (South Sudan)
 * `.ye` (Yemen)

 {{site.data.keyword.cis_short_notm}} manages the certificate expiration date. To edit the hostnames on your dedicated custom certificate, you must reorder then delete. For example, you order a dedicated custom certificate with the hostname `alpha.yourdomain.com`. To add the hostname `beta.yourdomain.com` to your dedicated custom certificate, order another dedicated custom certificate with the hostnames `alpha.yourdomain.com` and `beta.yourdomain.com`. Afterward, you _must_ delete the original dedicated custom certificate.

The first time when you order a dedicated certificate, the Domain Control Validation (DCV) process occurs, which generates a corresponding TXT record. If you delete the TXT record, the DCV process occurs again when you order another dedicated certificate. If you delete a dedicated certificate, the TXT record corresponding to the DCV process is not deleted.
{: note}

The following are common errors that are seen when you order dedicated certificates:

   * `Error connecting to certificate service.`
   * `Error while requesting from certificate service.`

If you receive an error when you order certificates, refresh the page and try again.

### Use a provisioned certificate
{: #use-provisioned-certificate}

IBM has partnered with several certificate authorities (CAs) to provide domain wildcard certificates for our customers. Manual verification might be required for setting up these certificates. Your support team can help you perform these additional steps.

### Certificate priority at our edge
{: #certificate-priority-at-our-edge}

The following list denotes the priority by which the certificates are displayed at our edge:
1. Uploaded custom
2. Dedicated custom
3. Dedicated wildcard
4. Universal

### Minimum TLS version
{: #security-minimum-tls-version}

See [Minimum TLS version](/docs/cis?topic=cis-cis-tls-options#minimum-tls-version). Higher levels of TLS provide more security, but might prevent customers from connecting to your site.

## Best practice 5: Configure rate limiting
{: #best-practice-rate-limiting}

The main use cases for rate limiting are as follows:

* Enforce granular access control to resources. This process includes access control based on criteria such as user agent, IP address, referrer, host, country, and world region.
    * Limit by user agent: A common use case is to limit the rate of requests performed by individual user agents.
    * Allow specific IP addresses or ASNs: Another use case when you control access to resources is to exclude or include IP addresses or Autonomous System Numbers (ASNs) from a rate-limiting rule.
    * Limit by referrer: Some applications receive requests that are originated by other sources (for example, used by advertisements that link to third-party pages). You can limit the number of requests that are generated by individual referrer pages to manage quotas or avoid indirect DDoS attacks.
    * Limit by destination host: Create a rate-limiting rule that uses the host as a counting characteristic.
* Protect against credential stuffing and account takeover attacks.
* Limit the number of operations performed by individual clients. This action includes preventing scraping by bots, accessing sensitive data, bulk creation of new accounts, and programmatic buying in e-commerce platforms.
    * Prevent content scraping (through query string)
    * Prevent content scraping (through body)
    * Limit requests from bots
* Protect REST APIs from resource exhaustion (targeted DDoS attacks) and resources from abuse in general.
    * Prevent volumetric attacks
    * Protect resources
* Protect GraphQL APIs by preventing server overload and limiting the number of operations.
    * Limit the number of operations
    * Prevent server overload
