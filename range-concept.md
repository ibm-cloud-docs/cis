---

copyright:
  years: 2018, 2026
lastupdated: "2026-04-29"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Range applications
{: #range-concept}

Range applications allow you to extend DDoS protection, TLS encryption, and custom rule policies to TCP and UDP services beyond traditional HTTP/HTTPS traffic. This secures your TCP-based services beyond just web traffic and provides comprehensive security and performance benefits within IBM Cloud CIS.
{: shortdesc}

Unlike standard web applications protected by CIS, Range applications enable your non-web services, such as VPN endpoints, NAT gateways, database ports, and custom TCP services, to leverage CIS global network and threat intelligence. Traffic destined for these services passes through the CIS infrastructure, where it benefits from multiple layers of security and performance enhancements, including:

* DDoS protection: Mitigate Layer 3/4 attacks against TCP/UDP protocols, including volumetric floods and protocol abuse, to protect non-web services from disruption.
* TLS encryption: Add TLS encryption to services that lack native support or have complex backend setups. This helps secure data in transit and protect against interception or theft.
* Custom rule integration: Enforce granular access controls by allowing, blocking, or challenging specific IP addresses, IP ranges, or other criteria. This reduces unauthorized access and minimizes attack surfaces.
* Secure HTTP(S) Range applications: Apply Layer 7 custom rules to protect HTTP(S)-based Range applications, enabling fine-tuned filtering and policy enforcement. For more information, see [About WAF custom rules](/docs/cis?topic=cis-custom-rules-overview).
* Configure load balancers: Support TCP health checks, automatic failover, and traffic steering to optimize performance and maintain high availability across Range-enabled services.
* Proxy protocol support: Preserve client IP visibility across proxy and load balancer setups, which is critical for accurate logging, security policy enforcement, and auditing.

Range applications are only available to Enterprise customers for an additional cost, and is priced per bandwidth usage.
{: note}

## Related links
{: #range-application-information}

* [Working with Range applications](/docs/cis?group=range)
* [About Range applications](/docs/cis?topic=cis-about-cis-range)
