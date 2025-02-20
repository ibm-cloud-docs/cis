---

copyright:
  years: 2024, 2025
lastupdated: "2025-02-20"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Exposed Credentials Check rule set
{: #exposed-credentials-check-ruleset}

The Exposed Credentials Check ruleset (part of Managed Rules) is a set of pre-configured rules for content management system applications that check against a public database of stolen credentials. When enabled in a rule, exposed credentials checking occurs when the rule expression evaluates to `true`.

The WAF checks the username and password pair in the request against a public database of known stolen credentials. When both the rule expression and the exposed credentials check are `true`, the rule match triggers the action that is configured in the rule.

The WAF can perform one of the following actions when it detects exposed credentials.

* **Exposed-Credential-Check Header:** Adds a HTTP header to HTTP requests with exposed credentials. Your application at the origin can then force a password reset, start a two-factor authentication process, or any other action. The `Exposed-Credential-Check` HTTP header is added with a value of `1`.
* **Managed Challenge:** Helps reduce the lifetimes of human time spent solving CAPTCHAs across the internet. Depending on the characteristics of a request, {{site.data.keyword.cis_short_notm}} dynamically chooses the appropriate type of challenge.
* **Block:** Blocks HTTP requests containing exposed credentials.
* **JS Challenge:** Presents a noninteractive challenge to the clients who are making HTTP requests with exposed credentials.
* **Log:** (Enterprise only) Logs requests with exposed credentials in the logs. Logging is recommended for validating a rule before you commit to a more severe action.
* **Interactive Challenge:** Presents an interactive challenge to the clients who are making HTTP requests with exposed credentials.

The default action for the rules in the Exposed Credentials Check managed ruleset is `Exposed-Credential-Check Header` (named `rewrite` in the API).

The best practice is to use only the `Exposed-Credential-Check Header` (`rewrite` in the API) and `Log` (`log`).
