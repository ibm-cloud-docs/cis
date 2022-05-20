---

copyright:
  years: 2018, 2022
lastupdated: "2022-04-12"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# WAF actions and rule sets
{: #waf-settings}

## WAF actions
{: #waf-actions}

The following table shows the actions that Web Application Firewalls (WAFs) can take.
{: shortdesc}

|Action| Definition|
|---|---|
|**Block** | Blocking an attack stops any action before it is posted to your website.|
|**Simulate** | To test for false positives, set the WAF to **Simulate** mode, which records the response to possible attacks without challenging or blocking.|
|**Challenge** | A challenge page asks visitors to submit a CAPTCHA to continue to your website.|
|**Threshold** (or sensitivity setting) | Set rules to trigger more or less, depending on sensitivity.|
{: caption="Table 1. WAF actions" caption-side="bottom"}

In Enterprise plans, you have the flexibility to turn on or off individual WAF rules for a particular URI in a domain, instead of the whole domain or subdomain. For more information, see the [waf-override-create](/docs/cis-cli-plugin?topic=cis-cli-plugin-cis-cli#create-waf-override) command.
{: note}

## {{site.data.keyword.cis_short_notm}} rule sets
{: #cis-ruleset-for-waf}

Select **View {{site.data.keyword.cis_short_notm}} Rules** to reveal the rule sets of this package. Rule sets are as follows:

* **Drupal** - Enable this rule set only if the Drupal CMS is used for this domain. 
* **Flash**[^A] - Enable this rule set only if Adobe Flash content is used for this domain.  
* **Joomla**[^B] - Enable this rule set only if the Joomla CMS is used for this domain.  
* **Magento**[^C] - Enable this rule set only if the Magento CMS is used for this domain. 
* **Miscellaneous** - Contains rules to deal with known malicious traffic, or patch flaws in specific web applications.
* **PHP**[^D] - Enable this rule set if PHP is used for this domain.  
* **Plone**[^E] - Enable this rule set only if the Plone CMS is used for this domain.  
* **Specials** - Contains a number of rules that were created to deal with specific attack types.
* **WHMCS**[^F] - Enable this rule set only if WHMCS is used for this domain.  
* **Wordpress** - Enable this rule set only if the WordPress CMS is used for this domain. 

[^A]: This rule set contains additional rules that complement the technology-specific protections provided by similar rules in the OWASP rule set.

[^B]: This rule set contains additional rules that complement the technology-specific protections provided by similar rules in the OWASP rule set.

[^C]: This rule set contains additional rules that complement the technology-specific protections provided by similar rules in the OWASP rule set.

[^D]: This rule set contains additional rules that complement the technology-specific protections provided by similar rules in the OWASP rule set.

[^E]: This rule set contains additional rules that complement the technology-specific protections provided by similar rules in the OWASP rule set.

[^F]: This rule set contains additional rules that complement the technology-specific protections provided by similar rules in the OWASP rule set.

**Specials** contains a number of rules appropriate for virtually all applications and websites on the internet. This rule set is the core of the security that our WAF offers, with rules that target common attacks like SQLi, XSS, and LFI. It is recommended that you always enable Specials.
{: tip}

Only enable the rule sets that correspond to your technology stack. For instance, if you use Wordpress, but no other technologies, enable only the Specials and Wordpress rule sets. Avoid enabling rule sets that are not relevant to your tech stack.

Select any of the specific rule sets to see further details about each of the rules included.

The {{site.data.keyword.cis_short_notm}} rule set lets you perform the following actions on each rule:

* **Disable** turns off the rule.
* **Simulate** logs the event, and does not block or challenge the visitor. You can still decide to set to **Block** or  **Challenge** after reviewing your logs.
* **Block** blocks the request entirely, with no option to bypass it for that request.
* **Challenge** displays a challenge (CAPTCHA) page that must be completed before the request in question is allowed access.

You might notice that the names of the rules don't reveal exactly how they work and that they are mostly a general summary of their function. This is deliberate. For security purposes, CIS does not reveal the code (or other exact information) used to filter traffic. This prevents malicious actors from reverse engineering it to bypass our defenses.

## OWASP rule set
{: #owasp-rule-set-for-waf}

The OWASP rule set for WAF contains generic attack detection rules. The OWASP rules protect against many common attack categories, including SQL injection, cross-site scripting, and local file inclusion. {{site.data.keyword.cis_short_notm}} provides, but does not curate these rules.

OWASP is an industry standard that provides a good security baseline. For more information, see:

* [OWASP on Github](https://github.com/SpiderLabs/owasp-modsecurity-crs){: external}
* [OWASP.org](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project){: external}

### Managing OWASP
{: #managing-owasp}

Unlike the [{{site.data.keyword.cis_short_notm}} rule set](#cis-ruleset-for-waf), OWASP allows you to set sensitivity.

A request can trigger a set of OWASP rules that have a high to low severity score associated with them. The final score is calculated based on all the rules triggered. After calculating the final score, {{site.data.keyword.cis_short_notm}} compares it to the sensitivity threshold selected in the beginning, and then either blocks, challenges, or simulates the request based on the option selected.

It is recommended that you set OWASP sensitivity to `low` initially, then review for false positives before increasing the sensitivity. If you set it to `high`, check the logs on {{site.data.keyword.cis_short_notm}}, and fine-tune the OWASP rule set to work for your application.

Keep in mind that OWASP rules can only be toggled on or off, unlike rules in the {{site.data.keyword.cis_short_notm}} rule sets, which can be set to **Disable**, **Simulate**, **Challenge**, or **Block**.

### Understanding the OWASP package
{: #understanding-owasp-package}

The OWASP ModSecurity Core Rule Set assigns a score to each request based on how many OWASP rules trigger. Some OWASP rules have a higher sensitivity score than others. After OWASP evaluates a request, {{site.data.keyword.cis_short_notm}} compares the final score to the Sensitivity configured for the domain.  If the score exceeds the Sensitivity, the request is actioned based on the Action configured within Package: 

The sensitivity score required to trigger the WAF for a specific Sensitivity is as follows:

|Sensitivity score|Trigger threshold|
|---|---|
|**Low**   |  60 and higher|
|**Medium**|  40 and higher|
|**High**  |  25 and higher|
{: caption="Table 2. Sensitivity and triggers" caption-side="bottom"}

The OWASP ModSecurity Core rule set takes the following actions:

|Action| Definition|
|---|---|
|**Block**|The request is discarded.|
|**Challenge**|The visitor receives a CAPTCHA challenge page.|
|**Simulate**|The request is allowed through but is logged in the Events log.|
{: caption="Table 3. OWASP ModSecurity Core Rule Set" caption-side="bottom"}

For Ajax requests, the following scores are applied instead:

|Sensitivity score|Trigger threshold|
|---|---|
|**Low**   | 120 and higher|
|**Medium**|  80 and higher|
|**High**  |  65 and higher|
{: caption="Table 4. Ajax request sensitivity and triggers" caption-side="bottom"}

Review the (Security) Events log to see the final score as well as the individual triggered rules.

### Managing OWASP packages
{: #manage-owasp-package}

The OWASP ModSecurity Core Rule Set contains several rules from the OWASP project. {{site.data.keyword.cis_short_notm}} does not write or curate OWASP rules. Click on a ruleset name under Group to reveal the rule descriptions. Unlike the {{site.data.keyword.cis_short_notm}} Managed Ruleset, specific OWASP rules are either turned On or Off.

To manage OWASP thresholds, set the Sensitivity to `Low`, `Medium`, or `High` in the **Package: OWASP ModSecurity Core Rule Set** section. Setting the Sensitivity to `Off` disables the entire OWASP package, including all its rules. Determining the appropriate Sensitivity depends on your business industry and operations. For instance, a Low setting is appropriate for large file uploads.

With a High Sensitivity, large file uploads trigger the WAF.
{: tip}

The Activity log displays Rule ID 981176 when a request is blocked by OWASP. Also, some OWASP rules listed in the Activity log do not appear in the list of rules under Package: OWASP ModSecurity Core Rule Set because disabling those rules is not recommended.
{: important}
