---

copyright:
  years: 2024, 2025
lastupdated: "2025-03-06"

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

Refer to [Traffic sequencing](/docs/cis?topic=cis-traffic-sequencing) to see the execution order from our partner, Cloudflare. This list will help you identify where your rule lands within the execution sequence, allowing you to make any necessary adjustments. 
