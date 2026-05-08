---

copyright:
  years: 2026
lastupdated: "2026-05-08"

keywords:

subcollection: cis

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why am I seeing Origin address is not globally routable in CIS
{: #ts-err-origin-adress-error}
{: troubleshoot}

The `Origin address is not globally routable` error occurs when the configured origin is not publicly reachable from the internet.
{: shortdesc}

CIS validates origin addresses when you add them to a load balancer pool. CIS routes traffic and performs health checks from the CIS global network. The origin must therefore be publicly accessible.
{: tsSymptoms}

If the origin uses a private IP address, internal hostname, or private-only endpoint, CIS cannot reach the origin and the validation fails.


This issue can occur in the following situations:
{: tsCauses}

* The origin uses a private IP address range.
* The origin is configured behind a private VPC load balancer.
* The application is exposed only within a Kubernetes or Red Hat OpenShift on IBM Cloud (ROKS) cluster.
* The origin does not have a public IP address or public DNS record.
* Firewall or network rules prevent access from the CIS network.

CIS health checks originate from the public CIS network. Private or non-routable addresses cannot be reached from this network.

To resolve the issue, complete the following actions:
{: tsResolve}

1. Configure the origin with a publicly routable IP address or public hostname.
1. Ensure that the origin is reachable from the public internet.
1. Restrict access by allowing only CIS IP ranges instead of allowing unrestricted public access.
1. Verify that firewalls, security groups, and network ACLs allow inbound traffic and health checks from the required IP ranges.
1. For VPC or Kubernetes workloads, expose the application through a public ingress endpoint or public load balancer.
