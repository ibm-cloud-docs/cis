---

copyright:
  years: 2026
lastupdated: "2026-01-21"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Parameters
{: #ddos-parameters}

Configure the HTTP DDoS Attack Protection managed ruleset to change the action that is applied to a given attack or modify the sensitivity level of the detection mechanism. You can [define overrides via Rulesets API](docs/cis?topic=cis-third-party-ddos#example-sensitivity-level-api). The following parameters are available in HTTP DDos Attack Proction:

* Action
* Sensitivity Level

You can configure the HTTP DDoS Attack Protection managed ruleset to change the action that is applied when an attack is detected or to adjust the sensitivity level of the detection mechanism.

You can configure the managed ruleset by defining overrides through the Rulesets API

The available parameters are:

* Action
* Sensitivity level

## Action
{: #ddos-action}

API property name: `action`.

The action determines how CIS handles HTTP requests that match rules in the HTTP DDoS Attack Protection managed ruleset

| Action | API value | Description |
| ---------- | ------------ | ----------- |
| Block | `block` | Blocks HTTP requests that match the rule expression. |
| Managed Challenge | `managed_challenge` | * Managed Challenges help to human time spent on solving Captchas across the internet. \n * Depending on the characteristics of a request, CIS dynamically choose the appropriate type of challenge based on specific criteria. |
| Interactive Challenge | `challenge` | Presents an interactive challenge to clients making HTTP requests that match the rule expression. |
| Log | `log` | Available only on Enterprise plans with Advanced DDoS Protection. Logs requests that match the expression of a rule detecting HTTP DDoS attacks. Recommended for validating a rule before committing to a more severe action. |
| Connection Close | Not applicable (Internal rule action that you cannot use in overrides) | Instructs the client to establish a new connection by disabling `keep-alive`, instead of reusing the existing connection. Existing requests are not affected. |
| Force Connection Close | Not applicable (Internal rule action that you cannot use in overrides). | * Closes active HTTP connections, forcing the client to reconnect. This action does not block individual requests. \n * For HTTP/2 and HTTP/3, the connection is closed even if it affects other requests on the same connection. \n * The performed action depends on the HTTP version: \n     * HTTP/1: set the [Connection header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Connection#directives){: external} to close. \n     * HTTP/2: send a [GOAWAY frame](https://datatracker.ietf.org/doc/html/rfc7540#section-6.8){: external} to the client. |
| DDoS Dynamic | Not applicable (Internal rule action that you cannot use in overrides). | Performs a specific action according to a set of internal guidelines defined by CIS. The executed action may be one of the listed actions or another undisclosed mitigation. |
{: caption="Lists of available Actions" caption-side="bottom"}

## Sensitivity Level
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

When you select **Log**, requests are logged and displayed in the dashboard without mitigation. As with Essentially Off, exceptionally large attacks are still mitigated to protect the CIS network.
