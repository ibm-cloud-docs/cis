---

copyright:
  years: 2018, 2025
lastupdated: "2025-08-19"

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

## Range application use cases
{: #range-use-cases}

Use cases for Range applications include:

VPN and Remote Access Services
:   Protect VPN concentrators and gateways that enable secure remote workforce connectivity, helping ensure they remain available and secure during attacks.

Network Address Translation (NAT) Devices
:   Secure NAT endpoints that manage inbound and outbound traffic flows, preventing abuse and maintaining reliable connectivity.

Database and Application Servers
:   Extend protection to critical database ports (for example, MySQL, PostgreSQL) and custom TCP-based applications, without directly exposing backend infrastructure to the internet.

Collaboration Tools and Third-Party Services
:   Protect integrations with services such as Zoom or Microsoft Teams, where traffic typically comes from a limited set of IP ranges, to avoid being mistakenly identified as DDoS activity.

## Supported protocols and use cases
{: #choosing-protocol-on}

The application type determines how traffic is routed from the CIS edge to your origin:

* TCP or UDP: Use TCP or UDP protocol when you want CIS to proxy traffic directly to your origin.
* HTTP or HTTPS: Required when using features like Edge functions or Bot Management. In this case, traffic is routed through the CIS pipeline instead of connecting directly to your origin.
* RDP: Securely connect using Remote Desktop Protocol (RDP), with built-in DDoS protection and access control.
* SSH: Securely access remote servers over SSH without exposing your origin IP.
* Minecraft: Protect and accelerate Minecraft servers with DDoS mitigation and improved network performance.

For protocol-specific limitations, see [Known issues and limitations](/docs/cis?topic=cis-known-limitations#limitations-protocols).
{: note}

### Security and port configuration
{: #security-port-configuration}

By default, the Range application listens on all ports, which may raise concerns during security audits. However, the Range application only proxies connections from edge ports explicitly configured in CIS.

When a TCP handshake is initiated on any port of a Range application IP, the handshake completes. If the port is configured for a Range application, the connection is proxied to the origin. If no application is configured on that port, the Range application immediately ends the connection without contacting the origin.

The Range application proxies traffic to the origin only when a Range application is configured for the requested port.

## Related links
{: #range-application-information}

[Working with Range applications](/docs/cis?group=range)
