---

copyright:
  years: 2026
lastupdated: "2026-03-03"

keywords:

subcollection: cis

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why am I seeing ERR_TOO_MANY_REDIRECTS in CIS?
{: #ts-redirect-loops}
{: troubleshoot}

The `ERR_TOO_MANY_REDIRECTS` error occurs when a browser is unable to load a website because it becomes stuck in a continuous redirect cycle. Instead of reaching the intended page, the request is repeatedly sent between URLs. In CIS, this issue most commonly appears after adding a [new domain](/docs/cis?topic=cis-getting-started#process-overview-new) or modifying security, SSL/TLS, or redirect configurations.

When you try to access a website:
* The browser sends a request to a URL (for example, `http://example.com`).
* The server or CIS responds with a redirect to another URL.
* That redirected URL triggers another redirect.
* The cycle continues indefinitely.

Because the browser never reaches a final destination page, it eventually stops and displays:
* `ERR_TOO_MANY_REDIRECTS`
* `The page isn’t redirecting properly`

`ERR_TOO_MANY_REDIRECTS` does not indicate a connectivity issue. It indicates a configuration conflict where redirect logic never resolves to a final destination.

A redirect loop happens when multiple components attempt to enforce conflicting rules.
{: tsSymptoms}

In CIS, this typically occurs because of one of the following configuration conflicts:
* SSL/TLS encryption mode misconfigurations
* Edge certificate settings conflict with origin behavior
* Conflicting redirect rules

To determine which scenario applies, consider what changed before the issue started:
{: tsCauses}

* Did the issue begin after modifying the SSL/TLS encryption mode?
* Did the issue begin after enabling Always Use HTTPS or HSTS?
* Did the issue begin after creating or editing redirect rules?

The resolution depends on which configuration conflict is causing the redirect loop. Review the following scenarios and apply the solution that matches your configuration.
{: tsResolve}

## Scenario 1: SSL/TLS encryption mode misconfigurations
{: #encryption-mode-misconfigure}

Your domain's SSL/TLS encryption mode determines how CIS connects to your origin server and validates how SSL certificates presented by your origin. This configuration causes redirect loops when the value you set in CIS conflicts with the settings at your origin web server.

### Flexible mode + origin forces HTTP → HTTPS
{: #end-to-end-flexible-encryption}

If the domain encryption mode is set to End-to-End flexible, CIS sends unencrypted requests to the origin server over HTTP.
1. CIS forwards the request to the origin using HTTP.
1. The origin server redirects the HTTP request to HTTPS.
1. CIS again connects to the origin over HTTP (because Flexible mode enforces HTTP to origin).
1. The origin again redirects to HTTPS.

This process repeats, creating a redirect loop.

### CA Signed mode + origin forces HTTPS → HTTP
{: #end-end-ca-signed}

When the domain encryption mode is set to End-to-end CA signed, CIS sends encrypted requests to your origin server over HTTPS.
1. CIS forwards the request to the origin using HTTPS.
1. The origin server redirects HTTPS requests to HTTP.
1. CIS continues sending HTTPS requests to the origin.
1. The origin continues redirecting to HTTP.

This creates an HTTPS-to-HTTP redirect loop.

Redirect loops occur when the SSL/TLS encryption mode configured in CIS conflicts with redirect behavior on the origin server:
{: tsSymptoms}

* In Flexible mode, CIS communicates with the origin over HTTP while the origin enforces HTTP-to-HTTPS redirection.
* In CA Signed mode, CIS communicates with the origin over HTTPS while the origin redirects HTTPS traffic back to HTTP.

Because both layers attempt to control protocol behavior differently, the request never reaches a final destination.
{: tsCauses}

Choose one of the following options:
* Remove the HTTP-to-HTTPS or HTTPS-to-HTTP redirect from the origin server.
* Change the SSL/TLS encryption mode to Full (or higher) if appropriate. This option requires a valid SSL certificate installed on the origin server.

Ensure that the encryption mode and the origin server configuration are compatible to prevent redirect loops.

If you are unsure whether your origin server is issuing redirects, contact your hosting provider or site administrator for assistance.
{: tsResolve}

## Scenario 2: Edge certificate settings conflict with origin behavior
{: #edge-certificare-settings}

Edge certificate settings in CIS determine how HTTPS is enforced between end users and CIS. When these settings do not align with your origin server configuration or domain encryption mode, they can unintentionally create redirect loops.

Redirect loops occur when multiple layers attempt to enforce different protocol behaviors (HTTP versus HTTPS), preventing the request from reaching a final destination.

The most common edge settings involved in this issue are **Always Use HTTPS** and **HTTP Strict Transport Security (HSTS)**.

### Always Use HTTPS conflicts with origin redirects
{: #always-use-https}

If you have **Always Use HTTPS** enabled for your domain, CIS redirects all `http` requests to `https` for all subdomains and hosts in your application.

When **Always Use HTTPS** is enabled:
{: tsSymptoms}

1. A user sends a request using `HTTP`.
1. CIS immediately redirects the request to `HTTPS`.
1. CIS forwards the `HTTPS` request to the origin server.
1. If the origin redirects `HTTPS` traffic back to `HTTP`, the request cycles again.
1. The browser eventually stops the repeated redirects and displays a redirect error.


A redirect loop occurs when:
* CIS upgrades HTTP traffic to HTTPS.
* The origin server downgrades HTTPS traffic back to HTTP.

Because both layers enforce opposite protocol behavior, the request continuously alternates between HTTP and HTTPS without reaching a final page.
{: tsCauses}

Use one of the following options:
{: tsResolve}

* Remove the `HTTPS-to-HTTP` redirect from the origin server.
* Disable **Always Use HTTPS**.

### HSTS forces HTTPS while origin downgrades to HTTP
{: #http-hsts}

HTTP Strict Transport Security (HSTS) is a security policy that instructs supported browsers to always access your domain using `HTTPS`. When enabled, CIS sends an `HSTS` response header that tells browsers to automatically convert future `HTTP` requests to `HTTPS`.

When HSTS is enabled:
{: tsSymptoms}

1. The browser receives the HSTS header from CIS.
1. The browser automatically converts future HTTP requests to HTTPS.
1. If the origin server redirects HTTPS traffic to HTTP, the browser upgrades it back to HTTPS.
1. This repeated upgrade/downgrade behavior creates a redirect loop.
1. The browser eventually stops loading the page and displays an error.

This typically occurs when:
{: tsCauses}

* The origin server redirects HTTPS requests to HTTP, or
* The domain encryption mode is set to `Off`.

HSTS enforces HTTPS at the client side, while the origin attempts to downgrade the connection. This protocol mismatch causes continuous redirection.

To resolve this issue:
{: tsResolve}

* Remove any `HTTPS-to-HTTP` redirects from the origin server and ensure the domain encryption mode is set to Flexible or higher.
* Alternatively, disable HSTS.

## Scenario 3: Conflicting redirect rules
{: #redirect-rules}

Redirect loops can also occur when multiple redirect configurations conflict with each other. This may involve redirect rules, page rules, load balancer rules, or application-level redirects that unintentionally overlap.

When more than one rule attempts to control the same request path, traffic can be redirected in a circular pattern.

A redirect loop occurs when:
* One rule redirects a request from URL A to URL B.
* Another rule redirects URL B back to URL A (or to another URL that eventually points back to A).
* The browser repeatedly follows these redirects.
* No final destination page is reached.

As a result, the browser stops the process and displays a redirect error.
{: tsSymptoms}

This typically happens because:
* Multiple redirect rules target overlapping URL patterns.
* Redirect rules and Page Rules enforce different behaviors.
* Both CIS and the origin server define redirects for the same traffic.
* Wildcard or broad match conditions unintentionally apply to unintended URLs.

Without careful rule order and validation, these configurations can create circular redirect paths.
{: tsCauses}

Review your various redirect rules and Page Rules to make sure no rules are in conflict with each other. Ensure that no rules redirect traffic in a circular pattern.
{: tsResolve}
