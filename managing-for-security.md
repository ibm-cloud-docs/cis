---
copyright:
  years: 2018
lastupdated: "2018-06-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Manage your IBM CIS for optimal security

The IBM Cloud Internet Services (CIS) security settings include safe defaults designed to avoid false positives and negative influence on your traffic. However, these safe default settings do not provide the best security posture for every customer. Take the following steps to be sure that your CIS account is configured in a safe and secure way.

**Recommendations and best practices:**

* Secure origin IP addresses by proxying and increasing obfuscation
* Configure your Security Level selectively
* Activate your Web Application Firewall (WAF) safely

## Best practice 1: Secure Your Origin IP Addresses

When a subdomain is proxied using IBM CIS, all traffic is protected because we actively respond with IP addresses specific to IBM CIS (for example, all of your clients connect to CIS proxies first, and your origin IP addresses are obscured).

### Use IBM CIS proxies for all DNS Records for HTTP(S) traffic from your origin

To improve the security of your origin IP address, all HTTP(S) traffic should be proxied.

**See the difference yourself - Query a non-proxied and a proxied record:**

```
$ dig nonproxied.theburritobot.com +short
1.2.3.4 (The origin IP address)

$ dig proxied.theburritobot.com +short
104.16.22.6 , 104.16.23.6 (CIS IP addresses)
```

### Obscure non-proxied origin records with non-standard names
Any records that cannot be proxied through IBM CIS, and that still use your origin IP, such as FTP, can be secured by creating additional obfuscation. In particular, if you require a record for your origin that cannot be proxied by IBM CIS, use a non-standard name. For example, instead of `ftp.example.com` use `[random word or-random characters].example.com.` This obfuscation makes dictionary scans of your DNS records less likely to expose your origin IP addreses.

### Use separate IP ranges for HTTP and non-HTTP traffic if possible
Some customers use separate IP ranges for HTTP and non-HTTP traffic, thereby allowing them to proxy all records pointing to their HTTP IP range, and to obscure all non-HTTP traffic with a different IP subnet.

## Best practice 2: Configure your Security Level selectively
Your **Security Level** establishes the sensitivity of our **IP Reputation Database**. To prevent negative interactions or false positives, configure your **Security Level** by domain to heighten security where necessary, and to decrease it where appropriate.

### Increase the Security Level for Sensitive Areas to 'High'
You can increase this setting by adding a **Page Rule** for administration pages or login pages, to reduce brute-force attempts:

1. Create a **Page Rule** with the URL pattern of your API (for example, `www.example.com/wp-login`). 
2. Identify the **Security Level** setting.
3. Mark the setting as **High**.
4. Select **Provision Resource**.

### Decrease the Security Level for non-sensitive paths or APIs to reduce false positives
This setting can be decreased for general pages and API traffic: 

1. Create a **Page Rule** with the URL pattern of your API (for example, `www.example.com/api/*`).
2. Identify the **Security Level** setting.
3. Turn Security Level to **Low** or **Essentially off**.
4. Select **Provision Resource**.

### What do Security Level settings mean?
Our Security Level settings are aligned with threat scores that certain IP addresses acquire from malicious behavior on our network. A threat score above 10 is considered high.

* **HIGH**: Threat scores greater than 0 are challenged.
* **MEDIUM**: Threat scores greater than 14 are challenged.
* **LOW**: Threat scores greater than 24 are challenged.
* **ESSENTIALLY OFF**: Threat scores greater than 49 are challenged.

We recommend that you review your Security level settings periodically, and you can find instructions in our [Best Practices for CIS Setup document](best-practices.html)

## Best practice 3: Activate your Web Application Firewall (WAF) safely
Your WAF is available in the **Security** section. We will walk through these settings in reverse order to ensure that your WAF is configured as safely as possible before turning it on for your entire domain. These initial settings can reduce false positives by populating **Security Events** for further tuning. Your WAF is updated automatically to handle new vulnerabilities as they are identified.

The WAF protects you against the following types of attacks:
* SQL injection attack
* Cross-site scripting
* Cross-site forgery

