---

copyright:
  years: 2026
lastupdated: "2026-02-06"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# HTTP DDoS Attack Protection managed ruleset
{: #http-ddos}
{: api}

The CIS HTTP DDoS Attack Protection managed ruleset is a set of pre-configured rules that are designed to detect and mitigate known Layer 7 (application-layer) DDoS attack vectors across the CIS global network. 

Currently, the HTTP DDoS Attack Protection ruleset is only available using the CIS API.
{: note}

The managed ruleset helps protect against:

* Known DDoS attack patterns and tools
* Suspicious request behavior
* Protocol violations
* Requests that generate excessive origin errors
* Traffic floods targeting the origin or cache
* Other application-layer attack vectors

The HTTP DDoS Attack Protection managed ruleset is always enabled for all CIS customers and cannot be disabled. However, you can customize how the ruleset responds to detected attacks.

The ruleset also provides visibility into Layer 7 DDoS attacks mitigated by CIS, allowing you to review both active and historical attack activity.

## Ruleset configuration
{: #ruleset-configuration}

If you expect large volumes of legitimate traffic, you can customize the HTTP DDoS Attack Protection settings to reduce false positives, where legitimate requests are incorrectly detected as attack traffic and blocked or challenged.

You can adjust the behavior of the rules in the managed ruleset by modifying the following parameters:

* The performed **action** when an attack is detected.
* The **sensitivity level** of attack detection mechanisms.

Certain actions and sensitivity levels are available only on specific CIS plans.

Currently, you can define account-level overrides for the HTTP DDoS Attack Protection managed ruleset only through the API.
{: note}

To adjust the rule behavior, use [ruleset APIs](/apidocs/cis#get-zone-entrypoint-ruleset) with the `ddos_l7` phase.

For more information on the available configuration parameters, see [Managed ruleset parameters](/docs/cis?topic=cis-ddos-parameters).

## Availability
{: #http-ddos-availability}

The HTTP DDoS Attack Protection managed ruleset protects CIS customers on all plans and applies to all zones. Customers can configure the ruleset at both the zone level and the account level.

Customers on Enterprise plans can create up to 10 overrides (or up to 10 rules when using the API) with custom [expressions](/docs/cis?topic=cis-custom-rules-fields-and-expressions&interface=cli) to tailor DDoS protection for different categories of incoming requests.

Customers on Standard plans can create one override only and cannot customize the rule expression. In this case, the single override (containing one or more configuration settings) applies to all incoming requests.

## Parameters
{: #ddos-parameters}

Configure the HTTP DDoS Attack Protection managed ruleset to change the action that is applied to a given attack or modify the sensitivity level of the detection mechanism. 

You can [define overrides using the Rulesets API](/docs/cis?topic=cis-third-party-ddos#example-sensitivity-level-api). 

The following parameters are available in the HTTP DDoS Attack Protection managed ruleset:

* Action
* Sensitivity level

You configure these parameters by defining overrides through the Rulesets API.

The available parameters are:

* Action
* Sensitivity level

### Action
{: #ddos-action}

API property name: `action`.

The action determines how CIS handles HTTP requests that match rules in the HTTP DDoS Attack Protection managed ruleset.

| Action | API value | Description |
| ---------- | ------------ | ----------- |
| Block | `block` | Blocks HTTP requests that match the rule expression. |
| Managed Challenge | `managed_challenge` | * Managed Challenges reduce the amount of time legitimate users spend solving CAPTCHAs by dynamically selecting an appropriate challenge based on request characteristics. |
| Interactive Challenge | `challenge` | Presents an interactive challenge to clients making HTTP requests that match the rule expression. |
| Log | `log` | Available only on Enterprise plans with Advanced DDoS Protection. Logs requests that match the expression of a rule detecting HTTP DDoS attacks. Recommended for validating a rule before committing to a more severe action. |
| Connection Close | Not applicable (Internal rule action that you cannot use in overrides) | Instructs the client to establish a new connection by disabling `keep-alive`, instead of reusing the existing connection. Existing requests are not affected. |
| Force Connection Close | Not applicable (Internal rule action that you cannot use in overrides). | * Closes active HTTP connections, forcing the client to reconnect. This action does not block individual requests. \n * For HTTP/2 and HTTP/3, the connection is closed even if it affects other requests on the same connection. \n * The performed action depends on the HTTP version: \n     * HTTP/1: set the [Connection header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Connection#directives){: external} to close. \n     * HTTP/2: send a [GOAWAY frame](https://datatracker.ietf.org/doc/html/rfc7540#section-6.8){: external} to the client. |
| DDoS Dynamic | Not applicable (Internal rule action that you cannot use in overrides). | Performs a specific action according to a set of internal guidelines defined by CIS. The executed action may be one of the listed actions or another undisclosed mitigation. |
{: caption="List of available actions" caption-side="bottom"}

### Sensitivity level
{: #sensitivity-level}

API property name: `sensitivity_level`.

The sensitivity level defines how aggressively the rule detects attacks by adjusting the mitigation thresholds:

* Higher sensitivity uses lower thresholds and detects attacks more aggressively.
* Lower sensitivity uses higher thresholds and is less aggressive.

The available sensitivity levels are:

| UI value | API value |
| ---------- | ------------ |
| High | `default` |
| Medium | `medium` |
| Low	| `low` |
| Essentially Off	| `eoff` |
{: caption="Available sensitivity levels" caption-side="bottom"}

The default sensitivity level is **High**.

When you select **Essentially Off**, the rule typically does not trigger mitigation actions, including Log. However, if an attack reaches an exceptional scale, CIS protection systems will still apply mitigation to protect the CIS network.

Selecting **Essentially Off** sets an extremely low sensitivity level. In most cases, traffic is not mitigated, but exceptionally large attacks are still mitigated to maintain network stability.

Sensitivity controls whether traffic is detected as an attack. Action controls what happens when an attack is detected.

When you select **Log**, requests are logged and displayed in the dashboard without mitigation. As with Essentially Off, exceptionally large attacks are still mitigated to protect the CIS network.

## Rule categories
{: #rule-categories}

The HTTP DDoS Attack Protection managed rules are grouped into the following categories (tags) based on the type of traffic and mitigation behavior.

| Name | Description |
| ---------- | ------------ |
| `botnets` | Rules that detect requests originating from known botnets. These rules have very high detection accuracy and a low risk of false positives. It is recommended that you keep these rules enabled. |
| `unusual-requests` | Rules that identify requests with suspicious characteristics that are not commonly observed in legitimate traffic. |
| `advanced` | Rules associated with features available to Advanced DDoS Protection customers. |
| `generic` | Rules that detect and mitigate floods of requests. These rules are effective against attacks without known signatures, but they may also trigger during unusually high volumes of legitimate traffic. To reduce the risk of false positives, these rules use a higher requests-per-second (rps) activation threshold. By default, these rules rate limit or challenge traffic, but you can override them to block traffic if required. |
| `read-only` | Highly targeted rules designed to mitigate DDoS attacks with a high confidence rate. These rules are `read-only`. You cannot override their sensitivity level or action. |
| `test` | Rules used to test the detection, mitigation, and alerting capabilities of CIS DDoS protection products. |
{: caption="Available rule categories" caption-side="bottom"}

## Related links
{: #http-ddos-attack-protection-ruleset}
 
* [DDoS attack concepts](/docs/cis?topic=cis-ddos-attack-concepts)
* [Preventing DDoS attacks](/docs/cis?topic=cis-preventing-ddos-attacks)
* [Responding to DDoS attacks](/docs/cis?topic=cis-responding-to-ddos-attacks)
* [Using Defense mode for DDoS attacks](/docs/cis?topic=cis-defense-mode-attack-ddos)
* [Third-party services and DDoS protection](/docs/cis?topic=cis-third-party-ddos)
* [About DDoS protection in CIS](/docs/cis?topic=cis-about-ddos)
