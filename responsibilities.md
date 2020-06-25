---

copyright:
  years: 2020
lastupdated: "2020-04-14"

keywords: Cloud Internet Services, cis, responsibilities, ha, high availability, disaster recovery

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

# Understanding your responsibilities when using {{site.data.keyword.cis_short_notm}}
{: #responsibilities-cis}

Learn about the management responsibilities and terms and conditions that you have when you use {{site.data.keyword.cis_full}}. For a high-level view of the service types in {{site.data.keyword.cloud}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} offerings](/docs/overview?topic=overview-shared-responsibilities).
{:shortdesc}

Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use {{site.data.keyword.cis_full_notm}}. For the overall terms of use, see [{{site.data.keyword.cloud}} Terms and Notices](/docs/overview/terms-of-use?topic=overview-terms).

  
## Incident and operations management
{: #incident-and-ops}

<!-- Include an introductory sentence or two about this table. Leave the cell blank for the responsible party column if they do not have responsibility for the given task.  -->

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your responsibilities |
|----------|-----------------------|--------|
|Availability| {{site.data.keyword.cis_full_notm}} provides high availability through multi-zone region deployment and automatic failover between different regions in case of a region-wide failure.  |  |
|Monitoring and ongoing operation of production environments| {{site.data.keyword.cis_full_notm}} provides continuous around the clock operational monitoring and coverage by on-call pesonnel with minimal response times.  |  |
|Deployments and cluster management| New features, updates, and bug fixes are continously delivered as needed in a manner transparent to the customer. Maintenance with client impact will be scheduled in advance with notifications posted to the {{site.data.keyword.cloud}} status page. | Set preferences to receive email notifications. Monitor the {{site.data.keyword.cloud}} status page for general announcements. |
|Incident management| Unplanned incidents with customer impact will be communicated using the CIE process. | Impacted customers can obtain a report about the incident upon request. |
{: caption="Table 1. Responsibilites for incident and operations" caption-side="top"}


## Change management
{: #change-management}

<!-- Include an introductory sentence or two about this table. Leave the cell blank for the responsible party column if they do not have responsibility for the given task.  -->

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your responsibilities |
|----------|-----------------------|--------|
|Updates, fixes, and new features| {{site.data.keyword.cis_full_notm}} will provide regular updates and bug fixes, as well as new features folliwing a continuous delivery model in a manner transparent to the customer. | |
|Updates to edge capabilities| Updates will be made regularly as part of continuous delivery. {{site.data.keyword.IBM_notm}} will send notifications for customer impacting changes. | Set preferences to receive email notifications. Monitor the {{site.data.keyword.cloud}} status page for general announcements.  |
{: caption="Table 2. Responsibilites for change management" caption-side="top"}


## Identity and access management
{: #iam-responsibilities}

<!-- Include an introductory sentence or two about this table. Leave the cell blank for the responsible party column if they do not have responsibility for the given task.  -->

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your responsibilities |
|----------|-----------------------|--------|
|Service and platform permissions| {{site.data.keyword.cis_full_notm}} will provide administrators a way to control access to work with an instance, domain, or subcategory. | Grant, revoke, and manage access to service instances, domains, and subcategories by using IAM, the {{site.data.keyword.cis_full_notm}} Access page, or the equivalent CLI. |
|Security monitoring| {{site.data.keyword.cis_full_notm}} will perform regular code scans and other measures to ensure ongoing security of the service.||
{: caption="Table 3. Responsibilites for identity and access management" caption-side="top"}

## Security and regulation compliance
{: #security-compliance}

<!-- Include an introductory sentence or two about this table. Leave the cell blank for the responsible party column if they do not have responsibility for the given task.  -->

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|----------|-----------------------|--------|
|Maintenance of controls| {{site.data.keyword.cis_full_notm}} maintains controls pertaining to industry standards for which it is certified.  | Customer responsibility description |
|Security and vulnerability updates| {{site.data.keyword.cis_full_notm}} applies security and vulnerability patches on a regular and timely schedule that is transparent to the user.  |  |
|Security of instance and domain configuration| | Customer is reponsibile for setting up and maintaining the security and compliance of their domain within {{site.data.keyword.cis_full}} |
{: caption="Table 4. Responsibilites for security and regulation compliance" caption-side="top"}

## Disaster recovery
{: #disaster-recovery}

The data for a domain in {{site.data.keyword.cis_full}} with its properties, settings, and configuration is stored and maintained in data centers across the network of our partner, Cloudflare. {{site.data.keyword.IBM_notm}} does not operate any data centers or maintain any customer data in the data path of the application. 

| Task | {{site.data.keyword.IBM_notm}} Responsibilities | Your responsibilities |
|----------|-----------------------|--------|
|Backup of domain configuration data |   | The customer is responsible for maintaining backup copies and records pertaining to the configuration of the customer's domain. This includes DNS records, firewall rules, and any custom configuration of the customer's domain. |
|Recovery and verification of domain configuration| {{site.data.keyword.IBM_notm}} is responsible for restoring the domains and configurations it manages, and for restoring full data path functionality between client and origin. | After disaster recovery, it is the customer's responsibility to verify their domain is functional, and their configuration is as expected. The customer is also responsible for the health of origins that are serving their site content.  |
|Recovery of control path capabilities| {{site.data.keyword.IBM_notm}} is responsible for recovering control path capabilities and making sure API, CLI, and/or UI are available to customers to manage their domains. {{site.data.keyword.IBM_notm}} will work with our partner, Cloudflare, to restore capabilities end to end.  |  |
{: caption="Table 5. Responsibilites for disaster recovery" caption-side="top"}
