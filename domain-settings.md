---

copyright:
  years: 2018, 2026
lastupdated: "2026-02-26"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Domain settings
{: #domain-settings-cis}

Domain settings define how a domain is secured, delivered, and managed at the edge. When you onboard a domain and delegate traffic to CIS name servers, inbound requests are processed at the CIS edge before being forwarded to the origin.

Domain settings establish the policies that protect applications from threats, ensure high availability through resilient traffic routing, and improve performance through edge optimization. Each domain operates as an independent configuration boundary, enabling tailored security, reliability, and performance controls for different applications or workloads.

## What domain settings control
{: #domain-settings-control}

Domain settings determine how your domain operates across DNS, security, performance, and traffic management.

* DNS behavior: Controls how DNS records resolve and whether traffic is routed directly to the origin or proxied through the edge network.
* TLS and HTTPS configuration: Defines how certificates are managed, which TLS versions are allowed, and whether HTTPS is enforced for incoming requests.
* Security features: Governs how traffic is inspected and mitigated by security capabilities such as the Web Application Firewall (WAF), DDoS protection, bot management, and configurable security levels.
* Performance optimization: Specifies caching, compressed, and protocol support (for example, `HTTP/2` or `HTTP/3`).
* Traffic handling: Determines how requests are redirected, rewritten, or processed before reaching the origin server.

## Why configure domain settings
{: #why-to-configure-domain}

Default settings provide baseline security and performance. However, most applications require customization to meet specific technical, security, or compliance requirements.

Configure domain settings to:

* Enforce security policies.
* Optimize performance for static and dynamic content.
* Control how traffic is cached and routed.
* Meet TLS and encryption standards.
* Reduce load on origin infrastructure.

Proper configuration ensures that your domain operates securely, efficiently, and in alignment with operational requirements.

## Advanced security
{: #advanced-security-feature}

Domain settings provide the configuration framework through which advanced security features are enabled, managed, and enforced for each domain. These settings include the following features, which you can change, enable, or disable.

* **Browser integrity check** - The browser integrity check looks for HTTP headers that are commonly abused by spammers. It denies traffic with those headers access to your page. It also blocks or challenges visitors that do not have a user agent, or who add a nonstandard user agent. This tactic is commonly used by abuse bots, crawlers, or APIs.
* **Challenge passage** - Controls how long a visitor that passed a challenge (or JavaScript challenge) gains access to your site before they are challenged again. This challenge is based on the visitor's IP, and therefore does not apply to challenges presented by WAF rules because they are based on an action that the user performs on your site.
* **Security level** - Sets the security level of your website to determine which visitors receive a challenge page.
* **Always use HTTPS** - Redirects all visitors to the HTTPS version.
* **Email obfuscation** - Prevents spam from harvesters and bots that try to access email addresses on your pages.
* **Automatic HTTPS rewrites** - Helps fix mixed content by changing `http` to `https` for all resources (or links) on your website that can be served with HTTPS.
* **Opportunistic encryption** - Allows browsers to benefit from the improved performance of HTTP/2 by informing them that your site is available over an encrypted connection.
* **Universal SSL** - Activates universal SSL certificates from your zone to the edge.
* **True client IP header** - Sends the user's IP address in the True-Client-IP header.
