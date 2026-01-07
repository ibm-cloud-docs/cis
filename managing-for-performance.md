---

copyright:
  years: 2018, 2026
lastupdated: "2026-01-06"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Managing your {{site.data.keyword.cis_short_notm}} deployment for best performance
{: #manage-your-cis-deployment-for-best-performance}

{{site.data.keyword.cis_full}} ({{site.data.keyword.cis_short_notm}}) can provide the fastest experience for your customers because it optimizes your images, and it stores your web content as near as possible to your end-users. Your content is loaded from proxied edge servers (which reduces latency).
{: shortdesc}

With {{site.data.keyword.cis_short_notm}}, you can enhance your site's performance further by using best practices to speed up the loading of your web content. Here are some specific best practices for enhancing the performance of your web content within {{site.data.keyword.cis_short_notm}}. 

**Recommended and best practices:**

* Cache as much of your static and semi-static web content as possible
* For event-driven content, purge your cache with the API

## Best practice 1: Cache as much static and semi-static content as possible
{: #best-practice-cache-static-content}

* Enable **Cache Everything** for static HTML web pages
* Use conservative **Time-to-live (TTL)** for your content that changes occasionally

### Utilize conservative TTLs (Time-to-Lives) for content that changes occasionally
{: #utilize-conservative-ttl}

If content rarely changes, you can set a conservative TTL to utilize our cache as much as possible. If you have a high percentage of re-validation requests, you could increase the TTLs of your content without negatively affecting your customers. By using the cache more effectively, you'll increase performance because you'll revalidate less often.

### How do I tell if items are being cached?
{: #how-do-i-tell-if-items-are-being-cached}

{{site.data.keyword.cis_short_notm}} adds the response header `CF-Cache-Status` when it attempts to cache an object. If caching is successful, the value of this header indicates its status with one of these keywords:

* **MISS:** The asset was not yet in the cache or the TTL had expired (that is, it had reached the cache-control maximum age of 0).
* **HIT:** The asset was delivered from the cache.
* **EXPIRED:** This asset was delivered from cache, but the next request requires revalidation.
* **REVALIDATED:** The asset was delivered from cache. The TTL was expired, but an `If-Modified-Since` request to the origin indicated that the asset had not changed. Therefore, the version in cache is considered valid again.

## Best practice 2: For event-driven content, purge your cache
{: #best-practice-api-purge-cache}

For example, every time a new post is added to your blog, you could easily purge the {{site.data.keyword.cis_short_notm}} cache. It is common to see event-driven content, and {{site.data.keyword.cis_short_notm}} makes it easy to guarantee that no stale content is reaching your users. The commands to purge the cache immediately across the entire global network are:

* Purge all files
* Purge by prefixes (Enterprise only)
* Purge by hostnames (Enterprise only)
* Purge by tags (Enterprise only)
* Purge by URLs

### Purge all files
{: #purge-cache-globally}

You have the option to force the entire cache to revalidate. You can reset all of the objects stored in the cache so that every request is routed to the origin server.

### Purge by prefixes (Enterprise only)
{: #purge-cache-prefix}

Enterprise plan users can purge the cache by URL prefix or path separators in the URL. For example, valid purge requests for a URL such as `https://www.example.com/foo/bar/baz/qux.jpg` include:

* `www.example.com/`
* `www.example.com/foo/`
* `www.example.com/foo/bar/`
* `www.example.com/foo/bar/baz/`
* `www.example.com/foo/bar/baz/qux.jpg`

Purging by prefix is useful when you want to purge everything within a directory, or increase control over cached objects in a particular path. It can also simplify the number of purge calls made.

### Purge by hostnames (Enterprise only)
{: #purge-cache-hostnames}

Purging by hostname is similar to purging by prefixes. Use a list of hostnames to purge the cache of any assets associated with those hostnames.

### Purge by tags (Enterprise only)
{: #purge-cache-by-cache-tag}

Tags let you define buckets of content that you want to purge. It is an excellent way to combine objects that are commonly changed together. An HTML blog post, for example, and all of its image content could be tagged together. Mobile-only content also could be bundled using cache-tags, so that you can purge everything when you push a new update to your mobile domain.

### Purge by URLs
{: #purge-by-urls}

With purge by URL, cached resources are immediately removed from the stored assets in your Content Delivery Network (CDN) across all data centers. New requests for the purged asset receive the latest version from your origin web server and add it back to your CDN cache within the specific data center that served the request.

### Use advanced caching features
{: #use-advanced-caching-features}

**Bypass Cache on Cookie:** Configured in a page rule, this feature allows you to serve a cached object unless a cookie of a specific name exists. For example, you can serve a cached version of the homepage unless you find a `SessionID` cookie indicating that the customer is logged in, and therefore should be presented with personalized content.
