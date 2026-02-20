---

copyright:
  years: 2026
lastupdated: "2026-02-20"

keywords:

subcollection: cis

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Troubleshooting ERR_TOO_MANY_REDIRECTS
{: #err-too-many-redirects}

After you [add a new domain](/docs/cis?topic=cis-getting-started#process-overview-new) to CIS, visitors might see `ERR_TOO_MANY_REDIRECTS` or `The page isn’t redirecting properly` errors.

These errors occur when the browser is caught in a redirect loop, repeatedly sending requests between URLs without reaching the final page.

This error is commonly caused by:
* An incorrect SSL/TLS encryption mode configuration.
* Various settings on the Edge Certificates page.
* A misconfigured redirect rule.

If you need help determining whether your origin web server is issuing redirects, contact your hosting provider or site administrator for assistance.
{: note}

## Encryption mode misconfigurations
{: #encrypt-mode-misconfiguration}

Your domain's SSL/TLS Encryption mode determines how CIS connects to your origin server and validates how SSL certificates presented by your origin. This configuration causes redirect loops when the value you set in CIS conflicts with the settings at your origin web server.

### End-to-end flexible encryption mode
{: #endtoend-flexible}

If the domain encryption mode is set to Flexible, Cloudflare sends unencrypted requests to the origin server over HTTP.

A redirect loop occurs if the origin server is configured to automatically redirect all HTTP requests to HTTPS. In this scenario, CIS sends an HTTP request to the origin, the origin redirects to HTTPS, and the cycle repeats.

To resolve this issue, choose one of the following options:

* Remove the HTTP-to-HTTPS redirect from the origin server.
* Change the SSL/TLS encryption mode to Full (or higher). This option requires a valid SSL certificate installed on the origin server.

Ensure that the encryption mode and the origin server configuration are compatible to prevent redirect loops.
