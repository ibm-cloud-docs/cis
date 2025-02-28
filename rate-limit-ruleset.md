---

copyright:
  years: 2024, 2025
lastupdated: "2025-02-28"

keywords: rate limiting, rules, rulesets, waf

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Rate-limiting rulesets
{: #rate-limit-rules}

Rate-limiting rules allow you to define rate limits for requests matching an expression, as well as the action to perform when those rate limits are reached.
{: shortdesc}

## Rule parameters
{: #rate-limit-rule-params}

As with other rules evaluated by the Ruleset Engine language, rate-limiting rules have the following basic parameters:

- An expression that specifies the criteria you are matching traffic on using the rules language.
- An action that specifies what to perform when there is a match for the rule and any additional conditions are met. In the case of rate-limiting rules, the action occurs when the rate reaches the specified limit.

Rate-limiting rules also require the following additional parameters:

- **Characteristics:** The set of parameters that define how the rate is tracked for this rule.
- **Period:** The period of time to consider (in seconds) when evaluating the rate.
- **Requests per period:** The number of requests over the period of time that will trigger the rate-limiting rule.
- **Duration (or mitigation timeout):** Once the rate is reached, the rate-limiting rule blocks further requests for the period of time defined in this field.
- **Action behavior:** By default, the rule action will be applied for the configured duration (or mitigation timeout), regardless of the request rate during this period.

## Important considerations
{: #rate-limit-faq}

Rate-limiting rules are evaluated in order, and some actions (like blocking) will stop the evaluation of other rules. For more information on actions and their behavior, see [Ruleset Engine rules actions](/docs/cis?topic=cis-cis-ruleset-engine#ruleset-engine-actions).

Refer to [Migrating to WAF custom rules](/docs/cis?topic=cis-migrating-to-custom-rules) to learn more about the differences between firewall rules and WAF custom rules. 
{: note}

Rate-limiting rules are not designed to allow a precise number of requests to reach the origin server. In some situations, there might be a delay (up to a few seconds) between detecting a request and updating internal counters. Due to this delay, excess requests could still reach the origin server before the mitigation action (such as blocking or challenging) is enforced.
{: important}

## Availability
{: #availability}

The rate-limiting ruleset feature is available for CIS users on the Enterprise Advanced and Enterprise Premier plans. For more information, see [Comparing CIS plans](/docs/cis?topic=cis-cis-plan-comparison).
