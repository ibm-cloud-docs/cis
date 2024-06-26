---

copyright:
  years: 2018, 2024
lastupdated: "2024-06-26"

keywords: 

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Managing {{site.data.keyword.cis_short_notm}} for optimal security
{: #manage-your-ibm-cis-for-optimal-security}

The {{site.data.keyword.cis_full}} ({{site.data.keyword.cis_short_notm}}) security settings include safe defaults designed to avoid false positives and negative influence on your traffic. However, these safe default settings do not provide the best security posture for every customer. Take the following steps to be sure that your {{site.data.keyword.cis_short_notm}} account is configured in a safe and secure way.
{: shortdesc}

[Recommendations and best practices](: tag-blue)

* Secure your origin IP addresses by proxying and increasing obfuscation
* Configure your security level selectively
* Activate your Web Application Firewall (WAF) safely

## Best practice 1: Secure your origin IP addresses
{: #best-practice-secure-origin-ip-address}

When a subdomain is proxied using {{site.data.keyword.cis_short_notm}}, all traffic is protected because {{site.data.keyword.cis_short_notm}} actively responds with IP addresses specific to {{site.data.keyword.cis_short_notm}} (for example, all of your clients connect to {{site.data.keyword.cis_short_notm}} proxies first, and your origin IP addresses are obscured).

### Use {{site.data.keyword.cis_short_notm}} proxies for all DNS records for HTTP(S) traffic from your origin
{: #use-cis-proxies-for-dns-records}

To improve the security of your origin IP address, you should proxy all HTTP(S) traffic.

**See the difference yourself - Query a non-proxied and a proxied record:**

```sh
dig nonproxied.theburritobot.com +short
1.2.3.4 (The origin IP address)

$ dig proxied.theburritobot.com +short
104.16.22.6 , 104.16.23.6 (CIS IP addresses)
```
{: pre}

### Obscure non-proxied origin records with non-standard names
{: #obscure-non-proxied-origin-records-with-non-standard-names}

Any records that cannot be proxied through {{site.data.keyword.cis_short_notm}}, and that still use your origin IP, such as FTP, can be secured by creating additional obfuscation. In particular, if you require a record for your origin that cannot be proxied by {{site.data.keyword.cis_short_notm}}, use a non-standard name. For example, instead of `ftp.example.com` use `[random word or-random characters].example.com.` This obfuscation makes dictionary scans of your DNS records less likely to expose your origin IP addresses.

### Use separate IP ranges for HTTP and non-HTTP traffic if possible
{: #use-separate-ipranges-for-traffic}

Some customers use separate IP ranges for HTTP and non-HTTP traffic, thereby allowing them to proxy all records pointing to their HTTP IP range, and to obscure all non-HTTP traffic with a different IP subnet.

## Best practice 2: Configure your security level selectively
{: #best-practice-configure-security-level-selectively}

Your **Security Level** establishes the sensitivity of our **IP Reputation Database**. To prevent negative interactions or false positives, configure your **Security Level** by domain to heighten security where necessary, and to decrease it where appropriate.

### Increase the security level for sensitive areas to 'High'
{: #increase-security-level-for-sensitive-areas}

You can increase this setting from the Advanced Security page for your domain or by adding a **Page Rule** for administration pages or login pages, to reduce brute-force attempts:

1. Create a **Page Rule** with the URL pattern of your API (for example, `www.example.com/wp-login`).
2. Identify the **Security Level** setting.
3. Mark the setting as **High**.
4. Select **Provision Resource**.

### Decrease the security level for non-sensitive paths or APIs to reduce false positives
{: #decrease-security-level-non-sensitive-paths-reduce-false-positives}

This setting can be decreased for general pages and API traffic:

1. Create a **Page Rule** with the URL pattern of your API (for example, `www.example.com/api/*`).
2. Identify the **Security Level** setting.
3. Turn Security Level to **Low** or **Essentially off**.
4. Select **Provision Resource**.

### What do security level settings mean?
{: #what-do-security-level-settings-mean}

Our security level settings are aligned with threat scores that certain IP addresses acquire from malicious behavior on our network. A threat score above 10 is considered high.

* **High**: Threat scores greater than 0 are challenged.
* **Medium**: Threat scores greater than 14 are challenged.
* **Low**: Threat scores greater than 24 are challenged.
* **Essentially off**: Threat scores greater than 49 are challenged.
* **Off**: Enterprise only
* **Defense mode**: Should only be used when your website is under a DDoS attack. Visitors receive an interstitial page for about five seconds while {{site.data.keyword.cis_short_notm}} analyzes the traffic and behavior to make sure it is a legitimate visitor trying to access your website. Defense mode might affect some actions on your domain, such as using an API. You are able to set a custom security level for your API or any other part of your domain by creating a page rule for that section.

It is recommended that you review your security-level settings periodically. You can find instructions in [Best practices for CIS setup](/docs/cis?topic=cis-best-practices-for-cis-setup).

## Best practice 3: Activate your Web Application Firewall (WAF) safely
{: #best-practice-activate-waf-safely}

Your WAF is available in the **Security** section. Here, we walk through these settings in reverse order to ensure that your WAF is configured as safely as possible before turning it on for your entire domain. These initial settings can reduce false positives by populating **Security Events** for further tuning. Your WAF is updated automatically to handle new vulnerabilities as they are identified. For more information, see [Using Security events capability](/docs/cis?topic=cis-using-the-cis-security-events-capability).

The WAF protects you against the following types of attacks:
* SQL injection attack
* Cross-site scripting
* Cross-site forgery

The WAF contains a default rule set which includes rules to stop the most common attacks. At this time, we allow you to either enable or disable the WAF and fine-tune specific rules in the WAF rule sets. See [WAF actions](/docs/cis?topic=cis-waf-actions) document for more details on the rule set and the behavior of each rule.

For more information, see [Web Application Firewall (WAF) concepts](/docs/cis?topic=cis-waf-q-and-a).

## Best practice 4: Configure your TLS settings
{: #best-practice-configure-tls-settings}

IBM {{site.data.keyword.cis_short_notm}} provides some options for encrypting your traffic. As a reverse proxy, we close TLS connections at our data centers and open a new TLS connection to your origin server.

TLS offers four modes of operation:
* **Off**: TLS is disabled in this mode, it is not recommended.
* **Client-to-edge**: TLS encrypts traffic from {{site.data.keyword.cis_short_notm}} to your clients, but not from {{site.data.keyword.cis_short_notm}} to your origin server(s).
* **End-to-end flexible**: TLS encrypts all traffic; however, you can use a self-signed certificate to secure traffic between {{site.data.keyword.cis_short_notm}} and your origin server(s).
* **End-to-end CA signed**: (Recommended) TLS encrypts all traffic; you must use a CA-signed certificate.
* **Authenticated origin pull**: (Enterprise only) TLS client certificate presented for authentication on origin pull. For more information see [Authenticated origin pull](/docs/cis?topic=cis-authenticated-origin-pull).

Refer to [TLS options](/docs/cis?topic=cis-cis-tls-options) for details.

IBM {{site.data.keyword.cis_short_notm}} allows you to use custom certificates, or you can use a wildcard certificate provisioned for you by {{site.data.keyword.cis_short_notm}}.

### Upload custom certificates
{: #upload-custom-certs}

You can upload your custom certificate by clicking **Add Certificate** and entering your certificate, private key, and bundle method. If you upload your own certificate, you gain immediate compatibility with encrypted traffic, and you maintain control over your certificate (for example, an Extended Validation (EV) certificate). {{site.data.keyword.cis_short_notm}} does not support certificate pinning through ordered or Universal certificates. If you wish to use certificate pinning, it is recommended that you upload and maintain your own custom certificate.

Remember that you are responsible for managing your certificate if you upload a custom certificate. For example, {{site.data.keyword.cis_short_notm}} won't track the certificate expiration date.
{: important}

### Order dedicated certificates
{: #order-dedicated-certs}

{{site.data.keyword.cis_short_notm}} makes managing your certificates easy by offering dedicated certificates. You no longer need to generate private keys, create certificate signing requests (CSR), or remember to renew certificates. You can order a dedicated certificate by clicking **Add Certificate** and ordering a wildcard certificate or entering hostnames to order a dedicated custom certificate. The type of certificates are:

* SHA-2/ECDSA signed certificate using P-256 key,
* SHA-2/RSA signed certificate using RSA 2048-bit key, and
* SHA-1/RSA signed certificate using RSA 2048-bit key.

{{site.data.keyword.cis_short_notm}} can issue for all TLDs except for `.cu`, `.iq`, `.ir`, `.kp`, `.sd`, `.ss`, and `.ye`. {{site.data.keyword.cis_short_notm}} manages the expiration date. To edit the hostnames on your dedicated custom certificate, you must reorder then delete. For example, you order a dedicated custom certificate with the hostname `alpha.yourdomain.com`. To add the hostname `beta.yourdomain.com` to your dedicated custom certificate, order another dedicated custom certificate with the hostnames `alpha.yourdomain.com` and `beta.yourdomain.com`. Afterwards you _must_ delete the original dedicated custom certificate.

The first time you order a dedicated certificate Domain Control Validation (DCV) process occurs, which generates a corresponding TXT record. If you delete the TXT record, the DCV process happens again when you order another dedicated certificate. If you delete a dedicated certificate, the TXT record corresponding to the DCV process is not deleted.
{: note}

The following are common errors seen when ordering dedicated certificates:
* `Error connecting to certificate service.`
* `Error while requesting from certificate service.`
{: note}

If you receive an error when ordering certificates, refresh the page and try again.

### Use a provisioned certificate
{: #use-provisioned-certificate}

IBM has partnered with several Certificate Authorities (CAs) to provide domain wildcard certificates for our customers. Manual verification could be required for setting up these certificates. Your support team can help you perform these additional steps.

### Certificate priority at our edge
{: #certificate-priority-at-our-edge}

The priority by which the certificates are displayed at our edge is:
1. Uploaded custom
2. Dedicated custom
3. Dedicated wildcard
4. Universal

### Minimum TLS version
{: #security-minimum-tls-version}

See [Minimum TLS version](/docs/cis?topic=cis-cis-tls-options#minimum-tls-version). Higher levels of TLS provide more security, but might prevent customers from connecting to your site.


