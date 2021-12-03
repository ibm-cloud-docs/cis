---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Advisory, Use of Caching, content caching, Cache-Control header

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# HIPAA advisory
{: #hipaa-advisory}

Use of caching (CDN) for regulated data (for example, PHI, ITAR) is **prohibited**. All regulated data flows that use {{site.data.keyword.cis_full}} must be set to **not cache**.
{: important}
{: shortdesc}

There are multiple ways to disable content caching by the CIS CDN.
- The origin server can set **no-cache** in the **Cache-Control** header for the regulated content
- Use the {{site.data.keyword.cis_short_notm}} page rules to disable caching for any content on a specified path, even if the origin does not send a **no-cache** **Cache-Control** header.
