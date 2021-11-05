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
{: #http-concepts}

HTTP/2 and HTTP/3 accelerate page load and are included in all {{site.data.keyword.cis_full}} plans.  HTTP/2 is enabled by default and requires an SSL certificate at the {{site.data.keyword.cis_short_notm}} edge network. Domains on Trial plans cannot disable HTTP/2.
{: shortdesc}

A browser and web server automatically negotiate the highest protocol available, so HTTP/3 takes precedence over HTTP/2.  {{site.data.keyword.cis_short_notm}} only uses HTTP/1.x between the origin web server and {{site.data.keyword.cis_short_notm}}.

To determine the protocol used for your connection, enter `example.com/cdn-cgi/trace` from a web browser or client and replace `example.com` with your domain name. If `http=h2` appears in the results that are returned, the connection occurred over HTTP/2. Other possible values are `http=http2+quic/99` for HTTP/3, and `http=http/1.x` for HTTP/1.x.

## HTTP/2
{: #http-2}

HTTP/2 improves page load times through:

* Connection multiplexing - Retrieves multiple resources in a single network request. Responses are sent when resources are available to avoid slowing page rendering.
* HTTP header compression - Compresses headers and simplifies HTTP requests to avoid resending headers.
* HTTP/2 Server Push - To improve page load speed, {{site.data.keyword.cis_short_notm}} provides additional resources for a client to cache without waiting for additional requests.

Not all browsers support HTTP/2 and use HTTP 1.x instead. Connection multiplexing is on a per-domain basis.
{: note}

## HTTP/3
{: #http-3}

HTTP/3 enables fast, reliable, and secure connections.  HTTP/3 encrypts internet transport by default using a protocol from Google called QUIC. Enable HTTP/3 via the Cloudflare Network app. Use the following methods to experiment with HTTP/3.

### Using Google Chrome as your HTTP/3 client
{: #chrome-client}

To use Chrome to connect to your website over HTTP/3, first download and install the [latest Canary build](https://www.google.com/chrome/canary/){: external}. Then, enable HTTP/3 support in Chrome Canary using the  `--enable-quic` and `--quic-version=h3-23` [command-line arguments](https://www.chromium.org/developers/how-tos/run-chromium-with-flags){: external}.

After Chrome starts, type your domain in the address bar. Check the protocol version using the **Network** tab in Chrome’s Developer Tools. If `http2+quic/99` doesn’t appear in the **Protocol** column when connecting to your domain, try reloading the page.

### Using cURL
{: #use-curl}

The cURL command-line tool supports HTTP/3.  [Download the latest version](https://github.com/curl/curl){: external} and follow [the instructions to enable HTTP/3 support](https://github.com/curl/curl/blob/master/docs/HTTP3.md#quiche-version){: external}.

For macOS, use Homebrew to install cURL with HTTP/3 support:

```sh
brew install --HEAD -s https://raw.githubusercontent.com/cloudflare/homebrew-cloudflare/master/curl.rb
```
{: pre}

Then, perform an HTTP/3 cURL with the `--http3` command-line flag:

```sh
./curl -I https://blog.cloudflare.com/ --http3
```
{: pre}

Confirm HTTP/3 appears in the response and that there were no error messages.
