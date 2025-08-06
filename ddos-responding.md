---

copyright:
  years: 2024, 2025
lastupdated: "2025-08-06"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Responding to DDoS attacks
{: #responding-to-ddos-attacks}

The CIS network automatically mitigates large DDoS attacks, but these attacks can still affect your application. All users should perform the following steps to better secure their application.
{: shortdesc}

1. Make sure the `ruleset_phase` parameter (with `ddos_l7`) in the [Ruleset API](/apidocs/cis#get-zone-entrypoint-ruleset) is set to the default settings (high sensitivity level and mitigation actions) for optimal DDoS activation.
1. Deploy WAF custom rules and rate-limiting rules to enforce a combined positive and negative security model. Reduce the traffic allowed to your website based on your known usage.
1. Make sure your origin is not exposed to the internet. Restrict access so that only CIS IP addresses can access your origin. As an extra security precaution, consider contacting your hosting provider and requesting new origin server IP addresses if they have been targeted directly in the past.
1. If you have Bot Management, consider using it in your WAF custom rules.
1. Enable caching as much as possible to reduce the strain on your origin servers.
1. To help counter attack randomization, update your cache settings to exclude the query string as a cache key. When the query string is excluded as a cache key, CIS’ cache will take in unmitigated attack requests instead of forwarding them to the origin. The cache can be a useful mechanism as part of a multilayered security posture.
