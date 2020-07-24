---

copyright:
  years: 2019
lastupdated: "2019-07-06"

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


# Assigning firewall rule actions
{: #actions}

Actions are the mechanisms for responding to requests that match the criteria you define in a firewall rule.
{: shortdesc}

The following table describes the actions that you can assign to your rules. These actions are listed in the default evaluation sequence applied by firewall rules when looking for a match.
{:shortdesc}

| Action | Description |
| ------- | :--------- |
|Log|Logs matching requests on the CIS edge for access with Enterprise Logpush and Logpull. Recommended for testing rule effectiveness before committing to a more severe action. Available to Enterprise customers only.|
|Allow|Allows matching requests to access the site, as long as no other CIS firewall features block the request, such as IP firewall or access rules.|
|Challenge (Captcha)|Requires a user to pass a Google reCaptcha Challenge before proceeding. If successful, CIS accepts the matched request; otherwise, it is blocked.|
|JS Challenge|Requires a user to pass a CIS JavaScript Challenge before proceeding. If successful, CIS accepts the matched request; otherwise, it is blocked.|
|Block|Blocks a matching request from accessing the site.|
