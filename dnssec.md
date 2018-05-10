---
copyright:
years: 2018
lastupdated: "2018-05-08"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
# DNS Security

DNS is the protocol that translates domain names such as `ibm.com` to IP addresses. Unfortunately, it has one major security flaw: the end user has no guarantee that no one tampered with the records received. For example, forged DNS records can redirect browsers to fetch content from a malicious website, add JavaScript to run on a page, or even route email to an attacker’s mail server.

DNSSEC, an introduction

DNSSEC is the protocol that ensures the authenticity of DNS records. It uses public-key cryptography to let the DNS server sign records with a private key, and allow the DNS resolvers to verify the signatures with a public key

To turn on DNS Security (DNSSEC), add a DS record to your registrar. See [How do I add a DS Record to my registrar? ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://support.cloudflare.com/hc/en-us/articles/209114378-How-do-I-add-a-DS-Record-to-my-registrar-){:new_window}, written by our partners at Cloudflare, for a detailed guide by registrar. 
