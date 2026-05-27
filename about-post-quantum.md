---

copyright:
  years: 2026
lastupdated: "2026-05-27"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# About post-quantum cryptography
{: #cis-pqc-overview}

Post‑quantum cryptography (PQC) is cryptographic mechanisms that are designed to remain secure against adversaries equipped with large‑scale quantum computers. These algorithms aim to protect encrypted data against future attacks that might break the widely used public‑key cryptography.

One of the primary drivers for PQC adoption is the [harvest‑now, decrypt‑later](https://en.wikipedia.org/wiki/Harvest_now,_decrypt_later){: external} threat model, in which attackers collect encrypted traffic to decrypt when quantum computing becomes practical.

Edge security and content delivery platforms, including CIS, play a key role in mitigating this risk by securing data in transit through modern TLS protocols and cryptographic best practices.

## PQC and TLS in CIS
{: #pqc-tls-cis}

CIS secures customer traffic with TLS 1.3, which provides the cryptographic foundation necessary for post‑quantum adoption. TLS 1.3 improves both security and performance compared to earlier TLS versions and enables more flexible cryptographic negotiation during the handshake.

### Cryptographic building blocks of TLS
{: #crypto-build-blocks-tls}

A secure TLS session relies on three distinct classes of cryptographic algorithms:
1. **Symmetric encryption algorithms**: Used to encrypt and decrypt data, ensuring confidentiality and integrity.
1. **Key agreement mechanisms**: Allows the client and server to establish shared session keys securely. Classical key exchange methods (such as elliptic‑curve‑based algorithms) are vulnerable to quantum attacks, making it a primary focus of PQC adoption efforts.
1. **Digital signature algorithms**: Signature algorithms authenticate servers through TLS certificates. These algorithms also need to evolve toward post‑quantum alternatives to ensure long‑term trust in a quantum‑capable future.

As a result, PQC transition efforts primarily impact key agreement and signature components, rather than data encryption itself.

### Hybrid key agreement: a practical transition model
{: #hybrid-key-agreement}

To balance security, compatibility, and operational stability, the industry widely adopts a hybrid key agreement approach. In this model, a TLS session establishes keys using:
* A well‑understood classical key agreement algorithm, and
* An additional post‑quantum key encapsulation mechanism (KEM)

Both mechanisms contribute cryptographic material to the final session key. This ensures that the connection remains secure even if one class of algorithm becomes vulnerable in the future.

CIS uses this standards‑aligned approach for connections from CIS to customer origin servers, enabling post‑quantum protection without requiring immediate, disruptive changes from clients.

## Post‑quantum connectivity from CIS to origin servers
{: #pqc-from-cis-to-origin}

CIS supports post‑quantum hybrid key agreement for securing connections between the CIS edge and customer origin servers. This protects backend traffic from long‑term cryptographic risks and aligns CIS with industry efforts to adopt quantum‑resistant primitives.

Post‑quantum key material is typically larger than classical cryptographic parameters. As a result:
* TLS handshake messages might increase in size
* Initial handshake messages might span multiple network packets.

Although this behavior is defined in the TLS 1.3 specification, it can reveal implementation issues in legacy infrastructure such as middle boxes, firewalls, and load balancers that incorrectly assume fixed message sizes. These considerations are relevant for origin connectivity, where customer‑controlled infrastructure plays a role, and factored into architecture and testing strategies.
