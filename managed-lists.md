---

copyright:
  years: 2025
lastupdated: "2025-06-26"

keywords: managed lists

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Using managed lists
{: #managed-lists}

{{site.data.keyword.cis_short_notm}} provides managed lists you can use in rule expressions. These lists are regularly updated.

The available managed lists depend on your CIS plan and product subscriptions. 
{: note}

## Managed IP lists
{: #managed-ip-lists}

You can use managed IP lists to access CIS IP threat intelligence. CIS provides the following managed IP lists:

| Display name | Name in expressions | Description |
| ------------ | ------------------- | ----------- |
| Cloudflare Open Proxies | `cf.open_proxies` | IP addresses of known open HTTP and SOCKS proxy endpoints, which are frequently used to launch attacks and hide attackers identity.|
| Cloudflare Anonymizers | `cf.anonymizer` | IP addresses of known anonymizers (open SOCKS proxies, VPNs, and TOR nodes). |
| Cloudflare VPNs | `cf.vpn` | IP addresses of known VPN servers. |
| Cloudflare Malware | `cf.malware` | IP addresses of known sources of malware. |
| Cloudflare Botnets, Command and Control Servers | `cf.botnetcc` | IP addresses of known botnet command-and-control servers. |
{: caption="Available managed IP lists" caption-side="bottom"}
