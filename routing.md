---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-01"

keywords: Smart Routing Route connections, routing decisions, Eliminate excess latency

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

# Routing
{:#cis-routing}

Eliminate excess latency by analyzing and optimizing routing decisions across the global Internet using real-time network connections. Reduce Internet latency on average by 35% and connection errors by 27%.
{: shortdesc}

## Smart Routing
{:#cis-smart-routing}

Route connections across the Internet efficiently by avoiding packet loss, congestion, and outages.

Smart Routing optimizes the paths your data takes across the Internet. Optimal paths are determined by analyzing latency and packet loss data collected from real-time network connections. Smart Routing uses this data to detect which transit providers are operating best between any two points on the planet.

The optimized route is different from the regular request path. It can take up to 24 hours to switch from the regular request path to the optimized route after you enable Smart Routing for your domain.
{:note}

## Tiered Caching
{:#cis-tiered-caching}

Increase cache hit ratios using concentrated connections to reduce requests to customer origins.

Tiered Caching reduces requests to customer origins and decreases the load on the origin server. Tiered Caching accomplishes this by first asking other PoPs if they have the requested data when a cache miss takes place. Customers will see a performance increase since distances between our PoPs are typically shorter than the distances between PoPs and origins. By taking advantage of the cached data, customers will benefit by seeing a decrease in the load on their origin server.

Tiered Caching also concentrates connections to origin servers so they come from a smaller number of PoPs. This allows fewer open connections going to the origin.
