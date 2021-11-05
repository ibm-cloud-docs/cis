---

copyright:
  years: 2018, 2020
lastupdated: "2020-06-05"

keywords: 

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
{:table: .aria-labeledby="caption"}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Troubleshooting {{site.data.keyword.cis_short_notm}} error codes
{: #troubleshooting-cis-error-codes}

Here are some common error messages you or your support team might see:

| Error Code | Reason |
| ------------- | ------------- |
| 1001 | DNS Resolution Error. Either the customer recently signed up and their DNS information has not yet propagated, or whomever is managing the DNS has a failure. |
| 521 | Origin web server refused connection from {{site.data.keyword.cis_short_notm}}. Either the origin web server is not running, or something is blocking {{site.data.keyword.cis_short_notm}} IP addresses. |
| 522 | Connection timeout to the origin server (30 second default). Either CIS might be rate-limited, the web server could be consuming all resources (shared server), or there might be network connectivity issues between the web server and {{site.data.keyword.cis_short_notm}}. |
| 523 | Origin server is unreachable. Ensure that the origin IP address for the DNS record is the same as the one appearing in the {{site.data.keyword.cis_short_notm}} DNS Settings page. |
| 524 | {{site.data.keyword.cis_short_notm}} could make a TCP connection but did not receive a response from the web server. A long-running application or database query is interfering. |
{: caption="Table 1. Error codes" caption-side="bottom"}

## 502 error “The dreaded 502”
{: #troubleshooting-cis-502-error}
{: help}
{: support}

This error is one of the most common ones you might see. It typically occurs when a portion of a network is unavailable; for example, at the start of a DDoS attack. A particular data center might be unavailable for a time. Traffic is re-routed. It is recommended that you run a trace route.

Here is what you might see: `Error 502 - bad gateway error`

What happened:

* A portion of the {{site.data.keyword.cis_short_notm}} network is having an issue.
* Usually the problem is limited to one server in one data center.
* It affects only a portion of the site's visitors.
* The {{site.data.keyword.cis_short_notm}} Technical Operations team deals with these.

What you can do:

* Send the results from `www.YOUR_DOMAIN.com/cdn-cgi/trace` in a case to [IBM Support](/docs/get-support?topic=get-support-using-avatar).
* Temporarily toggle your DNS Records to off (No proxy).
