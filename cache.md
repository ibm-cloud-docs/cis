---
copyright:
  years: 2018
lastupdated: "2018-03-13"
---

# Caching Concepts

This document contains some concepts and definitions related to caching and how it affects your IBM CIS deployment.

## What is Caching?

Caching is the process of storing files on our edge servers, which we do for the purpose of improving the response time when serving those files to customers. By storing the files closer to the customers, we can decrease the time it takes for the data to stream across the network, which commonly is called the **latency**.

By default, we cache **static files**, which include many types of image and text files (non-HTML files). By default we do not cache HTML files because we do not consider them to be static; however, it is possible to cache HTML files [using the Page Rules feature](using-page-rules.html).

Cached files have a specified expiration time, **Time-to-live (TTL)** after which they are purged from the cache. It also is possible to purge files from the cache manually. After files are removed from the cache, CIS goes back to your origin server to reload your files and update the cache with the latest versions.

A deeper explaination of the cache settings and your caching options can be found in the [Caching and Page Rules tutorial](caching-with-page-rules.html).
