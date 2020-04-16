---

copyright:
  years: 2018, 2019
lastupdated: "2019-12-13"

keywords: Use Page Rules, Page Rule

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


# Using page rules
{:#use-page-rules}

A page rule specifies some settings and values that you can apply to a specific URL pattern that references your domain. page rules help you manage security, performance, and reliability based on each individual URL in your site. The following table describes the page rules that are available to all customers, the behaviors they produce, and any special considerations you should keep in mind before using them.
{: shortdesc}

## Security
{:#page-rules-security}

| **Setting** | **Behavior** | **Considerations** |
|-----------|----------|----------------|
|**Browser Integrity Check**|Looks for common HTTP headers abused by spammers, and denies access to your page. It also blocks visitors that do not have a user agent or add a non-standard user agent (also commonly used by abuse bots, crawlers, or APIs). | |
|**Disable Security**|Disables the following features: Email Obfuscation, Server Side Excludes, WAF.|If a rule is set to disable security, and another rule is set to enable the WAF, the WAF rule takes precedence, regardless of the order in which they appear.|
|**Email Obfuscation**|Toggles Email Obfuscation on or off. | |
|**IP Geolocation Header**|Includes the country code of the visitor location with all requests to your website. The information can be found in the `CF-IPCountry` HTTP header. | |  
|**Security Level**|Controls how high a client threat score must be so that a client will encounter a challenge page. This setting can be used so that your site always presents visitors with the **Defense Mode** challenge when they visit your site. | |
|**Server Side Excludes**|Toggles Server Side Excludes on or off.  | |
|**TLS**|Controls which of the TLS modes is used. | |
|**WAF**|Toggles WAF on or off. | |  
|**Automatic HTTPS Rewrites**|Toggles Automatic HTTPS Rewrites on or off.  | |
|**Opportunistic Encryption**|Toggles Opportunistic Encryption on or off.  | |
|**Cache Deception Armor**|Toggles Cache Deception Armor on or off.  | |
|**Always Use HTTPS**|Converts any `http://` URL to an `https://` URL by creating a `301` redirect.|Using this setting disables configuring all other settings for the rule, because {{site.data.keyword.cis_short_notm}} forces a redirect to `HTTPS` for the request, which becomes a new request that is then evaluated against page rules. |
|**True Client IP Header**|{{site.data.keyword.cis_short_notm}} will send the end user's IP address in the `True-Client-IP` header.  |Enterprise only |

## Performance
{:#page-rules-performance}

| **Setting** | **Behavior** | **Considerations** |
|-----------|----------|----------------|
|**Browser Cache TTL**|Controls how long resources cached by client browsers remain valid. | |
|**Bypass Cache on Cookie**|Serve a cached object unless we see a cookie of a specific name, for example, serve a cached version of the homepage unless we see a `SessionID` cookie indicating the customer is logged in and therefore should be presented personalized content. | |
|**Cache Level**|**Bypass** - Resources that match that page rule are not cached. **No query string** - Only delivers resources from cache when there is no query string. **Ignore query string** - Delivers the same resource to everyone independent of the query string. **Standard** - Delivers a different resource each time the query string changes.  **Cache everything** - Resources that match the page rule are cached.|By default, HTML content is not cached. A page rule to cache static HTML content must be written. |
|**Edge Cache TTL**|Controls how long {{site.data.keyword.cis_short_notm}} will retain files in our cache. |This setting is optional when specifying cache level. |
|**Resolve Override**|Change the URL or IP that the request matching the page rule resolves to.||
|**Cache on Cookie**|Apply the `Cache Everything` option (`Cache Level` setting) based on a regular expression match against a cookie name. If you add both this setting and `Bypass Cache on Cookie` to the same page rule, `Cache On Cookie` takes precedence over `Bypass Cache on Cookie`.|Enterprise only |
|**Disable Performance**|Turn off:`Minify Web Content`, `Image Load Optimization`, `Image Size Optimization`, `Script Load Optimization`. |Enterprise only |
|**Minify Web Content**|Minify HTML, CSS and/or JavaScript files by removing all unnecessary characters from these files. |Enterprise only |
|**Image Load Optimization**|Improves load time for pages that include images based on network connection and device type by one of the following: **Image Virtualizing** - Replaces images with low resolution placeholder images that have the same dimensions as the original (including third party images). Once the page renders completely, full resolution images are then lazy-loaded (prioritizing images in the browser viewport). This process allows pages to render quickly and minimizes browser reflow. **Request Streamlining** - Combines multiple individual network requests for images into a single request. |Enterprise only |
|**Image Size Optimization**|Reduce image file size by removing metadata (date and time, camera manufacturer and model, etc.), and by compressing images when possible. Smaller file sizes mean faster load times for images and web pages. |Enterprise only |
|**Sort Query String**|Treats files with the same query strings as the same file in cache, regardless of the order of the query strings. |Enterprise only |
|**Response Buffering**|Enable or disable buffering of responses from the origin server. By default, {{site.data.keyword.cis_short_notm}} sends packets to the client as we receive them. Enabling Response Buffering means that {{site.data.keyword.cis_short_notm}} will wait until it has the entire file before forwarding it to the end user. |Enterprise only |
|**Script Load Optimization**|Improve paint times by asynchronously loading your Javascripts, including third party scripts, so that they do not block rendering the content of your pages. |Enterprise only |

## Reliability
{:#page-rules-reliability}

| **Setting** | **Behavior** | **Considerations** |
|-----------|----------|----------------|
|**Serve Stale Content**|Keeps a limited version of the site online if the server goes down. |For more information view [Managing your {{site.data.keyword.cis_short_notm}} deployment for optimal reliability](/docs/cis?topic=cis-manage-your-ibm-cloud-internet-services-deployment-for-optimal-reliability) |
|**Origin Cache Control**|Determine what content is cached from the origin and how often the content is updated |For more information view [Managing your {{site.data.keyword.cis_short_notm}} deployment for optimal reliability](/docs/cis?topic=cis-manage-your-ibm-cloud-internet-services-deployment-for-optimal-reliability) |
|**Forwarding URL** |URL to be used in case the site is unavailable. | Using this disables configuring all other settings because you are forwarding the request somewhere else. For more information view [Managing your {{site.data.keyword.cis_short_notm}} deployment for optimal reliability](/docs/cis?topic=cis-manage-your-ibm-cloud-internet-services-deployment-for-optimal-reliability)|
|**Host Header Override**|Replace the host header for URI matching the page rule to the value specified. This is commonly used for content hosted in an S3 bucket.|
|**Disable Apps**|Turn off all {{site.data.keyword.cis_short_notm}} Apps. | Enterprise only |
|**Origin Error Page Pass-through**|Disables {{site.data.keyword.cis_short_notm}} error pages that would trigger for issues sent from the origin server, and instead displays the error pages set at the origin. |Enterprise only ||

## Page rule URL patterns
{:#page-rule-url-patterns}

A page rule will take effect on a given URL pattern, matching the following format:

`<scheme>://<hostname><:port>/<path>`
{:pre}

An example using each component would be:

`https://www.example.com:80/image.png`
{:pre}

The *scheme* and *port* components are optional. If the scheme is omitted, it will cover both `http://` and `https://` protocols. If the port is not specified, then the rule will match all ports. You can perform basic wildcard matches by using a ‘*’ symbol in your rule pattern, allowing it to match a series of similar patterns rather than just one.

Here are three important things to remember with page rules:

 * Only one page rule will take effect on any given request.
 * Page rules are given priority in order from top to bottom.
 * Once a URL matches a rule, only that rule only will be applied; that is, if a page rule already has been triggered on a request, any subsequent rules that also match the URL pattern do not take effect. As a general rule, we recommend ordering your rules from _most specific_ to _least specific_.

Page rules can be disabled, in which case they will take no action. They still can be seen in the list and they can be edited. Setting the **Enabled** toggle to **Off** will create a page rule that initially is disabled.

For more information, please refer to the [Caching and page rules how-to document](/docs/cis?topic=cis-use-page-rules-with-caching).
