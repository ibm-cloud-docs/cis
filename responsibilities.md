---

copyright:
  years: 2020, 2025
lastupdated: "2025-05-08"

keywords: Cloud Internet Services, cis, responsibilities, ha, high availability, disaster recovery

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}
# Understanding your responsibilities when using {{site.data.keyword.cis_short_notm}}
{: #responsibilities-cis}

Learn about the management responsibilities and terms and conditions that you have when you use {{site.data.keyword.cis_full}}. For a high-level view of the service types in {{site.data.keyword.cloud}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} offerings](/docs/overview?topic=overview-shared-responsibilities).
{: shortdesc}

Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use {{site.data.keyword.cis_full_notm}}. For the overall terms of use, see [{{site.data.keyword.cloud}} Terms and Notices](/docs/overview?topic=overview-terms).

## Incident and operations management
{: #incident-and-ops}

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your responsibilities |
|----------|-----------------------|--------|
|Availability| {{site.data.keyword.cis_full_notm}} provides high availability through multi-zone region deployment and automatic failover between different regions in case of a region-wide failure. | |
|Monitoring and ongoing operation of production environments| {{site.data.keyword.cis_full_notm}} provides continuous around the clock operational monitoring and coverage by on-call personnel with minimal response times. | |
|Deployments and cluster management| New features, updates, and bug fixes are continuously delivered as needed in a manner transparent to the customer. Maintenance with client impact is scheduled in advance with notifications posted to the {{site.data.keyword.cloud}} status page. | Set preferences to receive email notifications. Monitor the {{site.data.keyword.cloud}} status page for general announcements. |
|Incident management| Unplanned incidents with customer impact are communicated using the CIE process. | Impacted customers can obtain a report about the incident upon request. |
|Logging | Logs system-level security events and patch activities. | Enable and manage logging for the customer's domains using [Logpush jobs](/docs/cis?topic=cis-logpush&interface=ui). |
{: caption="Responsibilities for incident and operations" caption-side="bottom"}

## Change management
{: #change-management}

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your responsibilities |
|----------|-----------------------|--------|
|Updates, fixes, and new features| {{site.data.keyword.cis_full_notm}} provides regular updates and bug fixes, as well as new features following a continuous delivery model in a manner transparent to the customer. | |
|Updates to edge capabilities| Updates are made regularly as part of continuous delivery. {{site.data.keyword.IBM_notm}} sends notifications for customer impacting changes. | Set preferences to receive email notifications. Monitor the {{site.data.keyword.cloud}} status page for general announcements. |
{: caption="Responsibilities for change management" caption-side="bottom"}

## Identity and access management
{: #iam-responsibilities}

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your responsibilities |
|----------|-----------------------|--------|
|Service and platform permissions| {{site.data.keyword.cis_full_notm}} provides administrators a way to control access to work with an instance, domain, or subcategory. | Grant, revoke, and manage access to service instances, domains, and subcategories by using IAM, the {{site.data.keyword.cis_full_notm}} Access page, or the equivalent CLI. |
|Security monitoring| {{site.data.keyword.cis_full_notm}} performs regular code scans and other measures to ensure ongoing security of the service.| |
|Logging| Logs access control actions within the CIS platform and IAM system. | Monitor access changes to CIS instances using IBM Cloud Activity Tracker Routing or other audit solutions. |
{: caption="Responsibilities for identity and access management" caption-side="bottom"}

## Security and regulation compliance
{: #security-compliance}

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
|Maintenance of controls| {{site.data.keyword.cis_full_notm}} maintains controls pertaining to industry standards for which it is certified.  |  |
|Security and vulnerability updates| {{site.data.keyword.cis_full_notm}} applies security and vulnerability patches on a regular and timely schedule that is transparent to the user. | |
|Security of instance and domain configuration| | Customer is responsible for setting up and maintaining the security and compliance of their domain within {{site.data.keyword.cis_full}}. | 
|Logging | Logs patch management and platform security operations to maintain compliance. | Customer is responsible for consuming and monitoring logs for their domains from configured Logpush job. | 
{: caption="Responsibilities for security and regulation compliance" caption-side="bottom"}

## Disaster recovery
{: #disaster-recovery}

The data for a domain in {{site.data.keyword.cis_full}} with its properties, settings, and configuration is stored and maintained in data centers across the network of our partner, Cloudflare. {{site.data.keyword.IBM_notm}} does not operate any data centers or maintain any customer data in the data path of the application.

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your responsibilities |
|----------|-----------------------|--------|
|Backup of domain configuration data | | The customer is responsible for maintaining backup copies and records pertaining to the configuration of the customer's domain. This includes DNS records, firewall rules, and any custom configuration of the customer's domain. |
|Recovery and verification of domain configuration| {{site.data.keyword.IBM_notm}} is responsible for restoring the domains and configurations it manages, and for restoring full data path functionality between client and origin. | After disaster recovery, it is the customer's responsibility to verify their domain is functional, and their configuration is as expected. The customer is also responsible for the health of origins that are serving their site content. |
|Recovery of control path capabilities| {{site.data.keyword.IBM_notm}} is responsible for recovering control path capabilities and making sure API, CLI, and/or UI are available to customers to manage their domains. {{site.data.keyword.IBM_notm}} works with our partner, Cloudflare, to restore capabilities end to end. | |
{: caption="Responsibilities for disaster recovery" caption-side="bottom"}
