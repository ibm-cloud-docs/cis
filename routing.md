---

copyright:
  years: 2018, 2025
lastupdated: "2025-07-04"

keywords: Smart Routing Route connections, routing decisions, Eliminate excess latency

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Smart routing and tiered caching
{: #cis-routing}

Reduce excess latency by optimizing routing decisions across the global internet by using real-time network data. On average, this technique can reduce internet latency by 30% and connection errors by 27%.
{: shortdesc}

## Smart Routing
{: #cis-smart-routing}

Smart Routing efficiently directs connections across the internet by avoiding packet loss, congestion, and outages. It optimizes the paths that your data takes by analyzing latency and packet loss from real-time network connections. Using this data, Smart Routing identifies the best transit providers between any two points worldwide to ensure that your traffic follows the most reliable route.

The optimized route differs from the regular request path. After you enable Smart Routing for your domain, it can take up to 24 hours to switch from the regular path to the optimized route.
{: note}

## Tiered Caching
{: #cis-tiered-caching}

Tiered Caching improves cache hit ratios by using a hierarchical approach that reduces requests to your origin servers and decreases their load. When a cache miss occurs, instead of immediately querying the origin, Tiered Caching asks other Points of Presence (PoPs) if they have the requested data. Since PoPs are typically closer to each other than to your origin, this reduces latency and speeds up content delivery.

Tiered Caching also concentrates connections to your origin servers so they come from fewer PoPs. This feature reduces the number of open connections to the origin, easing server load and improving performance.
