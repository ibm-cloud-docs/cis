---

copyright:
  years: 2024, 2025
lastupdated: "2025-07-07"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# About TLS
{: #about-tls}

TLS is a standard security protocol for establishing encrypted links between a web server and a browser in an online communication. A TLS certificate is necessary to create a TLS connection with a website and comprises the domain name, the name of the company, and additional data, such as company address, city, state, and country. The certificate also shows the expiration date and details of the issuing certificate authority (CA).
{: shortdesc}

## How Does TLS Work?
{: #how-does-tls-work}

When a browser initiates a connection with a TLS-secured website, it first retrieves the site's TLS Certificate to check whether the certificate is still valid. It verifies that the CA is one that the browser trusts, and that the certificate is used by the website for which it is issued. If any of these checks fail, you get a warning, which indicates that the website is not secured by a valid certificate.

When a TLS certificate is installed on a web server, it enables a secure connection between the web server and the browser that connects to it. The website's URL is prefixed with "HTTPS" instead of "HTTP" and a padlock is shown on the address bar. If the website uses an extended validation (EV) certificate, the browser might also show a green address bar.
