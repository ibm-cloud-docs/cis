---

copyright:
  years: 2024, 2026
lastupdated: "2026-02-06"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Responding to DDoS attacks
{: #responding-to-ddos-attacks}

The CIS network automatically mitigates large DDoS attacks, but these attacks can still affect your application. All users should perform the following steps to better secure their application.
{: shortdesc}

1. Make sure the `ruleset_phase` parameter (with `ddos_l7`) in the [Ruleset API](/apidocs/cis#get-zone-entrypoint-ruleset) is set to the default settings (high sensitivity level and mitigation actions) for optimal DDoS activation.
1. Deploy WAF custom rules and rate-limiting rules to enforce a combined positive and negative security model.
1. Limit inbound traffic to what your application actually needs.

   * Reduce the traffic allowed to your website based on your known usage.
   * Restrict access so that only CIS IP addresses can access your origin. As an extra security precaution, consider contacting your hosting provider and requesting new origin server IP addresses if they have been targeted directly in the past.
   * Ensure that your origin is not exposed to the internet.

1. If you have Bot Management enabled, consider integrating it into your custom WAF rules to further mitigate automated attacks.
1. Enable caching as much as possible to minimize strain on your origin during high-traffic events.

   To help counter attack randomization, update your cache settings to exclude the query string as a cache key. To counter attack randomization, update your cache settings to exclude the query string as a cache key. When excluded, CIS cache absorbs unmitigated attack requests instead of forwarding them to your origin. Caching is an important component of a multilayered security posture.

## Related links
{: #responding-to-ddos-attacks-related-links}

* [DDoS attack concepts](/docs/cis?topic=cis-ddos-attack-concepts)
* [About DDoS protection in CIS](/docs/cis?topic=cis-about-ddos)
* [Preventing DDoS attacks](/docs/cis?topic=cis-preventing-ddos-attacks)
* [Using Defense mode for DDoS attacks](/docs/cis?topic=cis-defense-mode-attack-ddos)
* [Third-party services and DDoS protection](/docs/cis?topic=cis-third-party-ddos)
* [HTTP DDoS Attack Protection managed ruleset](/docs/cis?topic=cis-http-ddos)
