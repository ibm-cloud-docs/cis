---

copyright:
  years: 2024, 2025
lastupdated: "2025-02-24"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# About rulesets
{: #about-rule-sets}

You can use the {{site.data.keyword.cis_short_notm}} Ruleset Engine to create and deploy rules and rulesets in {{site.data.keyword.cis_short_notm}} using the same basic syntax.
{: shortdesc}

## Main features
{: #rule-sets-main-features}

The following features apply to rulesets:

* **Powerful syntax**: Rule expressions use a powerful rules language similar to the [`wirefilter`](https://github.com/cloudflare/wirefilter){: external} syntax that allows you to create complex rules.
* **High-performance rule evaluation**: Allows you to have many rules in {{site.data.keyword.cis_short_notm}} with minimal impact on performance.
* **Engine powering {{site.data.keyword.cis_short_notm}}**: {{site.data.keyword.cis_short_notm}} will continue to build products on top of the Ruleset Engine, which means that you can use the same API methods for configuring different products with the same customization possibilities. The Ruleset Engine also supports the different phases of the request life cycle.

## Phases
{: #phases}

A phase defines a stage in the life of a request where you can execute rulesets. Phases are defined by {{site.data.keyword.cis_short_notm}} and cannot be modified.

Phases exist at the instance level and at the zone level. For the same phase, rules defined at the instance level are evaluated before the rules defined at the zone level.

Each phase has, at most, one entry point ruleset at the instance and zone level.

Currently, only phases at the zone level are available. This page is updated as instance and zone level phases become available in subsequent releases.

### Phase list
{: #phase-list}

The following table lists the phases that are available within the Ruleset Engine APIs.

|Phase name|Description|Supported interfaces|
|----------|-----------|-------------------|
| `http_request_firewall_managed`| Web Application Firewall (WAF)| API, CLI, UI |
| `http_request_firewall_custom` | Firewall rules | API |
| `http_ratelimit` | Rate-limiting rules | API, CLI |
| `ddos_l7` | HTTP DDoS Attack Protection rules | API |
{: caption="Available phases" caption-side="bottom"}

## Entry point ruleset
{: #entry-point-ruleset}

Entry point rulesets are abstracted away when using the {{site.data.keyword.cis_short_notm}} UI. They are required to deploy and override rulesets when using the API, CLI, SDK, or Terraform.
{: note}

An entry point ruleset contains a list of ordered rules that run in a phase at the instance or zone level. This ruleset is an entry point for all rules executed in a phase. Some of these rules might run other rulesets.

Each phase has, at most, one entry point ruleset at the instance level and at the zone level.

The `kind` field of a phase entry point ruleset has one of the following values:

* `root`: Used for a phase entry point ruleset at the instance level
* `zone`: Used for a phase entry point ruleset at the zone level

See [Deploying rulesets](/docs/cis?topic=cis-deploying-rule-sets) for detailed instructions on using entry point rulesets to deploy rulesets.

See [Overriding rulesets](/docs/cis?topic=cis-override-rule-sets) for detailed instructions on using entry point rulesets to override rulesets.


## Related links
{: #rule-sets-related-links}

* [{{site.data.keyword.cis_short_notm}} ruleset](/docs/cis?topic=cis-cis-rule-sets)
* [OWASP ruleset](/docs/cis?topic=cis-owasp-rule-set-for-waf)
* [Exposed credentials check](/docs/cis?topic=cis-exposed-credentials-check-ruleset)
