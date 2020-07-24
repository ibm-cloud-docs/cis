---

copyright:
  years: 2018, 2020
lastupdated: "2020-07-14"

keywords: OWASP Rule Set, Rule Set

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:term: .term}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}


# OWASP rule set
{:#owasp-rule-set-for-waf}

The OWASP rule set for WAF contains generic attack detection rules. The OWASP rules protect against many common attack categories, including SQL injection, cross-site scripting, and locale file inclusion. {{site.data.keyword.cis_full}} provides, but does not curate these rules.
{: shortdesc}

OWASP is an industry standard that provides a good security baseline. For more information, see:

  * [OWASP on Github](https://github.com/SpiderLabs/owasp-modsecurity-crs){:external}
  * [OWASP.org](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project){:external}

## Managing OWASP
{:#managing-owasp}

Unlike the [{{site.data.keyword.cis_short_notm}} rule set](/docs/cis?topic=cis-waf-settings#cis-ruleset-for-waf), OWASP allows you to set sensitivity.

A request can trigger a set of OWASP rules that have a high to low severity score associated with them. The final score is calculated based on all the rules triggered. After calculating the final score, {{site.data.keyword.cis_short_notm}} compares it to the sensitivity threshold selected in the beginning, and then either blocks, challenges, or simulates the request based on the option selected.

|Sensitivity score| Trigger threshold|
|------|---------------|
|Low   |  60 and higher|
|Medium|  40 and higher|
|High  |  25 and higher|

It is recommended that you set OWASP sensitivity to `low`. If you set it to `high`, check the logs on {{site.data.keyword.cis_short_notm}}, and fine-tune the OWASP rule set to work for your application.

Keep in mind that OWASP rules can only be toggled on or off, unlike rules in the {{site.data.keyword.cis_short_notm}} rule sets, which can be set to **Disable**, **Simulate**, **Challenge**, or **Block**.

## Dealing with false positives
{:#owasp-false-positives}

False positives can occur when a variable or value evaluates as true or positive, but it's actually a negative. In the context of our WAF, a false positive means that a request is blocked because it was mistakenly evaluated as malicious.

To deal with false positives and avoid them in the future, you must know how to spot them and correct them. Review the logs of blocked requests. Then, evaluate whether these requests were reasonably blocked within the context of the expected and normal traffic of your website.
