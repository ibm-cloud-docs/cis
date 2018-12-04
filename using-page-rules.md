---
copyright:
  years: 2018
lastupdated: "2018-03-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Use Page Rules

A Page Rule specifies some settings and values that you can apply to a specific URL pattern that references your domain. Page Rules help you manage security, performance, and reliability based on each individual URL in your site. The following table describes the Page Rules that are available to all customers, the behaviors they produce, and any special considerations you should keep in mind before using them.

## Security

| **Setting** | **Behavior** | **Considerations** |
|-----------|----------|----------------|
|**Browser Integrity Check**|Looks for common HTTP headers abused by spammers, and denies access to your page. It also blocks visitors that do not have a user agent or add a non-standard user agent (also commonly used by abuse bots, crawlers, or APIs). | |
|**Disable Security**|Disables the following features: <ul><li>Email Obfuscation</li> <li>Server Side Excludes</li> <li>WAF</li></ul>|If a rule is set to disable security, and another rule is set to enable the WAF, the WAF rule takes precedence, regardless of the order in which they appear.|
|**Email Obfuscation**|Toggles Email Obfuscation on or off. | |
|**IP Geolocation Header**|Includes the country code of the visitor location with all requests to your website. The information can be found in the `CF-IPCountry` HTTP header. | |  
|**Security Level**|Controls how high a client threat score must be so that a client will encounter a challenge page. This setting can be used so that your site always presents visitors with the **Defense Mode** challenge when they visit your site. | |
|**Server Side Excludes**|Toggles Server Side Excludes on or off.  | |
|**TLS**|Controls which of the TLS modes is used. | |
|**WAF**|Toggles WAF on or off. | |  
|**Automatic HTTPS Rewrites**|Toggles Automatic HTTPS Rewrites on or off.  | |
|**Opportunistic Encryption**|Toggles Opportunistic Encryption on or off.  | |
|**Cache Deception Armor**|Toggles Cache Deception Armor on or off.  | |
|**Always Use HTTPS**|Converts any `http://` URL to an `https://` URL by creating a `301` redirect.|Using this setting disables configuring all other settings for the rule, because IBM CIS forces a redirect to `HTTPS` for the request, which becomes a new request that is then evaluated against Page Rules. |

## Performance
| **Setting** | **Behavior** | **Considerations** |
|-----------|----------|----------------|
|**Browser Cache TTL**|Controls how long resources cached by client browsers remain valid. | |
|**Bypass Cache on Cookie**|Serve a cached object unless we see a cookie of a specific name, for example, serve a cached version of the homepage unless we see a `SessionID` cookie indicating the customer is logged in and therefore should be presented personalized content. | |
|**Cache Level**|**Bypass** - Resources that match that Page Rule are not cached.<br>**No query string** - Only delivers resources from cache when there is no query string.<br>**Ignore query string** - Delivers the same resource to everyone independent of the query string.<br>**Standard** - Delivers a different resource each time the query string changes.<br> **Cache everything** - Resources that match the Page Rule are cached.|By default, HTML content is not cached. A Page Rule to cache static HTML content must be written. |
|**Edge Cache TTL**|Controls how long IBM CIS will retain files in our cache. |This setting is optional when specifying cache level. |
|**Resolve Override**|Change the URL or IP that the request matching the page rule resolves to.||

## Reliability
| **Setting** | **Behavior** | **Considerations** |
|-----------|----------|----------------|
|**Serve Stale Content**|Keeps a limited version of the site online if the server goes down. |For more information view [Managing your CIS deployment for optimal reliability](managing-for-reliability.html) |
|**Origin Cache Control**|Determine what content is cached from the origin and how often the content is updated |For more information view [Managing your CIS deployment for optimal reliability](managing-for-reliability.html) |
|**Forwarding URL** |URL to be used in case the site is unavailable. | Using this disables configuring all other settings because you are forwarding the request somewhere else. For more information view [Managing your CIS deployment for optimal reliability](managing-for-reliability.html)|
|**Host Header Override**|Replace the host header for URI matching the page rule to the value specified. This is commonly used for content hosted in an S3 bucket.|
|**Disable Apps**|Turn off all CIS Apps. | Enterprise only |
|**Origin Error Page Pass-through**|Disables CIS error pages that would trigger for issues sent from the origin server, and instead displays the error pages set at the origin. |Enterprise only ||

## Page Rule URL patterns

A Page Rule will take effect on a given URL pattern, matching the following format:

`<scheme>://<hostname><:port>/<path>`

An example using each component would be:

`https://www.example.com:80/image.png`

The *scheme* and *port* components are optional. If the scheme is omitted, it will cover both `http://` and `https://` protocols. If the port is not specified, then the rule will match all ports. You can perform basic wildcard matches by using a ‘*’ symbol in your rule pattern, allowing it to match a series of similar patterns rather than just one.

Here are three important things to remember with Page Rules:

 * Only one Page Rule will take effect on any given request.
 * Page Rules are given priority in order from top to bottom.
 * Once a URL matches a rule, only that rule only will be applied; that is, if a Page Rule already has been triggered on a request, any subsequent rules that also match the URL pattern do not take effect. As a general rule, we recommend ordering your rules from _most specific_ to _least specific_.

Page Rules can be disabled, in which case they will take no action. They still can be seen in the list and they can be edited. Setting the **Enabled** toggle to **Off** will create a Page Rule that initially is disabled.

For more information, please refer to the [Caching and Page Rules how-to document](caching-with-page-rules.html).

