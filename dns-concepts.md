---

copyright:
  years: 2018, 2025
lastupdated: "2025-05-27"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# DNS concepts
{: #dns-concepts}

Domain Name System (DNS) underpins the web, working transparently in the background to convert human-readable website names into computer-readable numerical IP addresses. These addresses follow the [internet's RFC 1918 guidelines for IPv4 and RFC 4193 for IPv6](https://en.wikipedia.org/wiki/Private_network){: external}. In short, DNS servers match domain names, such as `ibm.com`, to their corresponding IP addresses, which most people never need to know. 
{: shortdesc}

To perform this translation, the DNS system queries a network of interconnected DNS servers across the internet. This process is somewhat like using a phone book or a map to find a specific location.

## Name servers
{: #dns-concepts-nameservers}

A name server provides services that respond to queries against a directory, translating meaningful, text-based web or host names into IP addresses.

Name server delegation occurs when a name server for a domain receives a request for a subdomain's records and responds by referring the requester to the delegated name server responsible for that subdomain. This allows decentralized management of large domains, such as `ibm.com`.

A custom domain name server lets you use the DNS provider's servers with the customized reference name of your own domain. For example, you can define your name server as `ns1.cloud.ibm.com` instead of the provider's default like `ns1.acme.com`.

## Proxying DNS records and global load balancers
{: #dns-concepts-proxying-dns-records}

{{site.data.keyword.cis_short_notm}} supports proxying for global load balancers and DNS records. When a record or load balancer is proxied, its traffic runs directly through {{site.data.keyword.cis_short_notm}}. 

Currently, DNS records of type **A**, **AAAA**, or **CNAME** can be proxied.
{: note}

### Setting proxy modes
{: #dns-proxy-modes}

Load balancers and DNS records support both DNS-only and HTTP proxy modes. You can have HTTP proxy and DNS-only domains in the same {{site.data.keyword.cis_short_notm}} instance, but the traffic routing behavior differs: traffic for records that are proxied flows through {{site.data.keyword.cis_short_notm}}, while traffic for records that are nonproxied (DNS-only mode) flows directly from the client to the origin. 

### HTTP proxy mode
{: #dns-http-proxy-mode}

In HTTP proxy mode, {{site.data.keyword.cis_short_notm}} announces IBM IP addresses externally, but protects (masks) your origin server IP addresses. The announced IP address records have an automatic TTL. Traffic flows through {{site.data.keyword.cis_short_notm}}, where all the security, performance, and reliability features, such as firewall rules and caching, are applied. The "automatic" TTL (five minutes) also reduces the number of authoritative queries made against {{site.data.keyword.cis_short_notm}}.

### DNS-only mode
{: #dns-dns-only-mode}

In DNS-only mode, records are resolved to the origin IP, and you can customize the TTL for your records. For global load balancers, {{site.data.keyword.cis_short_notm}} serves the addresses of the healthy origin servers directly, but relies on DNS resolvers respecting the short TTL to requery the {{site.data.keyword.cis_short_notm}} DNS for an updated list of healthy addresses.

In DNS-only mode, none of the {{site.data.keyword.cis_short_notm}} security, reliability, and performance features are applied.
{: important}

## Root record CNAME flattening
{: #dns-concepts-root-record-cname-flattening}

With the "CNAME Flattening" feature, {{site.data.keyword.cis_short_notm}} allows root records to overcome the IETF RFC restriction that if a root record is a CNAME, it can't have any other records for that domain. {{site.data.keyword.cis_short_notm}} authoritative servers overcome this restriction by returning the A records corresponding to the CNAME target instead of returning the CNAME itself, effectively hiding the CNAME. This technique allows other records, such as MX records, to be added to the domain even though the root record is a CNAME.

## Secure DNS
{: #dns-concepts-secure-dns}

DNSSEC is a technology that digitally "signs" DNS data so you can be confident it is valid. To eliminate vulnerability from the internet, DNSSEC must be deployed at each step in the lookup process—from the root zone to the final domain name (for example, `www.icann.org`).
