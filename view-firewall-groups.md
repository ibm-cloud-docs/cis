---

copyright:
  years: 2018, 2024
lastupdated: "2024-11-18"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Viewing firewall event groups
{: #view-firewall-groups}

If you have a large amount of firewall events, you may want to view the overall count of events based on different groupings. This example shows looking at firewall events per country in 15 minute groupings.
{: shortdesc}

The API call looks like:

```ssh
PAYLOAD='{ "query":
  "query ListFirewallEvents($zoneTag: string, $filter: FirewallEventsAdaptiveFilter_InputObject) {
      viewer {
        zones(filter: { zoneTag: $zoneTag }) {
          firewallEventsAdaptiveGroups(
            filter: $filter
            limit: 100
            orderBy: [datetimeFifteenMinutes_DESC]
          ) {
            dimensions {
              clientCountryName
              datetimeFifteenMinutes
            }
            count
          }
        }
      }
    }",
    "variables": {
      "zoneTag": "$CIS_DOMAIN_ID",
      "filter": {
        "datetime_geq": "2020-04-24T11:00:00Z",
        "datetime_leq": "2020-04-24T12:00:00Z"
      }
    }
  }'

curl   -X POST   -H "Content-Type: application/json"   -H "Authorization: IBM IAM TOKEN"   --data "$(echo $PAYLOAD)"   https://api.cis.cloud.ibm.com/v1/$CRN/zones/$ZONE_ID/graphql
```
{: pre}

An example response: 

```ssh
{
  "data":{
    "viewer":{
      "zones":[
        {
          "firewallEventsAdaptiveGroups":[
            {
              "count":3,
              "dimensions":{
                "clientCountryName":"NL",
                "datetimeFifteenMinutes":"2024-10-28T00:15:00Z"
              }
            },
            {
              "count":86,
              "dimensions":{
                "clientCountryName":"US",
                "datetimeFifteenMinutes":"2024-10-28T00:15:00Z"
              }
            },
            {
              "count":3,
              "dimensions":{
                "clientCountryName":"DE",
                "datetimeFifteenMinutes":"2024-10-28T00:15:00Z"
              }
            },
            {
              "count":15,
              "dimensions":{
                "clientCountryName":"CA",
                "datetimeFifteenMinutes":"2024-10-28T00:15:00Z"
              }
            },
            {
              "count":2,
              "dimensions":{
                "clientCountryName":"IN",
                "datetimeFifteenMinutes":"2024-10-28T00:15:00Z"
              }
            },
            {
              "count":366,
              "dimensions":{
                "clientCountryName":"PH",
                "datetimeFifteenMinutes":"2024-10-28T00:00:00Z"
              }
            },
            {
              "count":83357,
              "dimensions":{
                "clientCountryName":"US",
                "datetimeFifteenMinutes":"2024-10-28T00:00:00Z"
              }
            },
            {
              "count":146,
              "dimensions":{
                "clientCountryName":"BE",
                "datetimeFifteenMinutes":"2024-10-28T00:00:00Z"
              }
            },
            {
              "count":477,
              "dimensions":{
                "clientCountryName":"NL",
                "datetimeFifteenMinutes":"2024-10-28T00:00:00Z"
              }
            },
            {
              "count":58,
              "dimensions":{
                "clientCountryName":"KR",
                "datetimeFifteenMinutes":"2024-10-28T00:00:00Z"
              }
            },
            {
              "count":10,
              "dimensions":{
                "clientCountryName":"NZ",
                "datetimeFifteenMinutes":"2024-10-28T00:00:00Z"
              }
            },
            {
              "count":15202,
              "dimensions":{
                "clientCountryName":"CA",
                "datetimeFifteenMinutes":"2024-10-28T00:00:00Z"
              }
            },
            {
              "count":665,
              "dimensions":{
                "clientCountryName":"GB",
                "datetimeFifteenMinutes":"2024-10-28T00:00:00Z"
              }
            },
            {
              "count":1048,
              "dimensions":{
                "clientCountryName":"DE",
                "datetimeFifteenMinutes":"2024-10-28T00:00:00Z"
              }
            },
            {
              "count":3509,
              "dimensions":{
                "clientCountryName":"AU",
                "datetimeFifteenMinutes":"2024-10-28T00:00:00Z"
              }
            },
            {
              "count":114,
              "dimensions":{
                "clientCountryName":"ID",
                "datetimeFifteenMinutes":"2024-10-28T00:00:00Z"
              }
            },
            {
              "count":806,
              "dimensions":{
                "clientCountryName":"HK",
                "datetimeFifteenMinutes":"2024-10-28T00:00:00Z"
              }
            },
            {
              "count":66,
              "dimensions":{
                "clientCountryName":"PT",
                "datetimeFifteenMinutes":"2024-10-28T00:00:00Z"
              }
            },
            {
              "count":523,
              "dimensions":{
                "clientCountryName":"IN",
                "datetimeFifteenMinutes":"2024-10-28T00:00:00Z"
              }
            },
            {
              "count":43,
              "dimensions":{
                "clientCountryName":"FR",
                "datetimeFifteenMinutes":"2024-10-28T00:00:00Z"
              }
            },
            {
              "count":263,
              "dimensions":{
                "clientCountryName":"CN",
                "datetimeFifteenMinutes":"2024-10-28T00:00:00Z"
              }
            },
            {
              "count":1,
              "dimensions":{
                "clientCountryName":"AR",
                "datetimeFifteenMinutes":"2024-10-28T00:00:00Z"
              }
            },
            {
              "count":27,
              "dimensions":{
                "clientCountryName":"PE",
                "datetimeFifteenMinutes":"2024-10-28T00:00:00Z"
              }
            },
            {
              "count":19,
              "dimensions":{
                "clientCountryName":"XX",
                "datetimeFifteenMinutes":"2024-10-28T00:00:00Z"
              }
            },
            {
              "count":327,
              "dimensions":{
                "clientCountryName":"JP",
                "datetimeFifteenMinutes":"2024-10-28T00:00:00Z"
              }
            },
            {
              "count":1018,
              "dimensions":{
                "clientCountryName":"MX",
                "datetimeFifteenMinutes":"2024-10-28T00:00:00Z"
              }
            }
          ]
        }
      ]
    }
  },
  "errors":null
}
```
{: screen}
