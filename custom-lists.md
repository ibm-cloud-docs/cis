---

copyright:
  years: 2020, 2025
lastupdated: "2025-07-15"

keywords: IBM Cloud, observability

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# About custom lists
{: #custom-lists}

Custom lists in CIS allow you to group related data—such as IP addresses, hostnames, or Autonomous System Numbers (ASNs) into named collections that can be reused across multiple rule expressions. These lists simplify management, improve rule clarity, and provide a more scalable way to control access and filtering.
{: shortdesc}

## What are custom lists?
{: #about-custom-lists}

A custom list is a reusable set of similar data entries. Instead of hardcoding multiple values into every rule, you can define a custom list once and reference it by name in your custom security rules. This approach is ideal for managing dynamic threat intelligence feeds, trusted traffic sources, or internal network assets.

CIS supports the following types of custom lists:

* [IP address lists](/docs/cis?topic=cis-custom-list-types&interface=ui#lists-ip-address) for grouping IPv4 or IPv6 addresses.
* [Hostname lists](/docs/cis?topic=cis-custom-list-types&interface=ui#lists-hostnames) for specifying domain names or subdomains.
* [ASN lists](/docs/cis?topic=cis-custom-list-types&interface=ui#lists-asn) for identifying network ownership by Autonomous System Numbers. 

Lists with hostnames and ASNs are available only to Enterprise customers.
{: note}

Each list type has its own properties and CSV file format as shown in [Custom list types](/docs/cis?topic=cis-custom-list-types&interface=ui). 

## Managed versus custom lists
{: #managed-vs-custom-lists}

In addition to custom lists that you define, CIS also provides managed lists, which are predefined and maintained by IBM. These lists include curated sets of known threat sources or commonly targeted IP ranges, and can be used similar to custom lists. For information on managed lists, see [Using managed lists](/docs/cis?topic=cis-using-managed-lists&interface=ui).
