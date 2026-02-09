---

copyright:
  years: 2023, 2026
lastupdated: "2026-02-09"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Setting security headers
{: #setting-security-headers}

To help improve web application security, it is a best practice to set HTTP security headers at the edge or in your application. The following JavaScript example demonstrates how to implement these headers. By modifying the response headers in-flight, you can easily add protections like these common security headers without changing your back-end application.

X-XSS-Protection
:   Prevents a page from loading if an XSS attack is detected. [Learn more](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/X-XSS-Protection){: external}  For example: 

   `"X-XSS-Protection": "1; mode=block",`

X-Frame-Options
:   Helps prevent clickjacking attacks. [Learn more](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/X-Frame-Options){: external}   For example: 

    `"X-Frame-Options": "DENY",` 

X-Content-Type-Options
:   Stops browsers from MIME-sniffing a response away from the declared content-type. [Learn more](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/X-Content-Type-Options){: external}  For example: 

    `"X-Content-Type-Options": "nosniff",`

Permissions-Policy
:   Lets you control access to browser features. For example, to opt out of Federated Learning of Cohorts (FLoC): 

    `"Permissions-Policy": "interest-cohort=()",`

Referrer-Policy
:   Controls how much referrer information is included with requests. For example: 

    `"Referrer-Policy": "strict-origin-when-cross-origin",`

Strict-Transport-Security
:   Enforces secure (HTTPS) connections to your server. These headers are not automatically set because your website might get added to Chrome's HTTP Strict Transport Security (HSTS) preload list. For example: 

    `"Strict-Transport-Security" : "max-age=63072000; includeSubDomains; preload",`

Content-Security-Policy
:   Permits content from a trusted domain and all its subdomains. [Learn more](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Content-Security-Policy){: external}  For example: 

    `"Content-Security-Policy": "default-src 'self' example.com *.example.com",`

## Javascript example
{: #javascript-example}

```js
export default {
  async fetch(request) {
    const DEFAULT_SECURITY_HEADERS = {  
      "X-Content-Type-Options": "nosniff",
      "Referrer-Policy": "strict-origin-when-cross-origin",
      "Cross-Origin-Embedder-Policy": 'require-corp; report-to="default";',
      "Cross-Origin-Opener-Policy": 'same-site; report-to="default";',
      "Cross-Origin-Resource-Policy": "same-site",
    };
    const BLOCKED_HEADERS = [
      "Public-Key-Pins",
      "X-Powered-By",
      "X-AspNet-Version",
    ];

    let response = await fetch(request);
    let newHeaders = new Headers(response.headers);

    const tlsVersion = request.cf.tlsVersion;
    console.log(tlsVersion);
    // This sets the headers for HTML responses:
    if (
      newHeaders.has("Content-Type") &&
      !newHeaders.get("Content-Type").includes("text/html")
    ) {
      return new Response(response.body, {
        status: response.status,
        statusText: response.statusText,
        headers: newHeaders,
      });
    }

    Object.keys(DEFAULT_SECURITY_HEADERS).map((name) => {
      newHeaders.set(name, DEFAULT_SECURITY_HEADERS[name]);
    });

    BLOCKED_HEADERS.forEach((name) => {
      newHeaders.delete(name);
    });

    if (tlsVersion !== "TLSv1.2" && tlsVersion !== "TLSv1.3") {
      return new Response("You need to use TLS version 1.2 or higher.", {
        status: 400,
      });
    } else {
      return new Response(response.body, {
        status: response.status,
        statusText: response.statusText,
        headers: newHeaders,
      });
    }
  },
};
```
{: codeblock}
