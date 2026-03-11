---

copyright:
  years: 2026
lastupdated: "2026-03-11"

keywords: waf 

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# About WAF Attack Score
{: #waf-attack-score}

WAF Attack Score helps detect variations of known attacks by analyzing request behavior and payload characteristics. This capability complements [WAF managed rules](/docs/cis?topic=cis-managed-rules-overview) by identifying malicious traffic that does not exactly match existing rule signatures.
{: shortdesc}

WAF managed rules use continuously updated rulesets to detect well-known attack patterns with a lower false-positive rate. These rules are effective for established attack vectors but are not optimized to detect modified or obfuscated attacks, such as those generated through fuzzing techniques.

WAF Attack Score addresses this gap by using a machine learning model to evaluate each request and assign an attack score from 1 to 99, based on the likelihood that the request is malicious. Similar to [Bot Management](/docs/cis?topic=cis-about-bot-mgmt), you can use this score to identify and act on suspicious traffic that does not directly trigger a managed rule.

For maximum protection, CIS recommends using WAF managed rules and WAF Attack Score together to detect both known attacks and their variations.

## Available scores
{: #waf-available-score}

The CIS WAF provides the following attack score fields:

| Field | Type | Description | Required plan |
| ---------- | ----- | ------------ | ----------- |
| WAF Attack Score \n `cf.waf.score` | Number | A global score from 1–99 that combines the score of each WAF attack vector into a single score. | Enterprise |
| WAF SQLi Attack Score \n `cf.waf.score.sqli` | Number | A score from 1–99 classifying the [SQL injection (SQLi)](https://w3.terminology.g11n.ibm.com/standards/terminology/translationsearch/?ug=corporate&term=Structured+Query+Language+injection&sourceLanguage=English&view=details&targetLanguages=English&exact=true){: external} attack vector. | Enterprise |
| WAF XSS Attack Score \n `cf.waf.score.xss` | Number | A score from 1–99 classifying the [cross-site scripting (XSS)](https://w3.terminology.g11n.ibm.com/standards/terminology/translationsearch/?ug=corporate&term=cross-site+scripting&sourceLanguage=English&view=details&targetLanguages=English&exact=true){: external} attack vector. | Enterprise |
| WAF RCE Attack Score \n `cf.waf.score.rce` | Number | A score from 1–99 classifying the command injection or [remote code execution (RCE)](https://w3.terminology.g11n.ibm.com/standards/terminology/termsearch/?ug=corporate&term=remote+code+execution&sourceLanguage=English&view=list&targetLanguages=English){: external} attack vector. | Enterprise |
| WAF Attack Score Class \n `cf.waf.score.class` | String | The attack score class of the current request, based on the WAF attack score. Possible values: `attack`, `likely_attack`, `likely_clean`, and `clean`. | All plans |
{: caption="Available WAF scores" caption-side="bottom"}

You can use these fields in expressions of [custom rules](/docs/cis?topic=cis-custom-rules-fields-and-expressions) and [rate limiting rules](/docs/cis?topic=cis-custom-rules-fields-and-expressions). WAF Attack Score fields use the `Number` data type and range from `1` to `99`, with the following meanings:

* A score of 1 indicates that the request is very likely malicious.
* A score of 99 indicates that the request is likely clean.

The special score `100` indicates that the request reached the WAF Attack Score classification system, but the system did not assign a score.

In [Logpush](/docs/cis?topic=cis-logpush&interface=ui), you might also see a score of `0`. This value means that the request did not reach the stage where attack scores are calculated. For example, another rule or protection mechanism might have already mitigated the request. The value `0` does not appear in the CIS console.

The global WAF Attack Score is mathematically derived from individual attack vector scores, such as SQL injection (SQLi) and cross-site scripting (XSS) scores, using a weighted system. These scores are interdependent, and the global score is not a simple sum of the individual values. Lower global scores indicate a higher likelihood that the request is malicious, while higher scores indicate that the request is more likely clean.

The WAF Attack Score class field can have one of the following values, depending on the calculated request attack score:

| Console label |	Field value |	Description |
| ------------- | ----------- | ----------- |
| Attack | `attack` | Attack score between `1` and `20`. |
| Likely attack | `likely_attack` | Attack score between `21` and `50`. |
| Likely clean | `likely_clean` | Attack score between `51` and `80`. |
| Clean | `clean` | Attack score between `81` and `99`. |
{: caption="WAF Attack Score classes" caption-side="bottom"}

Requests with the special attack score of `100` appear in the CIS console with a WAF Attack Score Class value of `Unscored`. You cannot use this class value in rule expressions.

WAF Attack Score automatically detects and decodes Base64, JavaScript (Unicode escape sequences), and URL-encoded content. This decoding applies to all parts of the request, including the URL, headers, and request body.

## Rule recommendations
{: #waf-rule-recommendations}

Avoid blocking traffic based solely on WAF Attack Score values less than `50`. Scores in the Likely attack range (`21`–`50`) might include false positives and often require additional filtering criteria.

If you choose to block traffic based on the attack score, use one of the following approaches:

* Use a more strict WAF Attack Score value in your expression. For example, block traffic with a WAF Attack Score less than `20` or `15` (you might need to adjust the exact threshold).
* When you block incoming traffic based on the WAF Attack Score, combine a higher WAF Attack Score threshold with additional filters. For example, include a check for a specific URI path in your expression or use bot score as part of your criteria.

## Using WAF Attack Score
{: #using-waf-score}

To configure WAF Attack Score in a custom rule, follow these steps:

1. To create a custom rule, select one of the following:

   * If you are an Enterprise plan customer, [create a custom rule](/docs/cis?topic=cis-about-waf-custom-rules&interface=ui#create-custom-rule-ui) that blocks requests with a WAF Attack Score less than or equal to `20`. This value is the recommended starting threshold.

      * Equivalent rule expression: `cf.waf.score le 20`
      * Action: **Block**

   * If you are a Standard plan customer, create a custom rule by using the **WAF Attack Score Class** field instead. For example, block requests with a score class of `Attack`.

      * Equivalent rule expression: `cf.waf.score.class eq "attack"`
      * Action: **Block**

1. Monitor the rule closely during the first few days. Verify that the selected threshold or class value aligns with your traffic patterns. Adjust the rule if you observe false positives or missed threats.

1. Update the rule action. If you are an Enterprise plan customer and you created a rule with a **Log** action, change the rule action to a stronger action, like **Managed Challenge** or **Block**.

The WAF Attack Score and Bot Score measure different types of risk. WAF Attack Score identifies requests that resemble known attack patterns, including variations that WAF Managed Rules might not detect. Bot Score identifies automated traffic and evaluates the likelihood that a request originates from a bot. Use WAF Attack Score to detect malicious payloads and attack behavior. Use Bot Score to identify and manage automated traffic.
