---

copyright:
  years: 2022
lastupdated: "2022-12-05"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Why is my rule not working?
{: #order-of-execution}

You have a rule that should execute, but it isn't working.
{: tsSymptoms}

The order of execution can sometimes disrupt the rules you have in place.
{: tsCauses}

Check to confirm that the rule you are expecting to execute is not getting dropped because another rule is executing before it.
{: tsResolve}

The following list shows the execution order from our partner, Cloudflare. Evaluate where your rule lands in the order of execution and adjust the rule as needed.

1. L7 DDoS mitigation
1. URL rewrites
1. Page rules
1. Origin rules
1. Cache rules
1. Configuration rules
1. Redirect rules
1. IP Firewall (Access Rules)
1. Bots
1. Web Application Firewall (including CIS Rule set, OWASP, and Custom rules)
1. Header modification
1. Cloudflare Access
1. Edge Functions
1. Load balancing
