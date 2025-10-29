---

copyright:
  years: 2025
lastupdated: "2025-10-29"

keywords: HA for CIS, DR for CIS, CIS recovery time objective, CIS recovery point objective

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}


# Understanding high availability and disaster recovery for CIS
{: #ha-dr}

[High Availability](#x2284708){: term} (HA) is the ability for a service to remain operational and accessible in the presence of unexpected failures. [Disaster recovery](#x2113280){: term} (DR) is the process of recovering the service instance to a working state.
{: shortdesc}

Cloud Internet Services (CIS) is a global service designed to remain operational during regional outages. CIS is designed to meet the [Service Level Objectives (SLO)](/docs/resiliency?topic=resiliency-slo) with all plans.

CIS is a globally available GA service, with public API endpoints accessible worldwide through a global load balancer across three multi-zone regions: Dallas (`us-south`), Washington, DC (`us-east`), and London (`eu-gb`). In the event of an outage in one region, the global load balancer automatically routes API traffic to the nearest available region. Data is replicated across these regions for optimized latency and HA.

See [How IBM Cloud ensures high availability and disaster recovery](/docs/resiliency?topic=resiliency-ha-redundancy#zero-downtime) to learn more about the HA and DR standards in {{site.data.keyword.cloud_notm}}. You can also find information about [Service Level Agreements](https://www.ibm.com/support/customer/csol/terms/){: external}.

## High availability architecture
{: #ha-architecture}

CIS is architected to support HA across multiple layers of your IT infrastructure. You can design for HA at different levels, depending on business requirements, Service Level Agreements (SLAs), and available resources.

CIS separates its architecture into two core components: the control plane (API and configuration layer) and the data plane (traffic processing and enforcement layer). This separation is key to ensuring service continuity during component-specific issues.

* The CIS API control plane allows you to configure and manage services such as DNS records, firewall rules, and load-balancing policies. It runs on IBM Cloud and may experience occasional outages or maintenance windows. While rare, control plane availability might not always match that of the data plane. If unavailable, you may not be able to make changes, but existing configurations continue to be enforced.

* The CIS data plane, powered by [Cloudflare’s global Anycast network](https://www.cloudflare.com/learning/cdn/glossary/anycast-network/){: external}, is responsible for serving live traffic, including DNS resolution, DDoS protection, content delivery, and firewall enforcement. It is designed for extremely high uptime and resilience. The data plane continues to operate normally even when the control plane is down, preserving performance and security.

This architecture ensures that control plane disruptions do not impact end-user traffic, providing a resilient foundation for highly available application delivery.

CIS is designed to meet the following Service Level Objectives (SLOs):

| Availability Target | Target Value |
|---|---|
| Availability % | 99.999%  |
| Global Anycast Network Uptime | 100%         |
| DNS Resolution Time      | < 50 ms      |
| DDoS Mitigation Response Time | < 3 seconds |
| Configuration Propagation Time     | < 60 seconds |
{: caption="SLO for CIS" caption-side="bottom"}

These targets reflect the robustness of the data plane, which delivers the actual services to your users. You get the most value from CIS through the performance and reliability of this layer, which is engineered for global scale and HA.

The SLO is not a warranty and IBM will not issue credits for failure to meet an objective. Refer to the SLAs for commitments and credits that are issued for failure to meet any committed SLAs. For a summary of all SLOs, see [{{site.data.keyword.cloud_notm}} service level objectives](/docs/resiliency?topic=resiliency-slo).
{: note}

### High availability features
{: #ha-features}

HA in CIS is achieved through a globally distributed, resilient infrastructure and integrated service-level mechanisms. These features are designed to minimize downtime and ensure continuous service delivery even in the face of failures or network disruptions.

CIS supports the following HA features:

| Feature  | Description   | Consideration |
| ---------------------- | ----------------- | ----------------- |
| Cloudflare's Global Anycast Network                                  | Routes traffic through the nearest data center to reduce latency and reroute in case of failure. | Ensures consistent availability and low latency across regions.  |
| Redundant DNS infrastructure                            | Uses distributed DNS servers for HA and rapid failover.                           | Helps maintain DNS resolution even during regional disruptions. |
| Always-On DDoS protection                               | Automatically detects and mitigates large-scale DDoS attacks in real-time.                       | Does not require manual intervention; protection is active 24/7. |
{: caption="HA features for CIS" caption-side="bottom"}

As a customer, you can create and configure the following other HA options:

| Feature  | Description   | Consideration |
| ---------------------- | ----------------- | ----------------- |
| Load balancing with health checks | Distributes traffic across multiple, healthy origins to avoid single points of failure. | Health checks must be correctly configured to detect outages accurately. |
| Rate-limiting rules (not on by default) |  You can define rules to limit request rates per IP or endpoint to prevent overload. | Enterprise Plan only |
| Web Application Firewall (WAF) | Filters, monitors, and blocks malicious HTTP/S traffic based on predefined and custom rules.  |  Proper rule tuning is essential to avoid false positives or missed threats. |
| Custom rules |Allow you to define logic (for example, IP blocking, header inspection) to discard or redirect malicious traffic. | Misconfigured rules could block valid users or degrade service performance. |
| Range applications | Enables Layer 4 DDoS protection for TCP applications (for example, SSH, FTP) by proxying traffic through Cloudflare. | Enterprise Plan only |
| Bot management for bot mitigation | Identifies and mitigates automated, potentially harmful traffic to protect application uptime. | Enterprise Premier Plan only |
{: caption="Customer HA features for CIS" caption-side="bottom"}

## Disaster recovery architecture
{: #disaster-recovery-intro}

DR for CIS builds on the same architectural separation of the control plane and data plane, enabling resilient operations even during service disruptions. Outages in one plane do not necessarily affect the other, which is central to DR planning.

* The control plane, used for service configuration and management, runs on IBM Cloud and integrates with Cloudflare infrastructure. In a control plane outage (such as a regional IBM Cloud issue or Cloudflare management disruption), you might not be able to make changes or access analytics. However, existing configurations remain in effect, and your application traffic is not impacted. Deferred changes can be applied once services are restored.
* The data plane continues to enforce traffic policies and serve users during a control plane outage. In the rare event of a regional data plane disruption, Cloudflare’s Anycast network automatically reroutes traffic to healthy nodes, minimizing downtime and maintaining service continuity.

CIS provides mechanisms to protect your data and restore service functions. Business continuity plans are in place to achieve targeted [Recovery Point Objective](#x3429911){: term} (RPO) and [Recovery Time Objective](#x3167918){: term} (RTO) for the service. The following table outlines the targets IBM Cloud for the recovery of the CIS service.

| DR objective   | Target value |
|--------------| -------------------|
| RPO | Failover happens almost instantly (within seconds) if internal, as it switches to another web application. If Cloudflare experiences downtime or issues, data will be unavailable until they are back online, as CIS is a stateless service. |
| RTO  | Recovery time for the control plane is approximately 1 hour per web application, including verification and other processes. |
{: caption="RPO and RTO for CIS" caption-side="bottom"}

{{site.data.keyword.cloud_notm}} has [business continuity](#x3026801){: term} plans in place to provide for the recovery of services within hours if a disaster occurs. You are responsible for your data backup and associated recovery of your content.

To support DR readiness, you can monitor live service status through the [Cloudflare System Status](https://www.cloudflarestatus.com/){: external} page and configure alerts to detect incidents early. Best practices include minimizing the need for urgent config changes, using version-controlled configurations, and maintaining redundancy in your origin infrastructure.

This resilient architecture ensures most disruptions are isolated, and your applications remain available even during partial service outages.

### Disaster recovery features
{: #dr-features}

DR for CIS is supported through a combination of platform capabilities and customer-managed configurations. The service is designed to maintain resilience and minimize downtime through stateless architecture and global infrastructure.

CIS supports the following DR features:

| Feature | Description | Consideration |
| ----- | ----- | ------ |
| Stateless architecture | CIS does not persist your data, enabling quick re-deployment in disaster events. | Store configuration backups externally if needed. |
| Geo-distributed infrastructure | CIS leverages a global Anycast network to reduce regional DR risks. | Limits impact of localized failures and ensures traffic rerouting. |
{: caption="DR features for CIS" caption-side="bottom"}

As a customer, you can create and support the following other DR options:

| Feature | Description | Consideration  |
| ----- | ----- | ------ |
| Configuration export & backup | Manually export DNS records, WAF rules, and other CIS settings using the CIS API | Provides a backup in case configurations are lost or corrupted. Useful for offline review or reconfiguration. |
| Infrastructure as Code (IaC) | Use Terraform or similar tools to define and manage CIS configurations. | Enables consistent, repeatable deployments and rapid restoration of services in new or recovered environments. |
| Logpush & Security Event review | Use Logpush to export logs and review security events. | Helps you investigate incidents, analyze trends, and identify root causes during or after a disruption. |
| Traffic metrics & monitoring | Continuously monitor traffic volume, error rates, and performance metrics. | Spikes or anomalies in traffic can indicate issues such as DDoS attacks, misconfigurations, or origin failures. Early detection supports faster response. |
{: caption="Customer DR features for CIS" caption-side="bottom"}

### Planning for disaster recovery
{: #features-for-disaster-recovery}

The steps outlined in your HA and DR plans should be regularly reviewed and tested. As you build and refine your strategy, consider the following common failure scenarios and how CIS responds at both the control path (management/API layer) and data path (traffic processing layer).

CIS is built on a globally distributed, stateless architecture that minimizes the risk of persistent service failures. While the platform includes HA and DR capabilities by design, you are responsible for applying best practices, managing configuration state, and preparing for application-layer recovery as needed.

| Failure  | Resolution |
| ----------------- | ------------ |
| Control plane outage  | You might be unable to modify configurations or retrieve updated metrics/logs, but existing data path policies (such as DNS routing and WAF enforcement) remain active. IBM Cloud opens a Customer-Initiated Event (CIE) to restore control path functionality, and you are notified. Recovery time varies; see the [Cloudflare System Status](https://www.cloudflarestatus.com/){: external} page for updates. |
| Data path outage   | In rare cases, a localized outage in edge network might impact traffic. CIS will route requests to healthy data centers automatically. If needed, you can temporarily disable the CIS proxy (grey-cloud the record) to route traffic directly to their origin. |
| Regional failure  | CIS will continue to serve traffic globally, but if your origin servers are not deployed across multiple regions, end-user traffic can still experience downtime. You should deploy origin infrastructure redundantly and test failover scenarios to ensure full-stack availability.               |
| Configuration loss or misconfiguration  | CIS is stateless, so customer-defined configurations are not retained by default. Use Infrastructure as Code (for example, Terraform) or export configurations via the CIS API (GET calls). Recovery requires manually recreating resources (POST) using saved data. API changes (PATCH/PUT) can be tracked using Activity Tracker to help identify and revert unintended changes. |
| DDoS attack or malicious traffic   | CIS includes always-on DDoS protection, bot management, and rate limiting. These features operate at the data path and do not require control path interaction. Protections are enforced automatically, but you should monitor traffic metrics and tune thresholds to reflect their application profile. |
{: caption="DR scenarios for CIS" caption-side="bottom"}

## Your responsibilities for high availability and disaster recovery
{: #feature-responsibilities}

It is your responsibility to continuously test your plan for HA and DR when using CIS.

Interruptions in network connectivity and short periods of service unavailability may occur. You must ensure that your application includes [client availability retry logic](/docs/resiliency?topic=resiliency-high-availability-design#client-retry-logic-for-ha) to help maintain overall application availability.
{: note}

Use the following checklists for key CIS features to help you create, verify, and practice your HA and DR plans:

- Configuration backups
   - [ ] Regularly export and back up DNS, WAF, and security settings
   - [ ] Validate restoration of configuration backups in a test environment

- Origin infrastructure resilience
   - [ ] Deploy origin servers across multiple zones and regions on your web application
   - [ ] Test failover and recovery of origin endpoints during simulated outages
   - [ ] Configure the global load balancer with active health checks and multiple origin pools to enable automatic failover to healthy endpoints

- Monitoring and alerts
   - [ ] Set up notifications for CIS service health and performance metrics
   - [ ] Review Logpush security data to detect anomalies or compare against baseline metrics
   - [ ] Regularly review logs and dashboard data to detect anomalies

For more information about responsibility ownership between you and {{site.data.keyword.cloud_notm}} for CIS, see [Understanding your responsibilities when using CIS](/docs/cis?topic=cis-responsibilities-cis).

## Recovery time objective (RTO) and recovery point objective (RPO)
{: #rto-rpo-features}

| Feature  | RTO and RPO |
| ----------------- | ------------- |
| Stateless architecture  | RTO = Near-zero (no service state to recover); RPO = N/A (no persistent data stored in CIS) |
| DNS and WAF configuration backups | RTO = minutes (manual or IaC redeployment); RPO = based on frequency of customer configuration backups. Use CIS API to restore a previous configuration from a saved backup. The RTO depends on the size of the restore, while the RPO depends on when the last configuration backup was created. |
{: caption="RTO/RPO features for CIS" caption-side="bottom"}

## How IBM supports disaster recovery planning
{: #ibm-disaster-recovery}

A zone failure refers to the failure of one data center or availability zone within a region. CIS mitigates the impact in these ways:

* CIS leverages a globally distributed Anycast network that automatically reroutes traffic away from failed zones to healthy data centers, minimizing downtime.
* The stateless architecture of CIS enables rapid failover without data loss or service interruption when a zone becomes unavailable.
* IBM continuously monitors the health of CIS web applications and network endpoints to detect and respond to zone-level outages in real time.
* If IBM can’t restore the service instance, you must restore the service as described in [Disaster recovery architecture](#disaster-recovery-intro).

### How {{site.data.keyword.IBM_notm}} recovers from zone failures
{: #ibm-zone-failure}

CIS is designed with HA and resilience in both the control plane and the data plane, but it's important to understand how each behaves in the event of failure.

Control plane resiliency
:    The CIS control plane, which handles configuration and API requests, operates across multiple geographically distributed regions. If a regional control plane becomes unavailable, traffic is automatically redirected to the next closest available region. This failover is automated and requires no action from you, ensuring continued access to your CIS configuration even if a specific control plane region is temporarily unreachable.

Data plane availability
:    The CIS data plane runs on Cloudflare’s global Anycast network and is independent of IBM Cloud infrastructure. The data plane is responsible for serving live traffic, including DNS resolution, DDoS protection, WAF enforcement, and content caching. Cloudflare's network is engineered for extremely HA, providing 100% uptime for its data plane services under their SLA.

Because the data plane is globally distributed and operates outside of IBM Cloud, there is no concept of CIS-specific zone failures. If your traffic is impacted, it is typically due to issues with origin infrastructure, DNS configuration, or the way customer-managed zones are set up.

### How {{site.data.keyword.IBM_notm}} recovers from regional failures
{: #ibm-regional-failure}

CIS is architected for HA and resilience across regions. The CIS control plane operates in multiple geographic regions and includes automatic failover. If a control plane region becomes unavailable, requests are automatically redirected to another available region. No customer action is required.

For your own applications and infrastructure, CIS can support regional failover capabilities, but only if you configure them. To maintain service availability during regional disruptions, you must:

* Deploy your origin servers and backend resources across multiple regions.
* Use CIS features, such as global load balancing or DNS-based failover, to route traffic to healthy regions.
* Ensure health checks are in place to detect regional issues and trigger routing changes.

In short, CIS provides the global infrastructure and tools to enable regional failover, but it is up to you to architect your backend services and configure CIS accordingly for full DR coverage.

## Change management
{: #change-management-ha-dr}

Change management includes tasks such as upgrades, configuration changes, and deletion.

Grant users and processes the Identity and Access Management (IAM) roles and actions with the least privilege that is required for their work. For more information, see [How can I prevent accidental deletion of services?](/docs/resiliency?topic=resiliency-dr-faq#prevent-accidental-deletion).
{: tip}

Best practices for managing change in CIS also include:

* Plan and document all configuration changes by maintaining a detailed change log for your CIS settings, including DNS records, WAF rules, and traffic policies.
* Use audit logs and IBM Cloud Activity Tracker Event Routing to review prior configurations and track changes. Understanding what has changed allows for better testing, validation, and rollback if necessary.
* Create backups of critical CIS configurations before performing upgrades or major changes to ensure rapid recovery if needed.
* Schedule upgrades or high-impact configuration changes during low-traffic periods, and communicate planned changes to relevant stakeholders to minimize disruption.
* Backup the CIS configuration as the new baseline after performing a successful upgrade or implementing changes.
* Monitor CIS service health and performance metrics to detect any issues early and verify that changes behave as expected.
* Export and manually back up your CIS configuration before upgrading to a new service version or applying significant changes.

## How IBM maintains services
{: #ibm-service-maintenance}

All upgrades follow {{site.data.keyword.IBM_notm}} service best practices, including recovery plans and rollback processes. Regular maintenance might cause short interruptions, mitigated by [client availability retry logic](/docs/resiliency?topic=resiliency-high-availability-design#client-retry-logic-for-ha). Changes are rolled out sequentially, region by region, and zone by zone within a region. {{site.data.keyword.IBM_notm}} reverts updates at the first sign of a defect.

IBM provides advance notice for all planned maintenance activities. If a change is expected to affect your workloads, IBM communicates this through official notifications. To stay updated on maintenance, service announcements, and other updates, see the [Monitoring notifications and status](/docs/account?topic=account-viewing-cloud-status) page.
