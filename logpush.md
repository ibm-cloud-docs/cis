---

copyright:
  years: 2018, 2025
lastupdated: "2025-07-22"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Managing Logpush jobs
{: #logpush}

{{site.data.keyword.cis_full}} Enterprise-level plans have access to detailed logs of HTTP, DNS, and Range requests, as well as firewall events for their domains. These logs are helpful for debugging and analytics, especially when combined with other data sources, such as ingress or application server logs at the origin.
{: shortdesc}

## Before you begin
{: #before-you-begin-logpush-ui}

Before you create a Logpush job by using the UI, review the following information and satisfy any prerequisites:

* Currently, the {{site.data.keyword.cis_short_notm}} UI supports the following destinations:{: ui}
   - IBM Cloud Logs
   - Cloud Object Storage
   - Splunk
* Make sure to [enable log retention](/docs/cis?topic=cis-logpull#log-retention) before you use Logpush.
* Accepting the Logpush user invitation (`cislogp@us.ibm.com`) is a manual process completed by an authorized CIS team. The status in the console updates after the invitation has been accepted. Until then, the status remains `Pending`.
* If your destination is not explicitly supported by CIS, it might still be accessible by Logpush using a Custom HTTP destination. This includes your own custom HTTP log servers.

   To avoid errors, make sure that the destination can accept a gzipped file upload named `test.txt.gz`, containing the compressed content `{"content":"tests"}`.
   {: important}

* For Cloud Object Storage only:
   * You must have a Cloud Object Storage instance with a bucket that grants **Object Writer** access to the IBM Cloud account `cislogp@us.ibm.com`. This permission enables CIS to write request logs to the Object Storage bucket.{: cli}{: api}
   * Logpush uses publicly accessible HTTPS endpoints for Cloud Object Storage, ensuring encryption of log data in transit.
   * DNS, Range, and firewall event logs are not included in HTTP/HTTPS logs and require separate jobs. These jobs can use the same destination but must specify different paths with using Cloud Object Storage.  
   * After creating a Logpush job with Cloud Object Storage, you must verify ownership. This process is described in the next steps.

* For Splunk only: When you send logs to Splunk, CIS checks the IP address and port for accessibility and validates the certificate of the HTTP Receiver. If all parameters are valid, the Logpush job is created and begins sending events to the HTTP Event Collector (Splunk).

## Creating a Logpush job in the console
{: #logpush-setup-ui}
{: ui}

To create a Logpush job in the console, follow these steps:

1. Select **Account** > **Logs**, then click **Create**.
1. Select service:
   1. Select the service type you want from the available options.
   1. Select the dataset type.
   1. Optional: Enter a description and name.
   1. Select **Next**.
1. Configure destination:

   IBM Cloud Logs
   :   Enter the IBM Cloud Logs instance ID, instance region, and API key (user managed).

       An API key for the account where the IBM Cloud Logs instance is set up is required. You can use either a user API key or a service ID API key. This key is used to generate a bearer token for the Logpush job. The API key can be rotated by using the [Update a Logpush job API](/apidocs/cis#update-logpush-job-v2).

       For an IBM Cloud Logs service, the user or service ID must be granted the **Sender** IAM role.
       {: important}

   Cloud Object Storage
   :   Enter the Cloud Object Storage instance, bucket information (name and region), and bucket path (optional). Then, organize logs into daily folders (optional).

      Destination values for Cloud Object Storage must be unique. It is recommended to use a bucket path to avoid conflicts.

   Splunk
   :   Enter the Splunk endpoint, channel ID, and authentication token.

      You can choose to use insecure verification; however, this is not recommended.

   Custom HTTP Destination
   :   Enter your HTTP endpoint.

       Make sure the endpoint is properly URL-encoded and any necessary request headers are added as URL parameters formatted as "header_*" (e.g. `header_Authorization`).
       {: important}

1. For Cloud Object Storage jobs only, verify ownership. To do so, download the object that you received in your bucket and paste the token in the Ownership token text area. Then, click **Next**.

   You can resend the file from the Troubleshooting section, or return to the previous step if the bucket path is incorrect.

1. Select log fields:
   1. Verify that the Logpush details are correct.
   1. Select the Logpush settings from the Timestamp format and Frequency menus.
   1. Choose whether to enable the Logpush job by toggling the **Enablement** switch to **On**.
   1. Select the log fields to include in the Logpush job.

      You can use the switches to **Select all fields** or **Expand all fields**. You can also revert back to default settings.
      {: tip}

   1. Click **Done** to create your Logpush job.

## Creating a Logpush job from the CLI
{: #logpush-setup-cli}
{: cli}

You can use the [`ibmcloud cis logpush-job-create`](/docs/cis?topic=cis-cis-cli&interface=api#logpush-job-create) CLI to create a Logpush job.

To create a Logpush job for a specific domain and enable the job, run the following command:

```sh
ibmcloud cis logpush-job-create DNS_DOMAIN_ID --destination PATH --name JOB_NAME --fields all --enable true
```
{: pre}

Where:

`-destination`: Specifies the path to the destination. Paths for supported destinations are as follows:

   | IBM Cloud Logs |
   |---------------------|
   | `ibmcl://<INSTANCE_ID>.ingress.<REGION>.logs.cloud.ibm.com/logs/v1/singles?ibm_api_key=<IBM_API_KEY>` \n \n For example: \n `ibmcl://604a309c-585c-4a42-955d-76239ccc1905.ingress.us-south.logs.cloud.ibm.com/logs/v1/singles?ibm_api_key=zxzeNQI22dPwxxxxxxxx9jxdtn1EVK` \n \n An API key for the account where the IBM Cloud Logs instance is set up is required. You can use either a user API key or a service ID API key. This key is used to generate a bearer token for the Logpush job. The API key can be rotated by using the [Update a Logpush job API](/apidocs/cis#update-logpush-job-v2). \n \n **Important:** The user or the service ID must be granted the Sender IAM role on the IBM Cloud Logs service. |
   {: caption="IBM Cloud Logs path" caption-side="bottom"}
   {: #cli-table-11}
   {: tab-title="IBM Cloud Logs"}
   {: tab-group="pla"}
   {: class="simple-tab-table"}
   {: row-headers}

   | Cloud Object Storage |
   |---------------------|
   | `cos://<BUCKET_OBJECT_PATH>?region=<REGION>&instance-id=<IBM_ClOUD_OBJECT_STORAGE_INSTANCE_ID>` \n \n For example: \n `cos://cis-test-bucket/logs?region=us&instance-id=f75e6d90-4212-4026-851c-d572071146cd` |
   {: caption="Cloud Object Storage path" caption-side="bottom"}
   {: #cli-table-22}
   {: tab-title="Cloud Object Storage"}
   {: tab-group="pla"}
   {: class="simple-tab-table"}
   {: row-headers}

   | Custom HTTP |
   |---------------------|
   | `https://<HOSTNAME>?header_Authorization=Basic%20REDACTED&tags=host:<DOMAIN_NAME>,dataset:<LOGPUSH_DATASET>` \n \n For example: \n `https://logs.example.com?header_Authorization=a64Vxxxxx5Aq` |
   {: caption="Custom HTTP path" caption-side="bottom"}
   {: #cli-table-55}
   {: tab-title="Custom HTTP"}
   {: tab-group="pla"}
   {: class="simple-tab-table"}
   {: row-headers}

`--name`: Specifies the Logpush job name.

`--fields`: Specifies the list of log fields to be included in log files. Use commas to separate multiple fields. Use the command `ibmcloud cis logpush-available-fields DNS_DOMAIN_ID --dataset DATASET` to get a comprehensive list of available log fields, or use `all` to include all available fields in the log files.

`--enable`: Is the flag to enable or disable the Logpush job. Valid values are `true` or `false` (default).

### Cloud Object Storage: Verifying ownership
{: #next-step-cloud-object-storage}

After creating a Logpush job to send logs to Cloud Object Storage, you must validate ownership.

When a challenge token is written to a file in the specified Cloud Object Storage bucket, follow these steps:

* Download the file from your Cloud Object Storage bucket and open it.
* Copy the challenge token from the file and paste it into the command prompt to resolve the ownership challenge.

After {{site.data.keyword.cis_short_notm}} validates the ownership challenge, the Logpush job is created successfully. The job will then push request logs to your Cloud Object Storage bucket every 30 seconds or once 100,000 records are reached, whichever comes first. Note that multiple files might be pushed during a 30-second period or per 100,000 records.

You can also use the `{DATE}` token in the bucket path to organize Logpush logs into daily folders. For example: `cos://mybucket/cislog/{DATE}?region=us-south&instance-id=c84e2a79-ce6d-3c79-a7e4-7e7ab3054cfe`
{: tip}

### Command examples
{: #logpush-job-create-examples}

CLI examples for the supported destinations:

   IBM Cloud Logs
   :   Example

       ```sh
       ibmcloud cis logpush-job-create 601b728b86e630c744c81740f72570c3 --destination "ibmcl://604a309c-585c-4a42-955d-76239ccc1905.ingress.us-south.logs.cloud.ibm.com/logs/v1/singles?ibm_api_key=xxxxxxxx" --name logpushJobGen --enable true --fields RayID --dataset http_requests --frequency high -i 1a9174b6-0106-417a-844b-c8eb43a72f63
       ```
       {: pre}

   Cloud Object Storage
   :   Example

       ```sh
       ibmcloud cis logpush-job-create 31984fea73a15b45779fa0df4ef62f9b --destination cos://cis-test-bucket/logs?region=us&instance-id=f75e6d90-4212-4026-851c-d572071146cd --name logpushcreate --enable true --fields all --timestamps rfc3339 --dataset http_requests --frequency low -i cis-demo --output JSON
       ```
       {: pre}
   

   Custom HTTP
   :   Example

       ```sh
       ibmcloud cis logpush-job-create 601b728b86e630c744c81740f72570c3 --destination https://logs.example.com?header_Authorization=a64VuywesDu5Aq" --name logpushJobGen --enable true --fields RayID --dataset http_requests --frequency high -i 1a9174b6-0106-417a-844b-c8eb43a72f63
       ```
       {: pre}

## Creating a Logpush job with the API
{: #logpush-create-api}
{: api}

You can use the [Create a Logpush job](/apidocs/cis#create-logpush-job-v2) API to create a Logpush job when using IBM Cloud Logs, Cloud Object Storage, or Splunk.

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

### Creating a Logpush job to send logs to your destination
{: #logpush-destination}

To create a Logpush job to your destination (IBM Cloud Logs, Cloud Object Storage, or Splunk), follow these steps:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded Cloud Resource Name (CRN) of the service instance.

   `ZONE_ID`: The domain ID.

   `--request body`: Information to create the Logpush job body (`logpush_job_DESTINATION_req`) where `DESTINATION` is one of the following values:

   | IBM Cloud Logs |
   |---------------------|
   | `ibmcl`: Information to identify the IBM Cloud Logs instance where the data is pushed. Fields within the `ibmcl` object are: \n * `instance_id`: ID of the IBM Cloud Logs instance. \n * `region`: Region of the IBM Cloud Logs instance (for example, `us-south`). \n * `api_key`: An API key for the account where the IBM Cloud Logs instance is set up is required. You can use either a user API key or a service ID API key. This key is used to generate a bearer token for the Logpush job. The API key can be rotated by using the [Update a Logpush job](/apidocs/cis#update-logpush-job-v2) API. \n \n **Important**: The user or the service ID must be granted the **Sender** IAM role on the IBM Cloud Logs service. \n \n `ibmcl_names`: Optional field to customize the application and subsystem names used in IBM Cloud Logs. Fields within the `ibmcl_names` object are: \n * `application_name`: Custom application name for the job. \n * `subsystem_name`: Custom subsystem name for the job. |
   {: caption="IBM Cloud Logs destination" caption-side="bottom"}
   {: #pl-table-1}
   {: tab-title="IBM Cloud Logs"}
   {: tab-group="pl"}
   {: class="simple-tab-table"}
   {: row-headers}

   | Cloud Object Storage |
   |---------------------|
   | `cos`: Information to identify the Cloud Object Storage bucket where the data is pushed. Fields within the `cos` object are: \n * `bucket_name`: Name of your COS bucket where logs are sent (example: `cos-bucket001`). \n * `region`: Region of the Cloud Object Storage instance (for example, `us-south`). \n * `id`: ID of the COS instance. |
   {: caption="Cloud Object Storage destination" caption-side="bottom"}
   {: #pl-table-2}
   {: tab-title="Cloud Object Storage"}
   {: tab-group="pl"}
   {: class="simple-tab-table"}
   {: row-headers}

   | Splunk |
   |---------------------|
   | `splunk`: Information to identify the Splunk HTTP Event Collector (HEC) where the data is pushed. Fields within the `splunk` object are: \n * `endpoint_url`: URL of the Splunk HEC. \n * `channel_id`: A random GUID to uniquely identify the log push. \n * `skip_verify`: Boolean flag to skip validation of the HTTP Event Collector certificate. Only set this to `true` when the HEC is using a self-signed certificate. \n * `source_type`: The Splunk source type (for example: `cloudflare:json`). \n * `auth_token`: The Splunk authorization token. |
   {: caption="Splunk destination" caption-side="bottom"}
   {: #pl-table-4}
   {: tab-title="Splunk"}
   {: tab-group="pl"}
   {: class="simple-tab-table"}
   {: row-headers}

   | Custom HTTP |
   |---------------------|
   | `destination_conf`: Information to configure the Custom HTTP destination where the data is pushed. Headers can be specified to be used by Logpush with query parameters prefixed by `header_` (for example: `header_Authorization=XXXX`). |
   {: caption="Custom HTTP destination" caption-side="bottom"}
   {: #pl-table-5}
   {: tab-title="Custom HTTP"}
   {: tab-group="pl"}
   {: class="simple-tab-table"}
   {: row-headers}

   `name`: The name of the Logpush job.

   `enabled`: Whether the job is enabled. Either `true` or `false`.

   `logpull_options`: The configuration string. For example, `fields=RayID,ZoneID&timestamps=rfc3339`.

   `dataset`: The dataset that is pulled. One of `http_requests`, `dns_logs`, `range_events`, `firewall_events`.

   `frequency`: The frequency at which CIS sends batches of logs to your destination. Either `high` or `low`.

1. When all variables are initiated, create the Logpush job:

   **IBM Cloud Logs**

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
      "ibmcl_names": {
         "application_name": "cis-edge-logs",
         "subsystem_name": "stage-firewall-logs"
      }
      "dataset": "http_requests",
      "enabled": true,
      "logpull_options": "fields=RayID,ZoneID&timestamps=rfc3339",
      "name": "CIS-Edge-Requests",
      "frequency": "low"
   }'
   ```
   {: pre}

   **Cloud Object Storage**

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

   **Splunk**

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

   **Custom HTTP**

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
