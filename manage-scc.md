---

copyright:
  years: 2020
lastupdated: "2021-08-30"

keywords: security and compliance for CIS, CIS compliance, CIS security, security for CIS, Compliance for CIS

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Managing security and compliance with {{site.data.keyword.cis_short_notm}}
{: #manage-security-compliance}

{{site.data.keyword.cis_full}} is integrated with the {{site.data.keyword.compliance_short}} to help you manage security and compliance for your organization.
{: shortdesc}

With the {{site.data.keyword.compliance_short}}, you can monitor for controls and goals that pertain to {{site.data.keyword.cis_short_notm}}.

## Monitoring security and compliance posture with {{site.data.keyword.cis_short_notm}}
{: #monitor-cis}

As a security or compliance focal, you can use the {{site.data.keyword.cis_short_notm}} [goals](x2117978){: term} to help ensure that your organization is adhering to the external and internal standards for your industry. By using the {{site.data.keyword.compliance_short}} to validate the resource configurations in your account against a [profile](x2034950){: term}, you can identify potential issues as they arise.

All of the goals for {{site.data.keyword.cis_short_notm}} are added to the {{site.data.keyword.cloud_notm}} Best Practices Controls 1.0 profile but can also be mapped to other profiles.
{: note}

To start monitoring your resources, check out [Getting started with {{site.data.keyword.compliance_short}}](/docs/security-compliance?topic=security-compliance-getting-started).

### Available goals for {{site.data.keyword.cis_short_notm}}
{: #cis-available-goals}

* Check whether {{site.data.keyword.cis_short}} has Web Application Firewall enabled
* Check whether {{site.data.keyword.cis_short}} has TLS v1.2 set for all inbound traffic
* Check whether {{site.data.keyword.cis_short}} has DDoS protection enabled
* Check whether {{site.data.keyword.cis_short}} has TLS mode set to End-to-End CA signed


## Governing {{site.data.keyword.cis_short_notm}} resource configuration
{: #govern-cis}

As a security or compliance focal, you can use the {{site.data.keyword.compliance_short}} to define configuration rules for the instances of {{site.data.keyword.cis_short_notm}} that you create.

[Config rules](#x3084914){: term} are used to enforce the configuration standards that you want to implement across your accounts. To learn more about the data that you can use to create a rule for {{site.data.keyword.cis_short_notm}}, review the following table.

| Resource kind | Property | Operator | Value | Description |
|---------------|----------|---------------|-------|-------------|
| *zone* | *tls_mode* | *string_equals*  | *off*  \n *flexible*  \n *full*  \n *strict*  \n *origin_pull*  | A string indicating the TLS mode for encryption. |
| *zone* | *waf_enabled* | *string_equals* | *on*  \n *off* | A string indicating whether the WAF is turned on or off. |
{: caption="Table 1. Rule properties for {{site.data.keyword.cis_short_notm}}" caption-side="bottom"}

To learn more about constructing config rules, check out [Formatting rules and templates](/docs/security-compliance?topic=security-compliance-formatting-rules-templates).
