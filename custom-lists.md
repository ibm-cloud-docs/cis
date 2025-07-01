---

copyright:
  years: 2025
lastupdated: "2025-07-01"

keywords: custom lists

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# About custom lists
{: #custom-lists}

Custom lists in CIS allow you to group related data—such as IP addresses, hostnames, or Autonomous System Numbers (ASNs) into named collections that can be reused across multiple rule expressions. These lists simplify management, improve rule clarity, and provide a more scalable way to control access and filtering.
{: shortdesc}

## What are custom lists?
{: about-custom-lists}

A custom list is a reusable set of similar data entries. Instead of hardcoding multiple values into every rule, you can define a custom list once and reference it by name in your custom security rules. This approach is ideal for managing dynamic threat intelligence feeds, trusted traffic sources, or internal network assets.

CIS supports the following types of custom lists:

* [IP address lists](/docs/cis?topic=cis-custom-list-types&interface=ui#lists-ip-address) for grouping IPv4 or IPv6 addresses.
* [Hostname lists](/docs/cis?topic=cis-custom-list-types&interface=ui#lists-hostnames) for specifying domain names or subdomains.
* [ASN lists](/docs/cis?topic=cis-custom-list-types&interface=ui#lists-asn)  for identifying network ownership by Autonomous System Numbers. 

[NEED TO ADD?]{: tag-purple} Lists with hostnames and ASNs are available only to Enterprise customers. Refer to [Availability](https://developers.cloudflare.com/waf/tools/lists/#availability) for details.
{: note}

Each list type has its own properties and CSV file format as shown in [Custom list types](/docs/cis?topic=cis-custom-list-types&interface=ui). 

## Using custom lists in rules
{: #using-custom-lists-in-rules}

Once you’ve created a custom list, you can use it in your rule expressions to match incoming traffic based on the list’s contents. Custom lists are used with the `in` operator as shown:

```bash
<FIELD> in $<LIST_NAME>
```
{: pre}

This rule checks whether the specified field matches any item in the custom list.

The fields that you can use vary according to the list type:

| List type	 | Available fields |
| ------------ | ------------------- |
| IP address | Fields with type `IP address` listed in the [Fields reference](/docs/cis?topic=cis-custom-rules-fields-and-expressions#custom-rule-fields) |
| Hostname | `http.host` |
| ASN | `ip.src.asnum` |
{: caption="Available custom list type" caption-side="bottom"}

You can apply custom lists in a variety of use cases, such as:

* Blocking or allowing traffic from specific IP ranges
* Filtering requests by known domains
* Prioritizing routing for traffic from specific ISPs or regions

For details on how to build rule expressions with custom lists, see [Integrating lists in rules](/docs/cis?topic=cis-integrating-lists-in-rules). 

## Managed versus custom lists
{: #managed-vs-custom-lists}

In addition to custom lists that you define, CIS also provides managed lists, which are predefined and maintained by IBM. These lists include curated sets of known threat sources or commonly targeted IP ranges, and can be used similar to custom lists. For information on managed lists, see [Using managed lists](/docs/cis?topic=cis-managed-lists&interface=ui).
