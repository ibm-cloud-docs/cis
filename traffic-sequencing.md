---

copyright:
  years: 2024
lastupdated: "2024-04-09"

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Traffic sequencing
{: #traffic-sequencing}

When working with {{site.data.keyword.cis_short_notm}}, it can sometimes be difficult to tell which operation is going to run first (for example, whether firewall rules run before edge functions or page rules). To help you follow the traffic flow, keep in mind the following traffic sequence.

1. [DDoS](/docs/cis?topic=cis-distributed-denial-of-service-ddos-attack-concepts)
1. [URL rewrites](/docs/cis?topic=cis-url-normalization)
1. [Page Rules](/docs/cis?topic=cis-about-firewall-rules)
1. [IP Firewall](/docs/cis?topic=cis-actions)
1. WAF / Firewall Rules The general traffic sequence for CIS Firewall features is:
    1. [Firewall Rules](/docs/cis?topic=cis-about-firewall-rules)
    1. [WAF](docs/cis?topic=cis-waf-actions)
    1. [Rate Limiting](/docs/cis?topic=cis-cis-rate-limiting)

    Based on the actions and priority settings of the rules, steps in the firewall sequence can be bypassed. For example, a firewall rule with an early priority that allows certain traffic is processed first, and then skips over the rest of the rules in the sequence.
    {: note}

1. [Edge Functions](/docs/cis?topic=cis-working-with-edge-functions)
1. [Load Balancer](/docs/cis?topic=cis-configure-glb)
