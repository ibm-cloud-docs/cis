---

copyright:
  years: 2018, 2024
lastupdated: "2024-12-12"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Managing Logpush jobs
{: #logpush}

The IBM Log Analysis service is deprecated and will no longer be supported as of 30 March 2025. You can migrate jobs to IBM Cloud Logs or Cloud Object Storage.
{: deprecated}

{{site.data.keyword.cis_full}} Enterprise-level plans have access to detailed logs of HTTP and Range requests, and firewall events for their domains. These logs are helpful for debugging and analytics, especially when combined with other data sources, such as ingress or application server logs at the origin.
{: shortdesc}

The data from Logpush is the same as that from [Logpull](/docs/cis?topic=cis-logpull#logpull). However, unlike Logpull, which allows you to download request logs, Logpush provides the option to push the request logs to IBM Cloud Logs or a Cloud Object Storage bucket. 

You must [enable log retention](/docs/cis?topic=cis-logpull#log-retention) before you use Logpush.
{: note}

Range and firewall event logs are not included in HTTP/HTTPS logs and require separate jobs. These jobs can be sent to the same destination, but when using Cloud Object Storage, a different path must be used.

Logpush uses HTTPS endpoints for {{site.data.keyword.cos_full_notm}}, so the log data is encrypted while in motion.

## Creating a Logpush job with the API
{: #logpush-setup-api}
{: api}

Use the [Create a Logpush job](/apidocs/cis#create-logpush-job-v2) API to create a Logpush job when using IBM Cloud Logs or Cloud Object Storage.

### Creating a Logpush job with the API using IBM Cloud Logs
{: #logpush-setup-cloud-logs-api}
{: api}

To create a Logpush job with IBM Cloud Logs, follow these steps: 

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `--crn`
   :   The full url-encoded CRN of the service instance.

   `--zone_id`
  :   The domain ID.

   `--request body`
   :   Information to create the Logpush job body (`logpush_job_ibmcl_req`).  

      `ibmcl`: Information to identify the IBM Cloud Log instance where the data is pushed. Fields within the `ibmcl` object are as follows:

       * `instance_id`- ID of the Cloud Logs instance. 
       * `region`- Region of the Cloud Logs instance (for example, `us-south`).
       * `api_key`- An API key for the account where the Cloud Logs instance is set up is required. You can use either a user API key or a service ID API key. This key is used to generate a bearer token for the Logpush job. If the API key has an expiration date, it can be rotated by using the [Update a Logpush job](/apidocs/cis#update-logpush-job-v2) API. During the rotation process, the previous key remains active as a backup for one hour.
         
       You must grant IAM **Sender** permissions to the API key to request authorization to send logs to an IBM Cloud Logs instance.
       {: important}

      `name`: The name of the Logpush job.
      `enabled`: Whether the job is enabled. One of `true`, `false`.
      `logpull_options`: The configuration string. For example, `timestamps=rfc3339&timestamps=rfc3339`.
      `dataset`: The dataset that is pulled. One of `http_requests`, `range_events`, `firewall_events`.
      `frequency`: The frequency at which CIS sends batches of logs to your destination. One of `high`, `low`.

1. When all variables are initiated, create the Logpush job:

      ```sh
         {
         "ibmcl": { 
             "instance_id": "f8k3309c-585c-4a42-955d-76239cccf8k3", 
             "region": "us-south",
        	 	 "api_key": "f8k3NQI22dPwNVCcmS62YFL1tm9vaehY6C9jxdtnf8k3"
         },
         {
         "dataset": "firewall_events",
         "enabled": false,
         "name": "CIS-Firewall",
         "frequency": "low",
         "logpull_options": "fields=RayID,ZoneID&timestamps=rfc3339",
         "ownership_challenge": "xxxxxxx"
         }
      ```
      {: codeblock} 

### Creating a Logpush job with Cloud Object Storage API
{: #logpush-setup-cos-api}
{: api}

To create a Logpush job with Cloud Object Storage, follow these steps:

Before you create a Logpush job, you must have an {{site.data.keyword.cos_full_notm}} instance with a bucket that has **Object Writer** access that is granted to {{site.data.keyword.cloud}} account `cislogp@us.ibm.com`. This enables {{site.data.keyword.cis_short_notm}} to write request logs into the Cloud Object Storage bucket.
{: important}

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `--crn`
   :   The full url-encoded CRN of the service instance.

   `--zone_id`
  :   The domain ID.

   `--request body`
   :   Information to create the Logpush job body (`logpush_job_cos_req`).  

      `cos`- Information to identify the Cloud Object Storage bucket where the data is pushed.
      `name`- The name of the Logpush job.
      `enabled`- Whether the job is enabled. One of `true`, `false`.
      `logpull_options`- The configuration string. For example, `timestamps=rfc3339&timestamps=rfc3339`.
      `dataset`- The dataset that is pulled. One of `http_requests`, `range_events`, `firewall_events`.
      `frequency`- The frequency at which CIS sends batches of logs to your destination. One of `high`, `low`. 

1. When all variables are initiated, create the Logpush job:

      ```sh
         {
         "cos": {
             "bucket_name": "example_bucket",
             "path": "temp/",
             "id": "cos_instance_id",
             "region": "us-east"
         },
         {
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

[Managing user API keys]([/docs/account?topic=account-userapikey&interface=api)
