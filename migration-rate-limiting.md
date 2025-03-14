---

copyright:
  years: 2024, 2025
lastupdated: "2025-03-14"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Migrating to new rate-limiting rules
{: #migrating-to-rate-limiting}
 
The {{site.data.keyword.cis_short_notm}} WAF provides both automatic protection from vulnerabilities and the flexibility to create WAF custom rules.

{{site.data.keyword.cis_short_notm}} recommends that you create new ruleset-based, rate-limiting rules in the {{site.data.keyword.cis_short_notm}} dashboard to replace any existing rate-limiting rules that you might have configured in the previous rate-limiting rule handling.

The old and new implementation of rate-limiting rules have separate rules lists because the two implementations do not offer the same set of features. Re-create your rate limiting configuration (in the previous version) by using the new rate-limiting rules, either using the {{site.data.keyword.cis_short_notm}} dashboard, or the [Rulesets API](/apidocs/cis#get-instance-rulesets).

For more information on the new rate-limiting implementation, including the available features in each {{site.data.keyword.cis_short_notm}} plan, see the [Rate-limiting rules API](/apidocs/cis#list-all-zone-rate-limits).

Currently, the CIS dashboard shows only the legacy rate-limiting rules. To re-create the legacy rules or create new ones, you can use the [Rulesets API](/apidocs/cis#get-instance-rulesets) with the `http_ratelimit` [phase](/docs/cis?topic=cis-about-rule-sets#phase-list) or the CIS CLI. The CIS dashboard will be updated in the future to reflect both types of rules. 
{: important}

## Main differences between versions
{: #main-differences-rate-limiting}

Here are the key differences between the old and new rate-limiting rules.

### Billing model
{: #billing-model}

The version of rate limiting was billed based on usage and offered as an add-on for all plans, whereas the new version is included in {{site.data.keyword.cis_short_notm}} plans. For Enterprise plans, Rate Limiting is priced based on total contracted HTTP traffic. In addition to all the features of the version, the new rate-limiting rules introduce several new capabilities.

### Advanced scope expressions
{: #advanced-scope-expressions}

The version of rate limiting allowed you to scope the rules based on a single path and method of the request. In the new version, you can write rules similar to [firewall rules](/docs/cis?topic=cis-about-firewall-rules) or [WAF custom rules](/docs/cis?topic=cis-custom-rules-overview), combining multiple parameters of the HTTP request.

### Separate counting and mitigation expressions
{: #separate-counting-and-mitigation-expressions}

In the new version of Rate Limiting, counting and mitigation expressions are separate. The counting expression defines which requests are used to compute the rate. The mitigation expression defines which requests are mitigated after the threshold is reached. Using these separate expressions, you can track the rate of requests on a specific path such as `/login` and, when an IP exceeds the threshold, block every request from the same IP addressed at your domain.

### Number of rules per plan
{: #no-rules-per-plan}

The new rate-limiting ruleset allows for up to 100 rules per domain on enabled Enterprise plans. For more information, see [Comparing CIS plans](/docs/cis?topic=cis-cis-plan-comparison).
