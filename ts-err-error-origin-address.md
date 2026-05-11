---

copyright:
  years: 2026
lastupdated: "2026-05-11"

keywords:

subcollection: cis

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why am I seeing Origin address is not globally routable in CIS
{: #ts-err-origin-adress-error}
{: troubleshoot}

The `Origin address is not globally routable` error occurs when the configured origin is not reachable from the CIS global network.
{: shortdesc}

CIS validates origin addresses when you add them to a load balancer pool. CIS routes traffic and performs health checks from its public global network. Because of this, the origin must use a publicly routable IP address or hostname.
{: tsSymptoms}

If the origin uses a private IP address, internal hostname, or private-only endpoint, CIS cannot reach the origin and the validation fails.


This issue can occur in the following situations:
{: tsCauses}

* The origin uses a private IP address.
* The origin is behind a private VPC load balancer.
* The application is accessible only within a Kubernetes or Red Hat OpenShift cluster.
* The origin does not have a public IP address or public DNS record.
* Firewall or network rules block traffic from the CIS network.

CIS health checks originate from the public CIS network. Private or nonroutable addresses cannot be reached from this network.

To resolve the issue, complete the following actions:
{: tsResolve}

1. Configure the origin with a publicly routable IP address or hostname.
1. Ensure that the origin is reachable from the internet.
1. Allow required traffic from CIS/Cloudflare IP ranges.
1. Verify that firewalls, security groups, and network ACLs allow CIS health checks.
1. For VPC or Kubernetes workloads, access the application through a public ingress endpoint or public load balancer.
