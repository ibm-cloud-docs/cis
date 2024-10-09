---

copyright:
  years: 2018, 2024
lastupdated: "2024-10-09"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Using page rules
{: #use-page-rules}

A page rule specifies settings and values that you can apply to a specific URL pattern that references your domain. Page rules help you manage security, performance, and reliability based on each individual URL in your site. The following table describes the page rules that are available to customers, the behaviors they produce, and any special considerations you should keep in mind before you use them.
{: shortdesc}

## Security
{: #page-rules-security}

| **Setting** | **Behavior** | **Considerations** |
|-----------|----------|----------------|
|**Browser Integrity Check**|Looks for common HTTP headers that are abused by spammers, and denies access to your page. It also blocks visitors that do not have a user agent, or add a non-standard user agent (also commonly used by abuse bots, crawlers, or APIs). | |
|**Disable Security**|Disables the following features: **Email Obfuscation**, **Server Side Excludes** and **WAF** (Web Application Firewall).|If a rule is set to disable security, and another rule is set to enable the WAF, the WAF rule takes precedence regardless of the order in which they appear.|
|**Email Obfuscation**|Toggles email obfuscation feature on or off. When the email obfuscation feature is turned on, email addresses on your web page are obfuscated (hidden) from bots, but visible to humans. There are no visible changes to your website for visitors. | |
|**IP Geolocation Header**|Includes the country code of the visitor location with all requests to your website. The information can be found in the `CF-IPCountry` HTTP header. | |
|**Security Level**|Controls how high a client threat score must be so that a client encounters a challenge page. Use this setting to present visitors with a **Defense Mode** challenge when they visit your site. | |
|**Server Side Excludes**|Toggles server-side excludes on or off. Server-side excludes gives you the ability to hide sensitive content from suspicious visitors, but keep it visible to normal visitors. | SSE only works with HTML. |
|**TLS**|Controls which TLS mode is used. | |
|**WAF**|Toggles WAF rules on or off. | Individual WAF rules cannot be turned on or off using page rules.
|**Automatic HTTPS Rewrites**|Toggles automatic HTTPS rewrites on or off. Automatic HTTPS rewrites safely rewrite HTML source links from HTTP to HTTPS. | |
|**Opportunistic Encryption**|Toggles opportunistic encryption on or off. Opportunistic encryption allows clients to use traditionally insecure protocols over secure channels. | |
|**Cache Deception Armor**|Toggles cache deception armor on or off. Cache deception armor protects from web cache deception attacks while still allowing static assets to be cached. This setting checks that the URL's extension matches the returned content type. |
|**Always Use HTTPS**|Converts any `http://` URL to an `https://` URL by creating a `301` redirect.|Using this setting disables all other setting configurations for the rule because {{site.data.keyword.cis_short_notm}} forces a redirect to `HTTPS` for the request, which becomes a new request that is then evaluated against page rules. |
|**True Client IP Header**|{{site.data.keyword.cis_short_notm}} sends the user's IP address in the `True-Client-IP` header. |Enterprise only |
{: caption="Security rules" caption-side="bottom"}

## Reliability
{: #page-rules-reliability}

| **Setting** | **Behavior** | **Considerations** |
|-----------|----------|----------------|
|**Serve Stale Content**|Keeps a limited version of the site online if the server goes down. |For more information, view [Managing your {{site.data.keyword.cis_short_notm}} deployment for optimal reliability](/docs/cis?topic=cis-manage-your-ibm-cloud-internet-services-deployment-for-optimal-reliability). |
|**Origin Cache Control**|Determines what content is cached from the origin and how often the content is updated. |For more information, view [Managing your {{site.data.keyword.cis_short_notm}} deployment for optimal reliability](/docs/cis?topic=cis-manage-your-ibm-cloud-internet-services-deployment-for-optimal-reliability). |
|**Forwarding URL** |URL to use in case the website is unavailable. | Using this setting disables all other setting configurations because you are forwarding the request somewhere else. For more information, view [Managing your {{site.data.keyword.cis_short_notm}} deployment for optimal reliability](/docs/cis?topic=cis-manage-your-ibm-cloud-internet-services-deployment-for-optimal-reliability).|
|**Host Header Override**|Replaces the host header for the URI matching the page rule to the value specified. This is commonly used for content that is hosted in an S3 bucket.|
|**Disable Apps**|Turns off all {{site.data.keyword.cis_short_notm}} apps. | Enterprise only |
|**Origin Error Page Pass-through**|Disables {{site.data.keyword.cis_short_notm}} error pages that would trigger for issues that are sent from the origin server, and instead displays the error pages set at the origin. |Enterprise only |
{: caption="Reliability rules" caption-side="bottom"}

## Performance
{: #page-rules-performance}

| **Setting** | **Behavior** | **Considerations** |
|-----------|----------|----------------|
|**Browser Cache TTL**|Controls how long resources that are cached by client browsers remain valid. | |
|**Bypass Cache on Cookie**|Serves a cached object unless a cookie of a specific name is seen; for example, serve a cached version of the home page unless we see a `SessionID` cookie indicating that the customer is logged in and should be presented personalized content. |
|**Cache Level**|**Bypass** - Resources that match that page rule are not cached.  \n * **No query string** - Only delivers resources from cache when there is no query string.  \n * **Ignore query string** - Delivers the same resource to everyone independent of the query string.  \n * **Standard** - Delivers a different resource each time the query string changes.  \n * **Cache everything** - Resources that match the page rule are cached.|By default, HTML content is not cached. A page rule to cache static HTML content must be written. |
|**Edge Cache TTL**|Controls how long {{site.data.keyword.cis_short_notm}} retains files in the cache. |This setting is optional when specifying cache level. |
|**Resolve Override**|Changes the URL or IP that the request matching the page rule resolves to.| |
|**Cache on Cookie**|Applies the **Cache Everything** option (**Cache Level** setting) based on a regular expression match against a cookie name. If you add both this setting and **Bypass Cache on Cookie** to the same page rule, **Cache On Cookie** takes precedence over **Bypass Cache on Cookie**.|Enterprise only |
|**Disable Performance**|Turns off **Minify Web Content**, **Image Load Optimization**, **Image Size Optimization**, and **Script Load Optimization**. |Enterprise only |
|**Minify Web Content**|Minifies HTML, CSS and/or JavaScript files by removing all unnecessary characters from these files. |Enterprise only |
|**Image Load Optimization**|Improves load time for pages that include images based on network connection and device type by one of the following:  \n * **Image Virtualizing** - Replaces images with low-resolution placeholder images that have the same dimensions as the original (including third-party images). After the page renders completely, full resolution images are then lazy-loaded (prioritizing images in the browser viewport). This process allows pages to render quickly and minimizes browser reflow.  \n * **Request Streamlining** - Combines multiple individual network requests for images into a single request.| |
|**Image Size Optimization**|Reduces image file size by removing metadata (date and time, camera manufacturer, model, and so on), and by compressing images when possible. Smaller file sizes mean faster load times for images and web pages. | |
|**Sort Query String**|Treats files with the same query strings as the same file in cache, regardless of the order of the query strings. |Enterprise only |
|**Response Buffering**|Enables or disables buffering of responses from the origin server. By default, {{site.data.keyword.cis_short_notm}} sends packets to the client as we receive them. Enabling **Response Buffering** means that {{site.data.keyword.cis_short_notm}} waits until it has the entire file before forwarding it to the user. |Enterprise only |
|**Script Load Optimization**|Improves paint times by asynchronously loading your JavaScripts, including third-party scripts so that they do not block rendering the content of your pages. | |
{: caption="Performance rules" caption-side="bottom"}

## Page rule URL patterns
{: #page-rule-url-patterns}

A page rule takes effect on a specific URL pattern, matching the following format:

`<scheme>://<hostname><:port>/<path>`
{: pre}

An example that uses each component would be:

`https://www.example.com:80/image.png`
{: pre}

The *scheme* and *port* components are optional. If the scheme is omitted, it covers both `http://` and `https://` protocols. If the port is not specified, then the rule matches all ports. You can perform basic wildcard matches by using an asterisk (&asterisk;) symbol in your rule pattern, allowing it to match a series of similar patterns rather than just one.

Here are three important things to remember with page rules:

* Only one page rule takes effect on any given request.
* Page rules are given priority in order from top to bottom.
* After a URL matches a rule, only that rule is applied; that is, if a page rule was already triggered on a request, any subsequent rules that also match the URL pattern do not take effect. Generally, it is recommended to order your rules from *most specific* to *least specific*.

Page rules can be disabled, in which case they take no action. You can still see them in the list and edit them. Setting the **Enabled** toggle to **Off** creates a page rule that initially is disabled.

For more information, see [Using page rules with caching](/docs/cis?topic=cis-use-page-rules-with-caching).