The WAF contains a default rule set which includes rules to stop the most common attacks. At this time, we allow you to either enable or disable the WAF and fine-tune specific rules in the WAF rule sets. See the [WAF default rule set](waf-rule-set.html) document for more details on the default rule set and the behavior of each rule.

For more information about the WAF, please see the [WAF Concepts document](waf-concept.html)

## Best practice 4: Configure your TLS settings
IBM CIS provides some options for encrypting your traffic. As a reverse proxy, we close TLS connections at our datacenters and open a new TLS connection to your origin server.

TLS offers four modes of operation:
* **Off**: TLS is disabled in this mode, it is not recommended.
* **Client-to-edge**: TLS encrypts traffic from CIS to your clients, but not from CIS to your origin server(s).
* **End-to-end flexible**: TLS encrypts all traffic; however, you can use a self-signed certificate to secure traffic between CIS and your origin server(s).
* **End-to-end CA signed**: TLS encrypts all traffic; you must use a CA-signed certificate.

For more detail about your TLS options, please refer to [this document](ssl-options.html).

IBM CIS allows you to use custom certificates, or you can use a wildcard certificate provisioned for you by CIS.

### Upload custom certificates
You can upload your custom certificate by clicking **Add Certificate** button and entering your certificate, private key, and bundle method. If you upload your own certificate, you gain immediate compatibility with encrypted traffic, and you maintain control over your certificate (for example, an Extended Validation (EV) certificate). Remember that you'll be responsible for managing your certificate if you upload a custom certificate. For example, IBM CIS won't track the certificate expiration date. 

![custom-certificate](images/upload-custom-certificate.png)

### Order dedicated certificates
CIS makes managing your certificates easy by offering dedicated certificates. You no longer need to generate private keys, create certificate signing requests (CSR), or remember to renew certificates. You can order a dedicated certificate by clicking **Add Certificate** button and ordering a wildcard certificate or entering hostnames to order a dedicated custom certificate. The type of certificates are:

 * SHA-2/ECDSA signed certificate using P-256 key, 
 * SHA-2/RSA signed certificate using RSA 2048-bit key, and 
 * SHA-1/RSA signed certificate using RSA 2048-bit key. 
 
CIS can issue for all TLDs except for `.cu`, `.iq`, `.ir`, `.kp`, `.sd`, `.ss`, and `.ye`. CIS manages the expiration date. To edit the hostnames on your dedicated custom certificate, you must reorder then delete. For example, you order a dedicated custom certificate with the hostname `alpha.yourdomain.com`. To add the hostname `beta.yourdomain.com` to your dedicated custom certificate, order another dedicated custom certificate with the hostnames `alpha.yourdomain.com` and `beta.yourdomain.com`. Afterwards you _must_ delete the original dedicated custom certificate.

**Note**: The first time you order a dedicated certificate Domain Control Validation (DCV) process occurs, which generates a corresponding TXT record. If you delete the TXT record, the DCV process happens again when you order another dedicated certificate. If you delete a dedicated certificate, the TXT record corresponding to the DCV process is not deleted.

**Note**: The following are common errors seen when ordering dedicated certificates:
* `Error connecting to certificate service.`
* `Error while requesting from certificate service.`

If you receive an error when ordering certificates refresh the page and try again.

![dedicated-certificate](images/order-dedicated-certificate.png)

### Utilize a provisioned certificate
IBM has partnered with several Certificate Authorities (CAs) to provide domain wildcard certificates for our customers. Manual verification could be required for setting up these certificates. Your support team can help you perform these additional steps.

### Certificate priority at our edge
The priority by which the certificates are displayed at our edge is:
1. Uploaded custom
2. Dedicated custom
3. Dedicated wildcard
4. Universal

### Require Modern TLS
**Require Modern TLS** prevents older browsers from connecting using older, less secure versions of TLS. Any connections from browsers using TLS 1.1 or earlier are refused. TLS versions 1.2 and 1.3 are included in Modern TLS and are considered secure.
