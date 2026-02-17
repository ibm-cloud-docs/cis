---

copyright:
  years: 2018, 2026
lastupdated: "2026-02-17"

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

## Best practice 2: Activate your Web Application Firewall (WAF) safely
{: #best-practice-activate-waf-safely}

Your WAF is available in the **Security** section. Here, we walk through these settings in reverse order to ensure that your WAF is configured as safely as possible before you turn it on for your entire domain. These initial settings can reduce false positives by populating **Security Events** for further tuning. Your WAF is updated automatically to handle new vulnerabilities as they are identified. For more information, see [Using Security events capability](/docs/cis?topic=cis-using-the-cis-security-events-capability).

The WAF protects you against the following types of attacks:
* SQL injection attack
* Cross-site scripting
* Cross-site forgery

The WAF contains a default ruleset, which includes rules to stop the most common attacks. Currently, we allow you to either enable or disable the WAF and fine-tune specific rules in the WAF rulesets. See [WAF actions](/docs/cis?topic=cis-waf-actions) document for more details on the ruleset and the behavior of each rule.

For more information, see [Web Application Firewall (WAF) concepts](/docs/cis?topic=cis-waf-q-and-a).

## Best practice 3: Configure WAF Attack score safely
{: #waf-attack-score-rule}

WAF Attack Score strengthens your security posture by detecting variations of known attacks by using machine learning. It complements WAF managed rules by identifying malicious requests that do not match existing rule signatures.

To configure WAF Attack Score safely, begin with monitoring before enforcing blocking actions. This allows you to review scored traffic in Security Events and adjust thresholds to minimize false positives.

### Configuring WAF Attack score in custome rule
{: #waf-score-in-rule}

1. If you are an Enterprise customer, [create a custom rule](/docs/cis?topic=cis-about-waf-custom-rules&interface=ui#create-custom-rule-ui) that blocks requests with a WAF Attack Score less than or equal to 20. This value is the recommended starting threshold.

   | Field | Operator | Value |
   | ----- | -------- | ----- |
   | WAF Attack Score | less than or equal to | `20` |
   {: caption="Enterprise rule example" caption-side="bottom"}

     * Equivalent rule expression: `cf.waf.score le 20`
     * Action: _Block_

   If you are a Business customer, create a custom rule using the **WAF Attack Score Class** field instead. For example, block requests with a score class of Attack.

   | Field | Operator | Value |
   | ----- | -------- | ----- |
   | WAF Attack Score Class | Equals | `Attack` |
   {: caption="Business rule example" caption-side="bottom"}

     * Equivalent rule expression: `cf.waf.score.class eq "attack"`
     * Action: _Block_

1. Monitor the rule closely during the first few days. Verify that the selected threshold or class value aligns with your traffic patterns. Adjust the rule if you observe false positives or missed threats.

1. If you are an Enterprise customer and you created a rule with Log action, change the rule action to a more severe one, like _Managed Challenge_ or _Block_.

CIS recommends to use WAF managed rules together with WAF Attack Score. Managed rules protect against well known attack patterns, while Attack Score detects modified or obfuscated attacks—providing layered and adaptive protection for your domain.

## Best practice 3: Configure your TLS settings
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

Higher levels of TLS provide more security, but might prevent customers from connecting to your site. For more information, see [Minimum TLS version](/docs/cis?topic=cis-cis-tls-options#minimum-tls-version).

## Best practice 4: Configure rate limiting
{: #best-practice-rate-limiting}

Use rate-limiting rules to protect your site or API from malicious traffic by blocking client IP addresses that match a URL pattern or exceed a defined threshold. The main use cases for rate limiting are as follows:

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
