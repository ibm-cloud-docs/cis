---

copyright:
  years: 2018, 2025
lastupdated: "2025-12-11"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Best practices for {{site.data.keyword.cis_short_notm}} setup
{: #best-practices-for-cis-setup}



Because {{site.data.keyword.cis_full}} is positioned at the edge of your network, you’ll need to take a few steps to guarantee a smooth integration with your {{site.data.keyword.cis_short_notm}} services. Consider these recommended best practices for integrating {{site.data.keyword.cis_short_notm}} with your origin servers.
{: shortdesc}

You can do these steps either before or after you change your DNS and activate our proxy service. These recommendations allow {{site.data.keyword.cis_short_notm}} to connect to your origin servers properly. They’ll help you prevent any issues with API or HTTPS traffic, and help your logs capture the correct IP addresses of your customers, rather than the protective {{site.data.keyword.cis_short_notm}} IP addresses.

Here’s what you need to set up:

* Restore the originating IPs of your customers
* Incorporate {{site.data.keyword.cis_short_notm}} IP addresses
* Make sure that your security settings don't interfere with API traffic
* Configure your security settings as strictly as possible

## Best practice 1: Know how to restore the originating IPs of your customers
{: #best-practice-know-how-to-restore-originating-ip}

As a reverse proxy, CIS provides the origination IP in these headers:

* `CF-Connecting-IP`
* `X-Forwarded-For`
* `True-Client-IP` (optional)

You can restore user IP addresses by using various tools for infrastructures such as Apache, Windows IIS, and NGINX.

## Best practice 2: Incorporate {{site.data.keyword.cis_short_notm}} IP addresses to make integration smoother
{: #best-practice-incorporate-cis-ip-addresses}

Take the following two steps:

* Remove any rate limiting of {{site.data.keyword.cis_short_notm}} IP addresses
* Set up your ACLs to allow only {{site.data.keyword.cis_short_notm}} IP addresses and other trusted parties

You can find the updated list of IP ranges for IBM {{site.data.keyword.cis_short_notm}} [at this location](/docs/cis?topic=cis-cis-allowlisted-ip-addresses).

## Best practice 3: Configure your security settings as strictly as possible
{: #best-practice-configure-strict-security-settings}

{{site.data.keyword.cis_short_notm}} provides some options for encrypting your traffic. As a reverse proxy, the TLS connection is terminated at Cloudflare and a new TLS connection is opened to your origin servers. For your termination with {{site.data.keyword.cis_short_notm}}, you can upload a custom certificate from your account, use a wildcard certificate that is provisioned for you by {{site.data.keyword.cis_short_notm}}, or both.

### Upload a custom certificate
{: #strict-upload-custom-cert}

You can upload your public and private keys when you create an Enterprise domain. If you upload your own certificate, you gain immediate compatibility with encrypted traffic, and you maintain control over your certificate (for example, an Extended Validation (EV) certificate). Remember that you are responsible for managing your certificate if you upload a custom certificate. For example, IBM {{site.data.keyword.cis_short_notm}} doesn't track the certificate expiration dates.

### Alternatively, use a certificate provisioned by CIS
{: #strict-use-cert-cis-provisioned}

IBM {{site.data.keyword.cis_short_notm}} works with several Certificate Authorities (CAs) to provide domain wildcard certificates for our customers, by default. Manual verification might be required for setting up these certificates, and your support team can help you perform these additional steps.

### Change your TLS setting to End-to-End CA Signed
{: #strict-change-tls-setting}

Most of our Enterprise customers use the End-to-End CA Signed security setting. An **End-to-End CA Signed** setting requires a valid, CA-signed certificate installed on your web server. The certificate's expiration date must be in the future, and it must have a matching hostname or Subject Alternative Name (SAN).
