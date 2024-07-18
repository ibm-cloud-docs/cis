---

copyright:
  years: 2018, 2024
lastupdated: "2024-07-17"

keywords: whitelisted IP addresses, CIS Edges, allowlisted IP addresses

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.cis_short_notm}} allowlisted IP addresses
{: #cis-allowlisted-ip-addresses}

The following API lists all IP addresses used by the CIS proxy. The CIS proxy uses only addresses from this list, for both client-to-proxy and proxy-to-origin communication.

[https://api.cis.cloud.ibm.com/v1/ips](https://api.cis.cloud.ibm.com/v1/ips)

Polling this API one time a week is sufficient to get the information you need to update your allowlists.

The IP addresses the CIS proxy uses for communication with the origins are not necessarily the same as the ones used for client-to-proxy communication, although all addresses are derived from the same list.
{: note}
