---
copyright:
  years: 1994, 2017
lastupdated: "2018-12-05"
---
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# HIPAA Advisory

Use of Caching (CDN) for regulated data (for example, PHI, ITAR) is **prohibited**. All regulated data flows that use CIS must be set to **not cache**.
{:important}

There are multiple ways to disable content caching by the CIS CDN. 
- The origin server can set **no-cache** in the **Cache-Control** header for the regulated content
- Use the CIS Page Rules to disable caching for any content on a specified path, even if the origin does not send a **no-cache** **Cache-Control** header. 
