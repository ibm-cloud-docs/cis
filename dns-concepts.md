---

copyright:
  years: 2018, 2025
lastupdated: "2025-02-24"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# DNS concepts
{: #dns-concepts}

This document contains some concepts and definitions that are related to the internet's domain name system (DNS) and how it affects your {{site.data.keyword.cis_full}} ({{site.data.keyword.cis_short_notm}}) deployment.
{: shortdesc}

The Domain Name System (DNS) underpins the web. It works transparently in the background, converting human-readable website names into computer-readable, numerical IP addresses that follow the [internet's RFC 1918 guidelines for IPv4 and RFC 4193 for IPv6](https://en.wikipedia.org/wiki/Private_network){: external}. In short, DNS servers match domain names, such as `ibm.com`, to their associated IP addresses, which most people do not need to know.

The DNS system looks up this IP address and hostname information on a network of linked DNS servers across the internet, similarly to how people might look for some place using a phone book or a map.

## Name servers
{: #dns-concepts-nameservers}

A **name server** implements services that provide responses to queries against a directory service. It translates meaningful, text-based web or host identifiers into IP addresses.

**Name server delegation** takes place when a name server for a domain receives a request for a subdomain's records and responds with the name server's reference to the delegate server. This capability allows you to decentralize the management of a large domain (such as `ibm.com`).

A **custom domain name server** allows you to use the DNS provider's servers with the customized reference name of your own domain. For example, you can define your name server to be `ns1.cloud.ibm.com` instead of `ns1.acme.com`.

## Secure DNS
{: #dns-concepts-secure-dns}

**DNSSec** is a technology to digitally 'sign' DNS data so you know it is valid. To eliminate vulnerability from the internet, DNSSec must be deployed at each step in the lookup, from root zone to final domain name (for example, www.icann.org).

## Root record CNAME flattening
{: #dns-concepts-root-record-cname-flattening}

IBM {{site.data.keyword.cis_short_notm}} supports a the "CNAME Flattening" feature. With this method, root records can overcome the IETF RFC restriction that if a root record is a CNAME, it can't have any other records for that domain. {{site.data.keyword.cis_short_notm}} Authoritative servers overcome this restriction by returning the A records corresponding to the CNAME target instead of returning the CNAME itself, effectively hiding the CNAME. This technique allows other records such as MX records to be added to the domain, even though the root record is a CNAME.

## Proxying DNS records and global load balancers
{: #dns-concepts-proxying-dns-records}

IBM {{site.data.keyword.cis_short_notm}} supports proxying for global load balancers and DNS records. When a record or load balancer is proxied, it means that its traffic runs directly through {{site.data.keyword.cis_short_notm}}.

Currently, DNS records of type **A**, **AAAA**, or **CNAME** can be proxied.
{: note}

### Setting proxy modes
{: #dns-proxy-modes}

Load balancers and DNS records support both DNS-only and HTTP proxy modes. You can have HTTP proxy and DNS-only domains in the same {{site.data.keyword.cis_short_notm}} instance, but the traffic routing behavior differs as follows:

* Traffic for records that are proxied flows through {{site.data.keyword.cis_short_notm}}.
* Traffic for records that are nonproxied (DNS-only mode) flows directly from the client to the origin.

### HTTP proxy mode
{: #dns-http-proxy-mode}

In HTTP proxy mode, {{site.data.keyword.cis_short_notm}} announces IBM IP addresses externally, but protects (masks) your origin server IP addresses. The announced IP address records have an automatic TTL.

Using HTTP proxy mode offers the following benefits:

* Traffic flows through {{site.data.keyword.cis_short_notm}} where all the security, performance, and reliability features such as firewall rules and caching, are applied.
* The "automatic" TTL (five minutes) reduces the number of authoritative queries that are made against {{site.data.keyword.cis_short_notm}}.

### DNS-only mode
{: #dns-dns-only-mode}

In DNS-only mode, records are resolved to the origin IP and you can customize the TTL for your records. For global load balancers, {{site.data.keyword.cis_short_notm}} serves the addresses of the healthy origin servers directly, but relies on DNS resolvers respecting the short TTL to requery the {{site.data.keyword.cis_short_notm}} DNS for an updated list of healthy addresses.

In DNS-only mode, none of the {{site.data.keyword.cis_short_notm}} security, performance, and reliability features are applied.
{: important}
