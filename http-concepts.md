---

copyright:
  years: 2020
lastupdated: "2020-12-09"

keywords:

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"} 
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:term: .term}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic”}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# HTTP concepts
{:#http-concepts}

HTTP/2 accelerates page load and are included in all {{site.data.keyword.cis_full}} plans.  HTTP/2 is enabled by default and requires an SSL certificate at the {{site.data.keyword.cis_short_notm}} edge network. Domains on Trial plans cannot disable HTTP/2.
{:shortdesc}

A browser and web server automatically negotiate the highest protocol available, so HTTP/3 takes precedence over HTTP/2.  {{site.data.keyword.cis_short_notm}} only uses HTTP/1.x between the origin web server and {{site.data.keyword.cis_short_notm}}. HTTP/3 is not currently supported by {{site.data.keyword.cis_short_notm}}.

To determine the protocol used for your connection, enter `example.com/cdn-cgi/trace` from a web browser or client and replace `example.com` with your domain name. If `http=h2` appears in the results that are returned, the connection occurred over HTTP/2. Other possible values are `http=http2+quic/99` for HTTP/3, and `http=http/1.x` for HTTP/1.x.

## HTTP/2
{:#http-2}

HTTP/2 improves page load times through:

- Connection multiplexing - Retrieves multiple resources in a single network request. Responses are sent when resources are available to avoid slowing page rendering.
- HTTP header compression - Compresses headers and simplifies HTTP requests to avoid resending headers.
- HTTP/2 Server Push - To improve page load speed, {{site.data.keyword.cis_short_notm}} provides additional resources for a client to cache without waiting for additional requests.

Not all browsers support HTTP/2 and use HTTP 1.x instead. Connection multiplexing is on a per-domain basis.
{:note}

