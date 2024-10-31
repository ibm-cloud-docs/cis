---

copyright:
  years: 2020, 2024
lastupdated: "2024-10-09"

keywords: graphql

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Querying basics
{: #querying-basics}

There are several basic aspects of querying with GraphQL for metrics collection you should understand.
{: shortdesc}

## Structure of a GraphQL query
{: #graphql-structure}

GraphQL structures data as a graph. GraphQL uses a schema to define the objects and their hierarchy in your data graph. You can explore the edges of the graph by using queries to get the needed data. These queries must respect the structure of the schema.

A **node**, followed by its **fields**, is at the core of a GraphQL query. A node is an object of a specific **type**; the type specifies the fields that make up the object.

A field can be another node where the appropriate query would contain nested elements. Some nodes look like functions that can take on arguments to limit the scope of what they can act on. You can apply filters at each node.

## Cloudflare GraphQL schema
{: #graphql-schema}

A typical query against the Cloudflare GraphQL schema is made up of four main components:

* `viewer` - The root node.
* `zones` or `accounts` - Indicate the scope of the query (the domain
  area or account you want to query). The `viewer` can access one `zones` or
  `accounts`, or both.
* **data node** or **dataset** - Represent the data you want to query. `zones`
  or `accounts` may contain one or more datasets. 
* **fieldset** - A set of fields or nested fields of the **dataset**.

The query to the Cloudflare GraphQL API must be sent by an HTTP POST request with the payload in JSON format that consists of these fields:

```json
{
  "query": "",
  "variables": {}
}
```

From the above structure, the `query` field must contain a GraphQL query formatted as a single line string (which means all newline symbols should be stripped or escaped), when `variables` is an object that contains all values of used placeholders in the query itself.

## A single dataset example
{: #graphql-single}

In the following example, the GraphQL query fetches a `datetime`, `action`, and client request HTTP host as the `host` field of 2 WAF events from zone-scoped the `firewallEventsAdaptive` dataset.

```json
{
  viewer {
    zones(filter: { zoneTag: $tag }) {
      firewallEventsAdaptive(
        filter: {
          datetime_gt: $start
          datetime_lt: $end
        }
        limit: 2
        orderBy: [
          datetime_DESC
        ]
      ) {
        action
        datetime
        host: clientRequestHTTPHost
      }
    }
  }
}
```

In the query above, there are variable placeholders: `$tag`, `$start`, and `$end`. It provides values for those placeholders alongside the query by placing them into the `variables` field of the payload.

Define your variables:

```json
{
  "tag": "<zone-tag>",
  "start": "2020-08-03T02:07:05Z",
  "end": "2020-08-03T17:07:05Z"
}
```

There are multiple ways to send your query to Cloudflare GraphQL API. You can use you favourite GraphQL client or CLI to send a request using curl.
{: tip}

A sample of a response for the query above:

```json 
{
  "data": {
    "viewer": {
      "zones": [
        {
          "firewallEventsAdaptive": [
            {
              "action": "log",
              "host": "cloudflare.guru",
              "datetime": "2020-08-03T17:07:03Z"
            },
            {
              "action": "log",
              "host": "cloudflare.guru",
              "datetime": "2020-08-03T17:07:01Z"
            }
          ]
        }
      ]
    }
  },
  "errors": null
}
```
{: screen}

## Query multiple datasets in a single GraphQL API request
{: #graphql-multiple-datasets}

As previously mentioned, a query might contain one or multiple nodes (datasets). At the API level, the data extraction is done simultaneously, but the response is delayed until all dataset queries receive their results. If any fails during the execution, the entire query will be terminated, and the error will be returned.

A sample query for two datasets in one attempt:

```json
{
  viewer {
    zones(filter: { zoneTag: $tag }) {
      last10Events: firewallEventsAdaptive(
        filter: {
          datetime_gt: $start
          datetime_lt: $end
        }
        limit: 10
        orderBy: [
          datetime_DESC
        ]
      ) {
        action
        datetime
        host: clientRequestHTTPHost
      }
      top3DeviceTypes: httpRequestsAdaptiveGroups(
        filter: {
          date: $ts
        }
        limit: 10
        orderBy: [
          count_DESC
        ]
      ) {
        count
        dimensions {
          device: clientDeviceType
        }
      }
    }
  }
}
```

A set of variables for the previous query:

```json 
{
  "tag": "<zone-tag>",
  "start": "2022-10-02T00:26:49Z",
  "end": "2022-10-04T14:26:49Z",
  "ts": "2022-10-04"
}
```

A sample response for the query using the previous variables:

```json
{
  "data": {
    "viewer": {
      "zones": [
        {
          "last10Events": [
            {
              "action": "block",
              "country": "TR",
              "datetime": "2022-10-04T08:41:09Z"
            },
            {
              "action": "block",
              "country": "TR",
              "datetime": "2022-10-04T08:41:09Z"
            },
            {
              "action": "block",
              "country": "RU",
              "datetime": "2022-10-04T01:09:36Z"
            },
            {
              "action": "block",
              "country": "US",
              "datetime": "2022-10-03T14:26:49Z"
            },
            {
              "action": "block",
              "country": "US",
              "datetime": "2022-10-03T14:26:46Z"
            },
            {
              "action": "block",
              "country": "CN",
              "datetime": "2022-10-02T23:51:26Z"
            },
            {
              "action": "block",
              "country": "TR",
              "datetime": "2022-10-02T23:39:41Z"
            },
            {
              "action": "block",
              "country": "TR",
              "datetime": "2022-10-02T23:39:41Z"
            }
          ],
          "top3DeviceTypes": [
            {
              "count": 4580,
              "dimensions": {
                "device": "desktop"
              }
            }
          ]
        }
      ]
    }
  },
  "errors": null
}
```
{: screen}

