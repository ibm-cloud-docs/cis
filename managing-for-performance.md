---
  
copyright:
   years: 2018
lastupdated: "2018-03-13"
 
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Manage your CIS deployment for best performance

IBM Cloud Internet Services (CIS) can provide the fastest experience for your customers because it optimizes your images, and it stores your web content as near as possible to your end-users. Your content is loaded from proxied edge servers (which reduces latency).

With IBM CIS, you can enhance your site's performance further by using best practices to speed up the loading of your web content. Here are some specific best practices for enhancing the performance of your web content within CIS.

**Recommended and best practices:**

 * Cache as much of your static and semi-static web content as possible
 * For event-driven content, purge your cache using the API
 
## Best practice 1: Cache as much static and semi-static content as possible

  * Enable **Cache Everything** for static HTML web pages
  * Use conservative **Time to Live (TTL)** for your content that changes occasionally

### Utilize conservative TTLs (Time-to-Lives) for content that changes occasionally
If content rarely changes, you can set a conservative TTL to utilize our cache as much as possible. If you have a high percentage of re-validation requests, you could increase the TTLs of your content without negatively affecting your customers. By using the cache more effectively, you'll increase performance because you'll revalidate less often.

### How do I tell if items are being cached?
IBM CIS adds the response header `CF-Cache-Status` when it attempts to cache an object. If caching is successful, the value of this header indicates its status with one of these keywords:

* **MISS:** The asset was not yet in the cache or the TTL had expired (that is, it had reached the cache-control maximum age of 0).
* **HIT:** The asset was delivered from the cache.
* **EXPIRED:** This asset was delivered from cache, but the next request will require revalidation.
* **REVALIDATED:** The asset was delivered from cache. The TTL was expired, but an `If-Modified-Since` request to the origin indicated that the asset had not changed. Therefore, the version in cache is considered valid again.

## Best practice 2: For event-driven content, use the API to purge your cache
For example, every time a new post is added to your blog, you could easily purge the CIS cache using an API command. It is common to see event-driven content, and we make it easy to guarantee that no stale content is reaching your users. The  commands to purge the cache immediately across our entire global network are listed next. You can use our caching application or you can use the API.

  * Purge the cache by using a Cache-Tag
  * Purge the cache globally
  * Purge the cache by Page Rule

### Purge the cache by Cache-Tag
Cache-Tags let you define buckets of content that you wish to purge. It is an excellent way to combine objects that are commonly changed together. So an HTML blog post, for example, and all of its image content could be tagged together. Mobile-only content also could be bundled using cache-tags, so that you can purge everything when you push a new update to your mobile domain.

### Purge the cache globally
You also have the option to force our entire cache to revalidate. You can reset all of the objects stored in our cache so that every request is routed to the origin server.

### Purge the cache by Page Rule
Page Rules let you purge the entire cache based upon a regular expression. You can utilize a pre-defined Page Rule and re-validate all hits against that Page Rule. You can create up to 50 Page Rules per page.

### Use advanced caching features

**Bypass Cache on Cookie:** Configured in a Page Rule, this feature allows you to serve a cached object unless a cookie of a specific name exists. For example, you can serve a cached version of the homepage unless you find a `SessionID` cookie indicating that the customer is logged in, and therefore should be presented with personalized content.
