---

copyright:
  years: 2024
lastupdated: "2024-11-21"

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
  
1. [DDoS](/docs/cis?topic=cis-distributed-denial-of-service-ddos-attack-concepts)
1. [URL rewrites](/docs/cis?topic=cis-url-normalization)
1. [Page Rules](/docs/cis?topic=cis-about-firewall-rules)
1. [IP Firewall](/docs/cis?topic=cis-actions)
1. WAF / Firewall Rules - The general traffic sequence for CIS Firewall features is:
   1. [Firewall Rules](/docs/cis?topic=cis-about-firewall-rules)
   1. [WAF](/docs/cis?topic=cis-waf-actions)
   1. [Rate Limiting](/docs/cis?topic=cis-cis-rate-limiting) 
1. [Edge Functions](/docs/cis?topic=cis-working-with-edge-functions)
1. [Load Balancer](/docs/cis?topic=cis-configure-glb)
