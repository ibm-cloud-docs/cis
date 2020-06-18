---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-18"

keywords: edge functions, CIS,

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

# Working with Edge functions
{: #edge-functions}

{{site.data.keyword.cis_full}} Edge functions allow you to create new applications or modify existing applications, without having to configure or maintain infrastructure, by utilizing a serverless execution environment. Edge functions can be defined and uploaded to the Cloud edge to process requests before they reach the origin. {{site.data.keyword.cis_short_notm}} Edge functions can be used to modify HTTP requests and responses, make parallel requests, or generate responses from the Cloud edge.
{: shortdesc}

## How Edge functions work
{: #how-edge-functions-work}

Edge functions associates **actions** with URIs based on a defined domain. This association is called a **trigger**. Incoming requests to your site will be intercepted at the cloud's edge and matched against the triggers in your account or domain. If the request URL matches the trigger's URI the action associated with the trigger is executed. 

Edge functions are modeled on the [Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) available in modern web browsers, and use the same API whenever possible.

The Service Worker API allows you to intercept any request which is made to your site. Once your JavaScript is handling the request, you may elect to make any number of subrequests to your site or others, and finally return any response you would like to your visitor.

Unlike standard Service Workers, Edge functions run on CIS edge servers, not in the user’s browser. That means you can trust that your code will run in a trusted environment where it cannot be bypassed by malicious clients. It also means that the user does not need to be using a modern browser that supports Service Workers – you can even intercept requests from API clients that aren't browsers at all.

Internally, Edge functions use the same V8 JavaScript engine which is used in the Google Chrome browser to run workers on our infrastructure. V8 dynamically compiles your JavaScript code into ultra-fast machine code, making it very performant. This makes it possible for your code to execute in microseconds, and for our edge to execute many thousands of scripts per second.

While Edge functions does use V8, it does not use Node.js. The JavaScript APIs available to you inside workers are implemented by us directly. Working with V8 directly allows the code to run more efficiently and with the security controls needed to keep the customers and the infrastructure safe.


## Actions
{: #edge-functions-actions}

Actions are written in JavaScript and require an event listener to respond to a trigger event. Actions will not affect your traffic unless used by a trigger. 

### Enterprise vs standard plans
{: #edge-functions-enterprise-v-standard-plans}

Standard plans have a maximum of one action. The action is assigned a name that is the same as your domain. You may replace your action by uploading another file or update your action using the code editor. Uploading another file will remove the existing action.

Enterprise plans can upload an unlimited number of scripts. These can be given unique names.

### Create actions
{: #edge-functions-create-actions}

Select **Create** to add an action using the code editor. On Enterprise plans enter a name for your action. On Standard plans the name is not editable and is set to the name of your domain. After adding your Javascript code, select **Save** to create your action. 

### Upload actions
{: #edge-functions-upload-actions}

Use the **Upload** button to upload a Javascript file. On Enterprise plans the name of the action is the name of the file. On Standard plans the action name is set to the name of your domain.

Uploading or creating an action with the same name as an existing action will cause the existing action to be overwritten. Rename the action file before uploading or enter a unique name in the text input while creating to avoid this behavior.
{:note}

### Edit actions
{: #edge-functions-edit-actions}

Selecting an action opens the action in the editor for modification. Whenever you save your changes the action will upload to the cloud's edge. After updating select **Save**. If the action is in use, the changes will take effect immediately.

### Delete actions
{: #edge-functions-delete-actions}

Delete an action by clicking the **delete** icon in the **Actions** table. An action cannot be deleted while in use. To delete the action, remove it from the triggers, first. The **Uses** column shows the number of triggers that are associated with this action. Delete cannot be undone.


### Associated triggers
{: #edge-functions-associated-triggers}

Add a trigger and associate it with an action.

### Edge function known limitations
{: #edge-function-known-limitations}

Uploading an action with the same name as an existing action. The existing action will be overwritten. Rename the action file before uploading to avoid this behavior.


## Triggers
{: #triggers}

### About triggers
{: #about-triggers}

Triggers (routes) determine domain traffic routing to the Actions. Triggers associate certain URL patterns, based on a domain on the account, with a predefined action. The URL must contain the domain, but it can contain wildcards either as a prefix to the domain or at the end of the path. If no path is given on the pattern a `/` is added implicitly. The URL pattern cannot contain infix wildcards or query parameters. 

You must add a domain to add triggers. You may add triggers without having actions.

### Add triggers
{: #add-triggers}

Go to the **Triggers** tab and click **Add trigger**. Enter a URL pattern and select an action from the list of existing actions.

For an action you can also select **Avoid Edge Functions**. This allows the trigger's path to remain active but avoid using any Edge Function actions. For example, there is an action called `my-function` and a trigger with the path `gamma.cistest-load.com/*`. If the path `gamma.cistest-load.com/data` should not use the action `my-function` create another trigger with the path `gamma.cistest-load.com/data` and the option **Avoid Edge Functions**. This allows the path `gamma.cistest-load.com/data` to remain active without using the action `my-function`.

### Edit triggers
{: #edit-triggers}

Update a trigger using the menu option in the table row for a selected trigger. After updating select **Save**.

### Delete triggers
{: #delete-triggers}

Delete a trigger using the menu option in the table row for a selected trigger. This action cannot be undone.


## Use cases
{: #edge-functions-use-cases-examples}

These examples are for demonstration purposes only, and not intended for use in production.
{:important}
* [A/B Testing](/docs/cis?topic=cis-edge-functions-use-cases#ab-testing)
* [Adding a Response Header](/docs/cis?topic=cis-edge-functions-use-cases#add-response-header)
* [Aggregating Multiple Requests](/docs/cis?topic=cis-edge-functions-use-cases#aggregate-multiple-requests)
* [Conditional Routing](/docs/cis?topic=cis-edge-functions-use-cases#conditional-routing)
* [Hot-link Protection](/docs/cis?topic=cis-edge-functions-use-cases#hot-link-protection)
* [Originless Responses](/docs/cis?topic=cis-edge-functions-use-cases#originless-responses)
* [Post Requests](/docs/cis?topic=cis-edge-functions-use-cases#post-requests)
* [Setting a Cookie](/docs/cis?topic=cis-edge-functions-use-cases#setting-cookies)
* [Signed Requests](/docs/cis?topic=cis-edge-functions-use-cases#signed-requests)
* [Streaming Responses](/docs/cis?topic=cis-edge-functions-use-cases#streaming-responses)



## Edge functions request properties
{: #edge-functions-requests}

Here, we discuss the Cloudflare runtime APIs for CIS Edge functions. The Edge functions runtime provides the following cloudflare APIs for use by scripts running at the Edge. 
{:shortdesc}

### Constructor syntax
{:#contstructor-syntax}

```javascript
new Request(input [, init])
```
{:pre}

### Constructor parameters
{:#constructor-parameters}

- `input`: Can be either a USVString that contains the URL, or an existing `Request` object. Note that the `url` property is immutable, so when modifying a request and changing the URL, you must pass the new URL in this parameter.

- `init` (optional): An options object that contains custom settings to apply to the request. Valid options are:
  - `method`: The request method, such as `GET` or `POST`
  - `headers`: A `Headers`object
    - `body`: Any text to add to the request. 
      Requests using the `GET` or `HEAD` methods cannot have a body.
      {:note}
    - `redirect`: The mode respected when the request is fetched.  
      The default for requests generated from the incoming `fetchEvent` from the event handler is `manual`. Default for newly constructed Requests (in other words, `new Request(url)` ) is `follow`. Valid options:
      - `follow`: If a redirect reponse is returned to the fetch, another fetch is fired based on the `Location` header in the response until a non-redirect code is returned. For example, `await fetch(..)` could never return a `301` redirect.
      - `manual`: redirect responses return from a fetch.

### Properties
{:#request-properties}

All properties of an incoming `Request` object (`event.request`) are read only. To modify a request, you must create a new `Request` object and pass the options to modify to its constructor.

- `body`: A simple getter that exposes a `ReadableStream` of the contents.
- `bodyUsed`: A Boolean that declares if the body has been used in a response.
- `cf`: An object that contains data provided by our partners at Cloudflare.
- `headers`: Contain the associated `Headers` object for the request.
- `method`: The request method, such as `GET` or `POST`, associated with the request.
- `redirect`: The redirect mode to use: `follow` or `manual`.
- `url`: Contains the URL of the request.

### The `cf` object
{:#cf-object}

In addition to the properties on the standard `Request` object, you can use a `request.cf` object to control how features are applied as well as other custom information provided by Cloudflare. For example,

```
  if (request.cf.asn == 64512) {
    return new Response('Block the ASN 64512 response')
  }
```
{:codeblock}

If you are using [https://cloudflareworkers.com](https://cloudflareworkers.com){:external} to write and test your scripts, the `request.cf` content is not available in preview mode. You must be in production to run that content.
{:note}

These properties contain special information from an incoming request to help with your app's logic. All plans have access to:

- `asn`: ASN of the incoming request (for example, `395747`).
- `colo`: The three-letter airport code of the data center that the request hit (for example, `"DFW"`).
- `weight:` The browser-requested weight for the HTTP/2 prioritization.
- `exclusive:` The browser-requested HTTP/2 exclusive flag (1 for Chromium-based browsers, 0 for others).
- `group:` HTTP/2 stream ID for the request group (non-zero only for Firefox).
- `group-weight`: HTTP/2 weight for the request group (non-zero only for Firefox).
- `tlsCipher`: The cipher for the connection to {{site.data.keyword.cis_short_notm}} (for example, `"AEAD-AES128-GCM-SHA256"`).
- `country`: The two-letter country code of the incoming request. The same value is provided in the `CF-IPCountry` header (for example, `"US"`).
- `tlsClientAuth`: Set only when enabled for mTLS. The object has the following properties: `certIssuerDNLegacy`, `certIssuerDN`, `certIssuerDNRFC2253`, `certSubjectDNLegacy`, `certVerified`, `certNotAfter`, `certSubjectDN`, `certFingerprintSHA1`, `certNotBefore`, `certSerial`, `certPresented`, `certSubjectDNRFC2253`
- `tlsVersion`: The TLS version of the connection to CIS (for example, `TLSv1.3`).

**Standard** and **Enterprise** plans have access to:

- `requestPriority`: The browser-requested prioritization information in the request object (for example, `“weight=192;exclusive=0;group=3;group-weight=127”`).
- `city`: City of the incoming request (for example, `"Austin"`).
- `continent`: Continent of the incoming request (for example, `"NA"`).
- `httpProtocol`: HTTP Protocol (for example, `"HTTP/2"`).
- `latitude`: Latitude of the incoming request (for example, `"30.27130"`).
- `longitude`: Longitude of the incoming request (for example, `"-97.74260"`).
- `postalCode`: PostalCode of the incoming request (for example, `"78701"`).
- `region`: If known, the [ISO 3166-2](https://en.wikipedia.org/wiki/ISO_3166-2){:external} name for the first level region associated with the IP address of the incoming request. If it is not known, it is an empty string (for example, `"Texas"`).
- `regionCode`: If known, the [ISO 3166-2](https://en.wikipedia.org/wiki/ISO_3166-2){:external} code for the first level region associated with the IP address of the incoming request. If it is not known, it is an empty string (for example, `"TX"`).
- `timezone`: Timezone of the incoming request (for example, `"America/Chicago"`).

All plans can set these features on outbound requests.

- `cacheEverything`: This option forces {{site.data.keyword.cis_short_notm}} to cache the response for this request, regardless of what headers are seen on the response. This is equivalent to setting the page rule "Cache Level" to "Cache Everything" (for example, `true`).
- `scrapeShield`: Toggles ScrapeShield (for example, `false`).
- `polish`: Set Cloudflare Polish mode. The possible values are "lossy", "lossless" or "off" (for example, `lossless`).
- `minify`:  Website optimization to  Enable/disable Cloudflare Autominify for various file types. The value is an object containing Boolean fields for `javascript`, `css`, and `html` (for example, `{ javascript: true, css: true, html: false }`).
- `mirage`: Image optimization to enable/disable Cloudflare mirage. When you specify this option, the value should always be `false` (for example, `false`).
- `cacheTtl`: This option forces {{site.data.keyword.cis_short_notm}} to cache the response for this request, regardless of what headers are seen on the response. This is equivalent to setting two page rules: "Edge Cache TTL" and "Cache Level" (to "Cache Everything")(for example,`300`).
- `resolveOverride`: Redirects the request to an alternate origin server. You can use this to implement load balancing across several origins (for example,`us-east.example.com`).
  For security reasons, the hostname set in `resolveOverride` must be proxied on the same {{site.data.keyword.cis_short_notm}} zone of the incoming request. Otherwise, the setting is ignored. CNAME hosts are allowed, so to resolve to a host under a different domain or a DNS only domain first declare a CNAME record within your own zone’s DNS mapping to the external hostname, set proxy on {{site.data.keyword.cis_short_notm}}, then set resolveOverride to point to that CNAME record.
  {:note}

**Enterprise only:**

- `cacheKey`: A request's cache key is what determines if two requests are "the same" for caching purposes. If a request has the same cache key as some previous request, then we can serve the same cached response for both (for example, `'some-key'`).
- `cacheTtlByStatus`: This option is a version of the `cacheTtl` feature which chooses a TTL based on the response's status code. If the response to this request has a status code that matches, {{site.data.keyword.cis_short_notm}} caches for the instructed time, and override cache instructives sent by the origin (for example, `{ "200-299": 86400, 404: 1, "500-599": 0 }`).
  {{site.data.keyword.cis_short_notm}} still adheres to standard cache levels, so by default this overrides cache behavior for static files. If you wish to cache non-static assets, you must set a Cache Level of Cache Everything using a Page Rule.
  {:note}

An Edge Functions script runs after {{site.data.keyword.cis_short_notm}} security features, but before everything else. Therefore, an Edge Functions script cannot affect the operation of security features (since they are already finished), but it can affect other features, like Image Size Optimization, or how the response is cached at the edge.

Updating the `cf` object is similar to modifying a request. You can add the `cf` object to a `Request` by passing a custom object to [`fetch`](/reference/apis/fetch/).

```javascript
// Disable ScrapeShield for this request.
fetch(event.request, { cf: { scrapeShield: false } })
```
{:codeblock}

Invalid or incorrectly-named settings in the cf object will be silently ignored. Be careful to test that you are getting the behavior you want.
{:note}

