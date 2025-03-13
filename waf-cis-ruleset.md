---

copyright:
  years: 2018, 2025
lastupdated: "2025-03-13"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# WAF ruleset actions
{: #waf-actions}

CIS WAF capabilities are moving to the [Ruleset Engine rules language](/docs/cis?topic=cis-cis-ruleset-engine). For more information on this change, see [Migrating to managed rules](/docs/cis?topic=cis-migrating-to-managed-rules).
{: note}
 
The following table shows the actions that Web Application Firewalls (WAFs) can take.
{: shortdesc}

|Action|rulesets|Definition|
|---|---|----|
|**Block** | All | Blocks an attack stops any action before it is posted to your website.| 
|**Log** | All | To test for false positives, set the WAF to **Log** mode, which records the response to possible attacks without challenging or blocking.|
|**Challenge** | All |* Manged challenge: Dynamically chooses the appropriate type of challenge based on the characteristics of the request. \n * Interactive challenge: Solve a puzzle to proceed. \n * JavaScript challenge: A challenge page asks visitors to submit a CAPTCHA to continue to your website. |
{: caption="WAF actions" caption-side="bottom"}

In Enterprise plans, you have the flexibility to turn on or off individual WAF rules for a particular URI in a domain, instead of the whole domain or subdomain. For more information, see the [waf-override-create](/docs/cis?topic=cis-cis-cli) command.
{: note}
