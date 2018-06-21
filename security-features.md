---
copyright:
  years: 2018
lastupdated: "2018-06-21"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# How IBM Cloud Internet Services (CIS) keeps your work secure

IBM CIS is a globally distributed cloud service that blocks threats and limits abusive bots and crawlers, which can waste your bandwidth and server resources. IBM CIS works as a global HTTP(S) reverse proxy and a managed DNS service provider. Your web traffic is routed through our intelligent global network to optimize both your performance and your security.

![security-graphic.png](images/security-graphic.png)

Here’s a quick feature overview:

## Security features
 * Proxy [DNS records](dns-concepts.md#proxying-dns-records) or [GLB](glb.md) to use security features. This allows traffic to flow through our servers and the data can be monitored.
### Web Application Firewall (WAF)
 * WAF is implemented through two rule sets: [OWASP](waf-owasp-rule set.md) and [CIS](waf-cis-rule set.md).
### Unlimited DDoS mitigation
 * DDoS mitigation is typically an expensive service that can grow in cost when under attack. We include unlimited DDoS mitigation with CIS at no additonal cost.

## Security Standards and platform

 * TLS (SHA2 and SHA1)
 * IPv6
 * HTTP/2 and SPDY

## DNS

 * Global anycast network
 * DNSSEC

## Network attacks and mitigation

Generally, we see attacks that fall into two categories

| Layer 3 or Layer 4 attacks | Layer 7 attacks |
|------------------------------|-----------------|
|These attacks consist of a flood of traffic at ISO Layer 3 (the network layer), such as ICMP floods) or at Layer 4 (the transport layer), such as TCP SYN floods or reflected UDP floods) |These are attacks that send malicious ISO Layer 7 requests (the application layer), such as GET floods.  |
| Automatically blocked at our edge | We handle these with “Defense Mode,” WAF, and Security level settings |

## Summary

 * Defense Mode tests browser features that many malicious clients lack
 * The WAF blocks or challenges known request patterns that are likely to be malicious
