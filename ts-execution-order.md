---

copyright:
  years: 2022
lastupdated: "2022-08-16"

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

The following list shows the execution order from Cloudflare.

1. Edge Side Code (ESC)
2. IP Firewall (Access Rules)
3. Page Rules
4. Browser Integrity Check (BIC)
5. IP Reputation
6. L7 DDoS mitigation
7. Firewall Rules (including User Agent, Filter-Based, and Zone 8. Lockdown rules)
9. Rate Limiting
10. Cloudflare Access
11. Web Application Firewall (including CIS Rule set, OWASP, and Custom rules)
12. Edge Functions
