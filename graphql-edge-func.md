---

copyright:
  years: 2020
lastupdated: "2020-10-09"

keywords: 

subcollection: cis

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:term: .term}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:table: .aria-labeledby="caption"}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Querying Edge Functions metrics with GraphQL
{:#graphql-edge-func}

This example uses the GraphQL Analytics API to query for Edge Functions Metrics over a specified time period. You can query up to one week of data for dates up to three months ago.
{:shortdesc}

The following API call requests an Edge Functions script's metrics over a one day period, and outputs the requested fields. Adjust the `datetimeStart`, `datetimeEnd`, `accountTag`, and `scriptName` variables as needed.

## The API call
{:#api-call-edge-func}

```
PAYLOAD='{ "query":
  "query GetEdgeFunctionsAnalytics($accountTag: string, $datetimeStart: string, $datetimeEnd: string, $scriptName: string) {
      viewer {
        accounts(filter: {accountTag: $accountTag}) {
          workersInvocationsAdaptive(limit: 100, filter: {
            scriptName: $scriptName,
            datetime_geq: $datetimeStart,
            datetime_leq: $datetimeEnd
          }) {
            sum {
              subrequests
              requests
              errors
            }
            quantiles {
              cpuTimeP50
              cpuTimeP99
            }
            dimensions{
              datetimeHour
              scriptName
              status
            }
          }
        }
      }
    }",
    "variables": {
      "accountTag": "90f518ca7113dc0a91513972ba243ba5",
      "datetimeStart": "2020-05-04T00:00:00.000Z",
      "datetimeEnd": "2020-05-04T00:00:00.000Z",
      "scriptName": "edge-function-subrequest-test-client"
    }
  }'

curl \
  -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: IBM IAM TOKEN" \
  --data "$(echo $PAYLOAD)" \
  https://api.cis.cloud.ibm.com/v1/<crn>/zones/<zoneid>/graphql
```
{:codeblock}

The results are returned in JSON (as requested), so piping the output to jq makes them easier to read. For example:

```
curl \
  -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: IBM IAM TOKEN" \
  --data "$(echo $PAYLOAD)" \
  https://api.cis.cloud.ibm.com/v1/<crn>/zones/<zoneid>/graphql | jq .
{
  "data": {
    "viewer": {
      "accounts": [
        {
          "workersInvocationsAdaptive": [
            {
              "dimensions": {
                "datetime": "2020-05-04T18:10:35Z",
                "scriptName": "edge-function-subrequest-test-client",
                "status": "success"
              },
              "quantiles": {
                "cpuTimeP50": 206,
                "cpuTimeP99": 206
              },
              "sum": {
                "errors": 0,
                "requests": 1,
                "subrequests": 0
              }
            },
            {
              "dimensions": {
                "datetime": "2020-05-04T18:10:34Z",
                "scriptName": "edge-function-subrequest-test-client",
                "status": "success"
              },
              "quantiles": {
                "cpuTimeP50": 291,
                "cpuTimeP99": 291
              },
              "sum": {
                "errors": 0,
                "requests": 1,
                "subrequests": 0
              }
            },
            {
              "dimensions": {
                "datetime": "2020-05-04T18:10:49Z",
                "scriptName": "edge-function-subrequest-test-client",
                "status": "success"
              },
              "quantiles": {
                "cpuTimeP50": 212.5,
                "cpuTimeP99": 261.19
              },
              "sum": {
                "errors": 0,
                "requests": 4,
                "subrequests": 0
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
{:screen}
