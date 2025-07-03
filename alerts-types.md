---

copyright:
  years: 2021, 2025
lastupdated: "2025-07-03"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Alerts types
{: #types-alerts}

{{site.data.keyword.cis_short_notm}} offers the following alert types:
* **DDoS attack layer 7 alerts** are intended for WAF and CDN customers who want to receive a notification when an attack is mitigated.

   No action is necessary if you receive a DDoS attack layer 7 alert. Each alert includes a short description, the time the attack was detected and mitigated, the attack type, its maximum rate of attack, and the target.

* **Certificate alerts** include alerts that pertain to TLS certificates. The following alert types specify the renewal aspect you need.
    * **Dedicated/Advanced** receive notification for validation, issuance renewal, and expiration of Dedicated/Advanced certificates.
    * **Universal SSL** certificates are automatically refreshed and no user action is required.
    * **Mutual TLS** alert you when the mTLS certificate is expiring.
* **Logpush job alerts** alerts when the job is disabled due to consistent failures, not when a failure occurs the first time. Any impacted job destinations are included in the alert.
* **Web metrics report** is a weekly summary with reports from your account's web metrics.
* **Cloudflare maintenance report** shows scheduled, changed, or canceled Cloudflare maintenance windows.
* **Cloudflare incident report** shows ongoing Cloudflare incidents.
* **Security alerts** include WAF alerts and Advanced WAF alerts.
    * **WAF alerts** look for spikes across all services that generate log entries in firewall events. The mean time to detection is 2 hours.
    * **Advanced WAF alerts**. You can select the services to monitor, and each selected service is monitored separately. The mean time to detection is 5 minutes.
* **Load balancing health check alerts** are sent when a change occurs in the health status of a load balancing health check.
* **Pool toggle alerts** notify when the pool is enabled or disabled manually.

   No action is necessary if you receive a pool toggle alert. Each alert includes the state that the pool was toggled to, the time it occurred, and which user made the change.

## Limitation for security alerts
{: #limitations-advanced-security-events}

Security Events (WAF alerts and Advanced WAF alerts) alerts are not sent for each individual events, but only when a spike in traffic reaches the threshold for an alert to be sent.

These thresholds cannot be configured. [Z-score](https://en.wikipedia.org/wiki/Standard_score){: external} is used to determine the threshold.
