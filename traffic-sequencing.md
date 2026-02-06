---

copyright:
  years: 2024, 2026
lastupdated: "2026-02-06"

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Traffic sequencing
{: #traffic-sequencing}

Traffic sequencing refers to the order in which {{site.data.keyword.cis_full}} processes incoming web traffic. Understanding this sequence helps clarify how CIS applies different security and performance features, such as DDoS protection, firewall rules, and edge functions.
{: shortdesc}

When you work with {{site.data.keyword.cis_short_notm}}, it can sometimes be confusing to know the order in which different operations are applied to your traffic. For example, whether firewall rules run before edge functions or page rules. Traffic typically flows through CIS in the following order:

1. [Distributed Denial of Service (DDoS) protection](/docs/cis?topic=cis-about-ddos) - Initial defense to block large-scale attacks.
1. [URL rewrites](/docs/cis?topic=cis-url-normalization) - Adjustments to incoming URLs before further processing.
1. [Page rules](/docs/cis?topic=cis-about-firewall-rules) - Custom rules that modify how requests are handled.
1. [IP firewall rules](/docs/cis?topic=cis-actions) - Filtering based on IP addresses.
1. [Bot management](/docs/cis?topic=cis-about-bot-mgmt) - Identifies and manages automated traffic.
1. WAF and custom rules, which generally process in this order:
   1. [Custom rules](/docs/cis?topic=cis-about-waf-custom-rules&interface=ui)
   1. [WAF rules](/docs/cis?topic=cis-waf-actions)
   1. [Rate limiting](/docs/cis?topic=cis-cis-rate-limiting)

    Based on the actions and priority settings of the rules, steps in the firewall sequence can be bypassed. For example, a firewall rule with an early priority that allows certain traffic is processed first, and then skips over the rest of the rules in the sequence.
    {: note}

1. [Edge functions](/docs/cis?topic=cis-working-with-edge-functions) - Custom scripts that run on the edge to modify requests or responses.
1. [Global load balancer](/docs/cis?topic=cis-configure-glb) - Distributes traffic across your origin servers.

Knowing this sequence helps you understand how different security and performance features interact and which rules or functions take precedence.
