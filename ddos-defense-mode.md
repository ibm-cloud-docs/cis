---

copyright:
  years: 2024, 2025
lastupdated: "2025-02-24"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Defense mode for DDoS attacks
{: #defense-mode-attack-ddos}

When your site is under a DDoS attack, you can switch on defense mode to quickly mitigate the attack.
{: shortdesc}

Follow these steps to set your entire domain in defense mode when you are under attack.

1. Turn on “Defense mode" from the **Overview** screen.
1. Do not rate-limit or throttle requests from IBM {{site.data.keyword.cis_short_notm}}, because {{site.data.keyword.cis_short_notm}} needs the bandwidth to assist you with your situation.
1. Block specific countries and visitors if necessary.

## How defense mode works
{: #how-defense-mode-works}

The defense mode runs additional security checks to help mitigate layer 7 DDoS attacks. Validated users can gain access your website and suspicious traffic is blocked. Defense mode is designed to be used as one of the last resorts when a zone is under attack. In defense mode, access to your site is temporarily paused, which can impact your site analytics.

When enabled, visitors receive an interstitial page.

Defense mode is disabled by default for your domain.
{: note}

### Selectively apply defense mode
{: #selectively-apply-defense-mode}

To enable defense for specific pages or sections of your site, use a configuration rule to adjust the security level.

For example, consider the following incoming request matching scenario.

* Field: URI Path
* Operator: starts with
* Value: /admin

1. If you are using the Expression Editor, enter the following expression.

    ```sh
    (starts_with(http.request.uri.path, "/admin"))
    ```
    {: pre}

2. For defense mode, select **Add**.
3. Move the switch to **0n**.

To turn it on for specific ASNs (hosts/ISPs that own IP addresses), countries, or IP ranges, use IP Access Rules.

## Potential issues
{: #potential-issues}

Because defense mode requires your browser to support JavaScript to display and pass the interstitial page, there is an expected impact on third party analytics tools.
