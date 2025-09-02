---

copyright:
  years: 2024, 2025
lastupdated: "2025-09-02"

keywords:

subcollection: cis

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Troubleshooting 400 class errors
{: #html-4xx-errors}
{: troubleshoot}

The 4xx class error code responses occur when an issue is at the client end, and is potentially a network issue.
{: shortdesc}

* 4xx codes can be used as a response to any request method.
* An explanation is included in the origin server should be displayed by User-Agent, except for a HEAD request.
* Custom rules can return any response code in the range 400-499 in your HTML page, if the site owner has created a rule with Block action and configured a custom response code.

## Error 400: Bad request
{: #400-error}

The client did not send a correct request to the server. This is a client error, such as a malformed request syntax, invalid request, message framing, or deceptive request routing. For example, if the request contains a special character that is not correctly URL encoded (or percent-encoded), the `HTTP 400` error is returned.

If you're getting an HTTP error when using the {{site.data.keyword.cis_short_notm}} API, make sure that you are using the correct syntax, the correct parameters, and correct body for your API call.

## Error 401: Unauthorized
{: #401-error}

The request was sent without the proper authentication credentials.

## Error 403: Forbidden
{: #403-error}

If you're seeing a 403 error without {{site.data.keyword.cis_short_notm}} branding, this is always returned directly from the origin web server, not {{site.data.keyword.cis_short_notm}}, and is generally related to permission rules on your server. The top reasons for this error are:

* Permission rules you have set on the origin web server (in the Apache .htaccess for example)
* Mod_security rules
* IP deny rules. Ensure that {{site.data.keyword.cis_short_notm}}'s IP ranges aren't being blocked.

{{site.data.keyword.cis_short_notm}} will serve 403 responses if the request violated either a default WAF managed rule or a WAF managed rule enabled for that particular zone.

[Resolution]{: tag-green} If you're seeing a 403 response that contains {{site.data.keyword.cis_short_notm}} branding in the response body, this is the HTTP response code returned along with security features:

* WAF custom or managed rules with the challenge or block action
* Security level that is set to Medium by default
* Most 1xxx {{site.data.keyword.cis_short_notm}} error codes
* The Browser Integrity Check

## Error 404: Not found
{: #404-error}

The origin server was unable or unwilling to find the resource requested. This usually means the host server couldn't find the resource. To serve a more permanent version of this error, use a `410` error code.

These errors typically occur when someone mistypes a URL on your site when there is a broken link from another page, when a page that previously existed is moved or removed, or there is an error when a search engine indexes your site. For a typical site, these errors account for approximately 3% of the total page views, but they're often untracked by traditional analytics platforms.

Website owners usually implement a custom page to be served when this error is generated.

[Resolution]{: tag-green} {{site.data.keyword.cis_short_notm}} does not generate `404` errors for customer websites. {{site.data.keyword.cis_short_notm}} only proxies the request from the origin server. When you see a `404` for your site, contact your hosting provider for help.

## Error 405: Method not allowed
{: #405-error}

The origin server is aware of the requested resource, but the request method is not supported.

[Resolution]{: tag-green} The origin server must also provide an Allow header with a list of supported targets for that resource.

## Error 406: Not acceptable
{: #406-error}

The server can't produce a response that matches the list of acceptable values defined in the request's content negotiation headers, and the server is unwilling to supply a default representation.

[Resolution]{: tag-green} Instead of generating this error, you can serve the less-preferred method to the User-Agent.

## Error 407: Authentication required
{: #407-error}

The client did not send the required authentication with the request.

[Resolution]{: tag-green} Retry the request with the necessary authentication.

## Error 408: Request timeout
{: #408-error}

The origin server did not receive the complete request in a reasonable time. This error implies that the server does not want to wait and continue the connection.

[Resolution]{: tag-green} This error is not common because servers typically use the "close" connection option.

## Error 409: Conflict
{: #409-error}

The request did not complete because of a conflict with the current state of the resource. This error typically happens on a `PUT` request where multiple clients are attempting to edit the same resource.

[Resolution]{: tag-green} The server should generate a payload that includes enough information for the client to recognize the source of the conflict. Clients can and should try the request again.

{{site.data.keyword.cis_short_notm}} generates and serves a `409` response for an `Error 1001: DNS Resolution Error`.

## Error 410: Gone
{: #410-error}

The resource requested is permanently missing at the origin.

[Resolution]{: tag-green} The server is suggesting the links reference the resource should be removed. The server is not qualified to use this status code instead of a `404` response, or required to have this response for any specific period of time.

## Error 411: Length required
{: #411-error}

The client did not define the Content-Length of the request body in the headers, and this parameter is required to obtain the resource.

[Resolution]{: tag-green} The client can resend the request after adding the header field.

## Error 412: Precondition failed
{: #412-error}

The server denies the request because the resource failed to meet the conditions specified by the client.

For an example of version control, a client is modifying an existing resource and sets the `If-Unmodified-Since` header to match the date that the client downloaded the resource and began edits. If the resource was edited (likely by another client) after this date and before the upload of the edits, this response is generated because the date of the last edit comes after the date set in `If-Unmodified-Since` by the client.

[Resolution]{: tag-green} {{site.data.keyword.cis_short_notm}} will serve this response.

## Error 413: Payload too large
{: #413-error}

Refusal from the server to process the request because the payload sent from the client is larger than the server accepts. The server can close the connection.

If this refusal happens only temporarily, then the server should send a `Retry-After` header to specify when the client should try the request again.

The upload limit for the {{site.data.keyword.cis_short_notm}} depends on your plan. If you exceed this limit, your API call receives a `413 Request Entity Too Large` error.

| |Standard|Enterprise|
|-|--------|----------|
|Availability|Yes|Yes|
|Max upload size|200 MB|500 MB|
{: caption="Upload limit by plan" caption-side="bottom"}

[Resolution]{: tag-green} If you require a larger upload, break up requests into smaller chunks, change your DNS record to DNS-only, or upgrade your plan.

## Error 414: URI too long
{: #414-error}

Refusal from the server that the URI was too long to be processed. For example, if a client is attempting a `GET` request with an unusually long URI after a POST, this can be interpreted as a security risk and a `414` error is generated.

[Resolution]{: tag-green} {{site.data.keyword.cis_short_notm}} will generate this response for a URI longer than 32KB.

## Error 415: Unsupported media type
{: #415-error}

Refusal from the server to process the format of the current payload. One way to identify and fix this issue is to look at the `Content-Type` or `Content-Encoding` headers sent in the client's request.

## Error 416: Range not satisfiable
{: #416-error}

The `416` error response code indicates that a server can't serve the requested ranges. For example:

* `HTTP/1.1 416 Range Not Satisfiable`
* `Content-Range: bytes */12777`

[Resolution]{: tag-green} The most common reason for a `416` error is that the file doesn't include such ranges. Browsers usually request the entire file again or abort the operation.

## Error 417: Expectation failed
{: #417-error}

The server failed to meet the requirements specified in the `Expect` header of the client's request.

## Error 429: Too many requests
{: #429-error}

The client sent too many requests in the specified amount of time, according to the server (often known as “rate-limiting”). The server might respond with information allowing the requester to retry the request after a specific period of time.

The default global rate limit for the {{site.data.keyword.cis_short_notm}} API is 100 requests per minute per user, and applies cumulatively regardless of whether the request is made through the dashboard, API key, or API token. If you exceed this limit, all API calls for the next five minutes are blocked, receiving an `HTTP 429` response.

Some specific API calls have their own limits and are documented separately, such as Cache Purge APIs, GraphQL APIs, and rulesets APIs.

[Resolution]{: tag-green} Enterprise customers can contact Support to raise the limit.

{{site.data.keyword.cis_short_notm}} generates and sends this status code when a request is being rate limited. If visitors to your site are receiving these error codes, you are able to see this in the Rate Limiting Analytics.

## Error 451: Unavailable for legal reason
{: #451-error}

The server is unable to deliver the resource due to legal actions.

Typically search engines and ISPs are affected by this response code, not the origin server. The response should include an explanation in the response body with details of the legal demand.

## Error 499: Client close request
{: #499-error}

Error `499` is an nginx-specific response code to indicate when the connection has been closed by the client while the server is still processing its request, which makes the server unable to send a status code back.

This error is shown in {{site.data.keyword.cis_short_notm}} logs and status code analytics for Enterprise customers.

Because the {{site.data.keyword.cis_short_notm}} partner Cloudflare is built on nginx, there is a 499 HTTP code in Cloudflare logs and analytics for connections, which are terminated before {{site.data.keyword.cis_short_notm}} has finished processing the request. It is expected behavior to see these in your logs when clients close connections.
{: note}

To provide more context, a TCP connection must be established between {{site.data.keyword.cis_short_notm}} and the website's origin server before any higher protocol starts the “conversation”. To establish a connection, TCP uses a three-way handshake:

1. SYN: {{site.data.keyword.cis_short_notm}} sends three SYN packets to the origin server.
1. SYN+ACK: In response, the origin server replies with an SYN+ACK.
1. ACK: Finally, {{site.data.keyword.cis_short_notm}} sends an ACK back to the origin server.

At this point, both {{site.data.keyword.cis_short_notm}} and the origin server have received an acknowledgment of the connection, and communication is established. However, if the origin server does not send a SYN+ACK back to {{site.data.keyword.cis_short_notm}} within 15 seconds, {{site.data.keyword.cis_short_notm}} retries one more time.

Depending on the timeout value on the client side, you might see three different scenarios with their own status code generated.

* If the client has a shorter timeout (less than 30 seconds), they give up the connection, and {{site.data.keyword.cis_short_notm}} logs the `499` error.
* If the client has a higher timeout (more than 30 seconds), after the TCP connection is established, the HTTP transaction continues. In this case, {{site.data.keyword.cis_short_notm}} returns a normal status code of `HTTP 200`.
* If the client has a higher timeout and {{site.data.keyword.cis_short_notm}} was not able to establish the TCP handshake with the origin server, {{site.data.keyword.cis_short_notm}} returns `HTTP 522`.
