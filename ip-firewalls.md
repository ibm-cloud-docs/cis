---

copyright:
  years: 2018, 2026
lastupdated: "2026-02-09"
 
keywords: ip firewall, ip rules, user agent blocking, domain lockdown 

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# IP firewalls
{: #cis-ip-firewall} 
 
Legacy IP firewall rules are still supported, but custom rules provide greater flexibility and control. You can accomplish 99.99% or more of IP rule use cases using custom rules, along with advanced features like rule sequencing, custom responses, and detailed logging. For new configurations, it is recommended to use [custom rules](/docs/cis?topic=cis-custom-rules-overview) whenever possible.yes,
{: attention}

**Warning:** Since these legacy rules are evaluated earlier in the traffic sequence, allowing an IP, ASN, or country will bypass any configured WAF, custom, or rate limiting rules. 

{{site.data.keyword.cis_full_notm}} provides multiple mechanisms to control traffic, helping protect your domains, URLs, and directories from excessive requests, specific requesters, and targeted IP addresses.

## IP rules
{: #cis-ip-rules}

With IP rules you can control access for specific IP addresses, IP ranges, specific countries, specific ASNs, and certain CIDR blocks. Available actions on incoming requests are:

* Allow
* Block
* Challenge (Captcha)
* JavaScript challenge (Defense mode)

For example, if you notice that a particular IP is causing malicious requests, you can block that user by IP address.

IP rules operate at OSI Layer 3 and Layer 4, allowing you to control access for TCP, HTTP, and HTTPS traffic across individual IP addresses, ranges, countries, ASNs, or CIDR blocks. 
{: note}

## Domain lockdown
{: #cis-domain-lockdown}

Domain lockdown allows you to restrict access to specific subdomains or URL paths by allowlisting certain IP addresses or IP ranges. Any requests from IPs not on the allowlist are automatically blocked and receive an **Access Denied** response.

This capability is useful when you need more granular control than standard IP firewall rules, which apply to all subdomains of a domain or across all domains in your account. Domain lockdown lets you define restrictions at the subdomain or even URL path level.

Domain lockdown supports the following use cases:

* Specific subdomains - Restrict access to individual subdomains for specific IP addresses. For example, you can allow IP `1.2.3.4` access to the domain `foo.example.com` and allow IP `5.6.7.8` access to domain `bar.example.com`, without allowing access in the reverse direction.
* Specific URLs - Restrict access to specific URL paths. For example, you can allow IP `1.2.3.4` access to directory `example.com/foo/*` and allow IP `5.6.7.8` access to directory `example.com/bar/*`, but not allow the reverse.
 
All CIS plans have access to Domain Lockdown. The number of rules varies depending on Standard versus Enterprise plans.
{: note}  

You can configure multiple allowlisted IP addresses (both IPv4 and IPv6) and apply them to multiple targets. For example:

```bash
staging.example.com/*
example.com/wiki/*
```
{: pre}
 
```sh 
192.0.2.0/24
2001:db8::/64
203.0.113.5
```
{: pre}

Only requests from the specified IPs are allowed to access the listed URLs. All others are blocked.

You can also assign a priority to each domain lockdown rule to determine how overlapping rules are handled. Lower numbers indicate higher priority.
 
## User-agent blocking rules
{: #user-agent-blocking-rules}

With user-agent blocking rules, you can act on any `user-agent` string you select. This capability works like domain lockdown, except that the rule examines the incoming `user-agent` header instead of the IP address. You can choose how to handle a matching request with the same list of actions that you established in the IP rules (`block`, `challenge`, and `JS challenge`). 

User-agent blocking applies to your entire zone. You can't specify subdomains or URL paths in the same manner as you can with a domain lockdown.

This tool is useful for blocking any user-agent strings that you deem suspicious.
 
Matching is performed by using substring matching. You can match a full `user-agent` string or any portion of it. For example, entering `curl` or `Python-urllib` block those user agents.
{: note} 
