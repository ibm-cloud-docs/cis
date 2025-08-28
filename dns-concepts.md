---

copyright:
  years: 2018, 2025
lastupdated: "2025-08-28"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# DNS behavior and resolution logic
{: #dns-concepts}

The Domain Name System (DNS) underpins the web, working transparently in the background to convert human-readable website names into computer-readable numerical IP addresses. These addresses follow the [internet's RFC 1918 guidelines for IPv4 and RFC 4193 for IPv6](https://en.m.wikipedia.org/wiki/Private_network){: external}. In short, DNS servers match domain names, such as `ibm.com`, to their corresponding IP addresses, which most people never need to know.
{: shortdesc}

To perform this translation, the DNS system queries a network of interconnected DNS servers across the internet. This process is similar to using a phone book or a map to find a specific location.

## Name servers
{: #dns-concepts-nameservers}

A name server provides services that respond to queries against a directory, translating meaningful, text-based web or hostnames into IP addresses.

Name server delegation occurs when a domain's name server gets a request for a subdomain's records and responds by referring the requester to the delegated name server that manages the subdomain. This process allows decentralized management of large domains, such as `ibm.com`.

With a custom domain name server, you can use the DNS provider's servers with the customized reference name of your own domain. For example, you can define your name server as `ns1.cloud.ibm.com` instead of the provider's default like `ns1.acme.com`.

## Proxying DNS records and global load balancers
{: #dns-concepts-proxying-dns-records}

{{site.data.keyword.cis_short_notm}} supports proxying for global load balancers and DNS records. When a record or load balancer is proxied, its traffic runs directly through {{site.data.keyword.cis_short_notm}}.

Currently, DNS records of type **A**, **AAAA**, or **CNAME** can be proxied. For more information, see [DNS record types](/docs/cis?topic=cis-set-up-your-dns-for-cis&loginMethod=federated#adding-dns-records).
{: note}

### Setting proxy modes
{: #dns-proxy-modes}

Load balancers and DNS records support both DNS-only and HTTP proxy modes. You can have HTTP proxy and DNS-only domains in the same {{site.data.keyword.cis_short_notm}} instance, but the traffic routing behavior differs: traffic for records that are proxied flows through {{site.data.keyword.cis_short_notm}}, while traffic for records that are nonproxied (DNS-only mode) flows directly from the client to the origin.

### HTTP proxy mode
{: #dns-http-proxy-mode}

In HTTP proxy mode, {{site.data.keyword.cis_short_notm}} announces IBM IP addresses externally, but protects (masks) your origin server IP addresses. The announced IP address records have an automatic TTL. Traffic flows through {{site.data.keyword.cis_short_notm}}, where all the security, performance, and reliability features, such as firewall rules and caching, are applied. The "automatic" TTL (five minutes) also reduces the number of authoritative queries that are made against {{site.data.keyword.cis_short_notm}}.

### DNS-only mode
{: #dns-dns-only-mode}

In DNS-only mode, the records are resolved to the origin IP, and you can customize the TTL for your records. For global load balancers, {{site.data.keyword.cis_short_notm}} serves the addresses of the healthy origin servers directly, but relies on DNS resolvers, which respect the short TTL, to requery {{site.data.keyword.cis_short_notm}} DNS for an updated list of healthy addresses.

In DNS-only mode, none of the {{site.data.keyword.cis_short_notm}} security, reliability, and performance features are applied.
{: important}

## Root record CNAME flattening
{: #dns-concepts-root-record-cname-flattening}

The "CNAME flattening" feature in {{site.data.keyword.cis_short_notm}} makes it possible for the root records to bypass the IETF RFC restriction. This restriction states that if a root record is a CNAME, it can't have any other records for that domain. {{site.data.keyword.cis_short_notm}} authoritative servers bypass this restriction by returning the `A records` corresponding to the CNAME target instead of returning the CNAME itself, effectively hiding the CNAME. This technique allows other records, such as MX records, to be added to the domain even though the root record is a CNAME.

## Secure DNS
{: #dns-concepts-secure-dns}

DNSSEC is a technology that digitally "signs" DNS data so you can be confident that it is valid. To eliminate vulnerability from the internet, DNSSEC must be deployed at each step in the lookup process, from the root zone to the final domain name (for example, `www.icann.org`).

## Batch DNS record changes
{: #batch-dns-records}

{{site.data.keyword.cis_short_notm}} supports batch DNS record changes, allowing you to update multiple zone records in a single action. This approach reduces manual effort and simplifies domain management tasks, such as migrations, environment setups, or automation workflows. While the {{site.data.keyword.cis_short_notm}} console supports individual changes, batch operations are best performed by using API.

The [Batch DNS records](/apidocs/cis#create-dns-record-0fa00f) API endpoint allows you to perform multiple `DELETES`, `PATCHES`, `PUTS`, and `POSTS` in a single request.

Operations that are included in the `/batch` request body are always processed in the following order:
1. Deletes
1. Patches
1. Puts
1. Posts

Within each operation type, individual record changes are applied in the order in which they are processed. If any of the operations fail, no changes are applied, and the API returns the first error that it encounters.

### Key considerations for batch DNS records
{: #key-considerations-batch-dns}

When specifying each operation in the /batch request body, follow these guidelines for required fields and how unspecified fields are handled:

* `Deletes`: Only the `id` field is required for each record object. You can include additional fields, such as `name` for clarity, but all other fields are ignored.

* `Patches`: Apart from each record `id`, specify the fields that you want to update. All unspecified fields remain the same.

* `Puts`: Specify the `id`, `content`, `name`, and `type` of each record. Also specify any other fields that you want to set to non-default values. Any unspecified fields assume the default value for each [Record type](/docs/cis?topic=cis-set-up-your-dns-for-cis#adding-dns-records). This operation works as an overwrite, so all fields in a record are always affected.

* `Posts`: Used to create new records. The `id` field is not required. For field definitions, see the [Create DNS Record](/apidocs/cis#create-dns-record-e2ec84) endpoint and select the appropriate record type from the request body specification.

#### Example request
{: #example-request}

In this example, the proxied field for the first record that is listed in the `puts` assumes the default value `false`.

```json
{
  "deletes": [
    {
      "id": "023e105f4ecef8ad9ca31a8372d0c353"
    }
  ],
  "patches": [
    {
      "id": "023e105f4ecef8ad9ca31a8372d0c353",
      "comment": "Domain verification record",
      "name": "example.com",
      "proxied": true,
      "settings": {},
      "tags": [],
      "ttl": 3600,
      "content": "198.51.100.4",
      "type": "A"
    }
  ],
  "posts": [
    {
      "comment": "Domain verification record",
      "name": "example.com",
      "proxied": true,
      "settings": {},
      "tags": [],
      "ttl": 3600,
      "content": "198.51.100.4",
      "type": "A"
    }
  ],
  "puts": [
    {
      "id": "023e105f4ecef8ad9ca31a8372d0c353",
      "comment": "Domain verification record",
      "name": "example.com",
      "proxied": true,
      "settings": {},
      "tags": [],
      "ttl": 3600,
      "content": "198.51.100.4",
      "type": "A"
    }
  ]
}
```
{: codeblock}
