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


# Querying firewall events with GraphQL
{: #graphql-firewall-events-example}

This example uses the GraphQL Analytics API to query for firewall events over a specified time period.
{: shortdesc}

The following API call requests Firewall Events over a one-hour period, and outputs the requested fields. Be sure to replace `CIS_DOMAIN_ID` with your domain ID and API token, and adjust the `datetime_geg` and `datetime_leq` values to meet your needs.

## The API call
{: #api-call}

```sh
PAYLOAD='{ "query":
  "query ListFirewallEvents($zoneTag: string, $filter: FirewallEventsAdaptiveFilter_InputObject) {
      viewer {
        zones(filter: { zoneTag: $zoneTag }) {
          firewallEventsAdaptive(
            filter: $filter
            limit: 10
            orderBy: [datetime_DESC]
          ) {
            action
            clientAsn
            clientCountryName
            clientIP
            clientRequestPath
            clientRequestQuery
            datetime
            source
            userAgent
          }
        }
      }
    }",
    "variables": {
      "zoneTag": "CIS_DOMAIN_ID",
      "filter": {
        "datetime_geq": "2020-04-24T11:00:00Z",
        "datetime_leq": "2020-04-24T12:00:00Z"
      }
    }
  }'

curl \
  -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: IBM IAM TOKEN" \
  --data "$(echo $PAYLOAD)" \
  https://api.cis.cloud.ibm.com/v1/<crn>/zones/<zoneid>/graphql
```
{: codeblock}

The results are returned in JSON, so piping the output to jq makes them easier to read. For example:

```sh
curl \
  -X POST \
  -H "Content-Type: application/json" \
  --data "$(echo $PAYLOAD)" \
  https://api.cis.cloud.ibm.com/v1/<crn>/zones/<zoneid>/graphql | jq .
{
  "data": {
    "viewer": {
      "zones": [
        {
          "firewallEventsAdaptive": [
            {
              "action": "log",
              "clientAsn": "5089",
              "clientCountryName": "GB",
              "clientIP": "203.0.113.69",
              "clientRequestPath": "/%3Cscript%3Ealert()%3C/script%3E",
              "clientRequestQuery": "",
              "datetime": "2020-04-24T10:11:24Z",
              "source": "waf",
              "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.163 Safari/537.36"
            },
            {
              "action": "log",
              "clientAsn": "5089",
              "clientCountryName": "GB",
              "clientIP": "203.0.113.69",
              "clientRequestPath": "/%3Cscript%3Ealert()%3C/script%3E",
              "clientRequestQuery": "",
              "datetime": "2020-04-24T10:11:24Z",
              "source": "waf",
              "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.163 Safari/537.36"
            },
            {
              "action": "log",
              "clientAsn": "5089",
              "clientCountryName": "GB",
              "clientIP": "203.0.113.69",
              "clientRequestPath": "/%3Cscript%3Ealert()%3C/script%3E",
              "clientRequestQuery": "",
              "datetime": "2020-04-24T10:11:24Z",
              "source": "waf",
              "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.163 Safari/537.36"
            },
            {
              "action": "log",
              "clientAsn": "5089",
              "clientCountryName": "GB",
              "clientIP": "203.0.113.69",
              "clientRequestPath": "/%3Cscript%3Ealert()%3C/script%3E",
              "clientRequestQuery": "",
              "datetime": "2020-04-24T10:11:24Z",
              "source": "waf",
              "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.163 Safari/537.36"
            },
            {
              "action": "log",
              "clientAsn": "5089",
              "clientCountryName": "GB",
              "clientIP": "203.0.113.69",
              "clientRequestPath": "/%3Cscript%3Ealert()%3C/script%3E",
              "clientRequestQuery": "",
              "datetime": "2020-04-24T10:11:24Z",
              "source": "waf",
              "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.163 Safari/537.36"
            },
            {
              "action": "log",
              "clientAsn": "5089",
              "clientCountryName": "GB",
              "clientIP": "203.0.113.69",
              "clientRequestPath": "/%3Cscript%3Ealert()%3C/script%3E",
              "clientRequestQuery": "",
              "datetime": "2020-04-24T10:11:24Z",
              "source": "waf",
              "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.163 Safari/537.36"
            },
            {
              "action": "log",
              "clientAsn": "5089",
              "clientCountryName": "GB",
              "clientIP": "203.0.113.69",
              "clientRequestPath": "/%3Cscript%3Ealert()%3C/script%3E",
              "clientRequestQuery": "",
              "datetime": "2020-04-24T10:11:24Z",
              "source": "waf",
              "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.163 Safari/537.36"
            },
            {
              "action": "drop",
              "clientAsn": "5089",
              "clientCountryName": "GB",
              "clientIP": "203.0.113.69",
              "clientRequestPath": "/%3Cscript%3Ealert()%3C/script%3E",
              "clientRequestQuery": "",
              "datetime": "2020-04-24T10:11:24Z",
              "source": "waf",
              "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.163 Safari/537.36"
            },
            {
              "action": "log",
              "clientAsn": "58224",
              "clientCountryName": "IR",
              "clientIP": "2.183.175.37",
              "clientRequestPath": "/api/v2",
              "clientRequestQuery": "",
              "datetime": "2020-04-24T10:00:54Z",
              "source": "waf",
              "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/74.0.3729.169 Safari/537.36"
            },
            {
              "action": "log",
              "clientAsn": "58224",
              "clientCountryName": "IR",
              "clientIP": "2.183.175.37",
              "clientRequestPath": "/api/v2",
              "clientRequestQuery": "",
              "datetime": "2020-04-24T10:00:54Z",
              "source": "waf",
              "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/74.0.3729.169 Safari/537.36"
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
