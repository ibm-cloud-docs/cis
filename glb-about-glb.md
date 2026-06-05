---

copyright:
  years: 2026, 2026
lastupdated: "2026-06-05"

keywords: global load balancing, openshift routes, failover, disaster recovery, CIS, origin pools

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# About global load balancers
{: #about-global-load-balancers}

Traffic is routed to the highest-priority healthy origin pool and automatically fails over to secondary pools when needed to ensure continuous application availability. When pools are associated with specific regions, traffic is directed to the nearest or most appropriate regional pool. If no regional pools are available, traffic falls back to the default pool.
{: shortdesc}

You can configure global load balancing to:

- Distribute traffic across multiple regions
- Provide failover between application environments
- Route users to regional origin pools
- Improve application availability and throughput
- Optimize traffic routing based on steering policies

CIS global load balancing consists of the following core components:

- **Global load balancers**: Manage DNS-based traffic routing across configured origin pools.
- **Origin pools**: Groups of origin servers that receive application traffic. Pools can contain public IP addresses, hostnames, or load balancer virtual IPs. For more information, see [Origin pools](/docs/cis?topic=cis-glb-features-pools).
- **Health checks**: Monitor the health and availability of origins by sending periodic probes to configured endpoints. When an origin or pool becomes unhealthy, traffic is routed to another healthy pool. For more information, see [Health checks](/docs/cis?topic=cis-glb-features-healthchecks&interface=ui).
- **Traffic steering policies**: Control how traffic is distributed across origin pools. Supported steering modes include:
   - Off - Failover
   - Geo
   - Random
   - Dynamic latency

For more information, see [Traffic steering](/docs/cis?topic=cis-traffic-steering&interface=ui).

When regional pools are configured, CIS routes traffic according to regional proximity and availability. If no regional pools are available, traffic falls back to the default pool.

CIS global load balancing supports both proxied and non-proxied configurations:

- In non-proxied mode, CIS returns origin IP addresses directly through DNS resolution.
- In proxied mode, CIS terminates client connections and establishes a separate connection to the origin server. This configuration enables additional CIS capabilities such as TLS management, security inspection, caching, and firewall protection.

## Use cases: Red Hat OpenShift route failover
{: #glb-openshift-use-case}

You can use global load balancing to provide failover and disaster recovery (DR) between Red Hat OpenShift clusters that are deployed across multiple regions.

In this example, applications are deployed in two Red Hat OpenShift clusters:

- A primary cluster in Washington
- A secondary cluster in Dallas

Both clusters expose the same applications through Red Hat OpenShift routes. {{site.data.keyword.cis_full_notm}} global load balancing routes traffic to the primary cluster during normal operations and fails over traffic to the secondary cluster during a DR event.

### Creating a global load balancer for Red Hat OpenShift route failover
{: #create-glb-openshift-failover}

This workflow configures {{site.data.keyword.cis_short_notm}} global load balancing for Red Hat OpenShift routes by using failover traffic steering.

Follow this workflow to configure global load balancing for Red Hat OpenShift route failover:

1. Create two origin pools.
   - Configure the first origin pool for the Washington primary Red Hat OpenShift route.
   - Configure the second origin pool for the Dallas secondary Red Hat OpenShift route.
1. Create a global load balancer and set the traffic steering mode to **Off - Failover**.
1. Configure the Washington origin pool with higher priority.
1. Configure the Dallas origin pool as the fallback pool.

With the **Off - Failover** traffic steering mode:

- Traffic is routed to the primary origin pool during normal operations.
- Traffic fails over to the secondary origin pool when the primary pool becomes unhealthy.
- If all pools become unhealthy, traffic is routed to the configured fallback pool.
