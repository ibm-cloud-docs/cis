---

copyright:
  years: 2018, 2025
lastupdated: "2025-01-23"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Managing Logpush jobs
{: #logpush}

The IBM Log Analysis service is deprecated and will no longer be supported as of 30 March 2025. You can migrate jobs to IBM Cloud Logs, Cloud Object Storage, IBM QRadar, and Splunk.
{: deprecated}

{{site.data.keyword.cis_full}} Enterprise-level plans have access to detailed logs of HTTP, DNS, and Range requests, and firewall events for their domains. These logs are helpful for debugging and analytics, especially when combined with other data sources, such as ingress or application server logs at the origin.
{: shortdesc}

## Before you begin
{: #before-you-begin-logpush}

Before you create a Logpush job, review the following information and satisfy any prerequisites:

* [Enable log retention](/docs/cis?topic=cis-logpull#log-retention) before you use Logpush.
* Currently, the {{site.data.keyword.cis_short_notm}} UI supports the following destinations: IBM Cloud Logs, Cloud Object Storage, IBM QRadar, Splunk, and IBM Log Analysis (deprecated). 
* The data from Logpush is the same as that from [Logpull](/docs/cis?topic=cis-logpull#logpull). However, unlike Logpull, which allows you to download request logs, Logpush enables you to push the request logs to IBM Cloud Logs or an Cloud Object Storage bucket.
* Range and firewall event logs are not included in HTTP/HTTPS logs and require separate jobs. These jobs can be sent to the same destination, but when using Cloud Object Storage, you'll need to specify a different path.
* Logpush uses publicly accessible HTTPS endpoints for {{site.data.keyword.cos_full_notm}}, ensuring the log data is encrypted while in motion.
* When using Cloud Object Storage, you must verify ownership after creating a Logpush job. This task is described in the following procedure.

## Creating a Logpush job in the UI
{: #logpush-setup-ui}
{: ui}

To create a Logpush job in the UI, follow these steps:

1. Select **Account** > **Logs**, then click **Create**. 

1. Select service: 
   1. Select the wanted service type from the available options.
   1. Select the dataset type.
   1. Enter a description and name (_optional_), then select **Next**.
  
1. Configure destination: 

   IBM Cloud Logs
   :   Enter the IBM Cloud Logs instance ID, instance region, and API key (managed by user).  

       For an IBM Cloud Logs service, the user or the service ID must be granted the **Sender** IAM role.
       {: important}

   Cloud Object Storage
   :   Enter the Cloud Object Storage instance, bucket information (name and region), bucket path (_optional_). Then, organize logs into daily folders (_optional_).  

       Destination values for Cloud Object Storage must be unique. It is recommended to use a bucket path to avoid conflicts.

   IBM QRader
   :   Enter the QRader URL, then select a log source port. 

   Splunk
   :   Enter the Splunk endpoint, channel ID, and authentication token. You can opt to use insecure verification; however, this is not recommended. 

   IBM Log Analysis (deprecated)
   :   Enter LogDNA instance information (ID and region) and the ingestion key.

    Custom HTTP Destination
   :   Enter your HTTP endpoint.

       To avoid errors, make sure that the file uploaded to validate the destination accepts a gzipped test.txt.gz file with content as {"content":"test"} compressed.
       {: note}
   
1. For Cloud Object Storage jobs only, verify ownership. To do so, download the object that you received in your bucket, and paste the token in the Ownership token text area. Then, click **Next**.

   You can resend the file from the Troubleshooting section, or return to the previous step if the bucket path is incorrect.

1. Select log fields: 
   1. Verify that the Logpush details are correct.
   1. Select the Logpush settings from the Timestamp format and Frequency menus.
   1. Choose whether to enable the Logpush job by switching the **Enablment** switch to **On**.
   1. Select the log fields to include in the Logpush job.

      Use the switches to **Select all fields** or **Expand all fields**.  You can also revert back to default settings.
      {: tip}
   1. Click **Done** to create your Logpush job.

## Creating a Logpush job from the CLI
{: #logpush-setup-cli}
{: cli}
 
To create a Logpush job from the CLI, follow these steps:

Before you create a Logpush job using Cloud Object Storage, you must have an {{site.data.keyword.cos_full_notm}} instance with a bucket that has **Object Writer** access that is granted to {{site.data.keyword.cloud}} account `cislogp@us.ibm.com`. This enables {{site.data.keyword.cis_short_notm}} to write request logs into the {{site.data.keyword.cos_short}} bucket.
{: important}

To create a Logpush job for a specific domain and enable the job, run the following command:

```sh
ibmcloud cis logpush-job-create DNS_DOMAIN_ID --destination PATH --name JOB_NAME --fields all --enable true
```
{: pre}

Where:

`--destination`: Specifies the path to the destination. Paths for supported destinations are as follows:

   * IBM Cloud Logs

      ```sh
      ibmcl://<INSTANCE_ID>.ingress.<REGION>.logs.cloud.ibm.com/logs/v1/singles?ibm_api_key=<IBM_API_KEY>
      ```
      {: pre}
   
      For example:
      
      ```sh
      ibmcl://604a309c-585c-4a42-955d-76239ccc1905.ingress.us-south.logs.cloud.ibm.com/logs/v1/singles?ibm_api_key=zxzeNQI22dPwxxxxxxxx9jxdtn1EVK
      ```
      {: pre}
      
`--name`: Specifies the Logpush job name.

`--fields`: Specifies the list of log fields to be included in log files. Use commas to separate multiple fields.

   Use this command `ibmcloud cis logpull DNS_DOMAIN_ID --available-fields` to get a comprehensive list of available log fields, or use `all` to include all available fields in the log files.

`--enable`: Is the flag to enable or disable the Logpush job. Valid values are `true` or `false` (default).

For additional command options, see [`ibmcloud cis logpush-job-create`](/docs/cis?topic=cis-cis-cli&interface=api#logpush-job-create) in the CIS command reference.
{: note}

### Cloud Object Storage: Verifying ownership
{: #next-step-cloud-object-storage}

After creating a Logpush job to send logs to Cloud Object Storage, you must validate ownership. To do so, interactively address the {{site.data.keyword.cos_short}} bucket ownership challenge as follows:

```sh
COMMAND NEEDED
```
{: pre} 

When a challenge token is written to a file in the specified {{site.data.keyword.cos_short}} bucket, follow these steps:

* Download the file from your {{site.data.keyword.cos_short}} bucket and open it.
* Copy the challenge token from the file and paste it into the command prompt to resolve the ownership challenge.

After the ownership challenge is validated by {{site.data.keyword.cis_short_notm}}, the Logpush job is created successfully. The job will then push request logs to your {{site.data.keyword.cos_short}} bucket every 30 seconds or once 100,000 records are reached, whichever comes first. Note that multiple files might be pushed during a 30-second period or per 100,000 records.

You can also use the `{DATE} `token in the bucket path to organize Logpush logs into daily folders. For example: `cos://mybucket/cislog/{DATE}?region=us-south&instance-id=c84e2a79-ce6d-3c79-a7e4-7e7ab3054cfe`
{: tip}

A domain can have only one Logpush job. (WHERE DOES THIS BELONG?) 
  
### Command examples
{: #logpush-job-create-examples}

* IBM Cloud Logs

   ```sh
   ibmcloud cis logpush-job-create 601b728b86e630c744c81740f72570c3 --destination ibmcl://604a309c-585c-4a42-955d-76239ccc1905.ingress.us-south.logs.cloud.ibm.com/logs/v1/singles?ibm_api_key= tUygM_HyAllUXI9iEFUfpzsLOUAbz5jDuZip91BqEW_e --name logpushJobGen --enable true --fields RayID --dataset http_requests --frequency high -i 1a9174b6-0106-417a-844b-c8eb43a72f63
   ```
   {: pre}

* Cloud Object Storage

   ```sh
  ibmcloud cis logpush-job-create 31984fea73a15b45779fa0df4ef62f9b --destination cos://cis-test-bucket/logs?region=us&instance-id=f75e6d90-4212-4026-851c-d572071146cd --name logpushcreate --enable true --fields all --timestamps rfc3339 --dataset http_requests --frequency low -i cis-demo --output JSON
   ```
   {: pre}
  
* IBM QRadar

   ```sh
   NEED EXAMPLE
   ```
   {: pre}

* Splunk

   ```sh
   NEED EXAMPLE
   ```
   {: pre}

* Generic destination

   ```sh
   ibmcloud cis logpush-job-create 601b728b86e630c744c81740f72570c3 --destination https://logs.kmschr.com?header_Authorization=a64VuywesDu5Aq" --name logpushJobGen --enable true --fields RayID --dataset http_requests --frequency high -i 1a9174b6-0106-417a-844b-c8eb43a72f63
   ```
   {: pre}

## Creating a Logpush job with the API
{: #logpush-setup-api}
{: api}

Use the [Create a Logpush job](/apidocs/cis#create-logpush-job-v2) API to create a Logpush job when using IBM Cloud Logs or IBM Cloud Object Storage.

### Getting the available log fields for a dataset with the API
{: #logpush-setup-fields-api}

Log fields can be specified in the `logpull_options` of a Logpush Job to customize what is sent to the destination. To get the available log fields for a Logpush dataset, follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded CRN of the service instance.

   `ZONE_ID`: The domain ID.

   `DATASET`: The Logpush dataset being inspected. One of `http_requests`, `range_events`, `dns_logs`, `firewall_events`.

1. When all variables are initiated, create the Logpush job:

   ```sh
   curl -X GET https://api.cis.cloud.ibm.com/v2/$CRN/zones/$ZONE_ID/logpush/datas/$DATASET/fields \
   --header "Content-Type: application/json" \
   --header "X-Auth-User-Token: Bearer $IAM_TOKEN"'
   ```
   {: pre}

### Creating a Logpush job to send logs to IBM Cloud Logs
{: #logpush-setup-cloud-logs-api}

To create a Logpush job with IBM Cloud Logs, follow these steps: 

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded Cloud Resource Name (CRN) of the service instance.

   `ZONE_ID`: The domain ID.

   `--request body`: Information to create the Logpush job body (`logpush_job_ibmcl_req`).  

      `ibmcl`: Information to identify the IBM Cloud Log instance where the data is pushed. Fields within the `ibmcl` object are as follows:

       * `instance_id`: ID of the IBM Cloud Logs instance.   
       * `region`: Region of the IBM Cloud Logs instance (for example, `us-south`).
       * `api_key`: An API key for the account where the IBM Cloud Logs instance is set up is required. You can use either a user API key or a service ID API key. This key is used to generate a bearer token for the Logpush job. The API key can be rotated by using the [Update a Logpush job](/apidocs/cis#update-logpush-job-v2) API.
         
       The user or the service id must be granted the **Sender** IAM role on the Cloud Logs Service.
       {: important}

      `name`: The name of the Logpush job.
   
      `enabled`: Whether the job is enabled. One of `true`, `false`.

      `logpull_options`: The configuration string. For example, `fields=RayID,ZoneID&timestamps=rfc3339`.

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

   `CRN`: The full URL-encoded Cloud Resource Name (CRN) of the service instance.

   `ZONE_ID`: The domain ID.

   `--request body`: Information to create the Logpush job body (`logpush_job_cos_req`).  

      `cos`: Information to identify the Cloud Object Storage bucket where the data is pushed.
   
      `name`: The name of the Logpush job.
   
      `enabled`: Whether the job is enabled. One of `true`, `false`.
   
      `logpull_options`: The configuration string. For example, `fields=RayID,ZoneID&timestamps=rfc3339`.
   
      `dataset`: The dataset that is pulled. One of `http_requests`, `dns_logs`, `range_events`, `firewall_events`.
   
      `frequency`: The frequency at which CIS sends batches of logs to your destination. One of `high`, `low`. 

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

### Creating a Logpush job to send logs to QRadar
{: #enabling-logpush-qradar}

{{site.data.keyword.cis_short_notm}} checks the IP address's accessibility and port, and then validates the certificate of the HTTP Receive log source. If all parameters are valid, then a Logpush is created. The Logpush then begins sending events to the HTTP Receiver log source.

The following example shows how to send Firewall events to QRadar.

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded CRN of the service instance.

   `ZONE_ID`: The domain ID.

   `--request body`: Information to create the Logpush job body (`logpush_job_qradar_req`). 

      `qradar`: Information to identify the QRadar HTTP Receiever where the data is pushed.
   
      `name`: The name of the Logpush job.
   
      `enabled`: Whether the job is enabled. One of `true`, `false`.
   
      `logpull_options`: The configuration string. For example, `fields=RayID,ZoneID&timestamps=rfc3339`.
   
      `dataset`: The dataset that is pulled. One of `http_requests`, `range_events`, `dns_logs`, `firewall_events`.
   
      `frequency`: The frequency at which CIS sends batches of logs to your destination. One of `high`, `low`.

1. When all variables are initiated, create the Logpush job:

   ```sh
   curl -X POST https://api.cis.cloud.ibm.com/v2/$CRN/zones/$ZONE_ID/logpush/jobs \
   --header "Content-Type: application/json" \
   --header "X-Auth-User-Token: Bearer $IAM_TOKEN" \
   --data '{
      "qradar": { 
         "url": "https://example.qradar.ibmcloud.com",
         "port": 8088
      },
      "dataset": "firewall_events",
      "enabled": false,
      "name": "CIS-Firewall-QRadar",
      "frequency": "low",
      "logpull_options": "fields=RayID,CacheResponseBytes,CacheResponseStatus,CacheCacheStatus&timestamps=rfc3339"
   }' 
   ```
   {: pre} 

### Creating a Logpush job to send logs to Splunk
{: #enabling-logpush-splunk}
{{site.data.keyword.cis_short_notm}} checks the IP address's accessibility and port, and then validates the certificate of the HTTP Receive log source. If all parameters are valid, then a Logpush is created. The Logpush then begins sending events to the HTTP Event Collector.

The following example shows how to send HTTP events to Splunk.

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded CRN of the service instance.

   `ZONE_ID`: The domain ID.

   `--request body`: Information to create the Logpush job body (`logpush_job_splunk_req`).  

      `splunk`: Information to identify the Splunk HTTP Event Collector (HEC) where the data is pushed. Fields within the `splunk` object are as follows:

       * `endpoint_url`: URL of the Splunk HEC.
       * `channel_id`: A random GUID to uniquely identify the log push.
       * `skip_verify`: Boolean flag to skip validation of the HTTP Event Collector certificate. Only set this to `true` when the HEC is using a self-signed certificate.
       * `source_type`: The Splunk source type (for example: `cloudflare:json`).
       * `auth_token`: The Splunk authorization token.

      `name`: The name of the Logpush job.

      `enabled`: Whether the job is enabled. One of `true`, `false`.

      `logpull_options`: The configuration string. For example, `fields=RayID,ZoneID&timestamps=rfc3339`.

      `dataset`: The dataset that is pulled. One of `http_requests`, `range_events`, `dns_logs`, `firewall_events`.

      `frequency`: The frequency at which CIS sends batches of logs to your destination. One of `high`, `low`. 

1. When all variables are initiated, create the Logpush job:

   ```sh
   curl -X POST https://api.cis.cloud.ibm.com/v2/$CRN/zones/$ZONE_ID/logpush/jobs \
   --header "Content-Type: application/json" \
   --header "X-Auth-User-Token: Bearer $IAM_TOKEN" \
   --data '{
      "splunk": {
         "endpoint_url": "example.splunkcloud.com:8088/services/collector/raw",
         "channel_id": "def3c136-7a01-4655-b17f-8e25a780ef2c",
         "skip_verify": false,
         "source_type": "cloudflare:json",
         "auth_token": "Splunk fake3585-0f38-4d62-8b43-c4b78584fake"
      },
      "dataset": "http_requests",
      "enabled": true,
      "name": "CIS-Splunk-Logpush",
      "frequency": "high",
      "logpull_options": "fields=RayID,CacheResponseBytes,CacheResponseStatus,CacheCacheStatus&timestamps=rfc3339"
   }'
   ```
   {: pre}

### Creating a Logpush job to send logs to a generic destination
{: #enabling-logpush-generic}

If your destination is not explicitly supported by {{site.data.keyword.cis_short_notm}}, it may still be accessible by Logpush via a generic destination. This includes your own custom HTTP log servers.

Notice: To avoid errors, make sure that the destination can accept a gzipped file upload test.txt.gz with content as `{"content":"tests"}` compressed.
{: important}

The following example shows how to send HTTP events to a custom HTTP log destination.

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded CRN of the service instance.

   `ZONE_ID`: The domain ID.

   `--request body`: Information to create the Logpush job body (`logpush_job_splunk_req`).  

      `destination_conf`: Information to configure the generic destination where the data is pushed. Headers may be specified to be used by Logpush with query parameters prefixed by `header_` (for example: `header_Authorization=XXXX`)

      `name`: The name of the Logpush job.

      `enabled`: Whether the job is enabled. One of `true`, `false`.

      `logpull_options`: The configuration string. For example, `fields=RayID,ZoneID&timestamps=rfc3339`.

      `dataset`: The dataset that is pulled. One of `http_requests`, `range_events`, `dns_logs`, `firewall_events`.

      `frequency`: The frequency at which CIS sends batches of logs to your destination. One of `high`, `low`. 

1. When all variables are initiated, create the Logpush job:

   ```sh
   curl -X POST https://api.cis.cloud.ibm.com/v2/$CRN/zones/$ZONE_ID/logpush/jobs \
   --header "Content-Type: application/json" \
   --header "X-Auth-User-Token: Bearer $IAM_TOKEN" \
   --data '{
      "destination_conf": "https://logs.example.com?header_Authorization=a64VuywesDu5Aq",
      "dataset": "http_requests",
      "enabled": true,
      "name": "CIS-Custom-Logpush",
      "frequency": "high",
      "logpull_options": "fields=RayID,CacheResponseBytes,CacheResponseStatus,CacheCacheStatus&timestamps=rfc3339"
   }'
   ```
   {: pre} 
    
### Related link
{: #related-link-logpush}
{: api}

[Managing user API keys](/docs/account?topic=account-userapikey&interface=api)
