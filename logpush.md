---

copyright:
  years: 2018, 2020
lastupdated: "2020-02-20"

keywords: log push, logpush, time-based

subcollection: cis

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Logpush
{:#logpush}

{{site.data.keyword.cis_full}} customers on Enterprise accounts have access to detailed logs of HTTP requests for their domains. These logs are helpful for debugging, identifying configuration adjustments, and creating analytics, especially when combined with other data sources such as application server logs.
{: shortdesc}

The data from Logpush is exactly the same as that from [Logpull](#logpull). Unlike Logpull, which allows {{site.data.keyword.cis_short_notm}} Enterprise customers to download request logs, Logpush provides {{site.data.keyword.cis_short_notm}} Enterprise customers the option to push the request logs to {{site.data.keyword.cos_full}} ({{site.data.keyword.cos_short}}) buckets. You’re free to choose the method that’s most convenient.

Logpush uses HTTPS endpoints for {{site.data.keyword.cos_full_notm}}, so the log data is encrypted while in motion.

## Set up a Logpush job
{:#logpush-setup}

### Prerequisites
{:#logpush-prereq}

Before you create a Logpush job, you must have an {{site.data.keyword.cos_full_notm}} instance with a bucket that has **write access** granted to {{site.data.keyword.cloud}} account `cislogp@us.ibm.com`. This enables {{site.data.keyword.cis_short_notm}} to write request logs into the {{site.data.keyword.cos_short}} bucket. You can then proceed to use the following {{site.data.keyword.cis_short_notm}} CLI to create a Logpush job for a specified {{site.data.keyword.cis_short_notm}} domain.

### Set up Logpush with CLI
{:#logpush-setup-cli}

Use the following command to create a Logpush job for a specific domain and enable the job.
```
ibmcloud cis logpush-job-create DNS_DOMAIN_ID --destination BUCKET_PATH --name JOB_NAME --fields all --enable true
```
{:pre}
where,
  * `--destination` specifies the path to {{site.data.keyword.cos_short}} bucket
    * It follows the syntax: `cos://<bucket_path>?region=xxx&instance-id=xxxx`, in which `bucket_path` is the bucket name followed by an optional path-like structure, `region` and {{site.data.keyword.cos_short}} `instance-id` are {{site.data.keyword.cos_short}} bucket region and instance ID, which must be also given in the query arguments.
    * For example, `cos://mybucket/cislog?region=us-south&instance-id=c84e2a79-ce6d-3c79-a7e4-7e7ab3054cfe`.
  * `--name` specifies the Logpush job name.
  * `--enable` is the flag to enable or disable the Logpush job.
    * Valid values are `true` or `false`.
    * It is disabled (`false`) by default.
  * `--fields` specifies the list of log fields to be included in log files.
    * Multiple fields can be separated by commas.
    * Use command `ibmcloud cis logpull DNS_DOMAIN_ID --available-fields` to get the comprehensive list of available log fields, or use `all` to include all available fields in log files.
  * `--timestamps` sets the format in which response timestamps are returned. 
    * Valid values are `unix`, `unixnano`, and `rfc3339`.
    * Default value is `rfc3339`. 
  * `--dataset` is the category of logs you want to receive. 
    * This value cannot be changed after the job is created.
    * Valid values are `http_requests`, and `range_events`.
    * Default value is `http_requests`.
  * `-i` or, `--instance` is the instance name. 
    * If not set, the context instance specified by `ibmcloud cis instance-set INSTANCE` is used.

A domain can only have one Logpush job. Use the command line to interactively address the {{site.data.keyword.cos_short}} bucket ownership challenge. When a challenge token is written to a file in the given {{site.data.keyword.cos_short}} bucket, you must:
  * download the file from your {{site.data.keyword.cos_short}} bucket,
  * open the downloaded file,
  * copy and paste the challenge token in the command prompt to address the ownership challenge.

A Logpush job is created successfully after {{site.data.keyword.cis_short_notm}} validates the ownership challenge. The Logpush job pushes request logs to your {{site.data.keyword.cos_short}} bucket every 5 minutes.

You can use the token `{DATE}` in the bucket path to make the Logpush job push request logs in daily folders under the bucket path. For example, `cos://mybucket/cislog/{DATE}?region=us-south&instance-id=c84e2a79-ce6d-3c79-a7e4-7e7ab3054cfe`.
{:note}
