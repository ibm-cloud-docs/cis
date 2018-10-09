---

copyright:
  years: 2018
lastupdated: "2018-06-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# WAF settings
|Action| Definition|
|---|---|
Block | Blocking an attack will stop any action before it is posted to your website.
Simulate | To test for false positives, set the WAF to Simulate mode, which records the response to possible attacks without challenging or blocking.
Challenge | A challenge page asks visitors to submit a CAPTCHA to continue to your website.
Threshold or sensitivity setting | Set rules to trigger more or less, depending on sensitivity.

# CIS Rule Set for WAF

Select **View CIS Rules** to reveal the rule sets of this package. The rule sets follow:
  * Drupal
  * Flash
  * Joomla
  * Magento
  * Miscellaneous
  * PHP
  * Plone
  * Specials
  * WHMCS
  * Wordpress

**Specials** contains a number of rules appropriate for virtually all applications and websites on the internet. This rule set is the core of the security that our WAF offers, with rules that target common attacks like SQLi, XSS, and LFI. We recommend that you always leave Specials enabled.

Only enable the rule sets that correspond to your technology stack. For instance, if you use Wordpress but none of the other technologies, enable only the Specials and Wordpress rule sets. Avoid enabling rule sets that are not relevant to your tech stack.

Select any of the specific Rule Sets to see further details about each of the rules included.

CIS Rule set lets you perform four actions on each rule:
  1. **Disable**: Turns the rule off.
  2. **Simulate**: Logs the event and does not block or challenge the visitor (you can still decide to set to a block or challenge after reviewing your logs).
  3. **Block**: Block simply blocks the request entirely, with no option to bypass it for that request.
  4. **Challenge**: Displays a challenge (CAPTCHA) page that must be completed before the request in question is allowed access.

You may notice that the names of the rules don't reveal exactly how they work and that they are mostly a general summary of their function. This is deliberate.  For security purposes, we don't reveal the code (or other exact information) we use to filter traffic. This prevents malicious actors from reverse engineering it to bypass our defenses.
