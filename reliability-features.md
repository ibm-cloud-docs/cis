---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-25"

keywords: IBM Cloud Internet Services, reliable IBM Cloud Internet Services, Global Load Balancing

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# How {{site.data.keyword.cis_full_notm}} keeps your work reliable
{:#how-cis-keeps-your-work-reliable}

{{site.data.keyword.cis_full}} ({{site.data.keyword.cis_short_notm}}) helps you improve the reliability of your web services and applications, because it helps you avoid downtime caused by application and infrastructure outages. For example, with Global Load Balancing, you can deploy your web services and applications in multiple regions. IBM {{site.data.keyword.cis_short_notm}} routes your customer requests to the closest regions available when Global Load Balancing is enabled. If any region fails, the requests are routed to the next closest location, so that your customers are not affected by downtime. If your website or API fails, IBM {{site.data.keyword.cis_short_notm}} sends you notifications automatically, and it notifies you when it is restored.
{: shortdesc}


![reliability-graphic.png](images/reliability-graphic.png)

Here’s a quick feature overview:

## Reliability features
{:#cis-reliability-features}

 * Global load balancing
 * Proxy and non-proxy options for load balancing
 * Origin pools and health monitors
 * DNS management

### Summary
{:#cis-reliability-features-summary}

  * Health monitors check whether your origin pools are healthy.
  * In case of health monitor failure, your requests are re-routed to healthy origins.
  * You stay informed when your web service or API fails and when it is restored.
