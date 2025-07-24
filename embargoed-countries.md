---

copyright:
  years: 2024, 2025
lastupdated: "2025-07-24"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Adhering to IBM Cloud sanctions on embargoed countries
{: #adhering-to-embargoed-countries}

Compliance with IBM Cloud sanctions involves following restrictions related to specific embargoed countries: **Iran**, **Cuba**, **North Korea**, and **Syria**. Adhering to these sanctions is crucial for maintaining compliance with international laws and regulations.
{: shortdesc}

## Understanding sanctions and embargoes
{: #understanding-sanctions-embargoes}

Sanctions are restrictive measures that are imposed by governments or international organizations to influence the behavior of a country or group. Embargoes are a specific type of sanction that prohibits trade and other commercial activities with certain countries.

IBM Cloud is committed to complying with all applicable laws and regulations, including those laws related to sanctions and embargoes. Users must ensure that their use of IBM Cloud services doesn't involve any activities with the embargoed countries. For more information, see [Sanctions and Embargoes](/docs/overview?topic=overview-notices) in the IBM Cloud Notices page.

## Adding custom rules from the CLI
{: #custom-rules-cli}
{: cli}

CIS custom rules help you define specific conditions to control whether traffic is allowed or blocked. To block traffic from the embargoed countries, you can use the following custom rules expression:

   ```sh
   ibmcloud cis custom-waf rule-create DNS_DOMAIN_ID -i INSTANCE --match "(ip.geoip.country eq "IQ" and ip.geoip.country eq "KP" and ip.geoip.country eq "CU" and ip.geoip.country eq "SY")" --action block --description "Embargo" --enabled true
   ```
   {: pre}

Where:

`DNS_DOMAIN_ID`
:   Is the ID of the DNS domain.

`INSTANCE`
:   Is the name or ID of the instance.

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
		"expression": "ip.src.country eq \"IR\"",
		"description": "Filter traffic from Iran",
		"paused": false
	},
	{
		"expression": "ip.src.country eq \"CU\"",
		"description": "Filter traffic from Cuba",
		"paused": false
	},
	{
		"expression": "ip.src.country eq \"KP\"",
		"description": "Filter traffic from North Korea",
		"paused": false
	},
	{
		"expression": "ip.src.country eq \"SY\"",
		"description": "Filter traffic from Syria",
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
	},
	{
		"filter": {
			"id": "<Filter 2 ID>"
		},
		"action": "block",
		"paused": false
	},
	{
		"filter": {
			"id": "<Filter 3 ID>"
		},
		"action": "block",
		"paused": false
	},
	{
		"filter": {
			"id": "<Filter 4 ID>"
		},
		"action": "block",
		"paused": false
	}
           ]'
   ```
   {: codeblock}
