---

copyright:
  years: 2018, 2020
lastupdated: "2020-09-30"


keywords: 

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

# Using the Logpush service
{:#logpush}

{{site.data.keyword.cis_full}} Enterprise-level plans have access to detailed logs of HTTP and range requests for their domains. These logs are helpful for debugging and analytics, especially when combined with other data sources, such as ingress or application server logs at the origin.
{: shortdesc}

The data from Logpush is the same as that from [Logpull](/docs/cis?topic=cis-logpull#logpull). However, unlike Logpull, which allows you to download request logs, Logpush provides the option to push the request logs to {{site.data.keyword.cos_full}} ({{site.data.keyword.cos_short}}) buckets. You’re free to choose the method that’s most convenient.

Range logs are not included in HTTP(s) logs and require a separate job. These jobs can be pushed to the same {{site.data.keyword.cos_short}} bucket, but must have a different path.
{:tip}

Logpush uses HTTPS endpoints for {{site.data.keyword.cos_full_notm}}, so the log data is encrypted while in motion.

## Setting up Logpush using the console
{:#logpush-setup-ui}

**Prerequisite**: Before you create a Logpush job, you must have an [{{site.data.keyword.cos_full_notm}}](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage) instance with a bucket that has **write access** granted to {{site.data.keyword.cloud}} account `cislogp@us.ibm.com`. This enables {{site.data.keyword.cis_short_notm}} to write request logs into the {{site.data.keyword.cos_short}} bucket.

Follow these steps to add an application.

You can configure one log push job for each {{site.data.keyword.cos_short}} object (also known as a destination). This means that you can have two log pushes at a time going to the same bucket, but to different objects. For example, one with HTTP and another with Range, both referring to different objects in same bucket.
{:note}

1. Navigate to **Account** in your {{site.data.keyword.cis_short_notm}} instance and select the **Logs** tab.
1. In the **Log push** section, select the **HTTP/HTTPS** or **Range** tab.
1. Click **Create**.
1. Select a Cloud Object Storage instance from the list menu.
1. Select a bucket from the Bucket list menu.
1. Optionally, enter a bucket path.
1. Select the checkbox if you want to organize logs into daily subfolders.
1. Add a policy in your **Cloud Object Storage Instance** bucket with `cislogp@us.ibm.com` as a user with writer role.
1. Click the **Send ownership verification** button.
1. Download the object you received in your bucket, paste the token in the text area, then click **Verify ownership**.
1. Select the log fields that you want included in the log push, then click **Save**.

## Setting up Logpush using the CLI
{:#logpush-setup-cli}

**Prerequisite**: Before you create a Logpush job, you must have an {{site.data.keyword.cos_full_notm}} instance with a bucket that has **write access** granted to {{site.data.keyword.cloud}} account `cislogp@us.ibm.com`. This enables {{site.data.keyword.cis_short_notm}} to write request logs into the {{site.data.keyword.cos_short}} bucket.

To create a Logpush job for a specific domain and enable the job, run the following command:

```
ibmcloud cis logpush-job-create DNS_DOMAIN_ID --destination BUCKET_PATH --name JOB_NAME --fields all --enable true
```
{:pre}

Where:

* **--destination** specifies the path to the {{site.data.keyword.cos_short}} bucket.

   It follows the syntax: `cos://<bucket_path>?region=xxx&instance-id=xxxx`, where `bucket_path` is the bucket name followed by an optional path-like structure, `region` and {{site.data.keyword.cos_short}} `instance-id` are the {{site.data.keyword.cos_short}} bucket region and instance ID, which are required arguments.

   For example, `cos://mybucket/cislog?region=us-south&instance-id=c84e2a79-ce6d-3c79-a7e4-7e7ab3054cfe`.

* **--name** specifies the Logpush job name.
* **--enable** is the flag to enable or disable the Logpush job. Valid values are `true` or `false` (default).
* **--fields** specifies the list of log fields to be included in log files. Use commas to separate multiple fields.

   Use command `ibmcloud cis logpull DNS_DOMAIN_ID --available-fields` to get a comprehensive list of available log fields, or use `all` to include all available fields in the log files.

* **--timestamps** sets the format in which response timestamps are returned. Valid values are `unix`, `unixnano`, and `rfc3339` (default).
* **--dataset** is the category of logs that you want to receive. Valid values are `range_events` and `http_requests` (default).

   You cannot change this value after the job is created.

* **-i** or **--instance** is the instance name. If not set, the context instance specified by `ibmcloud cis instance-set INSTANCE` is used.

A domain can only have one Logpush job. Use the command line to interactively address the {{site.data.keyword.cos_short}} bucket ownership challenge. When a challenge token is written to a file in the given {{site.data.keyword.cos_short}} bucket, you must:

   * Download the file from your {{site.data.keyword.cos_short}} bucket and open it.
   * Copy and paste the challenge token in the command prompt to address the ownership challenge.

A Logpush job is created successfully after {{site.data.keyword.cis_short_notm}} validates the ownership challenge. The Logpush job pushes request logs to your {{site.data.keyword.cos_short}} bucket every 30 seconds or every 100,000 records, whichever comes first. More than one file might be pushed per 30-second period or per 100,000 records. 

Logpush jobs created prior to September 2020 might continue pushing every 5 minutes. Any modification to one of these older jobs triggers an update to the push frequency.
{:note}

You can use the token `{DATE}` in the bucket path to make the Logpush job push request logs in daily folders in the bucket path. For example: `cos://mybucket/cislog/{DATE}?region=us-south&instance-id=c84e2a79-ce6d-3c79-a7e4-7e7ab3054cfe`
{:tip}

