---

copyright:
  years: 2018, 2025
lastupdated: "2025-06-02"

keywords: Web Application Firewall Concepts, web application firewall

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Web Application Firewall protection
{: #waf-q-and-a}

A Web Application Firewall (WAF) protects web applications by filtering and monitoring HTTP traffic between the application and the internet. As a Layer-7 defense in the [OSI model](https://en.wikipedia.org/wiki/OSI_model){: external}, it targets threats at the application layer, such as cross-site forgery, cross-site scripting (XSS), file inclusion, and SQL injection.
{: shortdesc}

Unlike a traditional proxy that handles outgoing client traffic, a WAF functions as a reverse proxy, inspecting incoming traffic before it reaches the server. This setup blocks malicious requests and shields the application from direct exposure to the internet.

WAFs operate through configurable rule sets or policies that are designed to filter out malicious traffic and protect application vulnerabilities. One major benefit of a WAF is the ability to quickly modify these policies, enabling rapid responses to emerging threats, such as applying rate limiting during a [DDoS attack](https://en.wikipedia.org/wiki/Denial-of-service_attack){: external}.

CIS WAF offers a simple way to configure and manage security rules. Key features include quick activation after you redirect your DNS to CIS and options to apply custom rules. You also get detailed reporting that provides insights into blocked threats and identifies the specific rules or rule groups involved.
