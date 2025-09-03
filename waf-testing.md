---

copyright:
  years: 2025
lastupdated: "2025-08-29"

keywords: waf 

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Setting up and tuning CIS WAF security 
{: #waf-configuration}

Cloud Internet Services (CIS) inspects incoming web and API traffic and blocks unwanted requests using predefined rulesets. This topic walks you through the initial steps to configure the Web Application Firewall (WAF) and quickly enable protection against the most common web attacks.
{: shortdesc}

**Attention**: When performing a _penetration test (pentest)_, it is recommended to start with the most restrictive WAF configuration to evaluate the full defensive capabilities of CIS. To achieve this, configure the following settings:

* Enable all managed rules.
   * [CIS OWASP Core Ruleset](/docs/cis?topic=cis-owasp-rule-set-for-waf): Set paranoia level to 4 (`PL4`) and score threshold to **High** (`High-25 and higher`).
   * [CIS managed ruleset](/docs/cis?topic=cis-managed-rules-overview&interface=ui#managed-rulesets): Set the default ruleset (for all signatures) to **Block**.
* Create a custom rule to block any request with an Attack Score less than or equal to `20`. 

   Expression preview: `(cf.waf.score le 20)`

After testing, you can adjust this configuration to accommodate your application's expected behavior and reduce false positives. 
  
## Before you begin
{: #before-you-begin-waf}

Before testing WAF capabilities, make sure that you have a CIS instance set up in your IBM Cloud account and your domain added to CIS.

## Configuring WAF 
{: #waf-process}

Follow these high-level steps to configure WAF for your zones:

1. Deploy the CIS managed ruleset.

   The [CIS managed ruleset](/docs/cis?topic=cis-managed-rules-overview&interface=ui#managed-rulesets) protects against Common Vulnerabilities and Exposures (CVEs) and attack vectors using signature-based detection to identify common attacks, with a focus on minimizing false positives. 
   
   CIS updates these rulesets during emergency releases to respond to high-profile, zero-day threats.
   {: note}

   1. In the IBM Cloud console, open the **Navigation Menu** icon![Navigation Menu icon](../icons/icon_hamburger.svg), then click **Resource list** and expand **Security**. 
   1. Click your CIS instance name.
   1. Navigate to **Security > WAF** and make sure that the **CIS Managed Ruleset** Status toggle is enabled.

      By default, a subset of rules is enabled to balance protection with reduced false positives. You can review and enable additional rules based on your application's stack.

      In particular situations, enabling the managed ruleset can cause some false positives. False positives are legitimate requests inadvertently mitigated by the WAF. For information on addressing false positives, see [Handling false positives in managed rules](/docs/cis?topic=cis-handling-false-positives-managed-rules).

      For pentesting, it is recommended to enable all rules with the following settings:

         * Ruleset action: **Block**
         * Ruleset status: Enabled (enables all rules in the ruleset)

      For more information, see [Working with WAF managed rules](/docs/cis?group=working-with-waf-managed-rules).

1. Create a custom rule based on WAF Attack Score.

   WAF Attack Score is only available to Standard plan customers.
   {: note}
   
   The WAF Attack Score is a machine-learning layer that complements CIS's managed rulesets, providing additional protection against SQL injection (SQLi), cross-site scripting (XSS), and many remote code execution (RCE) attacks. It helps identify rule bypasses and potentially new, undiscovered attacks.

   [Create a custom rule](/docs/cis?topic=cis-about-waf-custom-rules&interface=ui) using the Attack Score field:

      The Attack Score field is a number from `1` (likely malicious) to `99` (likely clean) classifying how likely an incoming request is malicious or not. Allows you to detect new attack techniques before they are publicly known.
      {: note}

      * When incoming requests match:

         | Field | Operator | Value |
         |:------------| :-----------|:----------| 
         | WAF Attack Score | less than or equal to | `20` |
         {: caption="Rule conditions for detecting unverified low-score bot requests" caption-side="bottom"}
 
        Expression Preview:  `(cf.waf.score le 20)`

      * Choose action: **Block**

         If you're on the CIS Standard, Standard Next, or Free Trial plans, you can create a custom rule using the WAF Attack Score Class field instead. For example, use the following rule expression: `WAF Attack Score Class equals Attack`.

1. Create a custom rule based on Bot Score.

   The Bot Score feature is available only to CIS Enterprise Premier customers with [Bot Management](/docs/cis?topic=cis-about-bot-mgmt). Standard Next and Enterprise Advanced/Usage plans can use Super Bot Fight Mode, but note that no UI is currently available for configuration.

   Create a custom rule using the Bot Score and Verified Bot fields:
   
      Bot scores range from `1–99`. A score below `30` typically indicates automation. The Verified Bot field identifies bots that are transparent about their identity and purpose.
      {: note}

      * When incoming requests match:
      
         | Field | Operator | Value | Logic |
         |:------------| :-----------|:----------|:----------| 
         | Bot Score | less than | `20` | And |
         | Verified Bot | equals | Off |   |
         {: caption="Match conditions for applying a managed challenge to suspected bot traffic" caption-side="bottom"}

      * Choose action: **Managed Challenge**

         For more information about the bot-related fields you can use in expressions, see [Bot Management fields](/docs/cis?topic=cis-bot-management-fields).

         With these protections in place, your WAF setup provides robust mitigation against known and unknown threats while minimizing false positives.

1. Optional: Deploy the [CIS OWASP Core Ruleset](/docs/cis?topic=cis-owasp-rule-set-for-waf).

   After configuring the CIS Managed Ruleset and attack score, you can also deploy the CIS OWASP Core Ruleset. This managed ruleset is CIS's implementation of the OWASP ModSecurity Core Ruleset. Its attack coverage significantly overlaps with CIS managed ruleset by detecting common attack vectors, such as SQLi and XSS.

   This ruleset is prone to false positives and provides limited additional benefit when combined with CIS managed rules and WAF Attack Score. If you decide to deploy this managed ruleset, you must monitor and adjust its settings based on your traffic to prevent false positives.
   {: important}

   From the CIS dashboard, go to **Security > WAF** and ensure that the **CIS OWASP Core Ruleset** Status toggle is enabled.

      This deploys the ruleset with the default config: **paranoia level** = `PL1` and **score threshold** = `Medium (40+)`.

      **Ruleset configuration**: Unlike the signature-based CIS managed ruleset, the OWASP Core Ruleset is score-based. You select a certain paranoia level (levels vary from PL1 to PL4, where PL1 is the lowest level), which enables an increasing larger group of rules. You also select a score threshold, which decides when to perform the configured action. Low paranoia with a high score threshold usually leads to fewer false positives. For an example of how the OWASP Core Ruleset is evaluated, see the [OWASP evaluation example](/docs/cis?topic=cis-owasp-evaluation-example).

      Two common configuration strategies:

      * Strict first: Start with **paranoia level** = `PL4` and **score threshold** = `High - 25 and higher`. Reduce the score threshold and paranoia level until you achieve a good false positives/true positives rate for your incoming traffic.
      * Permissive first: Start from a more permissive configuration (**paranoia level** = `PL1`, **score threshold** = `Low - 60 and higher`) and increase both parameters to adjust your protection, trying to keep a low number of false positives.

      For more information on configuring the OWASP Core Ruleset, see [Using fields, functions, and expressions](/docs/cis?topic=cis-custom-rules-fields-and-expressions&interface=ui).
   
1. Review traffic in security dashboards.

   After configuring the WAF, monitor how your settings affect incoming traffic:

   * Use [CIS metrics](/docs/cis?group=metrics) to explore traffic patterns, including traffic not blocked by WAF rules. All data provided by traffic detections is available (for example, WAF Attack Score and Bot Score).
   * Use [Security Events](/docs/cis?topic=cis-using-the-cis-security-events-capability) to review mitigated traffic. 
   * Enterprise plans can access HTTP requests and security events using [CIS Logpush](/docs/cis?topic=cis-logpush&interface=ui).

## Rule recommendations 
{: #rule-recommendations}

CIS doesn't recommend blocking traffic solely based on the WAF Attack Score for all values below `50`, since the _Likely attack_ range (scores between `21` and `50`) tends to have false positives. However, if you choose to block traffic based on this score, you might consider one of the following:

* Use a stricter WAF Attack Score value in your expression. For example, block traffic with a WAF Attack Score below `20` or below `15` (you might need to adjust the exact threshold). 
* Combine a higher WAF Attack Score threshold with additional filters when blocking incoming traffic. For example, include a check for a specific URI path in your expression or use bot score as part of your criteria.

## Next steps
{: #next-steps-waf}

After your WAF is configured, you’ll have a solid baseline of protection against common and advanced web threats.

To further enhance protection, consider:

* [Allowlist certain IP addresses](/docs/cis?topic=cis-cis-allowlisted-ip-addresses)
* [Create custom rules that block traffic from embargoed countries](/docs/cis?topic=cis-adhering-to-embargoed-countries&interface=cli#custom-rules-cli)
* [Define rate limits](/docs/cis?topic=cis-cis-rate-limiting&interface=ui)
