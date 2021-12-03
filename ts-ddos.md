---

copyright:
  years: 2021
lastupdated: "2021-02-05"

keywords: 

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# What do I do if I’m under a DDoS attack?
{: #troubleshooting-cis-ddos-attack}
{: help}
{: support}

Your site is under DDoS attack.
{: tsCauses}

To help resolve a DDoS attack, take the following steps:
1. Turn on "Defense Mode" from your dashboard.
2. Set your DNS records for maximum security.
3. Do not rate-limit or throttle requests from {{site.data.keyword.cis_short_notm}}.
{: tsResolve}

During "Defense Mode", each new visitor is met with a "Captcha" security challenge, which they must pass before being given a cookie for unchallenged access. That way, botnet traffic is blocked until the "Defense Mode" is turned off. Visitors that do not meet the security challenge are added to the (bad) IP Reputation database.
