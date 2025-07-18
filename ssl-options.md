---

copyright:
  years: 2018, 2025
lastupdated: "2025-07-18"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Setting Transport Layer Security (TLS) options
{: #cis-tls-options}

The Transport Layer Security (TLS) options let you control whether visitors can browse your website over a secure connection, and when they do, how {{site.data.keyword.cis_full}} connects to your origin server.
{: shortdesc}

Use the latest version of the TLS protocol (TLS 1.3) for improved security and performance by switching from `Off` to `On`.
{: tip}

## TLS encryption modes
{: #tls-encryption-modes}

Set the TLS mode by selecting one of the following options from the Mode list.

These options are listed in the order from the most secure to the least secure (Off):
1. [Authenticated origin pull](#tls-encryption-modes-authenticated-origin): (Enterprise only)
1. [HTTPS only origin pull](#tls-encryption-modes-origin-only-pull) (Enterprise only)
1. [End-to-end CA signed](#tls-encryption-modes-end-to-end-ca-signed) (default and recommended)
1. [End-to-end flexible](#tls-encryption-modes-end-to-end-flexible) (edge to origin certificates can be self-signed)
1. [Client-to-edge](#tls-encryption-modes-client-to-edge) (edge to origin not encrypted, self-signed certificates are not supported)
1. [Off](#tls-encryption-modes-off) (not recommended)

### Authenticated origin pull
{: #tls-encryption-modes-authenticated-origin}

**Enterprise only.** In this mode, a secure connection is set up between the visitor and {{site.data.keyword.cis_short_notm}} and a secure connection between {{site.data.keyword.cis_short_notm}} and your web server. When {{site.data.keyword.cis_short_notm}} connects to your origin server, it presents a client certificate for authentication. This process helps ensure that only authorized requests from {{site.data.keyword.cis_short_notm}} can access your origin server. Use this mode if you want only trusted connections to reach your server. For more information, see [Authenticated origin pull](/docs/cis?topic=cis-authenticated-origin-pull).

### HTTPS only origin pull
{: #tls-encryption-modes-origin-only-pull}

**Enterprise only.** In this mode, a secure connection is set up between the visitor and {{site.data.keyword.cis_short_notm}}, and a secure and authenticated connection between {{site.data.keyword.cis_short_notm}} and your server. This mode has the same certificate requirements as end-to-end CA signed. However, it upgrades all connections between {{site.data.keyword.cis_short_notm}} and your origin webserver from HTTP to HTTPS, even if the visitor requests the original content over HTTP.

### End-to-end CA signed
{: #tls-encryption-modes-end-to-end-ca-signed}

This mode is the default and recommended setup. A secure connection is set up between the visitor and {{site.data.keyword.cis_short_notm}}, and a secure and authenticated connection between {{site.data.keyword.cis_short_notm}} and your web server. Your server must be set up to handle HTTPS connections, with a valid TLS certificate. This certificate must be signed by a certificate authority (CA), have an expiration date in the future, and respond for the request domain name (hostname). It is recommended that you use this TLS mode for best security practices, unless you understand the potential security threats of changing to one of the less strict modes.

![Diagram of End to end CA signed TLS](images/end-to-end-ca-signed.svg "Diagram of End to end CA signed TLS"){: caption="A diagram of end to end CA signed TLS" caption-side="bottom"}

### End-to-end flexible
{: #tls-encryption-modes-end-to-end-flexible}

In this mode, a secure connection is set up between your visitor and {{site.data.keyword.cis_short_notm}}, while a secure but non-authenticated connection between {{site.data.keyword.cis_short_notm}} and your web server. Your server must be set up to handle HTTPS connections, at a minimum with a self-signed certificate. However, the authenticity of this certificate is not verified. {{site.data.keyword.cis_short_notm}} connects to your origin web server when the address of your origin web server is correctly configured in your DNS settings. Use this mode if you can't obtain a certificate that is signed from a CA. Keep in mind that it is less secure compared to the end-to-end CA signed mode.

![Diagram of End to end flexible TLS](images/end-to-end-flexible.svg "Diagram of End to end flexible TLS"){: caption="A diagram of end to end flexible TLS" caption-side="bottom"}

### Client-to-edge
{: #tls-encryption-modes-client-to-edge}

In this mode, a secure encrypted connection is set up between your visitor and {{site.data.keyword.cis_short_notm}}, and a non-secure unencrypted connection between {{site.data.keyword.cis_short_notm}} and your web server. You don't need to have a TLS certificate on your web server, but your visitors still see the site as being HTTPS-enabled. This option is not recommended if you have any sensitive information on your website. This mode works only for redirecting traffic from port `443` (HTTPS) to port `80` (HTTP) and must be used only as a last resort if you are not able to set up TLS on your own web server. It is _less secure_ than any other option (even "Off"), and might cause trouble when you decide to switch away from it.

![Diagram of Client to edge TLS](images/client-to-edge.svg "Diagram of Client to edge TLS"){: caption="A diagram of client to edge TLS" caption-side="bottom"}

### Off
{: #tls-encryption-modes-off}

In this mode, no secure connection exists between your visitors and {{site.data.keyword.cis_short_notm}}, and between {{site.data.keyword.cis_short_notm}} and your web server. Visitors can view your website only over HTTP, and any visitor who attempts to connect with HTTPS receives an `HTTP 301 Redirect` to the plain HTTP version of your website. This mode is not recommended because it exposes all data and is least secure compared to the previous modes.

![Diagram of TLS Off](images/off.svg "Diagram of TLS Off"){: caption="A diagram of TLS Off" caption-side="bottom"}

## Traffic encryption - Minimum TLS version
{: #minimum-tls-version}

Set the minimum TLS version for traffic that tries to connect to your site by selecting one of the versions from the list.

By default, this version is set to `1.2`. Higher TLS versions provide additional security, but might not be supported by all browsers, which might prevent some customers from connecting to your site.
