---

copyright:
  years: 2024
lastupdated: "2024-07-17"

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
{: caption="Table 1. Operator names and behaviors" caption-side="bottom"}

## Datasets
{: #instant-logs-datasets}

Currently, the only dataset available is HTTP requests. The list of datasets might expand when other datasets become available through Cloudflare.

## Limitations
{: #instant-logs-limitations}

When the following conditions in the Instant Logs feature are met, the logs stream stops automatically.
- When there is only one active Instant Logs session per domain.
- When the maximum session time is 60 minutes.
- When the connection closes or is not listened to for more than five minutes.
