---

copyright:
  years: 2018, 2026
lastupdated: "2026-02-06"

keywords: ddos, distributed denial of service, Attack Concepts, Application layer attacks 
subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# About DDoS protection in CIS
{: #about-ddos}

CIS provides DDoS protection through DNS ingestion, traffic inspection, unlimited mitigation, and integrated Layer‑7 security features.
{: shortdesc} 

## How CIS ingests and protects traffic
{: #cis-on-demand-anti-ddos}
 
{{site.data.keyword.cis_full_notm}} ingests traffic by returning a {{site.data.keyword.cis_short_notm}} IP address on the DNS lookup for a domain, instead of the actual record for the origin server’s IP address. This allows CIS to ingest, single‑pass inspect, and re‑encrypt data before sending it to the origin server destination.

{{site.data.keyword.cis_short_notm}} can also act in DNS-only mode, returning the actual DNS record without obfuscating the IP, which disables DDoS and the other functions of {{site.data.keyword.cis_short_notm}}. To enable {{site.data.keyword.cis_short_notm}} protections, switch the "proxy" slider next to each DNS record to **on**; to disable protections, switch to **off**.

## Unlimited DDoS mitigation
{: #cis-unlimited-ddos-mitigation}
 
DDoS mitigation is typically an expensive service that can grow in cost when under attack. Unlimited DDoS mitigation is included with {{site.data.keyword.cis_short_notm}} at no additional cost.

## Layer‑7 mitigation options available in CIS
{: #cis-mitigate-layer7-attacks} 

Though DDoS is enabled by default in {{site.data.keyword.cis_short_notm}}, you can further configure Layer 7 security by:

* Configuring WAF ruleset sensitivity and response behavior
* Adding rate limiting
* Adding firewall rules

Use these features to customize Layer 7 mitigation of both volumetric and non-volumetric attacks.

## Mitigating non-volumetric attacks
{: #cis-mitigate-non-volumetric-attacks}
 
{{site.data.keyword.cis_short_notm}} WAF contains rulesets to mitigate non-volumetric attacks, including cross-site forgery, cross-site-scripting (XSS), file inclusion, and SQL injection. For additional information about WAF, see [Web Application Firewall concepts](/docs/cis?topic=cis-waf-q-and-a).

## Related links
{: #about-ddos-related-links}
 
* [DDoS attack concepts](/docs/cis?topic=cis-ddos-attack-concepts)
* [Preventing DDoS attacks](/docs/cis?topic=cis-preventing-ddos-attacks)
* [Responding to DDoS attacks](/docs/cis?topic=cis-responding-to-ddos-attacks)
* [Using Defense mode for DDoS attacks](/docs/cis?topic=cis-defense-mode-attack-ddos)
* [Third-party services and DDoS protection](/docs/cis?topic=cis-third-party-ddos)
* [HTTP DDoS Attack Protection managed ruleset](/docs/cis?topic=cis-http-ddos)
