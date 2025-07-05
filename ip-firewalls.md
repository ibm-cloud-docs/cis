---

copyright:
  years: 2018, 2025
lastupdated: "2025-07-05"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}


# IP firewalls
{: #cis-ip-firewall} 

Legacy IP firewall rules are still supported, but custom rules offer significantly more flexibility and control. You can accomplish 99.99% or more of IP rule use cases using custom rules, along with advanced features like rule sequencing, custom responses, and detailed logging. For new configurations, it is recommended to use custom rules whenever possible.
{: attention}

{{site.data.keyword.cis_full_notm}} offers several tools for controlling your traffic so that you protect your domains, URLs, and directories against volumes of traffic, certain groups of requesters, and particular requesting IPs.

## IP rules
{: #cis-ip-rules}

With IP rules you can control access for specific IP addresses, IP ranges, specific countries, specific ASNs, and certain CIDR blocks. Available actions on incoming requests are:
* Allowlist
* Block
* Challenge (Captcha)
* JavaScript challenge (Defense mode)

For example, if you notice that a particular IP is causing malicious requests, you can block that user by IP address.

IP rules apply to TCP, HTTP, and HTTPS [Range](/docs/cis?topic=cis-cis-range) apps, because IP rules are applied to Open System Interconnection (OSI) Layer 3 and Layer 4.
{: note}

## User-agent blocking rules
{: #user-agent-blocking-rules}

With user-agent blocking rules, you can act on any user-agent string you select. This capability works like domain lockdown, except that the block examines the incoming user-agent string instead of the IP. You can choose how to handle a matching request with the same list of actions that you established in the IP rules (block, challenge, and JS challenge). User-agent blocking applies to your entire zone. You can't specify subdomains in the same manner as you can with a domain lockdown.

This tool is useful for blocking any user-agent strings that you deem suspicious.

## Domain lockdown
{: #cis-domain-lockdown}

By using Domain lockdown, you can allowlist specific IP addresses and IP ranges, such that all other IPs are blocklisted. Domain lockdown supports the following items.

* Specific subdomains - For example, you can allow IP `1.2.3.4` access to the domain `foo.example.com` and allow IP `5.6.7.8` access to domain `bar.example.com`, without allowing the reverse.
* Specific URLs - For example, you can allow IP `1.2.3.4` access to directory `example.com/foo/*` and allow IP `5.6.7.8` access to directory `example.com/bar/*`, but not allow the reverse.

This capability is useful when you need more granularity in your access rules because, with IP rules, you can either apply the block to all subdomains of the current domain, or all domains on your account. You can't specify URIs.
