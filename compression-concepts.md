---

copyright:
  years: 2021, 2025
lastupdated: "2025-05-29"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Compression and optimization
{: #compression-concepts}

{{site.data.keyword.cis_full}} uses GZIP and Brotli compression for various content types to improve page load times. Compression is applied based on the browser’s `User-Agent`.
{: shortdesc}

If you're already using , CIS accepts your settings as long as the appropriate headers are passed in the server response.

CIS only supports  when communicating with your origin server, and can deliver content that is:

* Compressed using  or Brotli
* Uncompressed

CIS’s reverse proxy can convert between compressed and uncompressed formats. For example, it can fetch GZIP-compressed content from your origin and serve it uncompressed to clients. This process occurs independently of caching.

CIS removes the `Accept-Encoding` header and does not honor it.
{: note}

## Compressed content types
{: #what-gets-compressed}

In addition to serving stale content and minifying CSS, JS, and HTML, CIS compresses responses with GZIP or Brotli for compatible browsers. CIS returns GZIP or Brotli-encoded responses to compatible clients and browsers for the following content types:

```sh
text/html
text/richtext
text/plain
text/css
text/x-script
text/x-component
text/x-java-source
text/x-markdown
application/javascript
application/x-javascript
text/javascript
text/js
image/x-icon
image/vnd.microsoft.icon
application/x-perl
application/x-httpd-cgi
text/xml
application/xml
application/xml+rss
application/vnd.api+json
application/x-protobuf
application/json
multipart/bag
multipart/mixed
application/xhtml+xml
font/ttf
font/otf
font/x-woff
image/svg+xml
application/vnd.ms-fontobject
application/ttf
application/x-ttf
application/otf
application/x-otf
application/truetype
application/opentype
application/x-opentype
application/font-woff
application/eot
application/font
application/font-sfnt
application/wasm
application/javascript-binast
application/manifest+json
application/ld+json
```
{: codeblock}

If you don't want a particular response from your origin to be encoded, you can set **cache-control: no-transform** to disable encoding at your origin web server.
{: note}

### Enabling Brotli compression
{: #enable-brotli-compression}


1. Log in to your CIS account.
1. Choose the appropriate domain.
1. Click the Performance tab.
1. Click the Advanced tab.
1. Toggle the Brotli switch to `On`.

## Minification for HTML, JavaScript, and CSS
{: #html-js-css}

CIS uses **Minify web content** to remove all unnecessary characters from HTML, JavaScript and CSS files, without affecting their functionality.

* CSS and JavaScript minification operates on cached CSS and JS files only. 
* After CIS returns a cache HIT for the file, it is returned to browsers in minified form, which allows CIS to deliver a complete minification result. 
* To apply minification changes, purge your CIS cache.

## Image size optimization compression
{: #polish-compression}

CIS optimizes images cached in its edge network by stripping metadata and applying either lossy or lossless compression to speed up delivery. Off-site images are not optimized.

Image size optimization compression is only available as a page rule in the console. The domain level setting is available in the CLI.
{: note}

### Image size optimization compression options
{: #polish-comp-opt}

The following sections detail the image size optimization compression options.

#### Lossless
{: #lossless}

* Strips most metadata (for example, EXIF data).
* Retains all visual detail.
* Decompressed output matches the original image.

#### Lossy
{: #lossy}

* Strips metadata and reduces image size by approximately 15%.
* Some original data is permanently lost.
* For PNGs, results are effectively the same as lossless. 

With Lossless and Lossy modes attempt to remove as much metadata as possible, but complete removal is not guaranteed due to factors like caching.

#### WebP
{: #webp}

* WebP provides superior compression:
   * Approximately 26% smaller than PNG (lossless)
   * 25–34% smaller than JPEG (lossy)
* CIS creates and caches WebP versions.
* WebP is served only if:
   * The browser's `Accept` header includes WebP.
   * The compressed image is significantly smaller than the lossy or lossless version.

Supported `Accept` header example:

```sh
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
```
{: pre}

Currently, WebP is only supported in Firefox, Google Chrome, and Opera browsers.

Disable WebP at your origin to avoid caching issues with browsers that don’t support WebP.
{: important}

### Verifying that image size optimization is active
{: #verify-polish}

Activate image size optimization by using a [page rule](/docs/cis?topic=cis-use-page-rules#page-rules-performance) or [CLI domain settings](/docs/cis?topic=cis-cis-cli#domain-settings).

CIS adds the following headers to optimized images:

```sh
cf-bgj: imgq:85

cf-polished: qual=85, origFmt=jpeg, origSize=95005

cf-cache-status: HIT
```
{: codeblock}

The `cf-bgj` header confirms that CIS applied image size optimization and returns the image quality setting (`imgq`). The `cf-polished` header represents the image size optimization status and returns the image quality setting (`qual`) and original size (`origSize`). The `cf-cache-status` confirms that the image was cached and image size optimization can be applied.

WebP conversion doesn't change the image URL. The `Content-Type HTTP` header tells the browser the original format of an image.

### Common Cf-Polished statuses
{: #common-polished-status}

The following table lists common Cf-Polished statuses and how to troubleshoot them. If no Cf-Polished header is returned, try to use single-file cache purge to purge the image.

| Status | Definition | Recommendation |
|--------|------------|----------------|
|`input_too_large`| Image is too large or complex to process and needs a lower resolution.| Use PNG or JPEG images that are less than 1,000 px and 10 MB.|
|not_compressed or not_needed|Image was fully optimized at the origin server and no compression was applied.| |
|`webp_bigger`|Polish attempted to convert to WebP, but the image was optimized at the origin server and/or was created with a low quality setting.|Because the WebP version doesn’t exist, the status is set on the PNG or JPEG version of the response.|
|`cannot_optimize` or `internal_error`|Image is corrupted or incomplete at the origin server. |Upload a new version of the image to the origin server.|
|`format_not_supported`|Image format isn't supported (for example, BMP, TIFF) and/or the origin server is using extra optimization software that is not compatible with Polish.|Try converting the input image to a web-compatible format (for example, PNG, JPEG) and/or disabling any extra optimization software at the origin server.|
|`vary_header_present`|The origin web server sent a `Vary` header with a value other than `accept-encoding`.|If the origin web server is attempting to support WebP, disable WebP at the origin web server and let Polish perform the WebP conversion.|
{: caption="Common Cf-Polished statuses" caption-side="bottom"}

Optimization still works when `accept-encoding` isn't the only value in the `Vary` header.
{: note}
