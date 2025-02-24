---

copyright:
  years: 2024, 2025
lastupdated: "2025-02-24"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# OWASP ruleset
{: #owasp-rule-set-for-waf}

The OWASP core ruleset for WAF contains generic attack detection rules. The OWASP rules protect against many common attack categories, including SQL injection, cross-site scripting, and local file inclusion. {{site.data.keyword.cis_short_notm}} provides, but does not curate these rules.

OWASP is an industry standard that provides a good security baseline. For more information, see:

* [OWASP on GitHub](https://github.com/coreruleset/coreruleset){: external}
* [OWASP.org](https://owasp.org/www-project-modsecurity-core-rule-set/){: external}
* [OWASP Core Ruleset Documentation](https://coreruleset.org/docs/){: external}
* [OWASP Core Ruleset Changelog](https://github.com/coreruleset/coreruleset/blob/main/CHANGES.md){: external}

## Managing OWASP
{: #managing-owasp}

Depending on your WAF handling in CIS, you might be on a different version of OWASP. The OWASP v2.x uses sensitivity thresholds, and OWASP v3.x uses paranoia levels. Zones created on or after 8 May 2024 will use OWASP v3.x. Zones created before that date use OWASP v2.x and will be migrated by 14 February 2025, unless you manually migrate earlier.

## Understanding the OWASP package
{: #understanding-owasp-package}

The OWASP ModSecurity Core Ruleset assigns a score to each request based on how many OWASP rules trigger.

### OWASP v3.x
{: #owasp-v3x}

The paranoia level settings are part of the core ruleset. The paranoia level (PL) helps to define how aggressive the core ruleset is.

|Paranoia level|Description|
|:---:|---|
|**PL 1** | Provides a set of rules that rarely trigger a false alarm, though false alarms can happen depending on the local setup.|
|**PL 2** | Provides additional rules that detect more attacks, but the additional rules might also trigger new false alarms over legitimate HTTP requests.|
|**PL 3** | Provides more rules for certain specialized attacks. The risk of false alarms increases.|
|**PL 4** | Provides rules that are so aggressive they detect almost every possible attack. This paranoia level flags a lot of legitimate traffic as malicious.|
{: caption="Paranoia levels" caption-side="bottom"}

### OWASP v2.x
{: #owasp-v2x}

A request can trigger a set of OWASP rules that have a high to low severity score associated with them. The final score is calculated based on all the rules triggered. After calculating the final score, {{site.data.keyword.cis_short_notm}} compares it to the sensitivity threshold selected in the beginning, and then either blocks, challenges, or logs the request based on the option selected.

It is recommended that you set OWASP sensitivity to `low` initially, then review for false positives before increasing the sensitivity. If you set it to `high`, check the logs on {{site.data.keyword.cis_short_notm}}, and fine-tune the OWASP ruleset to work for your application.

Keep in mind that you can only toggle OWASP rules on or off, unlike rules in the {{site.data.keyword.cis_short_notm}} rulesets, which can be set to **Disable**, **Simulate**, **Challenge**, or **Block**.

The sensitivity score required to trigger the WAF for a specific sensitivity is as follows:

|Sensitivity score|Trigger threshold|
|---|---|
|**Low**   |  60 and higher|
|**Medium**|  40 and higher|
|**High**  |  25 and higher|
{: caption="Sensitivity and triggers" caption-side="bottom"}

With a high sensitivity, large file uploads trigger the WAF. (2.x only)
{: tip}

For Ajax requests, the following scores are applied instead:

|Sensitivity score|Trigger threshold|
|---|---|
|**Low**   | 120 and higher|
|**Medium**|  80 and higher|
|**High**  |  65 and higher|
{: caption="Ajax request sensitivity and triggers" caption-side="bottom"}

Review the (security) events log to see the final score, as well as the individual triggered rules.

## Managing OWASP packages
{: #manage-owasp-package}

The OWASP ModSecurity Core Ruleset contains several rules from the OWASP project. {{site.data.keyword.cis_short_notm}} does not write or curate OWASP rules. Click on a ruleset name under **Group** to reveal the rule descriptions. Unlike the {{site.data.keyword.cis_short_notm}} managed  ruleset, specific OWASP rules are either turned on or off.

To manage OWASP thresholds, set the paranoia level in the **Package: OWASP ModSecurity Core Ruleset** section. Setting the paranoia level to `P1` disables the entire OWASP package, including all its rules. Determining the appropriate paranoia level depends on your business industry and operations. For instance, a P1 setting is appropriate for large file uploads.

The activity log displays rule ID 981176 when a request is blocked by OWASP. Also, some OWASP rules listed in the activity log do not appear in the list of rules under Package: OWASP ModSecurity Core Ruleset because disabling those rules is not recommended.
{: important}
