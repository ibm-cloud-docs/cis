---

copyright:
  years: 2024, 2026
lastupdated: "2026-02-06"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Using Defense mode for DDoS attacks
{: #defense-mode-attack-ddos}

When your site is under a DDoS attack, you can switch on defense mode to quickly mitigate the attack. Defense mode uses additional security checks to help mitigate Layer 7 DDoS attacks, allowing validated users through while blocking suspicious traffic. The following guidance explains how to apply defense mode at the domain or page level and what to expect when it is enabled.
{: shortdesc}

To set your entire domain in defense mode when you are under attack, turn on “Defense mode" from the CIS **Overview** page. When enabled:

* Do not rate-limit or throttle requests from IBM {{site.data.keyword.cis_short_notm}}, because {{site.data.keyword.cis_short_notm}} needs the bandwidth to assist you with your situation.
* You can block specific countries and visitors if necessary.
* Visitors see an interstitial page, and access to your site may be temporarily paused, which can impact analytics.

Defense mode is disabled by default and intended as a last resort when a zone is under attack.
{: note}

## Applying defense mode selectively 
{: #selectively-apply-defense-mode}

Instead of enabling defense mode for the entire domain, you can apply it to specific pages or site sections by adjusting the security level with a configuration rule.

For example, consider the following incoming request matching scenario:

* Field: `URI Path`
* Operator: `starts with`
* Value: `/admin`

1. If you are using the Expression Editor, enter the following expression.

    ```sh
    (starts_with(http.request.uri.path, "/admin"))
    ```
    {: pre}

1. For defense mode, select **Add**.
1. Move the switch to **0n**.

To target specific ASNs (hosts/ISPs that own IP addresses), countries, or IP ranges, use **IP Access Rules**.

## Potential issues
{: #potential-issues}

Defense mode requires the browser to support JavaScript in order to display and pass the interstitial page. This requirement can affect third‑party analytics tools, which might not record traffic accurately while defense mode is active.

## Related links
{: #defense-mode-related-links}

* [DDoS attack concepts](/docs/cis?topic=cis-ddos-attack-concepts)
* [About DDoS protection in CIS](/docs/cis?topic=cis-about-ddos)
* [Preventing DDoS attacks](/docs/cis?topic=cis-preventing-ddos-attacks)
* [Responding to DDoS attacks](/docs/cis?topic=cis-responding-to-ddos-attacks)
* [Third-party services and DDoS protection](/docs/cis?topic=cis-third-party-ddos)
* [HTTP DDoS Attack Protection managed ruleset](/docs/cis?topic=cis-http-ddos)
