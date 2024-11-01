---

copyright:
  years: 2024
lastupdated: "2024-11-01"

keywords:

subcollection: cis
---

{{site.data.keyword.attribute-definition-list}}

# DNS resolution in partial (CNAME) configuration
{: #dns-resolution-in-cname-config}

[NEEDS REVIEW - ENTIRE]{: tag-red}

In a partial (CNAME) configuration, {{site.data.keyword.cis_short_notm}} handles DNS records a bit differently from full zones to internally resolve the origin server where proxied HTTP requests are sent to.

## Records within the same zone
{: #records-in-same-zone}

When you create a new DNS record in a partial zone, {{site.data.keyword.cis_short_notm}} automatically checks whether any of your CNAME records point to existing A, AAAA, or CNAME records within the same zone.

For example, CIS would show a warning if you have the following records in your partial zone:

```text
sub1.partialzone.com   CNAME   sub2.partialzone.com
sub2.partialzone.com   A       192.0.2.1
```
{: screen}

Because {{site.data.keyword.cis_short_notm}} contains both the CNAME and its target, the DNS resolution sends incoming HTTP requests to `sub1.partialzone.com` to the origin `192.0.2.1`.

This can cause issues if you already have DNS records for `sub2.partialzone.com` at your authoritative DNS provider. These records might point to `192.0.2.4`, another IP address, or another domain. However, because {{site.data.keyword.cis_short_notm}} contains the initial record and the target, it never queries your authoritative DNS provider for the record for `sub2.partialzone.com`.

![Path without authoritative dns](images/dns-resolution1.svg "DNS request path no authoritative dns"){: caption="Path a request takes without passing through an authoritative DNS" caption-side="bottom"}

If you don't have the target of the CNAME record within your partial zone this DNS resolution happens differently.

![Path with authoritative dns](images/dns-resolution2.svg "DNS request path with authoritative dns"){: caption="Path a request takes passing through an authoritative DNS" caption-side="bottom"}

## Records pointing to a partial zone within the same account
{: #records-partial-zone-same-account}

You can also create a CNAME record in a zone (partial or full setup) that points to a record in another partial zone within your account. In this case, {{site.data.keyword.cis_short_notm}} always resolves the CNAME target based on the value at your authoritative DNS provider of the partial target zone.

![Path within same account](images/dns-resolution3.svg "DNS request path within the same account"){: caption="Path a request takes within the same account" caption-side="bottom"}
