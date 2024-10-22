---

copyright:
  years: 2018, 2024
lastupdated: "2024-10-22"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Using the Logpush service
{: #logpush}

{{site.data.keyword.cis_full}} Enterprise-level plans have access to detailed logs of HTTP and Range requests, and firewall events for their domains. These logs are helpful for debugging and analytics, especially when combined with other data sources, such as ingress or application server logs at the origin.
{: shortdesc}

The data from Logpush is the same as that from [Logpull](/docs/cis?topic=cis-logpull#logpull). However, unlike Logpull, which allows you to download request logs, Logpush provides the option to push the request logs to an {{site.data.keyword.loganalysislong_notm}} instance, or an {{site.data.keyword.cos_full}} ({{site.data.keyword.cos_short}}) bucket. You must [enable log retention](/docs/cis?topic=cis-logpull#log-retention) before using Logpush.

Range and firewall event logs are not included in HTTP(s) logs and require separate jobs. These jobs can be pushed to the same {{site.data.keyword.cos_short}} bucket, but must have a different path.

Logpush uses HTTPS endpoints for {{site.data.keyword.cos_full_notm}}, so the log data is encrypted while in motion.

## Before you begin
{: #logpush-prerequisites}

Before you create a Logpush job, you must have an [{{site.data.keyword.loganalysisshort_notm}}](/docs/log-analysis?topic=log-analysis-getting-started) instance (for CLI and API use only) or an [{{site.data.keyword.cos_short}}](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage) instance with a bucket that has **write access** granted to {{site.data.keyword.cloud}} account `cislogp@us.ibm.com`. This enables {{site.data.keyword.cis_short_notm}} to write request logs into the {{site.data.keyword.cos_short}} bucket.

## Setting up Logpush using the console
{: #logpush-setup-ui}
{: ui}

You can use either Log Analysis instances or Cloud Object Storage buckets as destinations for logpush jobs.

The IBM Log Analysis service is deprecated and will no longer be supported as of 30 March 2025. [IBM Cloud Logs](/docs/cloud-logs) support is coming soon. Until then, users can migrate jobs to Cloud Object Storage (COS).
{: deprecated}

### Creating Logpush with Log Analysis
{: #logpush-loganalysis-ui}


To configure a logpush job using Log Analysis, follow these steps.

1. Select the service.
    * Choose IBM Log Analysis
    * Select the dataset type
    * Enter an description
    * Click "Next"
1. Configure the destination.
    * Select the Log Analysis instance from the list menu
    * Enter the region your Log Analysis instance is in
    * Enter the Ingress key
    * Click "Next"
1. Select the log fields that you want included in the log push.
    * Verify that the logpush details are correct
    * Select the logpush settings from the Timestamp and Frequency list menus
    * Choose whether to enable the logpush job using the Enabled switch
    * Select the log fields to include in the logpush job
    * Click **Connect destination**.

### Creating Logpush with COS
{: #logpush-cos-ui}

It is recommended that you set up an allowlist that ensures only [{{site.data.keyword.cis_short_notm}} IPs](/docs/cis?topic=cis-cis-allowlisted-ip-addresses) can push objects into the {{site.data.keyword.cos_short}} bucket. For more information on configuring an IP allowlist in {{site.data.keyword.cos_short}}, see [Setting a firewall](/docs/cloud-object-storage?topic=cloud-object-storage-setting-a-firewall).
{: tip}

Follow these steps to add an application.

You can configure one logpush job for each {{site.data.keyword.cos_short}} object (also known as a destination). This means that you can have two log pushes at a time going to the same bucket, but to different objects. For example, one with HTTP and another with Range, both referring to different objects in same bucket.
{: note}

1. Select the service.
    * Choose Cloud Object Storage
    * Select the dataset type
    * Enter an description
    * Copy the user ID to add to your COS bucket. Add a policy in your **Cloud Object Storage Instance** bucket with `cislogp@us.ibm.com` as a user with `Object Writer` role.
    * Click "Next"
1. Configure your destination.
    * Select a Cloud Object Storage instance from the list menu
    * Select a bucket from the Bucket name list menu
    * Enter a bucket region, if applicable
    * Optionally, enter a bucket path
    * Select the checkbox if you want to organize logs into daily subfolders
    * Click "Next"
1. Verify ownership.
    * Download the object you received in your bucket, and paste the token in the Ownership token text area
    * You can resend the file from the Troubleshooting section, or return to the previous step if the bucket path is incorrect
    * Click "Next"
1. Select the log fields that you want included in the log push.
    * Verify that the logpush details are correct
    * Select the logpush settings from the Timestamp and Frequency list menus
    * Choose whether to enable the logpush job using the Enabled switch
    * Select the log fields to include in the logpush job
    * Click **Create service**.



## Setting up Logpush using the CLI
{: #logpush-setup-cli}
{: cli}

**Prerequisite**: Before you create a Logpush job, you must have an {{site.data.keyword.cos_full_notm}} instance with a bucket that has **Object Writer** access granted to {{site.data.keyword.cloud}} account `cislogp@us.ibm.com`. This enables {{site.data.keyword.cis_short_notm}} to write request logs into the {{site.data.keyword.cos_short}} bucket.

### Creating Logpush with Log Analysis CLI
{: #logpush-loganalysis-cli}

To create a Logpush job for a specific domain and enable the job using Log Analysis, run the following command:

```sh
ibmcloud cis logpush-job-create DNS_DOMAIN_ID --destination https://logs.us-south.logging.cloud.ibm.com/logs/ingest?hostname=example.com&apikey=xxxxxxx --name JOB_NAME --fields all --enable true
```
{: pre}

Where:

* **--destination** specifies the path to the Log Analysis instance.
    The hostname is the domain name in CIS for which you are sending log data. You can find it by running `imbcloud cis domains -i <instance-name>`. The URL must match the region of your Log Analysis instance (for example, `https://logs.{LOGDNA_REGION}.logging.cloud.ibm.com/logs/ingest?hostname={DOMAIN_NAME}&apikey={LOGDNA_INGESTION_KEY}`). For more information, see [Log Analysis regions](/docs/log-analysis?topic=log-analysis-regions).
    {: note}

* **--name** specifies the Logpush job name.
* **--fields** specifies the list of log fields to be included in log files. Use commas to separate multiple fields.
* **--enable** is the flag to enable or disable the Logpush job. Valid values are `true` or `false` (default).
* **--dataset** is the dataset that is pulled. One of `http_requests`, `range_events`, `firewall_events`.
* **--frequency** is the frequency at which CIS sends batches of logs to your destination. One of `high`, `low`.

### Creating Logpush with COS CLI
{: #logpush-cos-cli}

To create a Logpush job for a specific domain and enable the job using COS, run the following command:

```sh
ibmcloud cis logpush-job-create DNS_DOMAIN_ID --destination BUCKET_PATH --name JOB_NAME --fields all --enable true
```
{: pre}

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
{: note}

You can use the token `{DATE}` in the bucket path to make the Logpush job push request logs in daily folders in the bucket path. For example: `cos://mybucket/cislog/{DATE}?region=us-south&instance-id=c84e2a79-ce6d-3c79-a7e4-7e7ab3054cfe`
{: tip}

## Setting up Logpush using the API
{: #logpush-setup-api}
{: api}

To create a logpush job using the API, take the following steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:
    * `crn`: the full url-encoded CRN of the service instance.
    * `zone_id`: the domain ID.
    *  **request body**: information to create the logpush job body. One of `logpush_job_cos_req`, `logpush_job_logdna_req`.
        * For COS, `cos`: information to identify the COS bucket where the data is pushed.
        * For Log Analysis, `logdna`: information to identify the Log Analysis instance where the data is pushed.
        * `name`: The name of the logpush job.
        * `enabled`: Whether the job is enabled. One of `true`, `false`.
        * `logpull_options`: The configuration string. For example, `timestamps=rfc3339&timestamps=rfc3339`
        * `dataset`: The dataset that is pulled. One of `http_requests`, `range_events`, `firewall_events`.
        * `frequency`: The frequency at which CIS sends batches of logs to your destination. One of `high`, `low`.

1. When all variables are initiated, create the logpush job:
    * Log Analysis example
      ```sh
         {
          "logdna": {
              "hostname": "example.com",
              "ingress_key": "***************************",
              "region": "us-east"
          },
          "dataset": "range_events",
          "enabled": false,
          "name": "CIS-Range-LogDNA",
          "frequency": "low",
          "logpull_options": "fields=RayID,ZoneID&timestamps=rfc3339"
         }
      ```
      {: codeblock}

    * COS example

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
