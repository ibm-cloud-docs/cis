---

copyright:
  years: 2024
lastupdated: "2024-11-12"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Understanding high availability for CIS
{: #ha}

[High availability](#x2284708){: term} (HA) is a core discipline in an IT infrastructure to keep your apps up and running, even after a partial or full site failure. The main purpose of high availability is to eliminate potential points of failures in an IT infrastructure.
{: shortdesc}

CIS is a globally available GA service, with public API endpoints accessible worldwide through a global load balancer across three multi-zone regions: Dallas (`us-south`), Washington, DC (`us-east`), and London (`eu-gb`). In the event of an outage in one region, the global load balancer automatically routes API traffic to the nearest available region. Data is replicated across these regions for optimized latency and high availability.

See [How IBM Cloud ensures high availability and disaster recovery](/docs/overview?topic=overview-zero-downtime#zero-downtime) to learn more about the high availability and disaster recovery standards in {{site.data.keyword.cloud_notm}}. You can also find information about [Service Level Agreements](/docs/overview?topic=overview-slas#slas).

## Responsibilities
{: #ha-responsibilities}

To find out more about responsibility ownership for using CIS between {{site.data.keyword.IBM_notm}} and the customer, see [Understanding your responsibilities when using CIS](/docs/cis?topic=cis-responsibilities-cis).

## What level of availability do I need?
{: #ha-level}

You can achieve high availability on different levels in your IT infrastructure and within different components of your cluster. The level of availability that is right for you depends on several factors, such as your business requirements, the service level agreements (SLAs) that you have with your customers, and the resources that you want to expend.

## What level of availability does {{site.data.keyword.cloud_notm}} offer?
{: #ha-service}

The level of availability that you set up for your cluster impacts your coverage under the {{site.data.keyword.cloud_notm}} high availability service level agreement terms.

Service level objectives (SLOs) describe the design points that the {{site.data.keyword.cloud_notm}} services are engineered to meet. CIS is designed to achieve the following availability target.

| Availability Target | Target Value   |
|---|---|
|  Availability % |   |
{: caption="SLO for CIS" caption-side="bottom"}

The SLO is not a warranty and {{site.data.keyword.IBM_notm}} will not issue credits for failure to meet an objective. Refer to the SLAs for commitments and credits that are issued for failure to meet any committed SLAs. For a summary of all SLOs, see [{{site.data.keyword.cloud_notm}} service level objectives](/docs/overview?topic=overview-slo).

## Locations
{: #ha-locations}

For more information about service availability within regions and data centers, see [Service and infrastructure availability by location](/docs/overview?topic=overview-services_region).
