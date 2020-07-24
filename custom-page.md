---

copyright:
  years: 2019, 2020
lastupdated: "2020-07-06"

keywords: Custom error page, Cloud Internet Services, Custom page

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

# Customizing error pages
{: #custom-page}

Cloud Internet Services (CIS) has a wide range of error codes that allow us to differentiate specific problems. By default, these error pages mention Cloudflare; however, you can customize and brand these error pages. Having custom error pages 
allows you to provide a consistent experience for your users, even in the event of a page load error.
{: shortdesc}

There are two groups of customizable error pages:

Challenges
* Basic security
* Web Application Firewall
* IP Firewall (Country block, Country challenge, IP (range) block)

CIS errors
* 502, 504, and CF 52X errors
* 10XX errors
* Errors related to `Serve Stale Content`

500, 501, 503, and 505 responses do not trigger custom error pages to avoid breaking specific API endpoints and other web applications. Custom error pages should be reserved for cases where the origin server cannot return a response for the request (520-526 errors).
{:note}

## Custom error template
{: #custom-error-template}

The following example is a basic custom error template. When creating your custom error templates, note that the maximum page size is 1.5 MB and the page cannot be blank. Additionally, all external resources are inlined using base64 encoding, making them approximately 50% larger when published.

```
<html>
<head></head>
<body>
::[REPLACE WITH TOKEN NAME]::
</body>
</html>
```

## Available custom error tokens
{: #available-custom-error-tokens}

Some types of custom error pages must include one of these tokens anywhere within the HTML of the custom error page. Only one page-specific token can be present per error page, so if you want to customize every error, you must create one custom error page for each error containing the respective token.

|Page Type |Token |
|------|------|
|All pages |	::CLIENT_IP::|
|All pages | 	::RAY_ID::|
|Basic Security (CAPTCHA Challenge) |	::CAPTCHA_BOX::|
|WAF (CAPTCHA Challenge) |	::CAPTCHA_BOX::|
|Country Challenge (CAPTCHA Challenge) |	::CAPTCHA_BOX::|
|Defense Mode (Interstitial Page) |	::IM_UNDER_ATTACK_BOX::|
|5XX Errors 	|::CLOUDFLARE_ERROR_500S_BOX::|
|1XXX Errors 	|::CLOUDFLARE_ERROR_1000S_BOX::|
|Serve Stale Content |	::ALWAYS_ONLINE_NO_COPY_BOX::|

## Styling error codes
{: #styling-error-pages}

Each tag has a unique class that you can use to style individual error codes. It is possible to use CSS to stylize the tags in the div/span/section since they all have class IDs.

Each page (challenge, 5xx errors) has a different ID, so use the preview option to get the proper ID.
{:tip}

## Publishing error pages
{: #publishing-error-pages}

After you're done customizing your error pages, it's time to publish them to our edge. This is done through the [Custom Page CLI](/docs/cis?topic=cis-cli-plugin-cis-cli#custom-page).

When you publish, the custom error page is requested once by us, then cached on the cloud's edge.

## Updating error pages
{: #updating-error-pages}

You can update an error page by re-publishing it.

If CIS cannot load your site, or you have blocked the US in the CIS firewall, publishing and previewing the error page does not work.
{:note}

## Troubleshooting error pages

*  If you encounter errors while attempting to preview or publish your custom error page, run it through a HTML validator and ensure that it is error free.
*  Make sure that the minimum page size is greater than 0. You must add content to your page.
*  Make sure that you are serving the custom error page with a 200 status code.
*  If we cannot load your site, or you have blocked the US in the IP firewall, publishing and previewing the error page does not work.
