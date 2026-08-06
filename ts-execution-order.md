---

copyright:
  years: 2024, 2026
lastupdated: "2026-08-06"

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

Refer to [Traffic sequencing](/docs/cis?topic=cis-traffic-sequencing) to see the execution order. This list helps you identify where your rule lands within the execution sequence, so you can make any necessary adjustments.
