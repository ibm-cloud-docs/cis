---

copyright:
  years: 2018, 2020
lastupdated: "2020-02-10"

keywords: DNS Security, public-key cryptography

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:term: .term}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# DNS Security
{:#dns-security}

DNS is the protocol that translates domain names such as `ibm.com` to IP addresses. Unfortunately, it has one major security flaw: the end user has no guarantee that no one tampered with the records received. For example, forged DNS records can redirect browsers to fetch content from a malicious website, add JavaScript to run on a page, or even route email to an attacker’s mail server.
{: shortdesc}

## DNSSEC, an introduction
{:#dnssec-introduction}

DNSSEC is the protocol that ensures the authenticity of DNS records. It uses public-key cryptography to let the DNS server sign records with a private key, and allow the DNS resolvers to verify the signatures with a public key

To turn on DNS Security (DNSSEC), add a DS record to your registrar. See [How do I add a DS Record to my registrar?](https://support.cloudflare.com/hc/en-us/articles/360006660072){:external}, written by our partners at Cloudflare, for a detailed guide by registrar.
