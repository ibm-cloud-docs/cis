---
copyright:
  years: 2018
lastupdated: "2018-03-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Web Application Firewall Concepts Q & A

The web application firewall protects against ISO Layer 7 attacks, which can be some of the most tricky. This document gives some details.

## What is a Web Application Firewall (WAF)?
A WAF or Web Application Firewall helps protect web applications by filtering and monitoring HTTP traffic between a web application and the Internet. A WAF is an ISO protocol layer-7 defense (in the [OSI model ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/OSI_model)), It is not designed to defend against all types of attacks. 

Deploying a WAF in front of a web application is like placing a shield between the web application and the internet. A proxy server protects a client machine’s identity by using an intermediary (for outgoing traffic), but a WAF is a type of reverse-proxy that protects the server from exposure by having the client's traffic pass through the WAF before reaching the server (for incoming traffic).

## What types of attacks can a WAF prevent?
A WAF typically protects web applications from attacks such as cross-site forgery, cross-site-scripting (XSS), file inclusion, and SQL injection, among others. A WAF usually is part of a suite of tools, which together can create a holistic defense against a range of attack vectors.

## How does a WAF work?

A WAF operates through a set of rules often called policies. These policies aim to protect against vulnerabilities in the application by filtering out malicious traffic. 

The value of a WAF comes from the speed and ease with which its policy modifications can be implemented, thereby allowing a faster response to varying attack vectors. For example, during a [DDoS attack ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/Denial-of-service_attack), rate limiting can be implemented by modifying WAF policies.
