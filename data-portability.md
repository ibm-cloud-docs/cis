---

copyright:
  years: 2024
lastupdated: "2024-10-31"

keywords:

subcollection: repo-name

---

{{site.data.keyword.attribute-definition-list}}



# Understanding data portability for CIS
{: #data-portability}

[See comments in the source file on Github]{: tag-red}

[Guidance here](https://test.cloud.ibm.com/docs/writing?topic=writing-data-portability-content-guidance)

**This topic should be placed in a topic group with the high availability, business continuity, and disaster recovery topic. I don't see any of these topics.**





Data portability involves a set of tools and procedures that enable customers to export the digital artifacts that are needed to implement similar workload and data processing on different service providers or on-premises software. It includes procedures for copying and storing the service customer content, including the related configuration that is used by the service to store and process the data, on the customer's own location.
{: shortdesc}

## Responsibilities
{: #data-portability-responsibilities}

{{site.data.keyword.cloud_notm}} services provide interfaces and instructions to guide the customer to copy and store the service customer content, including the related configuration, on their own selected location.

The customer is responsible for the use of the exported data and configuration for data portability to other infrastructures, which includes:

- The planning and execution for setting up alternative infrastructure on different cloud providers or on-premises software that provide similar capabilities to the {{site.data.keyword.IBM_notm}} services.
- The planning and execution for the porting of the required application code on the alternative infrastructure, including the adaptation of customer's application code, deployment automation, and so on.
- The conversion of the exported data and configuration to the format that's required by the alternative infrastructure and adapted applications.


To find out more about responsibility ownership for using {{site.data.keyword.cloud}} products between {{site.data.keyword.IBM_notm}} and customer see [Shared responsibilities for {{site.data.keyword.cloud_notm}} products](/docs/overview?topic=overview-shared-responsibilities).



For more information about your responsibilities for CIS, see [Understanding your responsibilities when using CIS](/docs/cis?topic=cis-responsibilities-cis).

## Data export procedures
{: #data-portability-procedures}

CIS provides the mechanisms to export your content that's uploaded, stored, and processed when you use the service.



In addition, CIS provides mechanisms to export settings and configurations that are used to process the customer's content.



## Exported data formats
{: #data-portability-data-formats}



CIS supports the following data format and schema of the exported data, configuration, and application:
* Example data format and schema


CIS doesn't support the export of the following data format and schema of the exported data, configuration, and application:
* Example of unsupported data format and schema

## Data ownership
{: #data-portability-ownership}

All exported data is classified as customer content. Apply the full customer ownership and licensing rights, as stated in the [IBM Cloud Service Agreement](https://www.ibm.com/terms/?id=Z126-6304_WS){: external}.



