---

copyright:
  years: 2018, 2020
lastupdated: "2020-03-10"

keywords: Web Application Firewall Concepts, web application firewall

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:term: .term}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Web Application Firewall concepts
{:#waf-q-and-a}

The web application firewall protects against ISO Layer 7 attacks, which can be some of the most tricky. This document gives some details.
{: shortdesc}

## What is a Web Application Firewall (WAF)?
{:#what-is-a-waf}

A WAF or Web Application Firewall helps protect web applications by filtering and monitoring HTTP traffic between a web application and the Internet. A WAF is an OSI protocol layer-7 defense (in the [OSI model ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/OSI_model)), It is not designed to defend against all types of attacks.

Deploying a WAF in front of a web application is like placing a shield between the web application and the internet. A proxy server protects a client machine’s identity by using an intermediary (for outgoing traffic), but a WAF is a type of reverse-proxy that protects the server from exposure by having the client's traffic pass through the WAF before reaching the server (for incoming traffic).

## What types of attacks can a WAF prevent?
{:#what-types-of-attacks-can-waf-prevent}

A WAF typically protects web applications from attacks such as cross-site forgery, cross-site-scripting (XSS), file inclusion, and SQL injection, among others. A WAF usually is part of a suite of tools, which together can create a holistic defense against a range of attack vectors.

## How does a WAF work?
{:#how-does-waf-work}

A WAF operates through a set of rules often called policies. These policies aim to protect against vulnerabilities in the application by filtering out malicious traffic.

The value of a WAF comes from the speed and ease with which its policy modifications can be implemented, thereby allowing a faster response to varying attack vectors. For example, during a [DDoS attack ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/Denial-of-service_attack), rate limiting can be implemented by modifying WAF policies.

## What are the key benefits of the IBM {{site.data.keyword.cis_short}} Web Application Firewall?
{:#key-benefits-of-cis-waf}

The {{site.data.keyword.cis_full}} WAF is an easy way to set up, manage, and customize security rules to protect your web applications from common web threats. See the following list for key features:

 * **Easy setup**: The {{site.data.keyword.cis_short_notm}} WAF is part of our overall service, which takes just a few minutes to set up. Once you redirect your DNS to us, you can switch on the WAF and set up the rules you need.

 * **Detailed reporting** See greater detail in the reporting, for example, threats blocked by rule/rule group.
