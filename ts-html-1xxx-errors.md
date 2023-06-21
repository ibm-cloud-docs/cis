---

copyright:
  years: 2021, 2023
lastupdated: "2023-05-09"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Troubleshooting 1000 class errors
{: #html-1xxx-errors}

The following error codes appear in the HTML body of 530 error messages. For more information, see [Error 530](/docs/cis?topic=cis-html-5xx-errors#530-error).
{: shortdesc}

## Error 1000: DNS points to prohibited IP
{: #1000-error}

{{site.data.keyword.cis_short_notm}} halted the request for one of the following reasons:

* An A record within your {{site.data.keyword.cis_short_notm}} DNS points to a {{site.data.keyword.cis_short_notm}} IP address.
* Your {{site.data.keyword.cis_short_notm}} DNS A or CNAME record references another reverse proxy (such as an nginx web server that uses the proxy_pass function) that then proxies the request to {{site.data.keyword.cis_short_notm}} a second time.
* The request X-Forwarded-For header is longer than 100 characters.
* The request includes two X-Forwarded-For headers.

### Resolution
{: #1000-resolution}

* If an A record within your {{site.data.keyword.cis_short_notm}} DNS points to a {{site.data.keyword.cis_short_notm}} IP address, update the IP address to your origin web server IP address.
* There is a reverse-proxy at your origin that sends the request back through the {{site.data.keyword.cis_short_notm}} proxy. Instead of using a reverse-proxy, contact your hosting provider or site administrator to configure an HTTP redirect at your origin.

## Error 1001: DNS resolution error
{: #1001-error}

Common causes for 1001 errors are:

* A web request was sent to a {{site.data.keyword.cis_short_notm}} IP address for a non-existent {{site.data.keyword.cis_short_notm}} domain.
* An external domain that is not on using {{site.data.keyword.cis_short_notm}} has a CNAME record to a domain active on {{site.data.keyword.cis_short_notm}}
* The target of the DNS CNAME record does not resolve.
* A CNAME record in your {{site.data.keyword.cis_short_notm}} DNS requires resolution via a DNS provider that is currently offline.
* Serve Stale Content is enabled for a Custom Hostname (SSL for SaaS) domain.

### Resolution
{: #1001-resolution}

A non-{{site.data.keyword.cis_short_notm}} domain cannot CNAME to a {{site.data.keyword.cis_short_notm}} domain unless the non-{{site.data.keyword.cis_short_notm}} domain is added to a {{site.data.keyword.cis_short_notm}} account.

Attempting to directly access DNS records used for {{site.data.keyword.cis_short_notm}} CNAME setups also causes error 1001.

Disable **Always Online** if using Custom Hostnames (SSL for SaaS).

## Error 1002: DNS points to Prohibited IP
{: #1002-error-dns}

Common causes for 1002 errors when a DNS points to a prohibited IP address are:

* A DNS record in your {{site.data.keyword.cis_short_notm}} DNS points to one of {{site.data.keyword.cis_short_notm}}'s IP addresses.
* An incorrect target is specified for a CNAME record in your {{site.data.keyword.cis_short_notm}} DNS.
* Your domain is not on {{site.data.keyword.cis_short_notm}} but has a CNAME that refers to a {{site.data.keyword.cis_short_notm}} domain.

### Resolution
{: #1002-dns-resolution}

Update your {{site.data.keyword.cis_short_notm}} A or CNAME record to point to your origin IP address instead of a {{site.data.keyword.cis_short_notm}} IP address:

1. Contact your hosting provider to confirm your origin IP address or CNAME record target.
1. Log in to your {{site.data.keyword.cis_short_notm}} account.
1. Select the domain that generates error 1002.
1. Select the DNS app.
1. Click Value for the A record to update.
1. Update the A record.

To ensure your origin web server doesn’t proxy its own requests through {{site.data.keyword.cis_short_notm}}, configure your origin webserver to resolve your {{site.data.keyword.cis_short_notm}} domain to:

* The internal NAT-ed IP address, or
* The public IP address of the origin web server.

## Error 1002: Restricted
{: #1002-error-restricted}

The most common cause of 1002: Restricted errors is when the {{site.data.keyword.cis_short_notm}} domain resolves to a local or disallowed IP address or an IP address not associated with the domain.

### Resolution
{: #1002-restricted-resolution}

If you own the website:

1. Confirm your origin web server IP addresses with your hosting provider
2. Log in to your {{site.data.keyword.cis_short_notm}} account
3. Update the A records in the {{site.data.keyword.cis_short_notm}} DNS to the IP address confirmed by your hosting provider

## Error 1003 Access Denied: Direct IP Access Not Allowed
{: #1003-error}

The most common cause of 1003 errors is when a client or browser directly accesses a {{site.data.keyword.cis_short_notm}} IP address.

### Resolution
{: #1003-resolution}

Browse to the website domain name in your URL instead of the {{site.data.keyword.cis_short_notm}} IP address.

## Error 1004: Host Not Configured to Serve Web Traffic
{: #1004-error}

Common causes of 1004 errors are:

* {{site.data.keyword.cis_short_notm}} staff disabled proxying for the domain due to abuse or terms of service violations.
* DNS changes have not yet propagated or the site owner’s DNS A records point to {{site.data.keyword.cis_short_notm}} IP addresses.

### Resolution
{: #1004-resolution}

If the issue persists beyond 5 minutes, contact {{site.data.keyword.cis_short_notm}} support.

## Errors 1006, 1007, 1008 or 1106 Access Denied: Your IP address has been banned
{: #1006-7-8-errors}

Common causes for errors 1006, 1007, and 1008 errors are:

* A {{site.data.keyword.cis_short_notm}} customer blocked traffic from your client or browser.
* Error 1006 also occurs in the {{site.data.keyword.cis_short_notm}} Edge Functions under the Preview tab when a customer uses Zone Lockdown or any other {{site.data.keyword.cis_short_notm}} security feature to block the Google Cloud Platform IPs that the Preview tab relies upon.

### Resolution
{: #1006-resolution}

Request the website owner to investigate their {{site.data.keyword.cis_short_notm}} security settings or allow your client IP address. Because the website owner blocked your request, {{site.data.keyword.cis_short_notm}} support cannot override a customer’s security settings.

## Errors 1009 Access Denied: Country or region banned
{: #1009-error}

A common cause of 1009 errors is when the owner of the website (for example, `example.com`) has banned the country or region your IP address in from accessing the website.

### Resolution
{: #1009-resolution}

Ensure your IP address is allowed under the IP Access Rules security feature.

## Error 1010: The owner of this website has banned your access based on your browser's signature
{: #1010-error}

A common cause of 1010 errors is when a website owner blocks your request based on your client's web browser.

### Resolution
{: #1010-resolution}

Notify the website owner of the blocking. If you cannot determine how to contact the website owner, lookup contact information for the domain via the Whois database. Site owners disable Browser Integrity Check via the **Security Advanced** tab.

Because the website owner performed the blocking, {{site.data.keyword.cis_short_notm}} support cannot override a customer’s security settings.

## Error 1011: Access Denied (Hotlinking Denied)
{: #1011-error}

A common cause of 1011 errors is when a request is made for a resource that uses {{site.data.keyword.cis_short_notm}} hotlink protection.

### Resolution
{: #1011-resolution}

Notify the website owner of the blocking. If you cannot determine how to contact the website owner, lookup contact information for the domain via the Whois database.  

Because the website owner performed the blocking, {{site.data.keyword.cis_short_notm}} support cannot override a customer’s security settings.

## Error 1012: Access Denied
{: #1012-error}

A common cause of 1012 errors is when a website owner forbids access based on malicious activity detected from the visitor’s computer or network (`ip_address`). The most likely cause is a virus or malware infection on the visitor’s computer.

### Resolution
{: #1012-resolution}

Update your antivirus software and run a full system scan. {{site.data.keyword.cis_short_notm}} cannot override the security settings the site owner has set for the domain. To request website access, contact the site owner to allow your IP address. If you cannot determine how to contact the website owner, look up contact information for the domain by using the Whois database.

Because the website owner performed the blocking, {{site.data.keyword.cis_short_notm}} support cannot override a customer’s security settings.

## Error 1013: HTTP hostname and TLS SNI hostname mismatch
{: #1013-error}

A common cause of 1013 errors is when the hostname sent by the client or browser via Server Name Indication (SNI) does not match the request host header.

Error 1013 is commonly caused by the following:

* your local browser setting the incorrect SNI host header
* a network proxying SSL traffic caused a mismatch between SNI and the Host header of the request.

### Resolution
{: #1013-resolution}

Test for an SNI mismatch via an online tool such as SSL Shopper.

Provide {{site.data.keyword.cis_short_notm}} Support a HAR file captured while duplicating the error.

## Error 1014: CNAME Cross-User Banned
{: #1014-error}

By default, {{site.data.keyword.cis_short_notm}} prohibits a DNS CNAME record between domains in different {{site.data.keyword.cis_short_notm}} accounts. CNAME records are permitted within a domain (`www.example.com` CNAME to `api.example.com`) and across zones within the same user account (`www.example.com` CNAME to `www.example.net`).

### Resolution
{: #1014-resolution}

To allow CNAME record resolution to a domain in a different {{site.data.keyword.cis_short_notm}} account, the domain owner of the CNAME target must contact {{site.data.keyword.cis_short_notm}} Support and specify the domains allowed to CNAME to their target domain.

## Error 1015: You are being rate limited
{: #1015-error}

A common cause of 1015 errors is when the site owner implemented Rate Limiting that affects your visitor traffic.

Unable to purge is another 1015 error code relating to {{site.data.keyword.cis_short_notm}} cache purge. Retry the cache purge and contact {{site.data.keyword.cis_short_notm}} support if errors persist.

### Resolution
{: #1015-resolution}

* If you are a site visitor, contact the site owner to request exclusion of your IP from rate limiting.
* If you are the site owner, review {{site.data.keyword.cis_short_notm}} Rate Limiting thresholds and adjust your Rate Limiting configuration.
* If your Rate Limiting blocks requests in a short time period (for instance, 1 second) try increasing the time period to 10 seconds.

For guidance on when you expect a new Edge function to exceed rate limits, see [Working wiht Edge functions](/docs/cis?topic=cis-working-with-edge-functions).

## Error 1016: Origin DNS error
{: #1056-error}

Error 1016 occurs when {{site.data.keyword.cis_short_notm}} cannot resolve the origin web server’s IP address.

Common causes for Error 1016 are:

* A missing DNS A record that mentions origin IP address.
* A CNAME record in the {{site.data.keyword.cis_short_notm}} DNS points to an unresolvable external domain.
* The origin host names (CNAMEs) in your {{site.data.keyword.cis_short_notm}} Load Balancer default, region, and fallback pools are unresolvable. Use a fallback pool configured with an origin IP as a backup in case all other pools are unavailable.
* When creating a Range app with a CNAME origin, you need first to create a CNAME on the {{site.data.keyword.cis_short_notm}} DNS side that points to the origin. 

### Resolution
{: #1016-resolution}

To resolve an error 1016:

* Verify your {{site.data.keyword.cis_short_notm}} DNS settings include an A record that points to a valid IP address that resolves via a DNS lookup tool.
* For a CNAME record pointing to a different domain, ensure that the target domain resolves via a DNS lookup tool.

## Error 1018: Could not find host
{: #1018-error}

Common causes of an 1018 error are:

* The {{site.data.keyword.cis_short_notm}} domain was recently activated and there is a delay propagating the domain’s settings to the {{site.data.keyword.cis_short_notm}} edge network.
* The {{site.data.keyword.cis_short_notm}} domain was created via a {{site.data.keyword.cis_short_notm}} partner (for example, a hosting provider) and the provider's DNS failed.

Error 1018 is returned via an HTTP 409 response code.

### Resolution
{: #1018-resolution}

Contact Support with the following details:

* Your domain name
* A screenshot of the 1018 error including the RayID mentioned in the error message
* The time and timezone the 1018 error occurred

## Error 1019: Compute server error
{: #1019-error}

A common cause of error 1019 is when a {{site.data.keyword.cis_short_notm}} Edge function script recursively references itself.

### Resolution
{: #1019-resolution}

Ensure your {{site.data.keyword.cis_short_notm}} Edge function does not access a URL that calls the same Edge function script.

## Error 1020: Access denied
{: #1020-error}

A common cause of an error 1020 is when a client or browser is blocked by a {{site.data.keyword.cis_short_notm}} customer’s firewall rules.

### Resolution
{: #1020-resolution}

If you are not the website owner, provide the website owner with a screenshot of the 1020 error message you received.

If you are the website owner:

1. Retrieve a screenshot of the 1020 error from your customer
1. Search the Firewall Events Log within the Overview tab of your Firewall app for the RayID or client IP Address from the visitor’s 1020 error message.
1. Convert the UTC timestamp of the 1020 error to your local timezone when searching in the Firewall Events Log.
1. Assess the cause of the block and either update the Firewall Rule or allow the visitor’s IP address in IP Access Rules.

## Error 1023: Could not find host
{: #1023-error}

Common causes of an error 1023 are:

* If the owner just signed up for {{site.data.keyword.cis_short_notm}} it can take a few minutes for the website's information to be distributed to our global network. 
* Something is wrong with the site's configuration. Usually, this happens when accounts have been signed up with a partner organization (for example, a hosting provider) and the provider's DNS fails.

Error 1023 is returned via a HTTP 409 response code.

### Resolution
{: #1023-resolution}

Contact Support with the following details:

* Your domain name
* A screenshot of the 1023 error including the RayID mentioned in the error message
* The time and timezone the 1023 error occurred

## Error 1025: Please check back later
{: #1025-error}

A common cause of error 1025 is when a request is not serviced because the domain has reached plan limits for Edge functions.

### Resolution
{: #1025-resolution}

Contact Support to adjust the limits for Edge functions.

## Error 1035: Invalid request rewrite (invalid URI path)
{: #1035-error}

Common causes of error 1035 are when the value or expression of your rewritten URI path is not valid, and when the destination of the URL rewrite is a path under `/cdn-cgi/`.

### Resolution
{: #1035-resolution}

Make sure that the rewritten URI path is not empty and that it starts with a `/` (slash) character.

For example, the following URI path rewrite expression is not valid:

`concat(lower(ip.geoip.country), http.request.uri.path)`

To fix the expression, add a `/` prefix:

`concat("/", lower(ip.geoip.country), http.request.uri.path)`

## Error 1036: Invalid request rewrite (maximum length exceeded)
{: #1036-error}

A common cause of error 1036 is when the value or expression of your rewritten URI path or query string is too long.

### Resolution
{: #1036-resolution}

Use a shorter value or expression for the new URI path/query string value.

## Error 1037: Invalid rewrite rule (failed to evaluate expression)
{: #1037-error}

A common cause of error 1037 is when the expression of the rewrite rule could not be evaluated. There are several causes for this error, but it can mean that one expression element contained an undefined value when it was evaluated.

For example, you get a 1037 error when using the following URL rewrite dynamic expression and the X-Source header is not included in the request:

`http.request.headers["x-source"][0]`

### Resolution
{: #1037-resolution}

Make sure that all the elements of your rewrite expression are defined. For example, if you are referring to a header value, ensure the header is set.

## Error 1040: Invalid request rewrite (header modification not allowed)
{: #1040-error}

A common cause of error 1040 is when you are trying to modify an HTTP header that HTTP Request Header Modification Rules cannot change.

### Resolution
{: #1040-resolution}

Make sure you are not trying to modify one of the reserved HTTP request headers.

## Error 1041: Invalid request rewrite (invalid header value)
{: #1041-error}

A common cause of error 1041 is when the added/modified header value is too long or it contains characters that are not allowed.

### Resolution
{: #1041-resolution}

* Use a shorter value or expression to define the header value.
* Remove the characters that are not allowed. See Format of HTTP request header names and values in Developer Docs for more information on the allowed characters.

## Error 1101: Rendering error
{: #1101-error}

A common cause of error 1101 is when an {{site.data.keyword.cis_short_notm}} Edge function throws a runtime JavaScript exception.

### Resolution
{: #1101-resolution}

Provide appropriate issues details to Support.

## Error 1102: Rendering error
{: #1102-error}

A common cause of error 1102 is when an Edge function exceeds a CPU time limit. CPU time is the time spent executing code (for example, loops, parsing JSON, etc). Time spent on network requests (fetching, responding) does not count towards CPU time.

### Resolution
{: #1102-resolution}

Contact the developer of your Edge function code to optimize code for a reduction in CPU usage in the active Edge function scripts.

## Error 1200: Cache connection limit
{: #1200-error}

Error 1200 occurs when there are too many requests queued on the edge that are awaiting process by your origin web server.  This limit protects {{site.data.keyword.cis_short_notm}}'s systems.

### Resolution
{: #1200-resolution}

Tune your origin webserver to accept incoming connections faster.  Adjust your caching settings to improve cache-hit rates so that fewer requests reach your origin web server.  Reach out to your hosting provider or web administrator for assistance.
