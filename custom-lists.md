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

A custom list contains one or more items of the same type (for example, IP addresses, hostnames, or ASNs) that you can reference collectively, by name, in rule expressions.
{: shortdesc}

CIS supports the following custom list types:

* [Lists with IP addresses](/docs/cis?topic=cis-custom-list-types&interface=ui#lists-ip-address) (also known as IP lists)
* [Lists with hostnames](/docs/cis?topic=cis-custom-list-types&interface=ui#lists-hostnames)
* [Lists with ASNs](/docs/cis?topic=cis-custom-list-types&interface=ui#lists-asn)(autonomous system ↗ numbers)

[NEED TO ADD?]{: tag-purple} Lists with hostnames and ASNs are available only to Enterprise customers. Refer to [Availability](https://developers.cloudflare.com/waf/tools/lists/#availability) for details.
{: note}

Each type has its own properties and CSV file format as shown in [Custom list types](/docs/cis?topic=cis-custom-list-types&interface=ui). 

For information on lists managed by CIS, such as Managed IP lists, see [Using managed lists](/docs/cis?topic=cis-managed-lists&interface=ui).

## Using custom lists
{: #using-custom-lists}

Use custom lists in rule expressions with the `in` operator and with a field supported by the custom list:

```bash
<FIELD> in $<LIST_NAME>
```
{: pre}

The fields that you can use vary according to the list item type:

| List item type	 | Available fields |
| ------------ | ------------------- |
| IP address | Fields with type `IP address` listed in the [Fields reference](/docs/cis?topic=cis-custom-rules-fields-and-expressions#custom-rule-fields) |
| Hostname | `http.host` |
| ASN | `ip.src.asnum` |
{: caption="Available custom list type" caption-side="bottom"}

For more information and examples,see [Integrating lists in rules](/docs/cis?topic=cis-integrating-lists-in-rules).
{: note}
