---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-26"

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


# OWASP Rule Set for WAF
{:#owasp-rule-set-for-waf}

The OWASP Rule Set contains generic attack detection rules. The OWASP rules protect against many common attack categories, including SQL Injection, Cross-Site Scripting, and Locale File Inclusion, among others. {{site.data.keyword.cis_full}} provides but does not curate these rules.
{: shortdesc}

OWASP is an industry standard that provides a good security baseline. See the following links for more information:
  * [OWASP on Github](https://github.com/SpiderLabs/owasp-modsecurity-crs)
  * [OWASP.org](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project)

## Managing OWASP
{:#managing-owasp}

Unlike the [{{site.data.keyword.cis_short_notm}} rule set](/docs/cis?topic=cis-waf-settings#cis-ruleset-for-waf), OWASP allows you to set Sensitivity.
A request may trigger a set of OWASP rules that have a high to low severity score associated with them. The final score is calculated based on all the rules triggered. After calculating the final score, {{site.data.keyword.cis_short_notm}} compares it to the sensitivity threshold selected in the beginning, and then either blocks or allows the request.

|Sensitivity score| Trigger threshold|
|------|---------------|
|Low   |  60 and higher|
|Medium|  40 and higher|
|High  |  25 and higher|

We suggest that you set OWASP sensitivity to `low`. If you set it to `high`, check the logs on {{site.data.keyword.cis_short_notm}}, and fine-tune the OWASP rule set to work for your application.

Keep in mind that OWASP rules can only be toggled _on_ or _off_, unlike rules in the {{site.data.keyword.cis_short_notm}} rule sets, which can be set to _Disable_, _Simulate_, _Challenge_, or _Block_.

## How to deal with False Positives?
{:#owasp-false-positives}

False positives can occur when variable or value evaluates as _true_ or _positive_ but it's actually a negative. In the context of our WAF, a false positive means that a request is blocked because it was mistakenly evaluated as malicious.

To deal with false positives and make sure to avoid them in the future, you must know how to spot them and correct them. Review the logs of blocked requests, and then evaluate whether these requests were reasonably blocked within the context of the expected and normal traffic of your website.
