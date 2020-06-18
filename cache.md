---

copyright:
  years: 2018, 2020
lastupdated: "2020-06-08"

keywords: IBM CIS deployment, query strings, HTML files

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

# Caching concepts
{:#caching-concepts}

This document contains some concepts and definitions related to caching and how it affects your {{site.data.keyword.cis_full}} deployment.
{:shortdesc}

## What is caching?
{:#what-is-caching}

Caching is the process of storing files on our edge servers, which we do for the purpose of improving the response time when serving those files to customers. By storing the files closer to the customers, we can decrease the time it takes for the data to stream across the network, which commonly is called the **latency**.

Cached files have a specified expiration time, **Time-to-live (TTL)** after which they are purged from the cache. It also is possible to purge files from the cache manually. After files are removed from the cache, {{site.data.keyword.cis_short_notm}} goes back to your origin server to reload your files and update the cache with the latest versions.

A deeper explanation of the cache settings and your caching options is located in the [Caching and Page Rules](/docs/cis?topic=cis-use-page-rules-with-caching) section.

### Cached content
{:#what-content-is-cached}

By default, we cache **static files**, which include many types of image and text files (non-HTML files). This only includes files from your websites and not third party resources from social networking sites, etc. Also, we currently do not cache by MIME type.

### Caching HTML
{:#how-do-i-cache-html}

We do not cache HTML files by default because we do not consider them to be static; however, if static HTML can be clearly distinguished from dynamic HTML it is possible to cache HTML files [using the Page Rules feature](/docs/cis?topic=cis-use-page-rules).


## Using query string sorting
{:#query-string-sorting}

**Enterprise Only** {{site.data.keyword.cis_short_notm}} treats URLs that have query strings in different orders as separate files in the cache. This means that if one user requests:

`/video/123456?title=0&byline=0&portrait=0&color=987654`

And another user requests:

`/video/123456?byline=0&color=987654&portrait=0&title=0`

{{site.data.keyword.cis_short_notm}} goes back to the origin, even though we have the file in our cache.

Query String Sort sorts the query strings _before_ they hit our cache, resulting in a higher cache hit rate. Enable Query String Sort using the toggle in the **Caching** page.

## Serving stale content
{:#serve-stale-content-caching}

**Serve stale content** keeps a limited version of the site online if the server goes down. Even if the content has expired, {{site.data.keyword.cis_short_notm}} will continue serving cached content to users when origin servers are offline.
