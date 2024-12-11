---

copyright:
  years: 2018, 2024
lastupdated: "2024-12-11"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Managing Logpush jobs
{: #logpush}

{{site.data.keyword.cis_full}} Enterprise-level plans have access to detailed logs of HTTP and Range requests, and firewall events for their domains. These logs are helpful for debugging and analytics, especially when combined with other data sources, such as ingress or application server logs at the origin.
{: shortdesc}

The data from Logpush is the same as that from [Logpull](/docs/cis?topic=cis-logpull#logpull). However, unlike Logpull, which allows you to download request logs, Logpush provides the option to push the request logs to an {{site.data.keyword.cos_full}} ({{site.data.keyword.cos_short}}) bucket. You must [enable log retention](/docs/cis?topic=cis-logpull#log-retention) before using Logpush.

Range and firewall event logs are not included in HTTP(s) logs and require separate jobs. These jobs can be pushed to the same {{site.data.keyword.cos_short}} bucket, but must have a different path.

Logpush uses HTTPS endpoints for {{site.data.keyword.cos_full_notm}}, so the log data is encrypted while in motion.

The IBM Log Analysis service is deprecated and will no longer be supported as of 30 March 2025. You can migrate jobs to Cloud Object Storage.
{: deprecated}

## Creating a Logpush job in the UI
{: #logpush-setup-ui}
{: ui}

Use Cloud Object Storage buckets as destinations for Logpush jobs.
    
### Creating a Logpush job with Cloud Object Storage in the UI
{: #logpush-cos-ui}
{: ui}

It is recommended that you set up an allowlist that ensures only [{{site.data.keyword.cis_short_notm}} IPs](/docs/cis?topic=cis-cis-allowlisted-ip-addresses) can push objects into the {{site.data.keyword.cos_short}} bucket. For more information on configuring an IP allowlist in {{site.data.keyword.cos_short}}, see [Setting a firewall](/docs/cloud-object-storage?topic=cloud-object-storage-setting-a-firewall).
{: tip}

Follow these steps to add an application.

**Prerequisite**: Before you create a Logpush job, you must have an [{{site.data.keyword.cos_short}}](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage) instance with a bucket that has **write access** granted to {{site.data.keyword.cloud}} account `cislogp@us.ibm.com`. This enables {{site.data.keyword.cis_short_notm}} to write request logs into the {{site.data.keyword.cos_short}} bucket. 

1. Select the service:
   1. Choose Cloud Object Storage.
   1. Select the dataset type.
   1. Enter a description.
   1. Copy the user ID to add to your Cloud Object Storage bucket. Add a policy in your **Cloud Object Storage Instance** bucket with `cislogp@us.ibm.com` as a user with `Object Writer` role.
   1. Click **Next**.

1. Configure your destination:
   1. Select a Cloud Object Storage instance from the menu.
   1. Select a bucket from the Bucket name menu.
   1. Enter a bucket region, if applicable.
   1. Optionally, enter a bucket path.
   1. Select the checkbox if you want to organize logs into daily subfolders.
   1. Click **Next**.

1. Verify ownership:
   1. Download the object that you received in your bucket, and paste the token in the Ownership token text area.

      You can resend the file from the Troubleshooting section, or return to the previous step if the bucket path is incorrect.
      {: note}

   1. Click **Next**.

1. Select the log fields that you want included in the log push:
   1. Verify that the Logpush details are correct.
   1. Select the Logpush settings from the Timestamp and Frequency menus.
   1. Choose whether to enable the Logpush job using the Enabled switch.
   1. Select the log fields to include in the Logpush job.
   1. Click **Create service**.

## Creating a Logpush job from the CLI
{: #logpush-setup-cli}
{: cli}

Use Cloud Object Storage CLI to create a Logpush job.

### Creating a Logpush job with Cloud Object Storage from the CLI
{: #logpush-cos-cli}
{: cli}

**Prerequisite**: Before you create a Logpush job, you must have an {{site.data.keyword.cos_full_notm}} instance with a bucket that has **Object Writer** access that is granted to {{site.data.keyword.cloud}} account `cislogp@us.ibm.com`. This enables {{site.data.keyword.cis_short_notm}} to write request logs into the {{site.data.keyword.cos_short}} bucket.

To create a Logpush job for a specific domain and enable the job using Cloud Object Storage, run the following command:

```sh
ibmcloud cis logpush-job-create DNS_DOMAIN_ID --destination BUCKET_PATH --name JOB_NAME --fields all --enable true
```
{: pre}

Where:

`--destination`
:   Specifies the path to the {{site.data.keyword.cos_short}} bucket.

   It follows the syntax: `cos://<bucket_path>?region=xxx&instance-id=xxxx`, where `bucket_path` is the bucket name followed by an optional path-like structure, `region` and {{site.data.keyword.cos_short}} `instance-id` are the {{site.data.keyword.cos_short}} bucket region and instance ID, which are required arguments.

   For example, `cos://mybucket/cislog?region=us-south&instance-id=c84e2a79-ce6d-3c79-a7e4-7e7ab3054cfe`.

`--name`
:   Specifies the Logpush job name.

`--enable`
:   Is the flag to enable or disable the Logpush job. Valid values are `true` or `false` (default).
  
`--fields`
:   Specifies the list of log fields to be included in log files. Use commas to separate multiple fields.

   Use command `ibmcloud cis logpull DNS_DOMAIN_ID --available-fields` to get a comprehensive list of available log fields, or use `all` to include all available fields in the log files.
 
 `--timestamps`
:   Sets the format in which response timestamps are returned. Valid values are `unix`, `unixnano`, and `rfc3339` (default).

 `--dataset`
:   Is the category of logs that you want to receive. Valid values are `range_events` and `http_requests` (default). You cannot change this value after the job is created.

 `-i` or `--instance`
:   Is the instance name. If not set, the context instance specified by `ibmcloud cis instance-set INSTANCE` is used.

A domain can have only one Logpush job. Use the command line to interactively address the {{site.data.keyword.cos_short}} bucket ownership challenge. When a challenge token is written to a file in the given {{site.data.keyword.cos_short}} bucket, you must:

* Download the file from your {{site.data.keyword.cos_short}} bucket and open it.
* Copy and paste the challenge token in the command prompt to address the ownership challenge.

A Logpush job is created successfully after {{site.data.keyword.cis_short_notm}} validates the ownership challenge. The Logpush job pushes request logs to your {{site.data.keyword.cos_short}} bucket every 30 seconds or every 100,000 records, whichever comes first. More than one file might be pushed per 30-second period or per 100,000 records.

Logpush jobs created before September 2020 might continue pushing every 5 minutes. Any modification to one of these older jobs triggers an update to the push frequency.
{: note}

You can use the token `{DATE}` in the bucket path to make the Logpush job push request logs in daily folders in the bucket path. For example: `cos://mybucket/cislog/{DATE}?region=us-south&instance-id=c84e2a79-ce6d-3c79-a7e4-7e7ab3054cfe`
{: tip}

## Creating a Logpush job with the API
{: #logpush-setup-api}
{: api}

Use Cloud Object Storage API to create a Logpush job.

### Creating a Logpush job with Cloud Object Storage API
{: #logpush-setup-cos-api}
{: api}

To create a Logpush job using the API, follow these steps:

**Prerequisite**: Before you create a Logpush job, you must have an {{site.data.keyword.cos_full_notm}} instance with a bucket that has **Object Writer** access that is granted to {{site.data.keyword.cloud}} account `cislogp@us.ibm.com`. This enables {{site.data.keyword.cis_short_notm}} to write request logs into the {{site.data.keyword.cos_short}} bucket.

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `crn`: The full url-encoded CRN of the service instance.
    * `zone_id`: The domain ID.
    *  **request body**: Information to create the Logpush job body (`logpush_job_cos_req`).
        * For COS, `cos`: Information to identify the Cloud Object Storage bucket where the data is pushed.
        * `name`: The name of the Logpush job.
        * `enabled`: Whether the job is enabled. One of `true`, `false`.
        * `logpull_options`: The configuration string. For example, `timestamps=rfc3339&timestamps=rfc3339`
        * `dataset`: The dataset that is pulled. One of `http_requests`, `range_events`, `firewall_events`.
        * `frequency`: The frequency at which CIS sends batches of logs to your destination. One of `high`, `low`.

1. When all variables are initiated, create the Logpush job:

      ```sh
         {
         "cos": {
             "bucket_name": "example_bucket",
             "path": "temp/",
             "id": "cos_instance_id",
             "region": "us-east"
         },
         "dataset": "firewall_events",
         "enabled": false,
         "name": "CIS-Firewall-COS",
         "frequency": "low",
         "logpull_options": "fields=RayID,ZoneID&timestamps=rfc3339",
         "ownership_challenge": "xxxxxxx"
         }
      ```
      {: codeblock}


## Related link
{: #related-link-logpush}

[Managing user API keys](/docs/account?topic=account-userapikey&interface=ui)
