---

copyright:
  years: 2021, 2026
lastupdated: "2026-02-18"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Alert types
{: #types-alerts}

{{site.data.keyword.cis_short_notm}} offers the following alert types:
* **DDoS attack alerts**
    * **Layer 7 alerts** are intended for WAF and CDN customers who want to receive a notification when an attack is mitigated.
    * **Layer 3/4 alerts** are intended for customers using Range applications who want to receive a notification when an attack is mitigated.

  No action is necessary if you receive a DDoS attack layer 7 alert. Each alert includes a short description, the time the attack was detected and mitigated, the attack type, its maximum rate of attack, and the target.

* **Certificate alerts** include alerts that pertain to TLS certificates. The following alert types specify the renewal aspect you need.
    * **Dedicated/Advanced** receive notification for validation, issuance renewal, and expiration of Dedicated/Advanced certificates.
    * **Universal SSL** certificates are automatically refreshed and no user action is required.
    * **Mutual TLS** alert you when the mTLS certificate is expiring.
* **Logpush job alerts** alerts when the job is disabled due to consistent failures, not when a failure occurs the first time. Any impacted job destinations are included in the alert.
* **Web metrics report** is a weekly summary with reports from your account's web metrics.
* **Cloudflare reports**
    * **Maintenance alerts** show scheduled, changed, or canceled Cloudflare maintenance windows.
    * **Incident alerts** show ongoing Cloudflare incidents.
* **Security Events alerts** include WAF alerts and Advanced WAF alerts.
    * **WAF alerts** look for spikes across all services that generate log entries in firewall events. The mean time to detection is 2 hours.
    * **Advanced WAF alerts** You can select the services to monitor, and each selected service is monitored separately. The mean time to detection is 5 minutes.
* **Bot detection alerts** notify when detected traffic patterns may indicate a bot attack.
* **Passive Origin Monitoring alerts** notify when CIS is unable to reach the application's origin. 
* **Origin error rate alerts** are sent when high levels of 5XX HTTP errors are received from the origin server.
* **Load balancing health check alerts** are sent when a change occurs in the health status of a load balancing health check.
* **Pool toggle alerts** notify when the pool is enabled or disabled manually.

   No action is necessary if you receive a pool toggle alert. Each alert includes the state that the pool was toggled to, the time it occurred, and which user made the change.
  
## Limitation for security alerts
{: #limitations-advanced-security-events}

* Security Events (WAF alerts and Advanced WAF alerts) alerts are not sent for each individual events, but only when a spike in traffic reaches the threshold for an alert to be sent. These thresholds cannot be configured. [Z-score](https://en.wikipedia.org/wiki/Standard_score){: external} is used to determine the threshold.
* Passive Origin Monitoring alerts are not sent for each individual events, but only when a spike in traffic reaches the threshold for an alert to be sent. Instances with these alerts set up will not receive duplicate alerts within the same four-hour time frame. The alert received will contain the most recent set of origins returning [521 errors](/docs/cis?topic=cis-html-5xx-errors#521-error).
