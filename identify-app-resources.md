---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: origin pools, application resources, Origin Pools section

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
{:table: .aria-labeledby="caption"}

# Identify your application resources
{:#identify-your-application-resources}

Identify the your application's resources, such as origin pools and health check mechanisms.
{: shortdesc}

1. Navigate to the **Origin Pools** section, and click **Create pool** to define a new origin pool.

   Origin pools are server resources delivering applications to your clients.

2. Assign a name to your Origin Pool, and select the health check mechanism defined earlier. Add your application server as your Origin. You may add one or more Origins by clicking **Add Origin**.

   If your application servers are sitting behind a local load balancer such as an IBM Cloud Load Balancer, then add your load balancer’s FQDN or virtual IP as your Origin instead of adding your individual servers.
   {:note}

3. Click **Provision Resource** to complete the creation of your Origin Pool.  

   ![IMAGE](images/reliability8.png)

   The Origin Pool will initially show up as **Unhealthy**. Its state will change to **Healthy** after a successful health check by the system. You may need to refresh your browser to see the state change.

   ![IMAGE](images/reliability9.png)

   If you have multiple origins within your Origin Pool, then use the healthy origin threshold to specify the minimum number of origins that must be healthy before declaring the pool healthy.
   {:note}

4. Define as many origin pools as the number of application farms you have. These farms may be within the same or different
geographic regions. In our example, we’ll create two origin pools representing an application farm in the United States west and east coasts.

   ![IMAGE](images/reliability10.png)
