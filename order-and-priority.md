---

copyright:
  years: 2018, 2025
lastupdated: "2025-02-28"

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Prioritizing options
{: #priority}

Firewall rules have been deprecated. CIS has moved existing firewall rules to WAF custom rules. For more information on this change, see [Migrating to custom rules](/docs/cis?topic=cis-migrating-to-custom-rules).
{: deprecated}

By default, the action you specify in a rule determines the evaluation sequence for your entire ruleset. However, you can set a **priority** option that allows you to force the evaluation sequence to occur before triggering a rule.
{: shortdesc}

You can manage a priority using the firewall rules UI in the {{site.data.keyword.cis_short_notm}} dashboard. Priority management is also available from the firewall rules API.

The firewall rules engine processes rules in parallel. If you do not specify priority in a large  ruleset, a matching conflict is possible. To avoid any conflicts, it is recommended that you explicitly control the evaluation sequence of your ruleset using a priority.
{: note}

Firewall rules do not have default priorities and do not force you to have a priority for every rule. This gives you the freedom to organize your ruleset the way you want. The numbering can be relatively arbitrary, as long as it makes sense for your particular situation. However, keep in mind the following issues:

* The evaluation sequence starts from the lowest priority number to the highest.
* The valid priority range is 1 to 2147483647.
* Avoid using the number 1 as a priority. Since no other rule can go above it, it makes it harder to renumber your rules.
* Rules with no priorities are evaluated last.

It is recommended that you group ranges of priority numbers into meaningful categories. For example:

* 5000-9999 - Trusted IP addresses
* 10000-19999 - Blocking rules for bad crawlers
* 20000-29999 - Blocking rules for abusive/spam users

These example priority numbers are valid since you can have many more rules than the limit associated with your domain plan. That limit applies solely to active rules.
{: note}
