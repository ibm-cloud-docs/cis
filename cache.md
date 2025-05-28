---

copyright:
  years: 2018, 2025
lastupdated: "2025-05-28"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Caching
{: #caching-concepts}

Caching is the process of storing files on edge servers to improve the response time when serving those files to customers. By storing files closer to users, caching reduces the time it takes for data to travel across the network, commonly known as latency.
:{ shortdesc}

By default, CIS caches static files, which include many types of image and text files (non-HTML files). The cache only includes files from your websites and does not cover third-party resources, such as those from social networking sites. Currently, CIS does not cache based on MIME type.

 CIS doesn't cache HTML files by default because they are generally considered dynamic. However, if static HTML can be clearly distinguished from dynamic HTML, it is possible to cache HTML files by using page rules.
{: note}

Cached files have a specified expiration time, called Time-to-Live (TTL), after which they are purged from the cache. You can also manually purge files from the cache at any time. After files are purged, CIS goes back to your origin server to reload the files and update the cache with the latest versions.

For detailed information on cache settings and options, see [Using page rules with caching](/docs/cis?topic=cis-use-page-rules-with-caching).
 
## Default caching behavior
{: #default-cache-behavior}

CIS caches static content based on your visitors' locations, the CIS data center they connect to, and how frequently the resource is requested at that data center.

Caching occurs only within the CIS data center serving the request. The following resources aren't cached by CIS:

- Off-site or third-party resources (for example, Facebook and Flickr)
- Content hosted on DNS records that aren't proxied

By default, CIS respects the origin web server’s cache headers unless an edge cache TTL page rule overrides them:

- CIS doesn't cache resources if the `cache-control` header is set to `private`, `no-store`, `no-cache`, or `max-age=0`, or if a cookie is present in the response.
- CIS caches resources if `cache-control` is `public` with a `max-age` greater than 0, or if the expires header specifies a future date.
- When both `max-age` and `expires` headers are set, `max-age` takes precedence.

When neither a `cache-control` directive nor an `expires` header is present, CIS caches certain HTTP response codes with the following default edge cache TTL:

|Response code|TTL  |
|-------------|--------|
|200, 206, 301|120 m|
|302, 303     |20 m |
|404, 410     |3 m  |
|403          |1 m  |
{: caption="Default cache response codes" caption-side="bottom"}

CIS provides several options to customize caching:

- Set caching behavior for individual URLs by using CIS page rules.
- Use CIS [edge functions](/docs/cis?topic=cis-edge-functions-use-cases#caching-using-fetch) or the [API](/docs/cis?topic=cis-edge-functions-use-cases#cache-api) to customize caching.
- Adjust caching levels, TTL, and more through the [CIS CLI](/docs/cis?topic=cis-cis-cli#cache).

The maximum file size that CIS caches is 512 MB for Trial and Standard Next customers, and 5 GB for Enterprise customers. Enterprise customers can request caching of larger files by [opening a support case](/docs/account?topic=account-open-case&interface=ui). 
{: tip}

## File extensions cached by default
{: #default-file-extensions}

CIS uses file extensions to cache content. The following file extensions are cached automatically:

| File extensions |  |  |  |
|:---------| :--------|:-------|:-------|
| `bmp` \n `class` \n `css` \n `csv` \n `doc` \n `docx` \n `ejs` \n `eot` \n `eps`|  `gif` \n `ico` \n `jar` \n `jpg` \n `js` \n `mid` \n `midi` \n `otf` \n `pdf` | `pict` \n `pls` \n `png` \n `ppt` \n `pptx` \n `ps` \n `svg` \n `svgz` \n `swf` | `tif` \n `tiff` \n `ttf` \n `webp` \n `woff` \n `woff2` \n `xls` \n `xlsx` |
{: caption="File extensions cached by default" caption-side="bottom"}

CIS doesn't cache by MIME type, and doesn't cache HTML by default. CIS does cache a website's `robots.txt`. You can cache more content by creating page rules.

## Serving stale content
{: #serve-stale-content-caching}

**Serve stale content** keeps a limited version of the site online if the server goes down. Even if the content expires, CIS continues serving cached content to users when origin servers are offline.

## Understanding CIS cache responses
{: #understanding-cis-cache-responses}

The output of the `CF-Cache-Status` header shows whether a resource is cached.

| Response code | Definition |
|---------------|------------|
|`HIT`|The resource was found in the CIS cache.|
|`MISS`|The resource wasn't found in the CIS cache and was served from the origin web server.|
|`EXPIRED`|The resource was found the cache but has since expired and was served from the origin web server.
|`STALE`|The resource was served from cache, but is expired. CIS couldn’t contact the origin to retrieve the updated resource.|
|`BYPASS`|The origin server instructed CIS to bypass cache by using a `cache-control` header set to `no-cache`, `private`, or `max-age=0`. BYPASS is returned when you enable origin cache-control. CIS also sets BYPASS when your origin web server sends cookies in the response header.|
|`REVALIDATED`|The resource is served from cache, but is stale. The resource was revalidated by either an `If-Modified-Since` header or an `If-None-Match header`.|
|`UPDATING`|The resource was served from the cache, but is expired. The resource is being updated by the origin web server. UPDATING is typically seen only for popular cached resources.|
|`DYNAMIC`|The resource wasn't cached by default and your current CIS caching configuration doesn't instruct CIS to cache the resource. Instead, the resource was requested from the origin web server. Use page rules to implement custom caching options.|
{: caption="Cache response codes and definitions" caption-side="bottom"}

## Using query string sorting
{: #query-string-sorting}

**Enterprise Only**: CIS treats URLs with query strings in different orders as separate files in the cache. For example, if one user requests:

`/video/123456?title=0&byline=0&portrait=0&color=987654`

and another requests:

`/video/123456?byline=0&color=987654&portrait=0&title=0`

CIS fetchs the file from the origin again, even if it’s already cached.

The Query String Sort feature sorts query strings "before" caching, increasing cache hit rates. You can enable Query String Sort by using the toggle on the **Caching** page.
