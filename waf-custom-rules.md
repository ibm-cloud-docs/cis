---

copyright:
  years: 2018, 2020
lastupdated: "2020-07-06"

keywords: WAF Custom Rules, Custom WAF Rules

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


# Requesting a custom rule
{:#waf-custom-rules}

Navigate to custom WAF rules through **Security > Web Application Firewall > Custom rules**. WAF rules are available on Enterprise plans and are created based on your unique requirements and/or website's traffic patterns. This means that you can ask us to block virtually any combination of characteristics of a request.
{: shortdesc}

Custom WAF rules cater to situations where the IBM WAF doesn’t have a rule in place already, and the attacker uses a specific pattern or user agent that is targeted specifically for your website's structure. In these situations, you can create a custom rule for your web property.

To request a rule, email wafsup@us.ibm.com with rule requirements or traffic patterns.

Provide as much information as possible, including:

* Access logs showing a sample of about 100 alleged malicious requests.
* A sample POST request including the POST data (if the requests have a POST body) to determine whether the request contains anything we can block or trigger on.
* Whether you want the requests to be outright blocked, or to be challenged, in case of potential false positives.
* The specific domains to which you want these rules applied.
* Whether you want the rules turned on or off by default.

After your custom WAF rules are created, you must enable all custom rules for them to take effect.
{:note}
