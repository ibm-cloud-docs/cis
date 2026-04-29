---

copyright:
  years: 2026
lastupdated: "2026-04-29"

keywords: range application, use cases, tls encryption, global tcp proxy

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# About Range applications
{: #about-cis-range}

Range applications extend DDoS protection, TLS encryption, and custom rule policies to TCP and UDP services, not just traditional HTTP/HTTPS traffic. These apps secure your TCP-based services beyond just web traffic and provide comprehensive security and performance benefits within IBM Cloud CIS.
{: shortdesc}

## Range application use cases
{: #about-range-use-cases}

Use cases for Range applications include:

Protecting a corporate VPN gateway
:   A company exposes a VPN for remote employees. A Range application ensures the VPN remains available during DDoS attacks while masking the origin IP.

Safeguarding NAT and network devices
:   Network Address Translations (NAT) devices manage inbound and outbound traffic. Range applications prevent abuse while maintaining reliable connectivity.

Securing a partner-accessible database
:   A MySQL or PostgreSQL database is accessed by trusted partners. Range applications allow traffic to pass securely without exposing the database server to the open internet.

Protecting collaboration and third-party integrations
:   A company integrates with collaboration platforms such as Zoom or Microsoft Teams. Because traffic originates from a known and limited set of IP ranges, a Range application allows this traffic to pass uninterrupted while preventing it from being misclassified as DDoS activity.

## Range application WAF support use cases
{: #range-application-use-cases-waf}

Range applications can be configured to operate at either Layer 7 (HTTPS) or Layer 4 (TCP), which determines whether WAF inspection is applied. The following use cases describe how WAF support varies based on the application type and traffic handling model.

### Enabling WAF inspection for HTTPS-based Range applications
{: #enable-range-app-https}

Use a Range application with type `HTTPS` (for example, port `9443`) when your application requires Layer 7 protection.

In this configuration, the TLS handshake is ended at the CIS edge. After TLS is terminated at the CIS edge, traffic is decrypted and inspected by the WAF. CIS can then re-encrypt the traffic before forwarding it to the origin, ensuring secure communication between CIS and the origin.

As a result, traffic is inspected and protected before it reaches the back-end service, while secure communication between CIS and the origin is maintained.

Example of traffic flow: `Client → HTTPS:443 → CIS (WAF inspection) → HTTPS:9443 → Origin`

### Using TCP-based Range applications without WAF support
{: #using-tcp-range-applications}

Use Range applications with `TCP` for services that require `layer 4` proxying.

In this configuration, CIS operates at the transport layer and does not stop TLS or inspect `layer 7` traffic. Because the traffic is forwarded as TCP, the payload is not decrypted and is not evaluated by the WAF.

As a result, WAF protections are not applied. Instead, CIS provides network level capabilities such as DDoS protection, IP masking, and secure TCP proxying while it forwards traffic directly to the origin.

Example of traffic flow: `Client → TCP → CIS (L4 proxy/DDoS protection) → TCP → Origin`

## Supported protocols and use cases
{: #about-choosing-protocol-on}

The application type determines how traffic is routed from the CIS edge to your origin:

* TCP or UDP: Use when you want CIS to proxy traffic directly to your origin.
* HTTP or HTTPS: Required for Edge functions or Bot Management; traffic is routed through the CIS pipeline.
* RDP: Securely connect by using Remote Desktop Protocol (RDP), with built-in DDoS protection and access control.
* SSH: Securely access remote servers over SSH without exposing your origin IP.
* Minecraft: Protect and accelerate Minecraft servers with DDoS mitigation and improved network performance.

For protocol-specific limitations, see [Known issues and limitations](/docs/cis?topic=cis-known-limitations#limitations-protocols).
{: note}

### Security and port configuration
{: #about-security-port-configuration}

By default, the Range application listens on all ports, which might raise concerns during security audits. However, the Range application only proxies connections from edge ports explicitly that are configured in CIS.

When a TCP handshake is initiated on any port of a Range application IP, CIS may complete the handshake at the edge. However, only ports explicitly configured for a Range application are proxied to the origin. Connections to other ports are immediately terminated at the edge without reaching the origin.

The Range application proxies traffic to the origin only when a Range application is configured for the requested port.
