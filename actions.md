---

copyright:
  years: 2019
lastupdated: "2019-04-24"

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


# Actions
{: #actions}

Actions are the mechanisms for responding to requests that match the criteria you define in a firewall rule.

The following table describes the actions you can assign to your rules, and are listed in the default evaluation sequence applied by Firewall Rules when looking for a match.
{:shortdesc}

| Action | Description |
| ------- | :--------- |
|_Log_|Logs matching requests on the CIS edge for access with Enterprise Logpush and Logpull. Recommended for testing rule effectiveness before committing to a more severe action. Available to Enterprise customers only.|
|_Allow_|Allows matching requests to access the site, as long as no other CIS Firewall features block the request (such as IP Firewall or Access Rules)|
|_Challenge (Captcha)_|Requires a user to pass a Google reCaptcha Challenge before proceeding. If successful, CIS accepts the matched request; otherwise, it is blocked.|
|_JS Challenge_|Requires a user to pass a CIS Javascript Challenge before proceeding. If successful, CIS accepts the matched request; otherwise, it is blocked.|
|_Block_|Blocks a matching request from accessing the site.|
