---

copyright:
  years: 2025
lastupdated: "2025-07-21"

keywords: managed lists

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Using managed lists
{: #using-managed-lists}

{{site.data.keyword.cis_short_notm}} provides managed lists you can use in rule expressions. These lists are regularly updated.

## Managed IP lists
{: #managed-ip-lists}

You can access CIS IP threat intelligence through managed IP lists. CIS offers several managed IP lists, but the specific lists available to you depend on your subscription plan.

| Display name | Name in expressions | Description |
| ------------ | ------------------- | ----------- |
| Cloudflare Open Proxies | `cf.open_proxies` | IP addresses of known open HTTP and SOCKS proxy endpoints, which are frequently used to launch attacks and hide attackers identity.|
| Cloudflare Anonymizers | `cf.anonymizer` | IP addresses of known anonymizers (open SOCKS proxies, VPNs, and TOR nodes). |
| Cloudflare VPNs | `cf.vpn` | IP addresses of known VPN servers. |
| Cloudflare Malware | `cf.malware` | IP addresses of known sources of malware. |
| Cloudflare Botnets, Command and Control Servers | `cf.botnetcc` | IP addresses of known botnet command-and-control servers. |

{: caption="Available managed IP lists" caption-side="bottom"}

## Listing managed lists in an instance from the CLI
{: #listing-managed-lists-cli}
{: cli}

To list managed lists in an instance from the CLI, run the following command:

```sh
cis managed-lists [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

### Command options
{: #command-listing-managed-lists-cli}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance specified by `cis instance-set INSTANCE` is used.

`--output`
:   Specify output format, only JSON is supported now.

### Command example
{: #example-listing-managed-lists-cli}

```sh
ibmcloud cis managed-lists -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9:: -o json
```
{: pre}

## Listing managed lists in an instance with the API
{: #listing-managed-lists-api}
{: api}

The following example lists managed lists in an instance:
```sh
curl -X GET https://api.cis.cloud.ibm.com/v1/$CRN/rules/managed_lists \
-H 'Content-Type: application/json' \
-H 'Accept: application/json' \
-H 'X-Auth-User-Token: Bearer xxxxxx'
```
{: pre}
