---

copyright:
  years: 2019
lastupdated: "2019-04-26"

keywords: resolve override, Cloud Object Storage, bucket resource

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Resolve Override with COS
{: #resolve-override-cos}

This section offers use cases in resolving overrides with Cloud Object Storage.
{: shortdesc}

## Use cases
{: #cos-use-cases}

Make the request matching the page rule resolve to a Cloud Object Storage (COS) bucket resource.


## Prerequisites
{: #cos-prerequisites}

The following steps assume you have an existing COS instance and bucket with public access. For information on public access see [Allowing public access](/docs/services/cloud-object-storage?topic=cloud-object-storage-iam-public-access).


## Create Page Rule steps
{: #cos-create-page-rule}

* Navigate to **Performance->Page Rules**.
* Click **Create rule** button.
* Input the desired value for URL match. For example, `*.foo.com/*`.
  * Note that the URL match must match your COS object name.
  * For example, if you have an object called reports.txt under the bucket `my-bucket1`, then both of these URL matches would be valid:
    * `*.foo.com/*`
    * `*.foo.com/reports.txt`
* Use the list menu to select **Resolve Override with COS** under the **Performance** section.
* Use the **Cloud Object Storage Instance** list to select the desired instance.
* Use the **Bucket** list to select the desired bucket.
* To create the Page Rule click the **Provision 1 Resource** button.


## Detailed explanation of concepts
{: #cos-detail-concepts}

When creating a **Resolve Override with COS** page rule, CIS will automatically create the other necessary resources for the COS integration. These include:

**CNAME**
* A CNAME DNS record for `<bucket-name>.<cos-endpoint>` as `<bucket-name>`.
* For example, if your CIS domain is `foo.com`, you have a COS bucket called `images` and your public COS endpoint is `s3.us-west.objectstorage.uat.test.net` then CIS will create a CNAME as `images.foo.com` that points to `images.s3.us-west.objectstorage.uat.test.net`.
If the Resolve Override with COS page rule is no longer needed the CNAME should be manually deleted along with the page rule.
{:note}

**Host Header Override**
* The Host Header Override setting will replace the host header for the URI matching the page rule to `<bucket-name>.<cos-endpoint>`.
* Using the previous example, the Host Header Override value will be set to `images.s3.us-west.objectstorage.uat.test.net`.

## Proxy DNS entries are required for domains that are to be matched by the page rule
{: #proxy-dns-entry}
To perform the actual rewrite and redirecton to the COS bucket, the domains that you want to use with this page rule (such as `www.foo.com`) must have DNS entries in {{site.data.keyword.cis_short_notm}} with the 'proxy' flag set.  See [Proxying DNS Records](/docs/cis?topic=cis-dns-concepts#dns-concepts-proxying-dns-records) for more information.  If all requests to `www.foo.com` are redirected, then a CNAME entry that points to `<bucket-name>` with proxy enabled is sufficient.

## Deleting the Page Rule
{: #cos-delete-page-rule}

If the Resolve Override with COS page rule is no longer needed, the CNAME should be _manually_ deleted along with the page rule.


## Editing the Page Rule
{: #cos-edit-page-rule}

After editing the page rule, the **Resolve Override with COS** will no longer be displayed on the page. However, the **Resolve Override** `<bucket>.<domain>` and **Host Header Override** `<bucket>.<cos-endpoint>` will replace **Resolve Override with COS**.

Making changes to the **Resolve Override** will _not_ automatically create a new CNAME record (for example, `<updated-bucket>.<domain>`). This is only done upon the initial creation of a page rule using **Resolve Override with COS**. To automatically create the CNAME record for the bucket follow the [Create Page Rule](#cos-create-page-rule) steps.
