---

copyright:
  years: 2026
lastupdated: "2026-08-05"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# About origin rules
{: #about-origin-rules}

Origin rules allow you to modify how requests are sent to your origin server. You can use origin rules to override origin settings such as the destination host header, origin host, or destination port before traffic is forwarded to the origin.

In {{site.data.keyword.cis_short_notm}}, origin rules are supported through the Rulesets API by using the `http_request_origin` phase.

## Rule execution order
{: #origin-rule-execution-order}

Origin rules are evaluated in the Ruleset Engine during the `http_request_origin` phase. Ruleset Engine rules take precedence over Page Rules. If a request matches both a Page Rule and a Ruleset Engine rule, the Ruleset Engine rule is applied.
