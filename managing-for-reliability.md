---

copyright:
  years: 2018, 2020
lastupdated: "2020-07-06"

keywords: Page Rules, web content, IBM CIS deployment

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Managing your {{site.data.keyword.cis_short_notm}} deployment for optimal reliability
{: #manage-your-ibm-cloud-internet-services-deployment-for-optimal-reliability}

To achieve optimal reliability for your {{site.data.keyword.cis_full}} deployment, you can set up a helpful DNS configuration and global load balancers. For additional reliability, you can use our page rules to be sure that your web content is delivered to your customers, even if your origin server or the cache has a problem. This document gives details about some best practices for making your {{site.data.keyword.cis_short_notm}} deployment optimally reliable.
{: shortdesc}

Generally, our recommended best practices are these:

* Set up your DNS to take advantage of {{site.data.keyword.cis_short_notm}} proxy servers and other features.
* Use one or more global load balancers to distribute your site traffic evenly.
* Set up appropriate page rules to manage your caching and other options.

Each of these items provides certain functionality you can use to create a more reliable {{site.data.keyword.cis_short_notm}} deployment.

Notice that the {{site.data.keyword.cis_short_notm}} interface is organized into sections for *security*, *reliability*, and *performance*.


## Setting up DNS
{: #setting-up-dns}

To get started setting up your DNS configuration, select **DNS** from the navigation menu.

For detailed information about setting up and managing your DNS for reliability, see [Setting up your Domain Name System for CIS](/docs/cis?topic=cis-set-up-your-dns-for-cis).


## Setting up global load balancers
{: #setting-up-glb}

To get started setting up your global load balancers, select **Global Load Balancers** from the navigation menu.

For detailed information about setting up and managing your global load balancers, see [Global load balancer concepts](/docs/cis?topic=cis-global-load-balancer-glb-concepts).

## Using page rules to increase reliability
{: #using-page-rules-to-increase-reliability}

Here are some recommended page rule settings to give your site maximum reliability:

* Serve Stale Content
* Origin Cache Control
* Forwarding URL

## Serve Stale Content
{: #serve-stale-content}

You can use the **Serve Stale Content** page rule setting to keep a limited version of your site online if your server goes down.

With **Serve Stale Content**, when your server goes down, {{site.data.keyword.cis_short_notm}} serves pages from our cache, so your visitors still see some of the pages they are trying to visit. Your visitors see a message at the top of the page telling them that they are in offline browsing mode. Serve Stale Content returns an HTTP status 503, however, 503 is also used by many other web applications. When your server comes back online, {{site.data.keyword.cis_short_notm}} bumps users back to regular browsing seamlessly.

If {{site.data.keyword.cis_short_notm}} does not have the requested page in its cache, your visitor sees an error page letting them know that the website page they are requesting is offline.

### Seting up Serve Stale Content
{: #setting-up-serve-stale-content}

To enable **Serve Stale Content**, follow these steps:

1. Use the navigation menu to select **Page Rules** under **Performance**.
2. Create a page rule with the URL pattern of your domain.
3. Add the **Serve Stale Content** setting with the toggle on.
4. Select **Provision Resource**.

### Serve Stale Content limitations
{: #limitations-serve-stale-content}

* **Serve Stale Content** caches the first 10 links from your root HTML, then just the first links from each of those pages, and finally the first links from each of those subsequent pages. This means that only some pages on your site are viewable when your origin server goes down.

* Recently added sites don't have a large cache of their site available, which means that **Serve Stale Content** might not work if you only added the site a few days ago.

* {{site.data.keyword.cis_short_notm}} does not show private content or handle form submission (POSTs) if your server is down. Visitors are shown an `error on checkout` page or `items require a login to view`.

* To trigger **Serve Stale Content**, your web server must be returning a standard HTTP Error code of 502 or 504 timeout. Serve Stale Content also works when we encounter issues contacting your origin (Errors 521 & 523), timeouts (522 & 524), SSL errors (525 & 526) or an unknown error (520). **Serve Stale Content** is not triggered for other HTTP response codes, such as 404s, 500, 503, database connection errors, internal server error, or empty replies from server.

* **Serve Stale Content** does not work if a "Cache Everything" page rule is enabled with the "Edge Cache Expire TTL" lower than the caching frequency, because the "Edge Cache Expire TTL" causes the **Serve Stale Content** cache to be purged in the corresponding interval.

## Origin Cache Control
{: #origin-cache-control}

You can use the **Origin Cache Control** Page Rule setting to determine what content is cached from your origin and how often the content is updated, which has an effect on reliability and on performance. By default, if no settings are changed and no headers that prevent caching are sent from your origin server, {{site.data.keyword.cis_short_notm}} caches all static content with certain extensions. These types of content include images, CSS, and JavaScript. This caching is primarily for performance reasons.

To set up **Origin Cache Control** use page rules to turn on specific headers that give the wanted behavior with respect to each resource of your content. To understand how to use **Origin Cache Control**, some more general explanation of page rules and overall caching behavior for {{site.data.keyword.cis_short_notm}} is required to provide context, which is covered in the next several sections. Three methods exist that you can use to control caching in general, and **Origin Cache Control** is the second one.

Setting **Origin Cache Control** invokes caching rules that seek to adhere closely to internet best practices and RFCs, primarily with respect to revalidation. For example, the {{site.data.keyword.cis_short_notm}} default behavior with `max-age=0` is not to cache at all, whereas setting **Origin Cache Control** caches, but it always revalidates.

### Setting up Origin Cache Control
{: #setting-up-origin-cache-control}

To enable **Origin Cache Control**, follow these steps:

1. Use the navigation menu to select **Page Rules** under **Performance**.
2. Create a page rule with the URL pattern that references your domain.
3. Add the **Origin Cache Control** setting with the toggle on.
4. Select **Provision Resource**.

### Page Rule precedence
{: #page-rule-precedence}

Two specific page rules take precedence for caching overall:

* If a page rule has **Cache Level** set to `Bypass`, the resources that match that page rule are not cached. {{site.data.keyword.cis_short_notm}} still acts as a proxy, and our other performance features remain active. However, your content is fetched from your origin server directly, instead of served from our cache.

* If a page rule has **Cache Level** set to `Cache everything`, resources that match the page rule are cached. **Using this page rule setting is the only way to tell us to cache resources beyond what we consider static, including HTML.**

If no page rule is set, we use the `Standard` caching mode, which is based the extension of the resource. We cache static resources only.

### Origin cache-control headers
{: #origin-cache-control-headers}

The second way to alter what {{site.data.keyword.cis_short_notm}} caches is through caching headers sent from the origin. {{site.data.keyword.cis_short_notm}} respects these settings, but you can override them by specifying an **Edge Cache TTL** page rule setting. Here are the headers we consider when deciding what resources to cache from your origin:

* If the **Cache-Control** header is set to `private`, `no-store`, `no-cache`,  or `max-age=0`, or if there is a cookie in the response, then {{site.data.keyword.cis_short_notm}} does not cache the resource. Note that sensitive material should not be cached, so you might consider using one of these headers in that case.

* If the **Cache-Control** header is set to `public` and the `max-age` is greater than 0, or if the `Expires` headers are set any time in the future, the resource is cached.

According to RFC rules, `Cache-Control: max-age` trumps `Expires` headers. If both are seen and they do not agree, `max-age` wins.
{: note}

### Using the `s-maxage` header
{: #using-the-s-maxage-header}

The third way to control caching behavior and browser caching behavior together is by using the **`s-maxage`** Cache-Control header.

Normally we respect the `max-age` directive:

`Cache-Control: max-age=1000`
{: pre}

But if you want to specify a cache timeout that's different from the browser, we can use `s-maxage`. Here's an example that tells {{site.data.keyword.cis_short_notm}} to cache the object for 200 seconds and the browser to cache the object for 60 seconds.

`Cache-Control: s-maxage=200, max-age=60`
{: pre}

Basically `s-maxage` is intended to be followed ONLY by reverse proxies (so the browser should ignore it) whilst on the other hand we ({{site.data.keyword.cis_short_notm}}) give priority to `s-maxage` if it is present. We respect whichever value is higher: the browser cache setting or the `max-age` header.

### Summary on cache control headers and page rules for reliability
{: #summary-cache-control-headers-page-rules}

To sum up, here are some main areas to consider for reliability with regard to caching:

* Check your origin's caching headers to make sure there are no overriding headers for cacheable resources (`Cache-Control` and `Expires`).

* {{site.data.keyword.cis_short_notm}} always caches static content by default, with the following TTL depending on the return code:

   ```sh
   200 301    120m;
   302 303    20m;
   403        5m; for reliability
   404        5m;
   any        0s;
   ```
   {: pre}

* To cache more, create a Page Rule with **Cache Level** set to `Cache everything` on the URL (if your web server returns a 404 when requesting this URL, this result is cached for 5m only).

* To avoid caching on a URL, create a page rule with **Cache Level** set to `Bypass`.


## Forwarding URL
{: #forwarding-url}

To ensure that your content is always available, create page rule with the **Forwarding URL** setting used, in case your site is unavailable.

When you enable a **Forwarding URL**, all of your other settings are disabled because you are sending all of your traffic to another URL.
{: note}

### Setting up a forwarding URL
{: #setting-up-forwarding-url}

To enable **Forwarding URL**, follow these steps:

1. Use the navigation menu to select **Page Rules** under **Performance**.
2. Create a page rule with the URL pattern that references your domain.
3. Add the **Forwarding URL** setting.
4. Select the forwarding type and enter the destination URL.
5. Select **Provision Resource**.

### Forwarding URL examples
{: #forwarding-examples}

Imagine that you want to make it easy for anyone coming to reach a URL such as:

`*www.example.com/+`
{: pre}

`*example.com/+`
{: pre}

This pattern matches:

```sh
http://example.com/+
http://www.example.com/+
https://www.example.com/+
https://blog.example.com/+
https://www.blog.example.com/+
```
{: pre}

It does not match:

```sh
http://www.example.com/blog/+  [extra directory before the +]
http://www.example.com+  [no trailing slash]
```
{: pre}

After you've created the pattern that matches what you want, add the **Forwarding URL** setting and select the forwarding type and enter the destination URL. For example:

`https://plus.google.com/yourid`
{: pre}

Select **Provision Resource**. Within a few seconds any requests that match the pattern are forwarded to the new URL with the specified redirect.

### Advanced forwarding options
{: #advanced-forwarding-options}

If you use a basic redirect, such as forwarding the root domain to `www.yourdomain.com`, you lose anything else in the URL. For example, you could set up the pattern:

`example.com`
{: pre}

And have it forward to:

`http://www.example.com`
{: pre}

But then if someone entered:

`example.com/some-particular-page.html`
{: pre}

Then they are redirected to:

`www.example.com`
{: pre}

instead of:

`www.example.com/some-particular-page.html`
{: pre}

The solution is to use variables. Each wildcard corresponds to a variable that can be referenced in the forwarding address. The variables are represented by a `$` followed by a number. To refer to the first wildcard you'd use `$1`, to refer to the second wildcard you'd use `$2`, and so on. To fix the forwarding from the root to `www` in the previous example, use the same pattern:

`example.com/*`
{: pre}

Then set up the following URL for traffic to forward to:

`http://www.example.com/$1`
{: pre}

In this case, if someone went to:

`example.com/some-particular-page.html`
{: pre}

They are redirected to:

`http://www.example.com/some-particular-page.html`
{: pre}
