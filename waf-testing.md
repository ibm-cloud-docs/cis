---

copyright:
  years: 2025
lastupdated: "2025-08-26"

keywords: waf 

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Setting up and tuning CIS WAF security 
{: #waf-configuration}

CIS inspects incoming web and API traffic and blocks unwanted requests using predefined rule sets, known as rulesets. This topic walks you through the initial steps to configure the Web Application Firewall (WAF) and quickly enable protection against the most common web attacks.
{: shortdesc}

If you're performing a penetration test (pentest), begin with the most restrictive WAF configuration, for example, enable all available rules and set actions to **Block**. This approach helps you evaluate the full protection capabilities of CIS. After testing, you can adjust the configuration to accommodate expected application behavior and reduce false positives.
{: attention}
  
## Before you begin
{: #before-you-begin-waf}

Before testing WAF capabilities, ensure you’ve set up a CIS instance in your IBM Cloud account and added your domain to CIS.

## Configuring WAF 
{: #waf-process}

Follow these high-level steps to configure WAF for your zones:

1. Deploy the CIS managed ruleset.

   The [CIS managed ruleset](/docs/cis?topic=cis-managed-rules-overview&interface=ui#managed-rulesets) protects against Common Vulnerabilities and Exposures (CVEs) and known attack vectors. It identifies common attacks using signatures and is designed to generate low false positives. CIS can also update this ruleset during emergency releases to protect against high-profile zero-day threats.

   1. In the IBM Cloud console, go to **Navigation Menu** icon![Navigation Menu icon](../icons/icon_hamburger.svg), click **Resource list**, then expand **Security**. 
   1. Click your CIS instance name.
   1. Navigate to **Security > WAF** and ensure that the **CIS Managed Ruleset** Status toggle is enabled.

      **Default settings and ruleset customization**: By default, only a subset of rules is enabled to balance protection with reduced false positives. You can review and enable additional rules based on your application stack.

      In particular situations, enabling the managed ruleset can cause some false positives. False positives are legitimate requests inadvertently mitigated by the WAF. For information on addressing false positives, see [Handling false positives in managed rules](/docs/cis?topic=cis-handling-false-positives-managed-rules).

      For pentesting, it is recommended to enable all rules with the following settings:

         * Ruleset action: **Block**
         * Ruleset status: Enabled (enables all rules in the ruleset)

      For more information, see [Working with WAF managed rules](/docs/cis?group=working-with-waf-managed-rules).

1. Create a custom rule based on WAF attack score.

   WAF attack score is only available to Standard plan customers.
   {: note}
   
   The WAF attack score is a machine-learning layer that complements CIS's managed rulesets, providing additional protection against SQL injection (SQLi), cross-site scripting (XSS), and many remote code execution (RCE) attacks. It helps identify rule bypasses and potentially new, undiscovered attacks.

  Do the following: 

   1. [Create a custom rule](/docs/cis?topic=cis-about-waf-custom-rules&interface=ui) using the Attack Score field:

      The Attack Score field is a number from 1 (likely malicious) to 99 (likely clean) classifying how likely an incoming request is malicious or not. Allows you to detect new attack techniques before they are publicly known.
      {: note}

      * When incoming requests match:

         | Field | Operator | Value |
         |:------------| :-----------|:----------| 
         | WAF Attack Score | less than | `20` |
         {: caption="Rule conditions for detecting unverified low-score bot requests" caption-side="bottom"}
 
        Expression Preview:  `(cf.waf.score lt 20)`

      * Choose action: **Block**

         If you're on the CIS Standard, Standard Next, or Free Trial plans, you can create a custom rule using the WAF Attack Score Class field instead. For example, use the following rule expression: `WAF Attack Score Class equals Attack`.

1. Create a custom rule based on bot score.

   The bot score feature is available only to CIS Enterprise Premier customers with [Bot Management](/docs/cis?topic=cis-about-bot-mgmt). Standard Next and Enterprise Advanced/Usage plans can use Super Bot Fight Mode, but note that no UI is currently available for configuration.

   1. Create a custom rule using the Bot Score and Verified Bot fields:
   
      Bot scores range from 1–99. A score below 30 typically indicates automation. The Verified Bot field identifies bots that are transparent about their identity and purpose.
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

1. Optional: Deploy the CIS [OWASP Core Ruleset](/docs/cis?topic=cis-owasp-rule-set-for-waf).

   After configuring the CIS Managed Ruleset and attack score, you can also deploy the OWASP Core Ruleset. This managed ruleset is CIS's implementation of the OWASP ModSecurity Core Ruleset. Its attack coverage significantly overlaps with CIS managed ruleset by detecting common attack vectors such as SQLi and XSS.

   The OWASP Core Ruleset is prone to false positives and offers only marginal benefits when added on top of CIS managed ruleset and WAF attack score. If you decide to deploy this managed ruleset, you must monitor and adjust its settings based on your traffic to prevent false positives.
   {: important}

   1. From your CIS instance, go to **Security > WAF** and ensure that the **CIS OWASP Core Ruleset** Status toggle is enabled.

      This deploys the ruleset with the default config: **paranoia level** = `PL1` and **score threshold** = `Medium (40+)`.

      **Ruleset configuration**: Unlike the signature-based CIS managed ruleset, the OWASP Core Ruleset is score-based. You select a certain paranoia level (levels vary from PL1 to PL4, where PL1 is the lowest level), which enables an increasing larger group of rules. You also select a score threshold, which decides when to perform the configured action. Low paranoia with a high score threshold usually leads to fewer false positives. For an example of how the OWASP Core Ruleset is evaluated, see the [OWASP evaluation example](/docs/cis?topic=cis-owasp-evaluation-example).

      Two common configuration strategies:

         * Strict first: Start with **paranoia level** = `PL4` and **score threshold** = `Low - 60 and higher`. Reduce the score threshold and paranoia level until you achieve a good false positives/true positives rate for your incoming traffic.
         * Permissive first: Start from a more permissive configuration (**paranoia level** = `PL1`, **score threshold** = `High - 25 and higher`) and increase both parameters to adjust your protection, trying to keep a low number of false positives.

      For more information on configuring the OWASP Core Ruleset in the console, see [Using fields, functions, and expressions](/docs/cis?topic=cis-custom-rules-fields-and-expressions&interface=ui).
   
1. Review traffic in security dashboards.

   After configuring the WAF, monitor how your settings affect incoming traffic:

      * Use [CIS metrics](/docs/cis?group=metrics) to explore traffic patterns, including traffic not blocked by WAF rules. All data provided by traffic detections is available (for example, WAF attach score and bot score).
      * Use [Security Events](/docs/cis?topic=cis-using-the-cis-security-events-capability) to analyze requests that are being mitigated by CIS security products.
      * Enterprise plans can also obtain data about HTTP requests and security events using [CIS Logpush jobs](/docs/cis?topic=cis-logpush&interface=ui).

## Next steps
{: #next-steps-waf}

After setting up your WAF configuration, you’ll have a strong baseline of protection against common and advanced web threats.

To further enhance protection, consider:

* [Allowlist certain IP addresses](/docs/cis?topic=cis-cis-allowlisted-ip-addresses)
* [Create custom rules that block traffic from embargoed countries](/docs/cis?topic=cis-adhering-to-embargoed-countries&interface=cli#custom-rules-cli)
* [Define rate limits](/docs/cis?topic=cis-cis-rate-limiting&interface=ui)
