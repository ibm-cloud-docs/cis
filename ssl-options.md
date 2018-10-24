---
copyright:
  years: 2018
lastupdated: "2018-10-23"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# TLS Options
The TLS options let you control whether visitors can browse your website over a secure connection, and when they do, how CIS will connect to your origin server.

## Automatic HTTPS rewrite
Automatic HTTPS rewrites help fix mixed content by changing “http” to “https” for all resources or links on your web site that can be served with HTTPS.

## TLS encryption modes

These options are listed in the order from the least secure (Off) to the most secure (End-to-End CA signed). 
 * Off (not recommended)
 * Client-to-Edge (edge to origin not encrypted, self-signed certificates are not supported) 
 * End-to-End flexible (edge to origin certificates can be self-signed) 
 * End-to-End CA signed (recommended)
 * HTTPS only origin pull (Enterprise only)

### Off 
No secure connection between your visitor and CIS, and no secure connection between CIS and your web server. Visitors can only view your website over HTTP, and any visitor attempting to connect using HTTPS will receive an `HTTP 301 Redirect` to the plain HTTP version of your website.

### Client-to-Edge
A secure connection between your visitor and CIS, but no secure connection between CIS and your web server. You don't need to have a TLS certificate on your web server, but your visitors still see the site as being HTTPS-enabled. This option is not recommended if you have any sensitive information on your website. This setting will only work for port 443->80. It should only be used as a last resort if you are not able to set up TLS on your own web server. It is _less secure_ than any other option (even “Off”), and could cause you trouble when you decide to switch away from it.

### End-to-End Flexible
A secure connection between your visitor and CIS, and secure connection (but not authenticated) between CIS and your web server. You must have your server configured to answer HTTPS connections, with a self-signed certificate at least. The authenticity of the certificate is not verified: from CIS’s point of view (when we connect to your origin webserver), it’s the equivalent of bypassing this error message. As long as the address of your origin webserver is correct in your DNS settings, you know that we’re connecting to your webserver, and not someone else’s.

### End-to-End CA Signed
Recommended. A secure connection between the visitor and CIS, and secure and authenticated connection between CIS and your web server. You must have your server configured to answer HTTPS connections, with a valid TLS certificate. This certificate must be signed by a certificate authority, have an expiration date in the future, and respond for the request domain name (hostname).

### HTTPS Only Origin Pull
*Enterprise only.* This mode has the same certificate requirements as End-to-End CA Signed and also upgrades all connections between CIS and your origin websever from HTTP to HTTPS, even if the original content requested is over HTTP.
