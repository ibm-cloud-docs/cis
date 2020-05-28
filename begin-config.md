---

copyright:
  years: 2018, 2020
lastupdated: "2020-05-21"

keywords: global load balancer configuration, glb configuration

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

# Begin Global Load Balancer configuration
{:#begin-global-load-balancer-configuration}

Start configuring your Global Load Balancer.

1. Navigate to the **Reliability** section to begin working with Global Load Balancers.
2. Scroll to the **Health Checks** section and click **Create health check** to define a custom health check.

   This configuration is optional. If you do not define any custom health checks, the system will use `/` as your default health check path.
   {:note}

3. Provide the path you wish to conduct your health checks on. You may use either HTTP or HTTPS protocols for your health checks.
4. When you expand the **Advanced options** menu, you can customize other parameters, such as the health check interval, the number of retries, the request method and response body.
5. Click **Create** to complete your health check configuration.
