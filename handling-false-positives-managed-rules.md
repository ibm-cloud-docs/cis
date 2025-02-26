---

copyright:
  years: 2024, 2025
lastupdated: "2025-02-26"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Handling false positives in managed rules
{: #handling-false-positives-managed-rules}

If you encounter a false positive caused by a managed rule, take one of the following steps.

* **Add an exception**: Exceptions allow you to skip the execution of WAF managed rulesets or some of their rules for certain requests.
* **Adjust the OWASP managed ruleset**: A request blocked by rule ID `6179ae15870a4bb7b2d480d4843b323c` and description `949110: Inbound Anomaly Score Exceeded` refers to the OWASP Core Ruleset. To resolve the issue, [configure the OWASP managed ruleset](/docs/cis?topic=cis-owasp-rule-set-for-waf).
* **Disable the corresponding managed rules**: Create an override to disable specific rules. This can avoid false positives, but also reduces the overall site security. For more information, see [Overriding managed rulesets](/docs/cis?topic=cis-overriding-rulesets&interface=cli).

If you contact Support to verify whether a WAF managed rule triggers as expected, [provide a HAR file](/docs/cis?topic=cis-generate-har-files) captured while sending the specific request that you want to verify.

## Recommendations
{: #recommendations-for-false-positives}

* If one specific rule causes false positives, disable that specific rule and not the entire ruleset.
* For false positives within the administrator area of your website, add an exception that disables a managed rule for the admin section of your site resources by using an expression similar to the following example.

```sh
http.host eq "example.com" and starts_with(http.request.uri.path, "/admin")
```
{: pre}
