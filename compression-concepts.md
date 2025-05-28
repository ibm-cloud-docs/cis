---

copyright:
  years: 2021, 2025
lastupdated: "2025-05-28"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Compression and optimization
{: #compression-concepts}

{{site.data.keyword.cis_full}} applies `gzip` and `brotli` compression to some types of content. {{site.data.keyword.cis_short_notm}} also compresses items based on the browser's UserAgent to speed up page loading time.
{: shortdesc}

If you're already using `gzip`, {{site.data.keyword.cis_short_notm}} accepts your `gzip` settings if you're passing the details in a header from your web server for the files.

{{site.data.keyword.cis_short_notm}} supports only the content type `gzip` toward your origin server and can also deliver only content that is compressed with either `gzip` or `brotli`, or not compressed.

{{site.data.keyword.cis_short_notm}}'s reverse proxy is also able to convert between compressed formats and uncompressed formats, meaning that it can pull content from a customer's origin server through `gzip` and serve it to clients uncompressed (or reversed). This conversion is done independently of caching.

The Accept-Encoding header is not respected and is removed.
{: note}

## What gets compressed
{: #what-gets-compressed}

In addition to {{site.data.keyword.cis_short_notm}}'s serving stale content and minification of CSS, JS, and HTML to speed up your site, {{site.data.keyword.cis_short_notm}} also provides `gzip` and `brotli` compression to help site owners.

{{site.data.keyword.cis_short_notm}} returns `gzip` or `brotli` encoded responses to compatible clients and browsers for the following content-types:

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

If you do not want a particular response from your origin to be encoded, you can disable encoding by setting **cache-control: no-transform** at your origin web server.

### Enable Brotli compression
{: #enable-brotli-compression}


1. Log in to your {{site.data.keyword.cis_short_notm}} account.
1. Choose the appropriate domain.
1. Click the Performance tab.
1. Click the Advanced tab.
1. Toggle the Brotli switch to `On`.

## HTML, JavaScript, and CSS compression features
{: #html-js-css}

{{site.data.keyword.cis_short_notm}} uses **Minify web content** to remove all unnecessary characters from HTML, JavaScript and CSS files, without changing their functionality.

CSS and JavaScript minification operates on cached CSS and JS files only. After {{site.data.keyword.cis_short_notm}} returns a cache HIT for the file, it is returned to browsers in minified form, which allows {{site.data.keyword.cis_short_notm}} to deliver a complete minification result. If you need to enable or disable minification for CSS and JavaScript, purge your {{site.data.keyword.cis_short_notm}} cache to see the effect of any minification change.


## Image size optimization compression
{: #polish-compression}

Image size optimization compresses resources that are cached in the {{site.data.keyword.cis_short_notm}} edge network by stripping metadata and applying lossy or lossless compression. Image size optimization accelerates image downloads by reducing image size. Image size optimization can't optimize off-site resources.

Image size optimization compression is only available as a page rule in the console. The domain level setting is available in the CLI.
{: note}

### Image size optimization compression options
{: #polish-comp-opt}

The following sections detail the image size optimization compression options.

#### Lossless
{: #lossless}

The lossless option attempts to strip most metadata (for example EXIF data), but doesn't change the image detail. Effectively, when uncompressed, a lossless image is identical to the original.

#### Lossy
{: #lossy}

The lossy option attempts to strip most metadata and compresses images by approximately 15 percent. When uncompressed, some of the redundant information from the original image is lost.

Lossy has the same effect as Lossless when applied to PNG.

With Lossless and Lossy modes, {{site.data.keyword.cis_short_notm}} attempts to strip as much metadata as possible. However, there is no guarantee that all metadata is stripped because other factors, such as caching status, might affect which metadata is finally sent in the response.

#### WebP
{: #webp}

WebP is a modern image format that provides superior lossless and lossy compression for images. WebP lossless images are approximately 26 percent smaller than PNGs, while lossy images are 25 to 34 percent smaller than JPEGs.

Image size optimization creates and caches a WebP version of the image. The image is then delivered to the browser if the Accept header from the browser includes WebP and the compressed image is significantly smaller than the lossy or lossless compression.

```sh
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
```
{: pre}

Currently, WebP is only supported in Firefox, Google Chrome, and Opera browsers.

To ensure WebP is not served from cache to a browser that lacks WebP support, disable WebP at your origin web server when you use image size optimization.
{: important}

### Verify that image size optimization is active
{: #verify-polish}

Activate image size optimization by using a [page rule](/docs/cis?topic=cis-use-page-rules#page-rules-performance) or [CLI domain settings](/docs/cis?topic=cis-cis-cli#domain-settings).

Image size optimization adds the following headers to image requests that are compressed:

```sh
cf-bgj: imgq:85

cf-polished: qual=85, origFmt=jpeg, origSize=95005

cf-cache-status: HIT
```
{: codeblock}

The `cf-bgj` header confirms that {{site.data.keyword.cis_short_notm}} applied image size optimization and returns the image quality setting (`imgq`). The `cf-polished` header represents the image size optimization status and returns the image quality setting (`qual`) and original size (`origSize`). The `cf-cache-status` confirms that the image was cached and image size optimization can be applied.

WebP conversion does not change the image URL. The `Content-Type HTTP` header tells the browser the original format of an image.

### Common Cf-Polished statuses
{: #common-polished-status}

The following table lists common Cf-Polished statuses and how to troubleshoot them. If no Cf-Polished header is returned, try to use single-file cache purge to purge the image.

| Status | Definition | Recommendation |
|--------|------------|----------------|
|`input_too_large`| The input image is too large or complex to process and needs a lower resolution.| Use .png or .jpeg images that are less than 1,000 px and 10 MB.|
|not_compressed or not_needed|The image was fully optimized at the origin server and no compression was applied.| |
|webp_bigger|Polish attempted to convert to WebP, but the image was optimized at the origin server and/or was created with a low quality setting.|Because the WebP version doesn’t exist, the status is set on the JPEG/PNG version of the response.|
|cannot_optimize or internal_error|The input image is corrupted or incomplete at the origin server. |Upload a new version of the image to the origin server.|
|format_not_supported|The input image format is not supported (for example, BMP, TIFF) and/or the origin server is using extra optimization software that is not compatible with Polish.|Try converting the input image to a web-compatible format (for example, PNG, JPEG) and/or disabling any extra optimization software at the origin server.|
|vary_header_present|The origin web server sent a Vary header with a value other than accept-encoding.|If the origin web server is attempting to support WebP, disable WebP at the origin web server and let Polish perform the WebP conversion.|
{: caption="Common Cf-Polished statuses" caption-side="bottom"}

Image size optimization still works when the accept-encoding is not the only header that is listed within the `Vary` header.
{: note}
