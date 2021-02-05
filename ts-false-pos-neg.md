---

copyright:
  years: 2020
lastupdated: "2020-11-13"

keywords: 

subcollection: cis

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:support: data-reuse='support'}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}
{:troubleshoot: data-hd-content-type='troubleshoot'}


# How do I troubleshoot false positives and false negatives in WAF?
{: #waf-false-pos-neg}
{: troubleshoot}

By default, the Web Application Firewall (WAF) is fully managed through the dashboard and is compatible with most websites and web applications. However, you might encounter false positives and false negatives.
{:shortdesc}

False positives happen when legitimate requests are detected and filtered as malicious. False negatives occur when malicious requests are not filtered.
{:tsCauses}

## Troubleshooting WAF false positives
{:#false-positives}

The definition of suspicious content is subjective for each website.  For example, PHP code posted to your website is suspicious unless your website teaches how to code and requires PHP code submissions from visitors.  Therefore, such a website must disable related WAF rules that interfere with normal operation.
{:tsSymptoms}

To test for false positives, set the WAF to Simulate mode, to record the response to possible attacks without challenging or blocking. Also, use the Firewall Analytics Activity log to determine which WAF rules caused false positives.

If you encounter a false positive, there are several potential resolutions:
{:tsResolve}

  - Add the client’s IP addresses to the IP Access Rules allowlist: If the browser or client visits from the same IP addresses, allowing is recommended.  
  - Disable the corresponding WAF rules. Doing so stops blocking or challenging false positives, but reduces overall site security. A request blocked by WAF Rule ID 981176 refers to OWASP rules. Decrease OWASP sensitivity to resolve the issue.
  - Bypass the WAF with a Firewall Rule: Create a Firewall Rule with the bypass action to deactivate the WAF for a specific combination of parameters. For example, bypass the WAF for a specific URL and a specific IP address or user agent.
  - Disable WAF for traffic to a URL (not recommended).  Disabling WAF using page rules lowers security on the particular URL endpoint.

If you contact IBM Support to verify whether a WAF rule triggers as expected, provide a HAR file captured while sending the specific request of concern.
{:note}

If one specific rule causes false positives, set rule’s Mode to Disable rather than turning Off the entire rule group. For false positives with the administrator content on your website, create a page rule to disable security for the admin section of your site resources, for example, `yoursite.com/admin`. 

## Troubleshooting WAF false negatives
{:#false-negatives}

To identify false negatives, review the HTTP logs on your origin web server.
{:tsResolve}

To reduce false negatives, use the following checklist:
  - Is Web Application Firewall `On` in the Firewall app under Managed Rules?
  - Is Web Application Firewall `Off` using page rules?
  - Not all WAF rules are enabled by default, so review individual WAF rule default actions.  For example, CIS allows requests with empty user agents by default. To block requests with an empty user agent, change the WAF rule Mode to `Block`.
  - Are DNS records that serve HTTP traffic proxied through CIS?
  - Does a firewall rule bypass CIS managed rules? 
  - Does an allowed country, ASN, IP range, or IP in IP access rules or firewall rules match the attack traffic?
  - Is the malicious traffic directed at your origin IP addresses to bypass CIS protection? Block all traffic except from CIS's IP addresses at your origin web server. 