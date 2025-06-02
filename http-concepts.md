---

copyright:
  years: 2020, 2025
lastupdated: "2025-06-02"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# HTTP/2 and HTTP/3 protocols
{: #http-concepts}

HTTP/2 and HTTP/3 accelerate page load times and are included in all {{site.data.keyword.cis_full}} plans. HTTP/2 is enabled by default and requires an SSL certificate at the {{site.data.keyword.cis_short_notm}} edge network. Domains on Trial plans can't disable HTTP/2.
{: shortdesc}

Browsers and web servers automatically negotiate the highest protocol available, so HTTP/3 takes precedence over HTTP/2. {{site.data.keyword.cis_short_notm}} uses HTTP/1.x only for communication between the origin web server and {{site.data.keyword.cis_short_notm}} edge.

To determine the protocol used for your connection, enter `example.com/cdn-cgi/trace` in a web browser or HTTP client, replacing `example.com` with your domain. The `http=` value in the results indicates the protocol:

* `http=h2` means that the connection used HTTP/2
* `http=http2+quic/99` indicates HTTP/3
* `http=http/1.x` indicates HTTP/1.x

## HTTP/2
{: #http-2}

HTTP/2 improves page load times through:

Connection multiplexing
:    Retrieves multiple resources over a single network connection. Responses are sent as resources become available, helping to avoid delays in page rendering.

HTTP header compression
:   Compresses headers and simplifies HTTP requests to avoid resending headers.

HTTP/2 server push
:   To improve page load speed, {{site.data.keyword.cis_short_notm}} provides additional resources for a client to cache without waiting for additional requests.

Not all browsers support HTTP/2 but use HTTP 1.x instead. Connection multiplexing is handled on a per-domain basis.
{: note}

## HTTP/3
{: #http-3}

HTTP/3 enables fast, reliable, and secure connections. By default, HTTP/3 encrypts internet transport by using QUIC, a protocol developed by Google. You can enable HTTP/3 through the Cloudflare Network application. The following methods show you how to experiment with HTTP/3.

### Using Google Chrome as your HTTP/3 client
{: #chrome-client}


To connect to your website over HTTP/3 using Chrome, first download and install the [most recent version of Chrome Canary build](https://www.google.com/chrome/canary/){: external}. Then, enable HTTP/3 support in Chrome Canary using the `--enable-quic` and `--quic-version=h3-23` [command-line arguments](https://www.chromium.org/developers/how-tos/run-chromium-with-flags){: external}.

After Chrome starts, enter your domain in the address bar. To verify the protocol version, open Chrome’s Developer Tools and go to the **Network** tab. If `http2+quic/99` doesn’t appear in the **Protocol** column, try reloading the page.

### Using cURL
{: #using-curl}


The cURL command-line tool supports HTTP/3. [Download the most recent version](https://github.com/curl/curl){: external} and follow [the instructions to enable HTTP/3 support](https://github.com/curl/curl/blob/master/docs/HTTP3.md#quiche-version){: external}.

For macOS, use Homebrew to install cURL with HTTP/3 support:

```sh
brew install --HEAD -s https://raw.githubusercontent.com/cloudflare/homebrew-cloudflare/master/curl.rb
```
{: pre}

Then, run an HTTP/3 cURL with the `--http3` command-line flag:

```sh
./curl -I https://blog.cloudflare.com/ --http3
```
{: pre}

Confirm that HTTP/3 appears in the response and that no error messages are present.
