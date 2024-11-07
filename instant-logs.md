---

copyright:
  years: 2024
lastupdated: "2024-11-07"

keywords: instant logs, logs

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Using the Instant Logs feature
{: #instant-logs}

Enterprise accounts can use the Instant Logs feature to access a live stream of the traffic for their domain from the API or CLI. By watching the data in real time, you can investigate an attack, troubleshoot, debug, or test changes that are made to your network. Instant Logs is lightweight and does not require any extra setup.
{: shortdesc}

## Creating Instant Logs from the CLI
{: #instant-logs-cli}
{: cli}

To create an Instant Logs Job from the CLI, send a POST request to the Instant Logs job endpoint with the following parameters:

- **Fields:** List any fields that are available in the HTTP request dataset.
- **Sample:** The sample rate of the records set by the client, for instance `"sample": 1` returns 100% of the records and `"sample": 10` returns 10% of the records.

    Instant Logs has a maximum data rate supported. For high volume domains, we sample server side as indicated in the "sampleInterval" parameter returned in the logs.
    {: note}

- **Filters:** Use filters to drill down into specific events. Filters consist of three parts: key, operator, and value.
    - **Keys:**
        - `ClientASN`
        - `CacheCacheStatus`
        - `ClientCountry`
        - `ClientIP`
        - `ClientRequestHost`
        - `ClientRequestMethod`
        - `ClientRequestPath`
        - `EdgeResponseStatus`
        - `SecurityActions`
        - `SecurityRuleIDs`
    - **Operators:** The following table shows the name and behavior of each operator.

| Name | Operator |
| -- | -- |
| Equals | `eq` |
| Not Equals | `neq` |
| Greater Than | `gt` |
| Greater Than or Equal to | `geq` |
| Less Than | `lt` |
| Less Than or Equal to | `leq` |
| Starts with | `startsWith` |
| Ends with | `endsWith` |
| Contains | `contains` |
| Is in | `In` |
{: caption="Operator names and behaviors" caption-side="bottom"}


## Creating an Instant Logs job
{: #create-instant-logs-job}

Create a session by sending a POST request to the Instant Logs job endpoint with the following parameters:

* **Fields** - List any field available in the [HTTP requests dataset](/docs/cis?topic=cis-log-fields#logpull-available-fields).
* **Sample** - The sample parameter is the sample rate of the records set by the client: `"sample": 1` is 100% of records `"sample":` 10 is 10% and so on.

   Instant Logs has a maximum data rate supported. For high volume domains, we sample server side as indicated in the "sampleInterval" parameter returned in the logs.
   {: note}

* **Filters** - Use filters to drill down into specific events. Filters consist of three parts: key, operator and value.

All supported operators can be found in the Filters page.

Here are three examples of filters:

* Filter when client IP country is not Canada:

   `"filter": "{\"where\":{\"and\":[{\"key\":\"ClientCountry\",\"operator\":\"neq\",\"value\":\"ca\"}]}}"`
   {: pre}

* Filter when the status code returned from CIS is either 200 or 201:

   `"filter": "{\"where\":{\"and\":[{\"key\":\"EdgeResponseStatus\",\"operator\":\"in\",\"value\":\"200,201\"}]}}"`
   {: pre}

*  Filter when the request path contains "/static" and the request hostname is "example.com":

   `"filter": "{\"where\":{\"and\":[{\"key\":\"ClientRequestPath\",\"operator\":\"contains\",\"value\":\"/static\"}, {\"where\":{\"and\":[{\"key\":\"ClientRequestHost\",\"operator\":\"eq\",\"value\":\"example.com\"}]}}"`
   {: pre}

Here is an example request using cURL:

```sh
curl https://api.cloudflare.com/client/v4/zones/{zone_id}/logpush/edge/jobs \
--header "X-Auth-Email: <EMAIL>" \
--header "X-Auth-Key: <API_KEY>" \
--header "Content-Type: application/json" \
--data '{
  "fields": "ClientIP,ClientRequestHost,ClientRequestMethod,ClientRequestURI,EdgeEndTimestamp,EdgeResponseBytes,EdgeResponseStatus,EdgeStartTimestamp,RayID",
  "sample": 100,
  "filter": "",
  "kind": "instant-logs"
}'
```
{: codeblock}

Response:

The response includes a new field named **destination_conf**. The value of this field is your unique WebSocket address that receives messages from Cloudflare’s global network.

```sh
{
  "errors": [],
  "messages": [],
  "result": {
    "id": <JOB_ID>,
    "fields": "ClientIP,ClientRequestHost,ClientRequestMethod,ClientRequestURI,EdgeEndTimestamp,EdgeResponseBytes,EdgeResponseStatus,EdgeStartTimestamp,RayID",
    "sample": 100,
    "filter": "",
    "destination_conf": "wss://logs.cloudflare.com/instant-logs/ws/sessions/<SESSION_ID>",
    "kind": "instant-logs"
  },
  "success": true
}
```
{: codeblock}

## Connecting to WebSocket
{: #connect-websocket}

Using a CLI utility, you can connect to the WebSocket and start immediately receiving logs.

`websocat wss://logs.cloudflare.com/instant-logs/ws/sessions/<SESSION_ID>`
{: pre}

Response:

After you are connected to the websocket, you will receive messages of line-delimited JSON.

## Datasets
{: #instant-logs-datasets}

Currently, the only dataset available is HTTP requests. The list of datasets might expand when other datasets become available through Cloudflare.

## Limitations
{: #instant-logs-limitations}

When the following conditions in the Instant Logs feature are met, the logs stream stops automatically.
- When there is only one active Instant Logs session per domain.
- When the maximum session time is 60 minutes.
- When the connection closes or is not listened to for more than five minutes.
