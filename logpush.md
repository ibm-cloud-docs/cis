---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-26"

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

IBM CIS customers on Enterprise accounts have access to detailed logs of HTTP requests for their domains. These logs are helpful for debugging, identifying configuration adjustments, and creating analytics, especially when combined with other data sources such as application server logs.

The data from Logpush is exactly the same as that from [Logpull](#logpull). Unlike Logpull, which allows CIS Enterprise customers to download request logs, Logpush provides CIS Enterprise customers the option to push the request logs to IBM Cloud Object Storage (COS) buckets. You’re free to choose the method that’s most convenient.

## Set up a Logpush job
{:#logpush-setup}

### Prerequisites
{:#logpush-prereq}

Before you create a Logpush job, you must have an IBM COS instance with a bucket that has **write access** granted to IBM Cloud account `cislogp@us.ibm.com`. This enables CIS to write request logs into the COS bucket. You can then proceed to use the following CIS CLI to create a Logpush job for a specified CIS domain.

### Set up Logpush with CLI
{:#logpush-setup-cli}

Use the following command to create a Logpush job for a specific domain and enable the job.
```
ibmcloud cis logpush-job-create DNS_DOMAIN_ID --destination BUCKET_PATH --name JOB_NAME --fields all --enable true
```
where,
  * `--destination` specifies the path to IBM COS bucket 
    * It follows the syntax: `cos://<bucket_path>?region=xxx&instance-id=xxxx`, in which `bucket_path` is the bucket name followed by an optional path-like structure, `region` and COS `instance-id` are IBM COS bucket region and instance ID, which must be also given in the query arguments.
    * For example, `cos://mybucket/cislog?region=us-south&instance-id=c84e2a79-ce6d-3c79-a7e4-7e7ab3054cfe`.
  * `--name` specifies the Logpush job name.
  * `--fields` specifies the list of log fields to be included in log files. 
    * Multiple fields can be separated by commas. 
    * Use command `ibmcloud cis logpull DNS_DOMAIN_ID --available-fields` to get the comprehensive list of available log fields, or use `all` to include all available fields in log files.
  * `--enable` is the flag to enable or disable the Logpush job. 
    * It is disabled by default.

A domain can only have one Logpush job. Use the command line to interactively address the COS bucket ownership challenge. When a challenge token is written to a file in the given COS bucket, you must:
  * download the file from your COS bucket, 
  * open the downloaded file, 
  * copy and paste the challenge token in the command prompt to address the ownership challenge. 
  
A Logpush job is created successfully after CIS validates the ownership challenge. The Logpush job pushes request logs to your COS bucket every 5 minutes.

You can use the token `{DATE}` in the bucket path to make the Logpush job push request logs in daily folders under the bucket path. For example, `cos://mybucket/cislog/{DATE}?region=us-south&instance-id=c84e2a79-ce6d-3c79-a7e4-7e7ab3054cfe`.
{:note}
