---

copyright:
  years: 2018, 2026
lastupdated: "2026-02-24"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Domain settings
{: #domain-settings-cis}



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
