---

copyright:
  years: 2018, 2025
lastupdated: "2025-06-03"

keywords: origin server, pool implementation, origin servers

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Global load balancing
{: #global-load-balancer-glb-concepts}

A global load balancer manages traffic across server resources that are located in multiple regions. While a single origin server can serve all website content if traffic volumes and latency are manageable, a global load balancer uses a pool approach to distribute traffic across multiple origins. This pooling provides several benefits, including:
{: shortdesc}

* Minimizing response time
* Increasing availability through redundancy
* Maximizing traffic throughput

A global load balancer routes traffic to the pool with the highest priority, distributing the load among the origin servers within that pool. If the primary pool becomes unavailable, traffic automatically routes to the next highest-priority pool.

When pools are assigned to specific regions, traffic that originates from those regions is sent to the corresponding regional pools first. Traffic falls back only to default pools (typically the lowest-priority pool) if all regional pools for that area are unavailable.

## How it works
{: #how-glb-works}

When you create a global load balancer in CIS, a DNS record is automatically added with the name of the load balancer. When a client makes a DNS request, the load balancer returns one of the origin IP addresses from the associated origin pool. For example, consider an origin pool that contains two origin IP addresses `169.61.244.18` and `169.61.244.19`. If a global load balancer named `glbcust.ibmmo.com` is created by using this pool, a client on the internet can run the following command:

```sh
$ ping glbcust.ibmmo.com
PING glbcust.ibmmo.com (169.61.244.18): 56 data bytes
```
{: pre}

In this example, {{site.data.keyword.cis_short_notm}}:

* Created a DNS record named `glbcust.ibmmo.com`.
* Used the global load balancer to resolve the DNS name to one of the IP addresses in the origin pool.

In this configuration, the global load balancer doesn't end the TCP connection.
{: note}

However, if you enable proxy mode for the DNS record or the global load balancer and set **Security > TLS > Mode** to anything other than **Off**, the behavior changes. {{site.data.keyword.cis_short_notm}} ends the client connection and establishes a second connection to the origin server.

In this proxied example, {{site.data.keyword.cis_short_notm}}:

* Still creates a DNS record named `glbcust.ibmmo.com`.
* Resolves the DNS name to a {{site.data.keyword.cis_short_notm}}-provided IP address.

Now, connections to `glbcust.ibmmo.com` are ended by {{site.data.keyword.cis_short_notm}}, and HTTPS certificates are hosted by {{site.data.keyword.cis_short_notm}} (which is required for TCP termination).

After the client connects to the application, the connection path looks like this:

`[client]<--tls-->[cis]<-->[origin server]`

This setup improves security and allows {{site.data.keyword.cis_short_notm}} to apply extra features like caching, firewall rules, and traffic inspection.
