---

copyright:
  years: 2018, 2019
lastupdated: "2019-10-31"

keywords: origin server, pool implementation, origin servers

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

# Global load balancer concepts
{: #global-load-balancer-glb-concepts}

This document contains some concepts and definitions related to the global load balancer and how it affects your {{site.data.keyword.cis_full}} deployment.
{: shortdesc}

## Global load balancer
{: #global-load-balancer-cis}

A global load balancer manages traffic across server resources located in multiple regions. The origin server can serve up all of the content for a website, provided that the web traffic does not extend beyond the server's processing capabilities and latency is not a primary concern. A global load balancer manages a _pool_ implementation that allows for the traffic to be distributed to multiple origins. This pool capability provides many benefits including:

* Minimizes response time
* Creates higher availability through redundancy
* Maximizes traffic throughput

A global load balancer routes traffic to the pool with the highest priority, distributing the load among its origin servers. See the following _Pool_ section for how traffic is distributed within a pool. If the primary pool becomes unavailable, traffic is routed automatically to the next pool in the list based on priority.

If pools are set up for specific regions, traffic from those regions is sent to the pools for the specified region first. Traffic falls back to the default pools only when all pools for a given region are down. In this case the fallback pool is the pool with the lowest priority.

### How it works
{: #how-glb-works}

When a global load balancer is created, a DNS record is automatically added for it with the name of the load balancer. The load balancer then returns one of the origin IP addresses to a client making a DNS request.

For example, an origin pool is created with two origins identifying IP addresses `169.61.244.18` and `169.61.244.19`. If a global load balancer is created with the name **`glbcust.ibmmo.com`** using the origin pool, then a client on the internet can execute the command:

```sh
$ ping glbcust.ibmmo.com
PING glbcust.ibmmo.com (169.61.244.18): 56 data bytes
```
{: pre}

In this example, {{site.data.keyword.cis_short_notm}}:

* Created a DNS record named `glbcust.ibmmo.com`.
* Used the global load balancer to resolve the DNS name to one of the IP addresses identified in the origin pool.

Notice that the global load balancer does not terminate the TCP connection.
{: note}

Setting a DNS element or global load balancer to proxy changes the behavior.
If, for example, you turn on proxy and **Security > TLS > Mode** to something besides `Off`, the {{site.data.keyword.cis_short_notm}} now terminates the TCP connection and establishes a second connection between {{site.data.keyword.cis_short_notm}} and the originator.

In this example, {{site.data.keyword.cis_short_notm}}:

* Created a DNS record named: `glbcust.ibmmo.com`.
* Used the global load balancer to resolve the DNS name to a {{site.data.keyword.cis_short_notm}} provided IP address.

Now, connections to `glbcust.ibmmo.com` are terminated by {{site.data.keyword.cis_short_notm}}, and HTTPS certificates are hosted by {{site.data.keyword.cis_short_notm}} (which is required for TCP termination).

After the client connects to the application the picture looks like this:

`[client]<--tls-->[cis]<-->[origin server]`
