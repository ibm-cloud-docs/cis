---

copyright:
  years: 2018, 2025
lastupdated: "2025-05-27"

keywords: Web Application Firewall Concepts, web application firewall

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Web Application Firewall concepts
{: #waf-q-and-a}

A Web Application Firewall (WAF) protects web applications by filtering and monitoring HTTP traffic between the application and the internet. As a Layer-7 defense in the [OSI model](https://en.wikipedia.org/wiki/OSI_model){: external}, it targets threats at the application layer. 

Unlike a traditional proxy, which handles outgoing traffic from a client, a WAF functions as a reverse proxy, inspecting incoming traffic before it reaches the server. This setup helps block malicious requests and shields the application from direct exposure to the internet.

CIS WAF offers a simple way to configure and manage security rules. Key features include:

* Easy setup – Enable the WAF in minutes after redirecting your DNS to CIS and begin applying custom rules.
* Detailed reporting – View in-depth insights into blocked threats, including the specific rules or rule groups involved.

## Types of attacks WAF can prevent
{: #what-types-of-attacks-can-waf-prevent}

A WAF typically protects web applications from attacks such as cross-site forgery, cross-site-scripting (XSS), file inclusion, and SQL injection, among others. A WAF usually is part of a suite of tools, which together can create a holistic defense against a range of attack vectors.

## How a WAF works
{: #how-does-waf-work}

A WAF operates through a set of rules often called policies. These policies aim to protect against vulnerabilities in the application by filtering out malicious traffic.

The value of a WAF comes from the speed and ease with which its policy modifications can be implemented, thereby allowing a faster response to varying attack vectors. For example, during a [DDoS attack](https://en.wikipedia.org/wiki/Denial-of-service_attack){: external}, rate limiting can be implemented by modifying WAF policies. 
