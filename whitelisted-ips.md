---
copyright:
  years: 2018
lastupdated: "2018-08-16"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# IBM Cloud CIS whitelisted IP addresses


|IPv4|IPv6|
|:-------------|:-------------|
|103.21.244.0/22 |2400:cb00::/32
| 103.22.200.0/22 |2405:8100::/32
| 103.31.4.0/22|2405:b500::/32
|104.16.0.0/12  |2606:4700::/32
| 108.162.192.0/18|2803:f800::/32
| 131.0.72.0/22|2c0f:f248::/32
|141.101.64.0/18|2a06:98c0::/29
| 162.158.0.0/15  |
| 172.64.0.0/13|
|173.245.48.0/20|
| 188.114.96.0/20 |
| 190.93.240.0/20|
|197.234.240.0/22|
| 198.41.128.0/17|


For programmatic access, you can retrieve this list via our partner's API: [https://api.cloudflare.com/client/v4/ips](https://api.cloudflare.com/client/v4/ips). This API is public and does not require any credentials. Polling this API once a week is sufficient to get the information you need to update your whitelists.
