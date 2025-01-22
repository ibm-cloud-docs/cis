---

copyright:
  years: 2018, 2025
lastupdated: "2025-01-22"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Managing Logpush jobs
{: #logpush}

The IBM Log Analysis (LogDNA) service is deprecated and will no longer be supported as of 30 March 2025. You can migrate jobs to IBM Cloud Logs, IBM Cloud Object Storage, and Splunk.
{: deprecated}

{{site.data.keyword.cis_full}} Enterprise-level plans have access to detailed logs of HTTP, DNS, and Range requests, and firewall events for their domains. These logs are helpful for debugging and analytics, especially when combined with other data sources, such as ingress or application server logs at the origin.
{: shortdesc}

The data from Logpush is the same as that from [Logpull](/docs/cis?topic=cis-logpull#logpull). However, unlike Logpull, which allows you to download request logs, Logpush provides the option to push the request logs to IBM Cloud Logs or an IBM Cloud Object Storage bucket. 

You must [enable log retention](/docs/cis?topic=cis-logpull#log-retention) before you use Logpush.
{: note}

Range and firewall event logs are not included in HTTP/HTTPS logs and require separate jobs. These jobs can be sent to the same destination, but when using Cloud Object Storage, a different path must be used. 

Logpush uses publicly accessible HTTPS endpoints for {{site.data.keyword.cos_full_notm}}, so the log data is encrypted while in motion. 

## Creating a Logpush job in the UI
{: #logpush-setup-ui}
{: ui}

Currently, the {{site.data.keyword.cis_short_notm}} UI supports the following destinations: IBM Cloud Logs, IBM Cloud Object Storage, IBM Log Analysis, and Splunk. 
{: note}
 
To create a Logpush job in the UI, follow these steps:

1. Select the service: 
   1. Choose the services from the available options.
   1. Select the dataset type.
   1. Enter a description and name.
  
1. Configure your destination: 

   Choose the fields for your destination:

   * IBM Cloud Logs: Enter the IBM Cloud Logs instance ID, instance region, and API key (managed by user).

      For an IBM Cloud Logs service, the user or the service ID must be granted the **Sender** IAM role.
      {: important}

   * IBM Cloud Object Storage: Enter the Cloud Object Storage instance, bucket information (name and region), bucket path (_Optional_). Then, orgalize logs into daily folders (_Optional_).  

      Destination values for IBM Cloud Object Storage must be unique. It is recommended to use a bucket path to avoid conflicts.

   * IBM Log Analysis: Enter LogDNA instance information (ID and region) and the ingestion key.
   * Splunk: Enter the Splunk endpoint, channel ID, and authentication token. You can opt to use insecure verification; however, this is not recommended. 

  1. For Cloud Object Storage jobs only, verify ownership. To do so, download the object that you received in your bucket, and paste the token in the Ownership token text area. Then, click **Next**.

      You can resend the file from the Troubleshooting section, or return to the previous step if the bucket path is incorrect.

1. Select the log fields that you want to include in the log push:
   1. Verify that the Logpush details are correct.
   1. Select the Logpush settings from the Timestamp and Frequency menus.
   1. Choose whether to enable the Logpush job by using the **Enable** switch.
   1. Select the log fields to include in the Logpush job.
   1. Click **Create service**. 

## Creating a Logpush job from the CLI
{: #logpush-setup-cli}
{: cli}
 
To create a Logpush job from the CLI, follow these steps:

IBM Cloud Object Storage only: Before you create a Logpush job, you must have an {{site.data.keyword.cos_full_notm}} instance with a bucket that has **Object Writer** access that is granted to {{site.data.keyword.cloud}} account `cislogp@us.ibm.com`. This enables {{site.data.keyword.cis_short_notm}} to write request logs into the {{site.data.keyword.cos_short}} bucket.
{: important}

Syntax:

```sh
ibmcloud cis logpush-job-create DNS_DOMAIN_ID --destination DESTINATION_URL --name JOB_NAME [--enable true|false] [--fields FIELD1,FIELD2,FIELD3|all] [--timestamps FORMAT] [--dataset DATASET] [--frequency FREQUENCY] [--cve-2021-44228 true|false] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

For example, to create a Logpush job for a specific domain and enable the job, run the following command:

```sh
ibmcloud cis logpush-job-create DNS_DOMAIN_ID --destination BUCKET_PATH --name JOB_NAME --fields all --enable true
```
{: pre}

Where:

`--destination`
:   Specifies the path to the destination: IBM Cloud Logs, IBM Cloud Object Storage, Log Analysis (logDNS), and a general path.

   * Syntax for a LogDNA path: `https://{LOGS_REGION_URL}?hostname={DOMAIN}&apikey={LOGDNA_INGRESS_KEY}`

   Example: `https://logs.eu-de.logging.cloud.ibm.com/logs/ingest?hostname=testv2_logpush&apikey=xxxxxx`
                                
   * Syntax for an IBM Cloud Object Storage path: `cos://<BUCKET_OBJECT_PATH>?region=<REGION>&instance-id=<IBM_ClOUD_OBJECT_STORAGE_INSTANCE_ID>`

   Example: `cos://cis-test-bucket/logs?region=us&instance-id=f75e6d90-4212-4026-851c-d572071146cd`

   * Syntax for an IBM Cloud Log path: `ibmcl://<INSTANCE_ID>.ingress.<REGION>.logs.cloud.ibm.com/logs/v1/singles?ibm_api_key=<IBM_API_KEY>`
   
   Example: `ibmcl://604a309c-585c-4a42-955d-76239ccc1905.ingress.us-south.logs.cloud.ibm.com/logs/v1/singles?ibm_api_key=zxzeNQI22dPwxxxxxxxx9jxdtn1EVK`

   * Syntax for a general path: `https://<HOSTNAME>?header_Authorization=Basic%20REDACTED&tags=host:<DOMAIN_NAME>,dataset:<LOGPUSH_DATASET>`

   Example: `https://logs.example.com?header_Authorization=a64Vxxxxx5Aq` 

`--name`
:   Specifies the Logpush job name.

`--enable`
:   Is the flag to enable or disable the Logpush job. Valid values are `true` or `false` (default).
  
`--fields`
:   Specifies the list of log fields to be included in log files. Use commas to separate multiple fields.

   Use this command `ibmcloud cis logpull DNS_DOMAIN_ID --available-fields` to get a comprehensive list of available log fields, or use `all` to include all available fields in the log files.
 
 `--timestamps`
:   Sets the format in which response timestamps are returned. Valid values are `unix`, `unixnano`, and `rfc3339` (default).

 `--dataset`
:   Is the category of logs that you want to receive. Valid values are `range_events`, `http_requests` (default), `firewall_events`, `dns_logs`. You cannot change this value after the job is created.

 `--frequency`
:   The frequency at which CIS sends batches of logs to your destination. Setting frequency to high sends your logs in larger quantities of smaller files. Setting frequency to low sends logs in smaller quantities of larger files. Valid values are `high` or `low`.

 `-i` or `--instance`
:   Is the instance name or ID. If not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

 `--output`
 :   Specify the output format, only JSON is supported.

A domain can have only one Logpush job. Use the command line to interactively address the {{site.data.keyword.cos_short}} bucket ownership challenge. When a challenge token is written to a file in the given {{site.data.keyword.cos_short}} bucket, you must:

* Download the file from your {{site.data.keyword.cos_short}} bucket and open it.
* Copy and paste the challenge token in the command prompt to address the ownership challenge.

A Logpush job is created successfully after {{site.data.keyword.cis_short_notm}} validates the ownership challenge. The Logpush job pushes request logs to your {{site.data.keyword.cos_short}} bucket every 30 seconds or every 100,000 records, whichever comes first. More than one file might be pushed per 30-second period or per 100,000 records.

You can use the token `{DATE}` in the bucket path to make the Logpush job push request logs in daily folders in the bucket path. For example: `cos://mybucket/cislog/{DATE}?region=us-south&instance-id=c84e2a79-ce6d-3c79-a7e4-7e7ab3054cfe`
{: tip} 

### Command examples
{: #logpush-job-create-examples}

* IBM Cloud Logs:

   `ibmcloud cis logpush-job-create 601b728b86e630c744c81740f72570c3 --destination ibmcl://604a309c-585c-4a42-955d-76239ccc1905.ingress.us-south.logs.cloud.ibm.com/logs/v1/singles?ibm_api_key= tUygM_HyAllUXI9iEFUfpzsLOUAbz5jDuZip91BqEW_e --name logpushJobGen --enable true --fields RayID --dataset http_requests --frequency high -i 1a9174b6-0106-417a-844b-c8eb43a72f63`

* IBM Cloud Object Storage:

   `ibmcloud cis logpush-job-create 31984fea73a15b45779fa0df4ef62f9b --destination cos://cis-test-bucket/logs?region=us&instance-id=f75e6d90-4212-4026-851c-d572071146cd --name logpushcreate --enable true --fields all --timestamps rfc3339 --dataset http_requests --frequency low -i cis-demo --output JSON`   

* General:

   `ibmcloud cis logpush-job-create 601b728b86e630c744c81740f72570c3 --destination https://logs.kmschr.com?header_Authorization=a64VuywesDu5Aq" --name logpushJobGen --enable true --fields RayID --dataset http_requests --frequency high -i 1a9174b6-0106-417a-844b-c8eb43a72f63`

## Creating a Logpush job with the API
{: #logpush-setup-api}
{: api}

Use the [Create a Logpush job](/apidocs/cis#create-logpush-job-v2) API to create a Logpush job when using IBM Cloud Logs or IBM Cloud Object Storage.

### Creating a Logpush job to send logs to IBM Cloud Logs
{: #logpush-setup-cloud-logs-api}

To create a Logpush job with IBM Cloud Logs, follow these steps: 

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`
   :   The full url-encoded CRN of the service instance.

   `ZONE_ID`
   :   The domain ID.

   `--request body`
   :   Information to create the Logpush job body (`logpush_job_ibmcl_req`).  

      `ibmcl`: Information to identify the IBM Cloud Log instance where the data is pushed. Fields within the `ibmcl` object are as follows:

       * `instance_id`- ID of the IBM Cloud Logs instance.   
       * `region`- Region of the IBM Cloud Logs instance (for example, `us-south`).
       * `api_key`- An API key for the account where the IBM Cloud Logs instance is set up is required. You can use either a user API key or a service ID API key. This key is used to generate a bearer token for the Logpush job. The API key can be rotated by using the [Update a Logpush job](/apidocs/cis#update-logpush-job-v2) API.
         
       The user or the service id must be granted the **Sender** IAM role on the Cloud Logs Service.
       {: important}

      `name`: The name of the Logpush job.
   
      `enabled`: Whether the job is enabled. One of `true`, `false`.

      `logpull_options`- The configuration string. For example, `fields=RayID,ZoneID&timestamps=rfc3339`.

      `dataset`: The dataset that is pulled. One of `http_requests`, `range_events`, `dns_logs`, `firewall_events`.
   
      `frequency`: The frequency at which CIS sends batches of logs to your destination. One of `high`, `low`.

1. When all variables are initiated, create the Logpush job:

```sh
curl -X POST https://api.cis.cloud.ibm.com/v2/$CRN/zones/$ZONE_ID/logpush/jobs \
--header "Content-Type: application/json" \
--header "X-Auth-User-Token: Bearer $IAM_TOKEN" \
--data '{
   "ibmcl": { 
         "instance_id": "f8k3309c-585c-4a42-955d-76239cccf8k3", 
         "region": "us-south",
         "api_key": "f8k3NQI22dPwNVCcmS62YFL1tm9vaehY6C9jxdtnf8k3"
   },
   "dataset": "http_requests",
   "enabled": true,
   "logpull_options": "fields=RayID,ZoneID&timestamps=rfc3339",
   "name": "CIS-Edge-Requests",
   "frequency": "low"
}'
```
{: pre}

### Creating a Logpush job to send logs to Cloud Object Storage
{: #logpush-setup-cos-api}

To create a Logpush job with Cloud Object Storage, follow these steps:

Before you create a Logpush job, you must have an {{site.data.keyword.cos_full_notm}} instance with a bucket that has **Object Writer** access that is granted to {{site.data.keyword.cloud}} account `cislogp@us.ibm.com`. This enables {{site.data.keyword.cis_short_notm}} to write request logs into the Cloud Object Storage bucket.
{: important}

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`
   :   The full url-encoded CRN of the service instance.

   `ZONE_ID`
   :   The domain ID.

   `--request body`
   :   Information to create the Logpush job body (`logpush_job_cos_req`).  

      `cos`- Information to identify the Cloud Object Storage bucket where the data is pushed.
   
      `name`- The name of the Logpush job.
   
      `enabled`- Whether the job is enabled. One of `true`, `false`.
   
      `logpull_options`- The configuration string. For example, `fields=RayID,ZoneID&timestamps=rfc3339`.
   
      `dataset`- The dataset that is pulled. One of `http_requests`, `range_events`, `firewall_events`.
   
      `frequency`- The frequency at which CIS sends batches of logs to your destination. One of `high`, `low`. 

1. When all variables are initiated, create the Logpush job:

```sh
curl -X POST https://api.cis.cloud.ibm.com/v2/$CRN/zones/$ZONE_ID/logpush/jobs \
--header "Content-Type: application/json" \
--header "X-Auth-User-Token: Bearer $IAM_TOKEN" \
--data '{
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
}'
```
{: pre}


## Related link
{: #related-link-logpush}
{: api}

[Managing user API keys](/docs/account?topic=account-userapikey&interface=api)
