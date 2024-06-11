---

copyright:
  years: 2018, 2024
lastupdated: "2024-05-15"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Managing access for {{site.data.keyword.cis_short_notm}}
{: #iam-and-cis}

Access to {{site.data.keyword.cis_full}} service instances for users in your account is controlled by {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). Every user that accesses the ({{site.data.keyword.cis_short_notm}}) service in your account must be assigned an access policy with an IAM role defined. The policy determines what actions that a user can perform within the context of the service or instance that you select. The allowable actions are customized and defined by the {{site.data.keyword.cloud_notm}} service as operations that are allowed to be performed on the service. The actions are then mapped to IAM user roles.

Policies enable access to be granted at different levels. Some access includes the following options:

* Access across all instances of the service in your account
* Access to an individual service instance in your account

After you define the scope of the access policy, you assign a role, which determines the user's level of access.

If you are configuring a VPC with {{site.data.keyword.cis_short_notm}}, you can prevent DDoS attacks by allowing traffic only through {{site.data.keyword.cis_short_notm}} (allowlist) in your VPC. Set your Network ACL and Security groups to allowlist {{site.data.keyword.cis_short_notm}} traffic.

Review the following table that outlines what actions each role allows within the ({{site.data.keyword.cis_short_notm}}) service. The platform and service roles for {{site.data.keyword.cis_short_notm}} are listed under "Internet Services". If you're using the CLI or API to assign access, use `internet-svcs` for the service name.

Platform management roles enable users to perform tasks on service resources at the platform level, for example, assign user access for the service and create or delete instances.

For more information about IAM roles, see [IBM Cloud IAM roles](/docs/account?topic=account-userroles).

| Platform management role | Description of actions |
|--------------------------|--------------------------|
| Manager | Create and delete instances, domains, and configurations. |
| Reader | View information about instances and domains. |
| Service Configuration Reader | Read services configuration for Governance management. |
| Writer | Change existing configurations. |
{: caption="Table 1. IAM user roles and actions" caption-side="bottom"}

For information about assigning user roles in the console, see [Managing access to resources](/docs/account?topic=account-assign-access-resources#assign-access-resources).
