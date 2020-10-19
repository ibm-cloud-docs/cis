---

copyright:
  years: 2018, 2020
lastupdated: "2020-10-19"

keywords: CIS Rule Set, WAF settings, WAF CIS Rules

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


# WAF actions and {{site.data.keyword.cis_short_notm}} rule set
{:#waf-settings}

## WAF actions
{:#waf-actions}

The following table shows the actions that Web Application Firewalls (WAFs) can take.
{: shortdesc}

|Action| Definition|
|---|---|
|**Block** | Blocking an attack stops any action before it is posted to your website.|
|**Simulate** | To test for false positives, set the WAF to **Simulate** mode, which records the response to possible attacks without challenging or blocking.|
|**Challenge** | A challenge page asks visitors to submit a CAPTCHA to continue to your website.|
|**Threshold** (or sensitivity setting) | Set rules to trigger more or less, depending on sensitivity.|

In Enterprise plans, you have the flexibility to turn on or off individual WAF rules for a particular URI in a domain, instead of the whole domain or subdomain. For more information, see the [waf-override-create](/docs/cis-cli-plugin?topic=cis-cli-plugin-cis-cli#create-waf-override) command.
{: note}

## {{site.data.keyword.cis_short_notm}} rule sets
{:#cis-ruleset-for-waf}

Select **View {{site.data.keyword.cis_short_notm}} Rules** to reveal the rule sets of this package. Rule sets are as follows:
 
   * **Drupal** - Enable this rule set only if the Drupal CMS is used for this domain. 
   * **Flash**<sup>1</sup> - Enable this rule set only if Adobe Flash content is used for this domain.  
   * **Joomla**<sup>1</sup> - Enable this rule set only if the Joomla CMS is used for this domain.  
   * **Magento**<sup>1</sup> - Enable this rule set only if the Magento CMS is used for this domain. 
   * **Miscellaneous** - Contains rules to deal with known malicious traffic, or patch flaws in specific web applications.
   * **PHP**<sup>1</sup> - Enable this rule set if PHP is used for this domain.  
   * **Plone**<sup>1</sup> - Enable this rule set only if the Plone CMS is used for this domain.  
   * **Specials** - Contains a number of rules that were created to deal with specific attack types.
   * **WHMCS**<sup>1</sup> - Enable this rule set only if WHMCS is used for this domain.  
   * **Wordpress** - Enable this rule set only if the WordPress CMS is used for this domain. 
   
<sup>1</sup> This rule set contains additional rules that complement the technology-specific protections provided by similar rules in the OWASP rule set.
  
**Specials** contains a number of rules appropriate for virtually all applications and websites on the internet. This rule set is the core of the security that our WAF offers, with rules that target common attacks like SQLi, XSS, and LFI. It is recommended that you always enable Specials.
{:tip}

Only enable the rule sets that correspond to your technology stack. For instance, if you use Wordpress, but no other technologies, enable only the Specials and Wordpress rule sets. Avoid enabling rule sets that are not relevant to your tech stack.

Select any of the specific rule sets to see further details about each of the rules included.

The {{site.data.keyword.cis_short_notm}} rule set lets you perform the following actions on each rule:

   * **Disable** turns off the rule.
   * **Simulate** logs the event, and does not block or challenge the visitor. You can still decide to set to **Block** or        
   * **Challenge** after reviewing your logs.
   * **Block** blocks the request entirely, with no option to bypass it for that request.
   * **Challenge** displays a challenge (CAPTCHA) page that must be completed before the request in question is allowed access.

You might notice that the names of the rules don't reveal exactly how they work and that they are mostly a general summary of their function. This is deliberate. For security purposes, CIS does not reveal the code (or other exact information) used to filter traffic. This prevents malicious actors from reverse engineering it to bypass our defenses.


