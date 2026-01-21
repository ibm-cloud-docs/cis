---

copyright:
  years: 2026
lastupdated: "2026-01-21"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# About HTTP DDoS Attack Protection
{: #http-ddos-attack}

The CIS HTTP DDoS Attack Protection managed ruleset is a set of pre-configured rules that are designed to detect and mitigate known Layer 7 (application-layer) DDoS attack vectors across the CIS global network.

The managed ruleset detects and mitigates:

* Known DDoS attack patterns and tools
* Suspicious request patterns
* Protocol violations
* Requests that generate a high volume of origin errors
* Excessive traffic targeting the origin or cache
* Additional application-layer attack vectors

The HTTP DDoS Attack Protection managed ruleset is always enabled. You can not disable it, but you can customize its behavior.

The managed ruleset also provides increased visibility into Layer 7 DDoS attacks mitigated by CIS, allowing you to review both ongoing and historical attacks.

## Ruleset configuration
{: #ruleset-configuration}

If you expect large volumes of legitimate traffic, you can customize the HTTP DDoS Attack Protection settings to reduce false positives, where legitimate requests are incorrectly detected as attack traffic and blocked or challenged.

You can adjust the behavior of the rules in the managed ruleset by modifying the following parameters:

* The performed **action** when an attack is detected.
* The **sensitivity level** of attack detection mechanisms.

Certain actions and sensitivity levels are available only on specific CIS plans.
Currently, you can define account-level overrides for the HTTP DDoS Attack Protection managed ruleset only through the API.
{: note}

To adjust rule behavior, see [Configure the managed ruleset via API](/apidocs/cis#get-zone-entrypoint-ruleset).

For more information on the available configuration parameters, see [Managed ruleset parameters](/docs/cis?topic=cis-ddos-parameters).

## Availability
{: #http-ddos-availability}

The HTTP DDoS Attack Protection managed ruleset protects CIS customers on all plans and applies to all zones. Customers can configure the ruleset at both the zone level and the account level.

Customers on Enterprise plans can create up to 10 overrides (or up to 10 rules when using the API) with custom [expressions](/docs/cis?topic=cis-custom-rules-fields-and-expressions&interface=cli) to tailor DDoS protection for different categories of incoming requests.

Customers on Standard plans can create one override only and cannot customize the rule expression. In this case, the single override—containing one or more configuration settings applies to all incoming requests.
