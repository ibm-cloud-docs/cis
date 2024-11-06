---

copyright:
  years: 2023, 2024
lastupdated: "2024-11-06"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# JavaScript detections
{: #javascript-detections}

{{site.data.keyword.cis_full}} ({{site.data.keyword.cis_short_notm}}) bot features include JavaScript detections. A small amount of JavaScript is injected into client devices using [Google’s Picasso fingerprinting technique](https://research.google/pubs/picasso-lightweight-device-class-fingerprinting-for-web-clients/){: external}. Picasso results are factored into bot scores and help {{site.data.keyword.cis_short_notm}} classify traffic as automated or human. `BotScoreSrc: Not Computed` and a score of `0` are relevant to Picasso JavaScript Fingerprinting requests. These requests are exempt from being blocked by any firewall rules.

This detection technique gathers general data about the machines reaching {{site.data.keyword.cis_short_notm}}. For example, if a particular user is accessing {{site.data.keyword.cis_short_notm}} via Google Chrome on a MacBook Pro, because there are millions of people using Google Chrome on a MacBook Pro, {{site.data.keyword.cis_short_notm}} cannot identify specific individuals. {{site.data.keyword.cis_short_notm}} also takes steps to anonymize and phase out data for added privacy.

JavaScript is only injected in response to requests for HTML pages or page views, excluding AJAX calls. API and mobile app traffic is unaffected. Additionally, code is not injected again until its 30-minute session life expires. The Picasso script is roughly 70 KB and execution time varies by device, anywhere from 90 ms to around 500 ms.

The snippets of JavaScript will contain a source pointing to the challenge platform with paths that start with `/cdn-cgi/challenge-platform/...`.

## Enable JavaScript detections
{: #enable-javascript-detections}

For no-cost Trial plans (Bot Fight Mode), JavaScript detections are automatically enabled and cannot be disabled.

For all other plans (Super Bot Fight Mode and Bot Management for Enterprise), JavaScript detections are optional. To adjust your settings, go to **Security > Bots**.

## Enforcing execution of JavaScript detections
{: #enforcing-execution-javascript-detections}

To ensure that visitors have previously run and passed JavaScript detections, you can create a firewall rule with the field `cf.bot_management.js_detection.passed` which performs a Managed Challenge action. Enter `(cf.bot_management.js_detection.passed)` into the **Expression preview** section as a singular rule.

## Considerations
{: #javascript-considerations}

* If you have a Content Security Policy (CSP):
    * Ensure that anything under `/cdn-cgi/challenge-platform/` is allowed. Your CSP should allow scripts that are served from your origin domain (`script-src self`).
    * If your CSP uses a `nonce` for script tags, {{site.data.keyword.cis_short_notm}} adds these nonces to the scripts it injects by parsing your CSP response header.
    * If your CSP does not use `nonce` for script tags and JavaScript Detection is enabled, you might see a console error such as

        ```text
        Refused to execute inline script because it violates the following Content Security Policy directive: "script-src 'self'". Either the 'unsafe-inline' keyword, a hash ('sha256-b123b8a70+4jEj+d6gWI9U6IilUJIrlnRJbRR/uQl2Jc='), or a nonce ('nonce-...') is required to enable inline execution.
        ```
        {: screen}

    * It is not recommended to use `unsafe-inline`. Instead, it is recommend that you use CSP `nonces` in script tags which are parsed and supported in the CDN.
