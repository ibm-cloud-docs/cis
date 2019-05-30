---

copyright:
  years: 2018
lastupdated: "2019-04-24"

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}

# Priority
{: #priority}

By default, the action you specify in a rule determines the evaluation sequence for your entire ruleset. To learn more, see [Actions](/docs/infrastructure/cis?topic=cis-actions).

However, a **priority** is an option that allows you to force the evaluation sequence to occur before triggering a rule.

You can manage a priority using the Firewall Rules UI in the CIS dashboard. Priority management is also available from the Firewall Rules API.

The Firewall Rules engine processes rules in parallel. If you do not specify priority in a large ruleset, a matching conflict is possible. To avoid any conflicts, it's recommended you explicitly controlling the evaluation sequence of your ruleset using a priority.
{: note}

## Prioritizing rules

Firewall Rules do not have default priorities and do not force you to have a priority for every rule. This gives you the freedom to organize your ruleset the way you want.

The numbering can be relatively arbitrary, as long as it makes sense for your particular situation. However, keep in mind the following issues:

* The evaluation sequence starts from the lowest priority number to the highest
* The valid priority range is 1 to 2147483647
* Avoid using the number 1 as a priority. Since no other rule can go above it, it makes it harder to renumber your rules
* Rules with no priorities are evaluated last

It's recommended that you group ranges of priority numbers into meaningful categories. For example:

* 5000-9999 - Trusted IP Addresses
* 10000-19999 - Blocking Rules for Bad Crawlers
* 20000-29999 - Blocking Rules for Abusive/Spam Users

The example priority numbers above are valid since you can have many more rules than the limit associated with your domain plan. That limit applies solely to active rules.
{: note}
