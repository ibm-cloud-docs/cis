---

copyright:
  years: 2021, 2026
lastupdated: "2026-02-20"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Alert types
{: #types-alerts}

{{site.data.keyword.cis_short_notm}} offers the following alert types:
* DDoS attack alerts include the following two types:
    * Layer 7 alerts notify WAF and CDN customers when an application-layer (L7) attack is detected and mitigated.
    * Layer 3/4 alerts are intended for customers using Range applications who want to receive a notification when an attack is mitigated.

   No action is necessary if you receive a DDoS layer 7 alert. Each alert includes a short description, the time the attack was detected and mitigated, the attack type, its maximum rate of attack, and the target.

* Certificate alerts pertain to TLS certificates. The following types relate to certificate validation, issuance, renewal, and expiration:
    * Dedicated/Advanced certificates receive notifications for validation, issuance renewal, and expiration.
    * Universal SSL certificates are automatically refreshed and no user action is required.
    * Mutual TLS alerts notify you when an mTLS certificate is expiring.
* Logpush job alerts are sent when the job is disabled due to consistent failures, not when a failure occurs for the first time. Any impacted job destinations are included in the alert.
* The Web Metrics report is a weekly summary of your account's web metrics.
* Cloudflare reports include the following alert types:
    * Maintenance alerts show scheduled, changed, or canceled Cloudflare maintenance windows.
    * Incident alerts show ongoing Cloudflare incidents.
* Security Events alerts include WAF alerts and Advanced WAF alerts.
    * WAF alerts look for traffic spikes across all services that generate firewall log entries. The mean time to detection is 2 hours.
    * Advanced WAF alerts allow you to select the services to monitor, and each selected service is monitored separately. The mean time to detection is 5 minutes.
* Bot detection alerts notify you when traffic patterns indicate a potential bot attack.
* Passive Origin Monitoring alerts notify you when CIS cannot reach the application’s origin server.
* Origin error rate alerts notify you when high levels of 5XX HTTP errors are received from the origin server.
* Load balancing health check alerts are sent when the status of a load balancing health check changes.
* Pool toggle alerts notify you when the pool is manually enabled or disabled.

   No action is necessary if you receive a pool toggle alert. Each alert includes the state that the pool was toggled to, the time it occurred, and which user made the change.

## Limitation for security alerts
{: #limitations-advanced-security-events}

The following limitations apply to security alerts, including Security Events alerts and Passive Origin Monitoring alerts.

* Security Events (WAF and Advanced WAF) alerts are not triggered for individual events. Instead, they are sent only when traffic spikes exceed the configured alert threshold. These thresholds cannot be configured. A [Z-score](https://en.wikipedia.org/wiki/Standard_score){: external} is used to determine the threshold.
* Passive Origin Monitoring alerts are not triggered for individual events. Instead, they are sent only when traffic spikes exceed the configured alert threshold. Instances configured with this alert do not receive duplicate notifications within the same four-hour window. Each alert includes the most recent list of origins returning [521 errors](/docs/cis?topic=cis-html-5xx-errors#521-error).
