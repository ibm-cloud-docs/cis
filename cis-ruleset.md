---

copyright:
  years: 2024, 2025
lastupdated: "2025-02-20"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.cis_short_notm}} rulesets
{: #cis-rule-sets}

Select **View {{site.data.keyword.cis_short_notm}} rules** to reveal the rulesets of this package. rulesets are as follows:

* **Drupal** - Enable this ruleset only if the Drupal CMS is used for this domain.
* **Flash**[^A] - Enable this ruleset only if Adobe Flash content is used for this domain.
* **Joomla**[^B] - Enable this ruleset only if the Joomla CMS is used for this domain.
* **Magento**[^C] - Enable this ruleset only if the Magento CMS is used for this domain.
* **Miscellaneous** - Contains rules to deal with known malicious traffic, or fix flaws in specific web applications.
* **PHP**[^D] - Enable this ruleset if PHP is used for this domain.
* **Plone**[^E] - Enable this ruleset only if the Plone CMS is used for this domain.
* **Specials** - Contains a number of rules that were created to deal with specific attack types.
* **WHMCS**[^F] - Enable this ruleset only if WHMCS is used for this domain.
* **Wordpress** - Enable this ruleset only if the WordPress CMS is used for this domain.

[^A]: This ruleset contains more rules that complement the technology-specific protections provided by similar rules in the OWASP ruleset.

[^B]: This ruleset contains more rules that complement the technology-specific protections provided by similar rules in the OWASP ruleset.

[^C]: This ruleset contains more rules that complement the technology-specific protections provided by similar rules in the OWASP ruleset.

[^D]: This ruleset contains more rules that complement the technology-specific protections provided by similar rules in the OWASP ruleset.

[^E]: This ruleset contains more rules that complement the technology-specific protections provided by similar rules in the OWASP ruleset.

[^F]: This ruleset contains more rules that complement the technology-specific protections provided by similar rules in the OWASP ruleset.

The **Specials** ruleset contains a number of rules appropriate for virtually all applications and websites on the internet. This ruleset is the core of the security that our WAF offers, with rules that target common attacks like SQLi, XSS, and LFI. It is recommended that you always enable Specials.
{: tip}

Enable only the rulesets that correspond to your technology stack. For instance, if you use Wordpress, but no other technologies, enable only the Specials and Wordpress rulesets. Avoid enabling rulesets that are not relevant to your tech stack.

Select any of the specific rulesets to see further details about each of the rules included.

Use the {{site.data.keyword.cis_short_notm}} ruleset to perform the following actions on each rule:

* **Disable** turns off the rule.
* **Log** logs the event and does not block or challenge the visitor. You can still decide to set to **Block** or **Challenge** after you review the logs.
* **Block** blocks the request entirely, with no option to bypass it for that request.
* **Challenge** displays a challenge (CAPTCHA) page that must be completed before the request in question is allowed access.

You might notice that the names of the rules don't reveal exactly how they work and that they are mostly a general summary of their function. This is deliberate. For security purposes, CIS does not reveal the code (or other exact information) used to filter traffic. Doing so prevents malicious actors from reverse-engineering it to bypass our defenses.
