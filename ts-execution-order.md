---

copyright:
  years: 2024
lastupdated: "2024-02-22"

keywords:

subcollection: cis

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why is my rule not working?
{: #order-of-execution}
{: troubleshoot}

You have a rule that should execute, but it isn't working.
{: tsSymptoms}

The order of execution can sometimes disrupt the rules you have in place.
{: tsCauses}

Check to confirm that the rule you are expecting to execute is not getting dropped because another rule is executing before it.
{: tsResolve}

The following list shows the execution order from our partner, Cloudflare. Evaluate where your rule lands in the order of execution and adjust the rule as needed.

1. DDoS
1. URL Rewrites
1. Page Rules
1. IP Firewall
1. WAF / Firewall Rules
1. Edge Functions
1. Load Balancer
