---

copyright:
  years: 2026
lastupdated: "2026-03-26"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Network port support for the CIS proxy
{: #support-network-ports}

Network ports control how the CIS proxy handles traffic for your domain and which services can be accessed.
{: shortdesc}

## Supported ports for proxied traffic
{: #network-ports-compatible-cis-proxy}

By default, the CIS proxy only handles traffic on specific HTTP and HTTPS ports.

### Supported HTTP ports
{: #http-ports-support}

CIS supports the following HTTP ports:

* `80`
* `8080`
* `8880`
* `2052`
* `2082`
* `2086`
* `2095`

### Supported HTTPS ports
{: #https-ports-support}

CIS supports the following HTTPS ports:

* `443`
* `2053`
* `2083`
* `2087`
* `2096`
* `8443`

## Traffic on unsupported ports
{: #enable-cis-proxy-additional}

The CIS proxy does not handle traffic on ports outside the supported lists. If your application uses a different port (for example, SSH on port 22), you must configure access by [creating a Range application](/docs/cis/build/cis-review-output?topic=cis-cis-range&interface=ui) for the hostname. Range applications support traffic on all ports; however, full TCP and UDP port support is available only on the Enterprise plan.

## Block traffic on other ports
{: #block-traffic-ports}

To block traffic on ports other than `80` and `443`, use WAF rules. To restrict traffic on nonstandard ports, choose one of the following options:

* If you are using the previous version of WAF managed rules, enable `rule ID 100015 (Anomaly: Port - Non-standard port (not 80 or 443))`.
* If you are using the current WAF, enable `rule ID 664ed6fe (Anomaly: Port - Non-standard port (not 80 or 443))`. This rule is part of the CIS Managed Ruleset and is disabled by default.

The WAF [CIS Managed Ruleset](/docs/cis?group=available-managed-rulesets) includes a rule that blocks the traffic at the application layer (layer 7), preventing HTTP/HTTPS requests over nonstandard ports from reaching the origin server.

Due to the anycast network, some ports might appear open because they are used by shared services. This behavior is expected and does not mean that your application is publicly accessible.

## Control traffic by port using custom rules
{: #cis-control-traffic-by-port}

CIS allows you to control how traffic is handled on specific ports by using web application firewall (WAF) custom rules.

CIS evaluates incoming requests at the edge and exposes request attributes as fields that can be used in rule expressions. The `cf.edge.server_port` field represents the destination port on which the request is received at the CIS edge.

By using this field in custom rule expressions, you can define policies to allow, block, or challenge traffic based on the port.

### Restrict traffic by port
{: #restrict-traffic-port}

To restrict traffic on specific ports, create a custom rule that matches the `cf.edge.server_port` field. For example, to allow traffic only on standard HTTP and HTTPS ports (`80` and `443`), create a rule that blocks all other ports:

```sh
cf.edge.server_port ne 80 and cf.edge.server_port ne 443
```
{: screen}

### Match a specific port
{: #match-specific-port}

To apply rules to a specific port, match the `cf.edge.server_port` field with the required value:

```sh
cf.edge.server_port eq 8443
```
{: screen}

Custom rules are evaluated at the application layer (layer 7) and can be used to enforce port based access controls before requests reach the origin server.

For more information about available fields and expression syntax, see [Custom rules fields and expressions](/docs/cis/build/cis-review-output?topic=cis-custom-rules-fields-and-expressions).
