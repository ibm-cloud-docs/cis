---

copyright:
  years: 2018, 2020
lastupdated: "2020-06-10"

keywords: IBM Cloud Internet Services, reliable IBM Cloud Internet Services, Global Load Balancing

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

# How {{site.data.keyword.cis_full_notm}} keeps your work reliable
{:#how-cis-keeps-your-work-reliable}

{{site.data.keyword.cis_full}} ({{site.data.keyword.cis_short_notm}}) helps you improve the reliability of your web services and applications, because it helps you avoid downtime caused by application and infrastructure outages. For example, with Global Load Balancing, you can deploy your web services and applications in multiple regions. IBM {{site.data.keyword.cis_short_notm}} routes your customer requests to the closest regions available when Global Load Balancing is enabled. If any region fails, the requests are routed to the next closest location, so that your customers are not affected by downtime. If your website or API fails, IBM {{site.data.keyword.cis_short_notm}} sends you notifications automatically, and it notifies you when it is restored.
{: shortdesc}


![reliability-graphic.png](images/reliability-graphic.png)

## Reliability features
{:#cis-reliability-features}

 * Global load balancing: The GLB service distributes your traffic across multiple servers with a combination of origin pools, health checks, and a load balancer.
   * Proxy and non-proxy options for load balancing
   * Origin pools and health checks
   * Global anycast network: The available health check regions are based on [the Cloudflare Global Anycast Network](https://www.cloudflare.com/network/){:external}.
 * DNS management: Manage your DNS records, control proxying, and enable DNS Security.
   * DNS Security cryptographically signs a zone to ensure that the DNS records provided to the user are the same as the DNS records published on the DNS server.


### Summary
{:#cis-reliability-features-summary}

  * Health monitors check whether your origin pools are healthy.
  * In case of health monitor failure, your requests are re-routed to healthy origins.
  * You stay informed when your web service or API fails and when it is restored.
