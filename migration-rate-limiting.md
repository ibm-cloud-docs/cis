---

copyright:
  years: 2024, 2025
lastupdated: "2025-05-22"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Migrating to new rate-limiting rules
{: #migrating-to-rate-limiting}
 
The {{site.data.keyword.cis_short_notm}} WAF provides both automatic protection from vulnerabilities and the flexibility to create WAF custom rules.

{{site.data.keyword.cis_short_notm}} recommends that you create new ruleset-based, rate-limiting rules to replace any existing rate-limiting rules that you might have configured in the previous rate-limiting rule handling.

The old and new implementation of rate-limiting rules have separate rules lists because the two implementations do not offer the same set of features. Recreate your rate limiting configuration (in the previous version) by using the new rate-limiting rules with the [Rulesets API](/apidocs/cis#get-instance-rulesets).

If you're using the older version of rate limiting, you have access to both the legacy and new versions of the product. Both sets of rules are applied to incoming traffic, with the new rate-limiting logic running first. For more information on the new rate-limiting implementation, including the available features in each {{site.data.keyword.cis_short_notm}} plan, see the [Rate-limiting rules API](/apidocs/cis#list-all-zone-rate-limits).
{: note}

## Main differences between versions
{: #main-differences-rate-limiting}

Here are the key differences between the legacy and new rate-limiting rules.

### Advanced scope expressions
{: #advanced-scope-expressions}

The version of rate limiting allowed you to scope the rules based on a single path and method of the request. In the new version, you can write rules similar to [firewall rules](/docs/cis?topic=cis-about-firewall-rules) or [WAF custom rules](/docs/cis?topic=cis-custom-rules-overview), combining multiple parameters of the HTTP request.

### Separate counting and mitigation expressions
{: #separate-counting-and-mitigation-expressions}

In the new version of Rate Limiting, counting and mitigation expressions are separate. The counting expression defines which requests are used to compute the rate. The mitigation expression defines which requests are mitigated after the threshold is reached. Using these separate expressions, you can track the rate of requests on a specific path such as `/login` and, when an IP exceeds the threshold, block every request from the same IP addressed at your domain.

## Relevant changes for API users
{: #relevant-changes-for-api-users}

The new rate-limiting rules are based on the [Ruleset Engine rules language](/docs/cis?topic=cis-cis-ruleset-engine). To configure rate-limiting rules with the API, you must use the [Rulesets API](/apidocs/cis#get-instance-rulesets){: external}. The Rulesets API is used on all recent {{site.data.keyword.cis_short_notm}} security products to provide a uniform user experience when interacting with the {{site.data.keyword.cis_short_notm}} API.

The [previous Rate Limiting API](/apidocs/cis#list-all-zone-rate-limits) is being deprecated. Migrate your API calls to the new [Rulesets API](/apidocs/cis#get-instance-rulesets).{: external}
{: deprecated}

It is also recommended that you manually migrate your rate-limiting rules by recreating them with the Rulesets API using the `http_ratelimit` phase. This lets you take full advantage of the new features and refine your rate-limiting logic during the transition.

After 30 July 2025, the legacy rate-limiting APIs will no longer support creating or modifying rules. Any existing rate-limiting rules will be automatically migrated to the new framework after this date.
