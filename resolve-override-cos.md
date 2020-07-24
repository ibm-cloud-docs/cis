---

copyright:
  years: 2019, 2020
lastupdated: "2020-07-07"

keywords: resolve override, Cloud Object Storage, bucket resource

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

# Using resolve override with Cloud Object Storage
{: #resolve-override-cos}

The following use case makes the request matching the page rule resolve to a COS bucket resource.
{: shortdesc}

## Prerequisites
{: #cos-prerequisites}

The following steps assume you have an existing COS instance and bucket with public access. For information on public access see [Allowing public access](/docs/cloud-object-storage?topic=cloud-object-storage-iam-public-access).

## Proxy DNS entries are required for domains that are to be matched by the page rule
{: #proxy-dns-entry}

To perform the actual rewrite and redirection to the COS bucket, the domains that you want to use with this page rule (such as `www.foo.com`) must have DNS entries in {{site.data.keyword.cis_short_notm}} with the `proxy` flag set.  See [Proxying DNS Records](/docs/cis?topic=cis-dns-concepts#dns-concepts-proxying-dns-records) for more information.  If all requests to `www.foo.com` are redirected, then a CNAME entry that points to `<bucket-name>` with proxy enabled is sufficient.

## Create page rule steps
{: #cos-create-page-rule}

1. Navigate to **Performance > Page Rules**.
1. Click **Create rule**.
1. Input the value you want for the URL match. For example, `*.foo.com/*`.
   * The URL match must be the same as your COS object name. For example, if you have an object called `reports.txt` under the bucket `my-bucket1`, then both of these URL matches would be valid:
     * `*.foo.com/*`
     * `*.foo.com/reports.txt`
1. Use the list menu to select **Resolve Override with COS** under the **Performance** section.
1. Use the **Cloud Object Storage Instance** list to select the instance you want.
1. Use the **Bucket** list to select the bucket you want.
1. Click **Create** to complete the rule.

## Editing a page rule
{: #cos-edit-page-rule}

After editing the page rule, the **Resolve Override with COS** is no longer displayed on the page. However, the **Resolve Override** `<bucket>.<domain>` and **Host Header Override** `<bucket>.<cos-endpoint>` replace **Resolve Override with COS**.

Making changes to the **Resolve Override** does _not_ automatically create a new CNAME record (for example, `<updated-bucket>.<domain>`). This is only done upon the initial creation of a page rule using **Resolve Override with COS**. To automatically create the CNAME record for the bucket follow the [Create page rule](#cos-create-page-rule) steps.

## Deleting the page rule
{: #cos-delete-page-rule}

If the Resolve Override with COS page rule is no longer needed, the CNAME should be _manually_ deleted along with the page rule.

## What happens in the background
{: #cos-detail-concepts}

When creating a **Resolve Override with COS** page rule, CIS automatically creates the other necessary resources for the COS integration. These include:

* **CNAME**
  * A CNAME DNS record for `<bucket-name>.<cos-endpoint>` as `<bucket-name>`.
  * For example, if your CIS domain is `foo.com`, you have a COS bucket called `images` and your public COS endpoint is `s3.us-west.objectstorage.uat.test.net` then CIS creates a CNAME as `images.foo.com` that points to `images.s3.us-west.objectstorage.uat.test.net`.

  If the Resolve Override with COS page rule is no longer needed the CNAME should be manually deleted along with the page rule.
  {:note}

* **Host Header Override**
  * The Host Header Override setting replaces the host header for the URI matching the page rule to `<bucket-name>.<cos-endpoint>`.
  * Using the previous example, the Host Header Override value is set to `images.s3.us-west.objectstorage.uat.test.net`.
