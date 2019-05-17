---

copyright:
  years: 2019
lastupdated: "2019-05-06"

keywords: Custom error page, Cloud Internet Services, Custom page

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}

# Custom page
{: #custom-page}

Cloud Internet Services (CIS) has a wide range of error codes that allow us to differentiate specific problems. By default, these error pages mention Cloudflare; however, you can customize and brand these error pages. Having custom error pages allows to provide a consistent experience for your users, even in the event of a page load error.

There are two groups of customizable error pages:

Challenges
* Basic security
* Web Application Firewall
* IP Firewall (Country block, Country challenge, IP (range) block)

CIS errors
* 502, 504, and CF 52X errors
* 10XX errors
* Errors related to `Server Stale Content` 

500, 501, 503, and 505 responses do not trigger custom error pages to avoid breaking specific API endpoints and other web applications. Custom error pages should be reserved for cases where the origin server cannot return a response for the request (520-526 errors).
{:note}

## Customizing your error pages
{: #customize-error-page}

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

Some types of custom error pages must include one of the below tokens anywhere within the HTML of the custom error page. Only one page specific token may be present per error page, so if you wish to customize every error you must create one custom error page for each error containing the respective token.

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

## Styling
{: #styling-error-pages}

Each tag has a unique class that you can use to style individual error codes. It is possible to use CSS to stylize the tags in the div/span/section since they all have class IDs. 

Each page (challenge, 5xx errors) has a different ID, so use the preview option to get the proper ID.
{:tip}

## Publishing
{: #publishing-error-pages}

Once you're done customizing your error pages, it's time to publish them to our edge. This is done through the [Custom Page CLI](/docs/cis-cli-plugin?topic=cis-cli-plugin-cis-cli-commands#custom-page).

When you publish, the custom error page is requested once by us, then cached on the cloud's edge.

## Updating
{: #updating-error-pages}

Error pages can be updated by re-publishing them. 
If we cannot load your site or you have blocked the US in the CIS firewall, publishing and previewing the error page will not work.
{:note}

## Troubleshooting custom error pages

*  If you encounter errors while attempting to preview or publish your custom error  page, run it through a HTML validator and ensure that it is error free.
*  Make sure that the minimum page size is greater than 0. You will need to add content to your page.
*  Make sure that you are serving the custom error page with a 200 status code.
*  If we cannot load your site or you have blocked the US in the IP Firewall, publishing and previewing the error page will not work.