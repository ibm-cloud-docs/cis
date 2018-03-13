---
copyright:
  years: 2018
lastupdated: "2018-03-05"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Managing your IBM CIS for optimal Security

The Cloud Internet Services (CIS) security settings include safe defaults designed to avoid false positives and negative influence on your traffic. However, these safe default settings do not provide the best security posture for every customer. Take the following steps to be sure that your CIS account is configured in a safe and secure way:

**Recommendations and best practices:**

* Secure origin IP addresses by proxying and increasing obfuscation
* Configure your Security Level selectively
* Activate your Web Application Firewall (WAF) safely

## Best practice 1: Secure Your Origin IP Addresses

When a subdomain is proxied using IBM CIS, all traffic is protected because we actively respond with IP addresses specific to IBM CIS (for example, all of your clients connect to CIS proxies first, and your origin IP addresses are obscured).

### Use CIS proxies for all DNS Records for HTTP(S) traffic from your origin

To improve the security of your origin IP address, all HTTP(S) traffic should be proxied.

**See the difference yourself - Query a non-proxied and a proxied record:**

```
$ dig greycloud.theburritobot.com +short
1.2.3.4 (The origin IP address)

$ dig orangecloud.theburritobot.com +short
104.16.22.6 , 104.16.23.6 (CIS IP addresses)
```

### Obscure non-proxied origin records with non-standard names
Any records that cannot be proxied through IBM CIS, and that still use your origin IP, such as FTP, can be secured by creating additional obfuscation. In particular, if you require a record for your origin that cannot be proxied by IBM CIS, use a non-standard name. For example, instead of `ftp.example.com` use `[random word or-random characters].example.com.` This obfuscation makes dictionary scans of your DNS records less likely to expose your origin IP addreses.

### Use separate IP ranges for HTTP and non-HTTP traffic if possible
Some customers use separate IP ranges for HTTP and non-HTTP traffic, thereby allowing them to proxy all records pointing to their HTTP IP range, and to obscure all non-HTTP traffic with a different IP subnet.

## Best practice 2: Configure your Security Level selectively
Your **Security Level** establishes the sensitivity of our **IP Reputation Database**. IBM CIS sees over 1 billion unique IP addresses every month, from more than 4 million websites, which allows our system to identify malicious actors and prevent them from reaching your web assets. To prevent negative interactions or false positives, configure your **Security Level** by domain to heighten security where necessary, and to decrease it where appropriate.

### Increase the Security Level for Sensitive Areas to 'High'
You can increase this setting by adding a **Page Rule** for administration pages or login pages, to reduce brute-force attempts:

1. Create a **Page Rule** with the URL pattern of your API (for example, `www.example.com/wp-login`). 
2. Identify the **Securty Level** setting.
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

We recommend that you review your Security level settings periodically, and you can find instructions in our [Best Practices for Setup document](best-practices.html#best-practice-3-review-your-security-settings-to-make-sure-they-dont-interfere-with-api-traffic)

## Best practice 3: Activate your Web Application Firewall (WAF) safely
Your WAF is available in the **Security** section. We will walk through these settings in reverse order to ensure that your WAF is configured as safely as possible before turning it on for your entire domain. These initial settings can reduce false positives by populating the Traffic Application with WAF events for further tuning. Your WAF is updated automatically to handle new vulnerabilities as they are identified.

The WAF protects you against the following types of attacks:
* SQL injection attack
* Cross-site scripting
* Cross-site forgery

The WAF contains a default rule set which includes rules to stop the most common attacks. At this time, we allow you to either enable or disable the WAF. See the [WAF default rule set](waf-rule-set.html) document for more details on the default rule set and the behavior of each rule.

## Best practice 4: Configure your TLS settings
CIS provides some options for encrypting your traffic. As a reverse proxy, we close TLS conections at our datacenters and open a new TLS connection to your origin server.

TLS offers four modes of operation:
* **Off**: TLS is disabled in this mode, it is not recommended.
* **Client-to-edge**: TLS encrypts traffic from CIS to your clients, but not from CIS to your origin server(s).
* **End-to-end flexible**: TLS encrypts all traffic; however, you can use a self-signed certificate to secure traffic between CIS and your origin server(s).
* **End-to-end CA signed**: TLS encrypts all traffic; you must use a CA-signed certificate.

For more detail about your TLS options, please refer to [this document](ssl-options.html).

CIS allows you to use custom certificates, or you can use a wildcard certificate provisioned for you by CIS.

### Upload a custom certificate
You can upload your custom certificate by clicking **Add Certificate** button and entering your certificate, private key, and bundle method. If you upload your own certificate, you gain immediate compatibility with encrypted traffic, and you maintain control over your certificate (for example, an Extended Validation (EV) certificate). Remember that you'll be responsible for managing your certificate if you upload a custom certificate. For example, CIS won't track the certificate expiration dates. 

![custom-certificate](images/upload-custom-certificate.png)

### Utilize a provisioned certificate
CIS has partnered with several Certificate Authorities (CAs) to provide domain wildcard certificates for our customers. Manual verification could be required for setting up these certificates your support team can help you perform these additional steps.
