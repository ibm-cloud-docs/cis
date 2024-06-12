---

copyright:
  years: 2018, 2024
lastupdated: "2024-05-08"

keywords: 

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Using the {{site.data.keyword.cis_short_notm}} Security Events capability
{: #using-the-cis-security-events-capability}

Reviewing Security Events gives you insight into your web traffic and into any potentially malicious activity against your website. Reviewing Security Events also helps you optimize your WAF configuration.
{: shortdesc}


## The {{site.data.keyword.cis_short_notm}} Security Events Table
{: #cis-security-events-table}

The Security Events Table shows you detailed information about web requests that are blocked by the WAF. Each entry shows one blocked request.
* **Triggered rule** indicates which rule blocked the request. Any of the following actions is available:
    * **Block**: A hard block.
    * **Challenge**: A CAPTCHA page that humans can bypass.
    * **Simulate**: A request that is allowed through normally, but is logged.

Sometimes the triggered rule is not identified. In this case the UI shows a `-` instead of the rule ID.
* **IP Address**: Shows the source IP address of the web request.
* **Location**: Shows the country associated with the source IP of the web request.
* **Host**: Shows the hostname of the server that has been reached by the web request.
* **Date**: Shows the day the event occurred.


## {{site.data.keyword.cis_short_notm}} Security Events Details
{: #cis-security-events-details}

When viewing Security Events, you can click the arrow on an event to expand the details for that event.
One section of your screen shows the event details, along with the Ray-Id. The other section shows request details such as Header, URI, Protocol, the type of firewall that blocked the request, and User Agent.

Suppose, for example, you see that the triggered rule for an event has an ID of `981176`. This means that the block was caused by OWASP. When any rules in the OWASP rule set is matched, the “threat score” of the request increases. The **Paranoia level** setting (`P1` to `P4`) for your zone translates to a threshold. If the cumulative score of all the matched OWASP rules exceeds that threshold, rule `981176` is triggered and blocks the request.

This means that all requests blocked by OWASP show on your Security Events as blocked by `981176`. Expand the event details and view the **Event Triggers** section to see the individual OWASP rules that matched to increase the request’s threat score.

## What do I do if valid traffic is blocked?
{: #what-do-i-do-if-valid-traffic-is-blocked}

Expand each event to see event details. The **Event Triggers** section displays all the individual OWASP rules that matched for OWASP rule-triggered events. Decide whether this traffic looks normal for your website, or if it was appropriately blocked. If you decide that this block is a false positive, you can go back to your WAF configuration and disable individual OWASP rules until this request no longer exceeds your sensitivity threshold.

## Security event retention policy
{: #retention-policy}

Enterprise plans retain security events for 90 days. Standard plans retain security events for 30 days. 

