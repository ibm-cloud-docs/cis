---

copyright:
  years: 2024
lastupdated: "2024-03-28"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# URL normalization
{: #url-normalization}

URL normalization modifies the URLs of incoming requests so that they conform to a consistent formatting standard.

When you enable URL normalization, all incoming URLs are normalized before they pass to subsequent global network features that accept a URL input. Rule expressions that filter traffic based on URLs will then trigger correctly, regardless of the format of the incoming URL. If you turn off URL normalization, CIS forwards the URL to the origin in its original form.

URL normalization does not perform redirects, and doesn't change the address shown in the visitor’s browser. The normalization operation happens on the global network and affects CIS features that are executed later and (optionally) the URL received at the origin server.

URL normalization requires that you proxy the DNS records of your domain (or subdomain) through {{site.data.keyword.cis_short_notm}}.
{: note}

## URL normalization settings
{: #url-normalization-settings}

The following settings manage URL normalization.

Normalization type (default: RFC-3986)
:   Selects the type of normalization to perform:
    * **RFC-3986** – Applies URL normalization strictly according to [RFC 3986](https://datatracker.ietf.org/doc/html/rfc3986){: external}.
    * **{{site.data.keyword.cis_short_notm}}** – In addition to what is defined in RFC 3986, applies extra URL normalization techniques.

Normalize incoming URLs (default: On)
:   Configures the URLs of all incoming traffic to {{site.data.keyword.cis_short_notm}}:
    * When enabled, all incoming URLs are normalized before they pass to subsequent {{site.data.keyword.cis_short_notm}} features that can receive a URL as input, such as Page Rules, WAF custom rules, Workers, and Access.
    * When disabled, incoming URLs are not normalized before passing to subsequent {{site.data.keyword.cis_short_notm}} features.

Normalize URLs to origin (default: Off)
:   Configures URLs sent to the origin:
    * When enabled, requests sent to the origin are normalized.
    * When disabled, requests sent to the origin are not modified.

    You can only view and enable this option when Normalize incoming URLs is enabled.
