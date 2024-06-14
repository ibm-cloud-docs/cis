---

copyright:
  years: 2021
lastupdated: "2021-04-30"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Configuring secondary DNS
{: #configuring-secondary-dns}

Secondary DNS allows {{site.data.keyword.cis_full}} ({{site.data.keyword.cis_short_notm}}) to act as a secondary DNS provider to another organization's primary DNS. With secondary DNS, DNS entries are edited in a system outside of {{site.data.keyword.cis_short_notm}} and changes are transferred to the {{site.data.keyword.cis_short_notm}} infrastructure. If the current DNS provider does not support zone transfer, {{site.data.keyword.cis_short_notm}} cannot become a secondary DNS provider.

By default, secondary DNS domains cannot use the {{site.data.keyword.cis_short_notm}} proxy or any {{site.data.keyword.cis_short_notm}} features. To enable, contact your {{site.data.keyword.cis_short_notm}} support team. 

## Prerequisites
{: #sec-dns-prereq}

1. Contact your {{site.data.keyword.cis_short_notm}} support team to request secondary DNS. Open a Support ticket to enable the secondary DNS feature.
1. Update configuration parameters at the primary DNS provider:
    Allow traffic to the primary DNS servers from {{site.data.keyword.cis_short_notm}} IP addresses.
    Before configuring {{site.data.keyword.cis_short_notm}} as your secondary DNS provider, allow traffic to the primary DNS servers from port `53`  and update your Access Control Lists (ACLs). The Allow Ranges are where the {{site.data.keyword.cis_short_notm}} AXFR requests originate, and  Notify IPs are the IP addresses where you notify the {{site.data.keyword.cis_short_notm}} secondary DNS to initiate a pull of new zone information  from your primary DNS servers.
    Consult your DNS provider's documentation for instructions on configuring the primary zone. 
 
     Allow Range: 
     `198.41.144.240/28`
     `198.41.150.240/28`
     `2a06:98c0:3601::/48`
     `2a06:98c0:1401::/48`
 
     Notify IPs: 
     `172.65.30.82`
     `172.65.50.145`
     `2606:4700:60:0:317:26ee:3bdf:5774`
     `2606:4700:60:0:35a:4be3:4144:c5ee`
     
    For example, to run a BIND server as a primary, add the following statements to your zone file: 

    ```sh
    allow-transfer {162.158.64.0/21;198.41.144.240/28;198.41.150.0/23;198.41.152.0/22;198.41.246.0/23;198.41.250.0/24;198.41.252.0/24;2a06:98c0:1400::/48;2a06:98c0:1401::/48;2a06:98c0:3600::/48;2a06:98c0:3601::/48;2400:cb00:36::/48;2606:4700:1101::/64;198.41.144.240/28;2a06:98c0:3601::/48;}
    ```
    {: codeblock}

    ```sh
    also-notify { 198.41.246.49; 2a06:98c0:3600::53;172.65.30.82;172.65.50.145;2606:4700:60:0:317:26ee:3bdf:5774;2606:4700:60:0:35a:4be3:4144:c5ee;}
    ```
    {: codeblock}

    When configuring your primary DNS settings, choose TCP notify over UDP to minimize the chances of packet loss.
1. Determine the configuration parameters from the primary zone:
    * Primary IP address – The IP address that {{site.data.keyword.cis_short_notm}} should accept zone transfers from.
    * Zone transfer type – Whether the zone transfers are full (AXFR) or incremental (IXFR).
    * TSIG secret (Optional) – The secret string used to authenticate zone transfers.
    * TSIG algorithm (Optional) – The algorithm used to authenticate zone transfers.

After the list of prerequisites is completed, configure the secondary zone in {{site.data.keyword.cis_short_notm}}.

## Configuring a secondary zone through the API
{: #config-sec-dns-api}

Currently, DNSSEC is not supported when {{site.data.keyword.cis_short_notm}} is configured as a secondary DNS provider.
{: note}

Configure secondary DNS through the API by using a command-line utility like cURL or a browser plug-in, such as Postman. An IAM authorization token is required for all API calls.

### Step 1: Create the secondary zone
{: #step1-create-sec-zone}

Note the two {{site.data.keyword.cis_short_notm}} name servers in the API response. If the {{site.data.keyword.cis_short_notm}} name servers do not contain secondary in the name, confirm that the {{site.data.keyword.cis_short_notm}} support team enabled secondary DNS. For example: 

```sh
"name": "cis-demo.com",
"status": "pending",
"paused": false,
"type": "secondary",
"development_mode": 0,
"name_servers": [
"ns0068.secondary.cloudflare.com",
    "ns0159.secondary.cloudflare.com"
],
"original_name_servers": [
    "ns1.yourdomain.com",
    "ns2.yourdomain.com"
],
```
{: codeblock}

Create a secondary zone through the Create Zone API by setting **type** to `secondary`:

```sh
curl -X POST "https://api.cis.cloud.ibm.com/v1/zones" 
-H "Authorization: IAM_TOKEN"
-H "Content-Type: application/json"
--data '{"name":"examplesecondaryzone.fyi",”jump_start”: true, "type":"secondary"}'
```
{: codeblock}

### Step 2: Configure TSIG (optional)
{: #config-tsig}

In the following example request, **name** and **secret** must be provided by the primary DNS provider and **algo** must reflect the correct TSIG algorithm from the primary DNS server. The TSIG **name** must be lowercase to prevent zone transfer failures.

```sh
#POST https://api.cis.cloud.ibm.com/v1/<CRN>/zones/<zone_id>/secondary_dns/tsigs 
{"name": ":tsig_secret_name", 
"secret": ":tsig_secret_string", 
"algo": "hmac-sha512"}
```
{: codeblock}

A successful POST request responds with an ID. Include this ID when adding a primary server.

### Step 3: Add a primary
{: #add-a-primary}

You can add multiple primary name servers by using the API.

```sh
#POST 
https://api.cis.cloud.ibm.com/v1/<CRN>/zones/<zone_id>/secondary_dns/primaries/
{"ip": ":primary_ip",
"port": 53, 
"ixfr_enable": true, 
"tsig_id": ":tsig_tag"}
•   :primary_ip is the IPv4/IPv6 address of the primary name server.
•   :tsig_tag (optional) is the ID provided in the previous step if configured.
```
{: codeblock}

A successful `POST` request responds with an ID for the primary DNS server, and must be included when you create a secondary zone through the API. 

### Step 4: Link primary to secondary zone
{: #link-primary-to-secondary}

```sh
#POST https://api.cis.cloud.ibm.com/v1/<CRN>/zones/<zone_id>/secondary_dns
{"id": ":zone_tag", 
"name": ":zone_name", 
"primaries": [ ":zone_primary_tag" ], 
"auto_refresh_seconds": 86400 }
• :zone_tag is the zone ID of the domain that is configured for the secondary DNS.
• :zone_name is the domain name that is configured for the secondary DNS.
• :zone_primary_tag is the list of primary IDs created in the previous step.
```
{: codeblock}

The DNS table is read-only for secondary zones because records are managed through the primary DNS provider's primary server. 

### Step 5: Force zone transfer
{: #force-zone-transfer}

```sh
curl -X POST "https https://api.cis.cloud.ibm.com/v1/<CRN>/zones/<zone_id>/secondary_dns/force_axfr \
-H "Authorization: IAM_TOKEN"
-H "Content-Type: application/json"
• :zone_tag is the zone ID of the domain that is configured for the secondary DNS.
```
{: codeblock}

### Step 6: Add secondary name servers to your registrar
{: #add-secondary-nameserver-to-registrar}

Add the {{site.data.keyword.cis_short_notm}} secondary DNS name servers to the existing name servers specified at your registrar. Review the instructions in the [Prerequisites](#sec-dns-prereq) section to locate the names of your secondary name servers.

### Step 7: Testing secondary DNS
{: #test-secondary-dns}

Add a TXT record to the primary DNS provider to test transfer to the {{site.data.keyword.cis_short_notm}} secondary DNS servers.  Then, verify the TXT record is visible when querying {{site.data.keyword.cis_short_notm}} name servers. Replace `nsNNNN` with the correct name of a secondary DNS server for the domain:

`dig @nsNNN.secondary.cloudflare.com :zone_name txt +short`

For example, in this BIND as a primary server scenario:

1. Add a TXT record to the primary zone data, and increase the `Serial` number (necessary for `IXFR`).
2. Use the `rndc reload` command to reload zone data.
3. Verify that the TXT record is visible.

The DNS data is displayed on the Metrics page, but only for DNS requests that {{site.data.keyword.cis_short_notm}} name servers answer.
