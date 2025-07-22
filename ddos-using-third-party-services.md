---

copyright:
  years: 2025, 2025
lastupdated: "2025-07-22"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Third-party services and DDoS protection
{: #third-party-ddos}

When you integrate third-party services, such as Content Delivery Networks (CDNs), VPNs, or NAT devices with CIS, it is important to understand how these components interact with Distributed Denial of Service (DDoS) protection systems. The following sections describe recommended configuration settings and adjustments to DDoS rules to make sure that these services work seamlessly together. The goal is to maintain strong traffic filtering, reduce potential risks, and avoid any negative impact on performance.

## Using a third-party CDN in front of CIS
{: #using-third-party-cdn-in-cis}

Some CIS customers choose to place a third-party CDN in front of CIS to cache and serve their resources.

However, it is "not" recommended to place a third-party CDN in front of CIS. Some CDN providers might introduce discrepancies into HTTP requests that deviate from protocol standards and protocol best practices. Also, because traffic to CIS then originates from a limited set of the CDN's IP addresses, this can (in rare cases) cause the traffic to be misidentified as a DDoS attack. For example, when you use the Akamai CDN in front of CIS, the high volume of traffic from a limited set of IPs can resemble attack behavior to CIS.

Instead, it is recommended to use CIS and the [underlying Cloudflare network](https://www.cloudflare.com/en-gb/network/){: external} and its CDN capabilities, which provide the following benefits:
* Reduced latency by removing an extra network hop between vendor data centers.
* Immediate DDoS protection at the first point of contact with the internet (an industry best practice).

If you use a third-party CDN in front of CIS and CIS mitigates a DDoS attack, you must still pay your CDN provider for the attack traffic the provider that is processed before mitigation.
{: note}

## Recommended DDoS configuration adjustments for CDN or proxy
{: #recommend-ddos-configuration-cdn}

If you use a CDN or proxy in front of CIS, it is recommended that you change the action and/or sensitivity level of the following DDoS rules named:

* `HTTP requests with unusual HTTP headers or URI path (signature #1) with the rule ID ...3486aee1`
* `HTTP requests with unusual HTTP headers or URI path (signature #56) with the rule ID ...e269dfd6`
* `HTTP requests with unusual HTTP headers or URI path (signature #57) with the rule ID ...f35a42a0`
* `Requests coming from known bad sources with the rule ID ...3a679c52`

## Recommended DDoS configuration adjustments for VPN and NAT
{: #recommended-ddos-configuration-adjustments-vpn-nat}

Without an Advanced DDoS Protection subscription, you can't customize DDoS rule actions, such as setting them to `Log`. However, you can still adjust rule sensitivity to reduce the likelihood of false positives if unintended blocking occurs.
{: note}

If your organization uses VPNs, NATs, or third-party services that generate high traffic volumes (over 100 Mbps), you might need to adjust your DDoS configuration to avoid disruptions. Both HTTP-based (Layer 7) and network-layer (Layer 4) traffic can trigger managed DDoS rules. The following recommendations help you use expression filters and tune rule sensitivity to better accommodate legitimate high-volume traffic:

* Use expression filters to exclude specific traffic from the rules. You can exclude a combination of source ports, source IP addresses, destination ports, destination IP addresses, and protocol.

* Reduce the sensitivity level of relevant managed rules. Setting a rule to "Essentially Off" prevents the rule from being triggered. For more information on rule adjustments, see the [HTTP DDoS Attack Protection managed ruleset](/apidocs/cis#get-zone-entrypoint-ruleset) (phase `ddos_l7`) and the [Network-layer DDoS Attack Protection managed ruleset](/apidocs/cis#get-zone-entrypoint-ruleset)(phase `ddos_l4`).

   To see an example API call for adjusting the L7 ruleset, see [Adjusting the sensitivity of DDoS L7 ruleset with the API](/docs/cis?topic=cis-third-party-ddos&q=expression+filters&tags=cis&loginMethod=federated#example-sensitivity-level-api).
   {: note}

For Enterprise users, DDoS ruleset actions can be configured by using the Ruleset API to log matching traffic. While no dedicated UI exists for the DDoS ruleset, setting a rule’s action to `Log` allows visibility into flagged traffic through API-accessible logs. This action can help you gather insights before you apply exclusions or change the rule sensitivity.

### Example: Adjusting the sensitivity of DDoS Layer 7 ruleset with the API
{: #example-sensitivity-level-api}

To adjust the sensitivity of the DDoS Layer 7 ruleset:

```sh
curl -X PUT https://api.cis.cloud.ibm.com/v1/$CRN/rulesets/phases/ddos_l7/entrypoint
--header "Content-Type: application/json"
--header "X-Auth-User-Token: Bearer $IAM_TOKEN"
--data '{
  "action":"execute",
  "description":"ddos override",
  "enabled":true,
  "expression":"true",
  "action_parameters":{
    "id":"4d21379b4f9f4bb088e0729962c8b3cf",
    "overrides":{
      "rules":[
        {
          "id":"dd42da7baabe4e518eaf11c393596a9d",
          "sensitivity_level":"eoff"
        },
	{
          "id":"78da7447eca94fabbcb405fc923e2920",
          "sensitivity_level":"medium"
	}
      ]
    }
  }
}'
```
{: codeblock}

The DDoS Layer 7 ruleset always uses the ID `4d21379b4f9f4bb088e0729962c8b3cf`. Also, the `expression` field must always be set to `true`.
{: note}

In this example, two commonly triggered rules in high-traffic scenarios are being overridden:

`"HTTP requests causing a high number of origin errors."` - `dd42da7baabe4e518eaf11c393596a9d`
`"HTTP requests causing a high request rate to origin."` - `78da7447eca94fabbcb405fc923e2920`

To retrieve rule IDs and descriptions, use this API call:

```sh
curl -X GET https://api.cis.cloud.ibm.com/v1/$CRN/rulesets/4d21379b4f9f4bb088e0729962c8b3cf
--header "Content-Type: application/json"
--header "X-Auth-User-Token: Bearer $IAM_TOKEN"
```
{: pre}
