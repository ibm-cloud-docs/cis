---

copyright:
  years: 2026
lastupdated: "2026-08-05"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Origin rules settings
{: #origin-available-settings}

You can configure the following settings in an origin rule.

## Host header
{: #host-header-settings}

The host header setting allows you to rewrite the HTTP `Host` header of incoming requests. The Host header identifies the website or application that the request is intended for on the destination server.

Use this setting when your content is hosted on a third-party server that accepts only host headers that match its own server name. For example, you can update incoming requests from `Host: example.com` to `Host: thirdpartyserver.example.net`.

### Considerations
{: #host-header-considerations}

* In most cases, when you rewrite the HTTP `Host` header, you must also configure a DNS record override. The host header override updates only the header value; the DNS record override handles the re-routing of the request.

* When an origin rule performs a host header override, the Server Name Indication (SNI) value of the original request is also updated to the same value. To set an SNI value that is different from the host header value, add an SNI override in the same origin rule, or create a separate origin rule.

## Server Name Indication
{: #sni-settings}

The Server Name Indication(SNI) setting allows you to override the SNI value of a request. SNI is an extension to the TLS protocol that enables the server to present the correct certificate for a given hostname during the TLS handshake.

### Considerations
{: #sni-considerations}

* The new SNI value must be a valid hostname on the same CIS account, though it can belong to a different zone.
* Only static values are supported when you override SNI.
* An SNI override takes precedence over SNI rewrites of custom origins when you use CIS for SaaS configurations.

## DNS record
{: #dns-record-settings}

The DNS record setting allows you to override the resolved hostname of incoming requests, which determines which origin server receives the request. This is also referred to as a resolve override.

Use this setting when you serve an application from a specific URL path — for example, `mydomain.com/app` and the application is hosted on a different server or by a third party. A DNS record override redirects requests for that endpoint to the appropriate server.

### Considerations
{: #dns-considerations}

* You must specify a valid hostname in the DNS record override. The hostname must exist on the same CIS account, though it can belong to a different zone. You can configure a CNAME, A, or AAAA record that points to a third-party hostname or IP address, either proxied or unproxied.
* In most cases, when you configure a DNS record override, you must also configure a host header override. The DNS record override handles the re-routing of the request; the host header override updates the `Host` HTTP header value. Defining a host header override also updates the SNI value of the original request to the same value. To set a different SNI value, add an SNI override in the same origin rule or create a separate origin rule.

The following examples show DNS records that configure a `resolve.example.com` hostname to point to an external hostname and IP address.

| DNS record type | Name | Target | IPv4 address | TTL | Proxy status |
| --------------- | ---- | ---- | ------ | ------------ | --- | ------------ |
| `CNAME` record | `resolve.example.com` | `domain.s3.amazonaws.com` | - | `Auto` | Proxied |
| `A` record | `resolve.example.com` | - | `203.0.113.1` | `Auto` | Proxied |
{: caption="DNS record type exmples" caption-side="bottom"}

## Destination port
{: #destination-port-settings}

The Destination port setting allows you to override the destination port of a request, redirecting incoming requests to a port that you specify.

For example, you can override the destination port for requests to `mydomain.com`, so that they are served by the application that runs on port 9000 (`mydomain.com:9000`).

The destination port must be between 1 and 65,535.
