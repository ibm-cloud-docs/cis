---

copyright:
  years: 2024, 2026
lastupdated: "2026-01-20"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Adhering to IBM Cloud sanctions on embargoed countries
{: #adhering-to-embargoed-countries}

Compliance with IBM Cloud sanctions involves the following restrictions that are related to specific embargoed countries: **Iran**, **Cuba**, **North Korea**, and **Syria**. Adhering to these sanctions is crucial for maintaining compliance with international laws and regulations.
{: shortdesc}

## Understanding sanctions and embargoes
{: #understanding-sanctions-embargoes}

Sanctions are restrictive measures that are imposed by governments or international organizations to influence the behavior of a country or group. Embargoes are a specific type of sanction that prohibits trade and other commercial activities with certain countries.

IBM Cloud is committed to complying with all applicable laws and regulations, including those laws related to sanctions and embargoes. Users must ensure that their use of IBM Cloud services doesn't involve any activities with the embargoed countries. For more information, see [Sanctions and Embargoes](/docs/overview?topic=overview-notices) in the IBM Cloud Notices page.

## Adding custom rules from the CLI
{: #custom-rules-cli}
{: cli}

CIS custom rules help you to define conditions that allow or block traffic. To block the traffic from US-embargoed countries, create the country-blocking custom rule and place it first in the custom rules order. Use the following commands to create the rule and add it as the first custom rule.

   ```sh
   ibmcloud cis custom-waf rule-create DNS_DOMAIN_ID -i INSTANCE --match "(ip.geoip.country in {\"CU\" \"IR\" \"SY\" \"KP\"})" --action block --description "Embargo" --enabled true
   ibmcloud cis custom-waf rule-order-update $DNS_DOMAIN_ID -i INSTANCE RULE_ID --index 1
   ```
   {: pre}

Where:

`DNS_DOMAIN_ID`
:   The ID of the DNS domain.

`INSTANCE`
:   The name or ID of the instance.

`RULE_ID`
:   The ID of the custom rule for blocking the embargoed countries.

## Adding custom rules with the API
{: #custom-rules-api}
{: api}

To add a custom rule with the API, follow these steps:

1. First, create a filter for each embargoed country by sending the following request:

   ```sh
   curl --request POST \
   --url https://api.cis.cloud.ibm.com/v1/<CRN>/zones/<ZONE ID>/filters \
   --header 'Accept: application/json' \
   --header 'Authorization: Bearer <TOKEN>' \
   --header 'Content-Type: application/json' \
   --data '[
        {
                "expression": "(ip.geoip.country in {"IR" "CU" "SY" "KP"})",
                "description": "Block Traffic from US Embargoed Countries",
                "paused": false
        }
      ]'
   ```
   {: codeblock}

1. Create a firewall rule to block traffic from these countries

   ```sh
   curl --request POST \
   --url https://api.cis.cloud.ibm.com/v1/<CRN>/zones/<ZONE ID>/firewall/rules \
   --header 'Accept: application/json' \
   --header 'Authorization: Bearer <TOKEN>' \
   --header 'Content-Type: application/json' \
   --data '[
	{
		"filter": {
			"id": "<Filter 1 ID>"
		},
		"action": "block",
		"paused": false
	} ]'
   ```
   {: codeblock}
