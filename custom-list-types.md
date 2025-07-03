---

copyright:
  years: 2025
lastupdated: "2025-07-03"

keywords: custom lists

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Custom list types
{: #custom-list-types}

CIS supports the following custom list types:

* Lists with IP addresses (also known as IP lists)
* Lists with hostnames
* Lists with ASNs (autonomous system numbers)

Lists with hostnames and ASNs are only available to Enterprise customers. For more information, see [List availability](/docs/cis?topic=cis-lists#lists-availability).
{: note}

For more information about lists, see [About lists](/docs/cis?topic=cis-lists).

## Lists with IP addresses (IP lists)
{: #lists-ip-address}

List items in custom lists with IP addresses must be in one of the following formats:

- Individual IPv4 addresses
- IPv4 CIDR ranges with a prefix from `/8` to `/32`
- IPv6 CIDR ranges with a prefix from `/12` to `/64`

You can combine individual addresses and CIDR ranges in the same list.
{: note}

To specify an IPv6 address, enter it as a CIDR range with a `/64` prefix, the largest supported prefix for IPv6 CIDR ranges.

For example, instead of `2001:db8:6a0b:1a01:d423:43b9:13c5:2e8f`, enter one of the following:

- `2001:db8:6a0b:1a01:0000:0000:0000:0000/64`
- `2001:db8:6a0b:1a01::/64` (using the [double colon notation](https://tools.ietf.org/html/rfc5952#section-4.2){: external})

The IPv6 address topology describes the last 64 bits as the host identifier. Matching on a `/128` prefix would identify a specific IPv6 address, but not the host in general. It would be possible for an attacker to change their specific IPv6 address from a single machine.

You can use uppercase or lowercase characters for IPv6 addresses in lists. However, when you save the list, uppercase characters are converted to lowercase.

CSV file format 

When uploading items to a custom list with IP addresses using a CSV file, use the following file format (enter one item per line):

```text
<IP_ADDRESS_1>,<DESCRIPTION>
<IP_ADDRESS_2>
```

The `<DESCRIPTION>` field is optional.

## Lists with hostnames
{: #lists-hostnames}

Available to Enterprise customers.
{: note}

List items in custom lists with hostnames must be Fully Qualified Domain Names (FQDNs). An item might contain a `*` prefix/subdomain wildcard, which must be followed by a `.` (period). An item cannot include a scheme (for example, `https://`) or a URL path.

For example, the following entries would be valid for a custom list with hostnames:

- `example.com`
- `api.example.com`
- `*.example.com`

However, `example.com/path/subfolder` would not be a valid entry.

You can add any valid hostname (a valid FQDN) to a custom list with hostnames. The hostnames do not need to belong to the current CIS account.

CSV file format 

When uploading items to a custom list with hostnames using a CSV file, use the following file format:

```text
<HOSTNAME_1>,<DESCRIPTION>
<HOSTNAME_2>
```

The `<DESCRIPTION>` field is optional.

## Lists with ASNs
{: #lists-asn}

Available to Enterprise customers.
{: note}

List items in custom lists with ASNs must be integer values.

For example, the following entries would be valid for a list with ASNs:

- `1`
- `13335`
- `64512`

CSV file format 

When uploading items to a custom list with ASNs using a CSV file, use the following file format:

```text
<ASN_1>,<DESCRIPTION>
<ASN_2>
```

The `<DESCRIPTION>` field is optional.
