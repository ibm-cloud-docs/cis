---

copyright:
  years: 2018, 2020
lastupdated: "2020-06-08"

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
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Caching concepts
{:#caching-concepts}

This document contains some concepts and definitions related to caching and how it affects your {{site.data.keyword.cis_full}} deployment.
{:shortdesc}

## What is caching?
{:#what-is-caching}

Caching is the process of storing files on our edge servers, which we do for the purpose of improving the response time when serving those files to customers. By storing the files closer to the customers, we can decrease the time it takes for the data to stream across the network, which commonly is called the **latency**.

Cached files have a specified expiration time, **Time-to-live (TTL)** after which they are purged from the cache. It also is possible to purge files from the cache manually. After files are removed from the cache, {{site.data.keyword.cis_short_notm}} goes back to your origin server to reload your files and update the cache with the latest versions.

A deeper explanation of the cache settings and your caching options is located in the [Caching and Page Rules](/docs/cis?topic=cis-use-page-rules-with-caching) section.

### Cached content
{:#what-content-is-cached}

By default, we cache **static files**, which include many types of image and text files (non-HTML files). This only includes files from your websites and not third party resources from social networking sites, etc. Also, we currently do not cache by MIME type.

### Caching HTML
{:#how-do-i-cache-html}

We do not cache HTML files by default because we do not consider them to be static; however, if static HTML can be clearly distinguished from dynamic HTML it is possible to cache HTML files [using the Page Rules feature](/docs/cis?topic=cis-use-page-rules).

## Default caching behavior
{:#default-cache-behavior}

{{site.data.keyword.cis_short_notm}} caches static content depending on where your visitors come from, which {{site.data.keyword.cis_short_notm}} data center your visitors reach, and how often visitors request a resource at the specific data center.

{{site.data.keyword.cis_short_notm}} only caches a resource within the {{site.data.keyword.cis_short_notm}} data center that serves the request and doesn’t cache:

- off-site or third-party resources (for example, Facebook and Flickr)
- content hosted on unproxied DNS records

By default, {{site.data.keyword.cis_short_notm}} respects the origin web server’s cache headers in the following manner unless overridden by an edge cache TTL page rule:

- If the `cache-control` header is set to `private`, `no-store`, `no-cache`, or `max-age=0`, or if there is a cookie in the response, then {{site.data.keyword.cis_short_notm}} does not cache the resource.
- Otherwise, if `cache-control` is set to `public` and the `max-age` is greater than 0, or if the `expires` header is a date in the future, {{site.data.keyword.cis_short_notm}} caches the resource.
- If both `max-age` and an `expires` header are set, `max-age` is used.

By default, {{site.data.keyword.cis_short_notm}} caches certain HTTP response codes with the following edge cache TTL when no `cache-control` directive or `expires` response header are present:

|Response code|TTL  |
|-------------|-----|
|200, 206, 301|120m;|
|302, 303     |20m; |
|404, 410     |3m;  |
|403          |1m;  |


{{site.data.keyword.cis_short_notm}} provides several cache customization options:

- Specify caching behavior for individual URLs via {{site.data.keyword.cis_short_notm}} page rules
- Customize caching with {{site.data.keyword.cis_short_notm}} [edge functions](/docs/cis?topic=cis-edge-functions-use-cases#caching-using-fetch) or the [API](/docs/cis?topic=cis-edge-functions-use-cases#cache-api)
- Adjust caching level, cache TTL, and more via the [{{site.data.keyword.cis_short_notm}} CLI](/docs/cis?topic=cis-cli-plugin-cis-cli#cache)

The maximum file size {{site.data.keyword.cis_short_notm}} caches is 512MB for Trial and Standard customers and 5GB for Enterprise customers. Enterprise customers can open a Support case to request caching of larger files. 
{:tip}

## File extensions cached by default
{:#default-file-extensions}

{{site.data.keyword.cis_short_notm}} uses file extensions to cache content. The following file extensions are cached automatically:
- bmp
- class
- css
- csv
- doc
- docx
- ejs
- eot
- eps
- gif
- ico
- jar
- jpg
- js
- mid
- midi
- otf
- pdf
- pict
- pls
- png
- ppt
- pptx
- ps
- svg
- svgz
- swf
- tif
- tiff
- ttf
- webp
- woff
- woff2
- xls
- xlsx

{{site.data.keyword.cis_short_notm}} does not cache by MIME type, and doesn't cache HTML by default. {{site.data.keyword.cis_short_notm}} does cache a website's `robots.txt`. You can cache additional content by creating page rules.

## Understanding {{site.data.keyword.cis_short_notm}} cache responses

The output of the `CF-Cache-Status` header shows whether a resource is cached.

| Response code | Definition |
|---------------|------------|
|HIT|The resource was found in the {{site.data.keyword.cis_short_notm}} cache.|
|MISS|The resource was not found in the {{site.data.keyword.cis_short_notm}} cache and was served from the origin web server.|
|EXPIRED|The resource was found in cache but has since expired and was served from the origin web server.
|STALE|The resource was served from cache but is expired. {{site.data.keyword.cis_short_notm}} couldn’t contact the origin to retrieve the updated resource.|
|BYPASS|The origin server instructed {{site.data.keyword.cis_short_notm}} to bypass cache via a `cache-control` header set to `no-cache`, `private`, or `max-age=0`. BYPASS is returned when enabling origin cache-control. {{site.data.keyword.cis_short_notm}} also sets BYPASS when your origin web server sends cookies in the response header.|
|REVALIDATED|The resource is served from cache but is stale. The resource was revalidated by either an `If-Modified-Since` header or an `If-None-Match header`.|
|UPDATING|The resource was served from cache but is expired. The resource is currently being updated by the origin web server. UPDATING is typically seen only for very popular cached resources.|
|DYNAMIC|The resource was not cached by default and your current {{site.data.keyword.cis_short_notm}} caching configuration doesn't instruct {{site.data.keyword.cis_short_notm}} to cache the resource.  Instead, the resource was requested from the origin web server. Use page rules to implement custom caching options.|



## Using query string sorting
{:#query-string-sorting}

**Enterprise Only** {{site.data.keyword.cis_short_notm}} treats URLs that have query strings in different orders as separate files in the cache. This means that if one user requests:

`/video/123456?title=0&byline=0&portrait=0&color=987654`

And another user requests:

`/video/123456?byline=0&color=987654&portrait=0&title=0`

{{site.data.keyword.cis_short_notm}} goes back to the origin, even though we have the file in our cache.

Query String Sort sorts the query strings _before_ they hit our cache, resulting in a higher cache hit rate. Enable Query String Sort using the toggle in the **Caching** page.

## Serving stale content
{:#serve-stale-content-caching}

**Serve stale content** keeps a limited version of the site online if the server goes down. Even if the content has expired, {{site.data.keyword.cis_short_notm}} continues serving cached content to users when origin servers are offline.
