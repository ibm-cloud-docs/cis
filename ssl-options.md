---

copyright:
  years: 2018, 2024
lastupdated: "2024-12-18"

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

These options are listed in the order from the least secure (Off) to the most secure (End-to-End CA signed).
* [Off](#tls-encryption-modes-off) (not recommended)
* [Client-to-Edge](#tls-encryption-modes-client-to-edge) (edge to origin not encrypted, self-signed certificates are not supported)
* [End-to-End flexible](#tls-encryption-modes-end-to-end-flexible) (edge to origin certificates can be self-signed)
* [End-to-End CA signed](#tls-encryption-modes-end-to-end-ca-signed) (default and recommended)
* [HTTPS only origin pull](#tls-encryption-modes-origin-only-pull) (Enterprise only)

### Off
{: #tls-encryption-modes-off}

No secure connection between your visitor and {{site.data.keyword.cis_short_notm}}, and no secure connection between {{site.data.keyword.cis_short_notm}} and your web server. Visitors can only view your website over HTTP, and any visitor attempting to connect using HTTPS receives an `HTTP 301 Redirect` to the plain HTTP version of your website.

![Diagram of TLS Off](images/off.svg "Diagram of TLS Off"){: caption="A diagram of TLS Off" caption-side="bottom"}

### Client-to-Edge
{: #tls-encryption-modes-client-to-edge}

A secure connection between your visitor and {{site.data.keyword.cis_short_notm}}, but no secure connection between {{site.data.keyword.cis_short_notm}} and your web server. You don't need to have a TLS certificate on your web server, but your visitors still see the site as being HTTPS-enabled. This option is not recommended if you have any sensitive information on your website. This setting only works for port 443->80. It should only be used as a last resort if you are not able to set up TLS on your own web server. It is _less secure_ than any other option (even "Off"), and could cause you trouble when you decide to switch away from it.

![Diagram of Client to edge TLS](images/client-to-edge.svg "Diagram of Client to edge TLS"){: caption="A diagram of Client to edge TLS" caption-side="bottom"}

### End-to-End flexible
{: #tls-encryption-modes-end-to-end-flexible}

A secure connection between your visitor and {{site.data.keyword.cis_short_notm}}, and secure connection (but not authenticated) between {{site.data.keyword.cis_short_notm}} and your web server. You must have your server configured to answer HTTPS connections, with a self-signed certificate at least. The authenticity of the certificate is not verified: from {{site.data.keyword.cis_short_notm}}’s point of view (when we connect to your origin webserver), it’s the equivalent of bypassing this error message. As long as the address of your origin webserver is correct in your DNS settings, you know that we’re connecting to your webserver, and not someone else’s.

![Diagram of End to end flexible TLS](images/end-to-end-flexible.svg "Diagram of End to end flexible TLS"){: caption="A diagram of End to end flexible TLS" caption-side="bottom"}

### End-to-End CA signed
{: #tls-encryption-modes-end-to-end-ca-signed}

Default and recommended. A secure connection between the visitor and {{site.data.keyword.cis_short_notm}}, and secure and authenticated connection between {{site.data.keyword.cis_short_notm}} and your web server. You must have your server configured to answer HTTPS connections, with a valid TLS certificate. This certificate must be signed by a certificate authority, have an expiration date in the future, and respond for the request domain name (hostname). It is recommended that you keep using this TLS mode for best security practices, unless you understand the potential security threats of changing to one of the less strict modes.

![Diagram of End to end CA signed TLS](images/end-to-end-ca-signed.svg "Diagram of End to end CA signed TLS"){: caption="A diagram of End to end CA signed TLS" caption-side="bottom"}

### HTTPS Only Origin Pull
{: #tls-encryption-modes-origin-only-pull}

**Enterprise only.** This mode has the same certificate requirements as End-to-End CA Signed and also upgrades all connections between {{site.data.keyword.cis_short_notm}} and your origin webserver from HTTP to HTTPS, even if the original content requested is over HTTP. 


## Traffic encryption - Minimum TLS version
{: #minimum-tls-version}

Set the minimum TLS version for traffic trying to connect to your site by selecting one of the versions from the list.

By default, this is set to `1.2`. Higher TLS versions provide additional security, but might not be supported by all browsers. This could result in some customers being unable to connect to your site.
