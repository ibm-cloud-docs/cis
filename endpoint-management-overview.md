---

copyright:
  years: 2026
lastupdated: "2026-10-19"

keywords: endpoint management, API gateway, API operations, endpoint discovery, endpoint labeling, sensitive data detection

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# About endpoint management
{: #endpoint-management-overview}

Endpoint Management provides a unified inventory for managing API endpoints in your {{site.data.keyword.cis_short}} zone. An LLM endpoint represents an endpoint identified by its HTTP method, hostname pattern, and path pattern.
{: shortdesc}

[Endpoint Management (all plans) and AI Security for Apps](/docs/cis?topic=cis-release-notes#cis-october-1926) and its mitigation features (Enterprise plans only) are available for evaluation and testing. These features are provided at no additional charge during the beta period. To provide feedback or report issues, open a support case in the [IBM Cloud Support Center](/docs/support?topic=support-open-case&interface=ui). For IBM internal users, post in [#ibmcloud-cis](https://ibm.enterprise.slack.com/archives/C8XKQ9FPB).
{: beta}

{{site.data.keyword.cis_short}} continuously discovers endpoints from your zone's traffic and adds them to the inventory. You can also add endpoints manually. Endpoint Management is available from **Security** > **Endpoint management** in the {{site.data.keyword.cis_short}} console.

Endpoint Management is required for AI Security for Apps. To enable AI Security scanning on an endpoint, you must save it as an endpoint and apply the `cf-llm` managed label. For more information, see [Labeling endpoints](/docs/cis?topic=cis-endpoint-management-labeling) and [About AI Security for Apps](/docs/cis?topic=cis-ai-security-overview).

## LLM endpoints
{: #endpoint-management-llm}

An LLM endpoint is the core unit in endpoint management. Each endpoint is uniquely identified by the combination of its HTTP method, hostname pattern, and path pattern. {{site.data.keyword.cis_short}} computes an endpoint ID from these three values. Changing any of these values creates a different endpoint ID.

Endpoints support variable fields in path and hostname patterns. Variable segments are enclosed in braces, such as `/api/user/{var1}/details`. Supported hostname variable formats include `{hostVar1}.example.com` and `foo.{hostVar1}.example.com`. Hostname variables must comprise the entire domain segment and cannot be combined with other text in the same field.

Endpoints can be in two states:

Candidate
:   Endpoints that {{site.data.keyword.cis_short}} has discovered but that have not been promoted. Candidate endpoints can provide context for matching, edge security detections, and Sequence Analytics without any further action required.

Saved
:   Endpoints that have been promoted or added manually. Saved endpoints are tracked for performance metrics and are eligible for profile learning, labeling, and sensitive data detection.

## Endpoint discovery
{: #endpoint-management-discover}

{{site.data.keyword.cis_short}} continuously identifies endpoints from observed traffic and adds them to the inventory as candidate endpoints. Discovery does not start profile learning. Discovered candidates can provide context for matching and security detections without being promoted.

For more information, see [Endpoint discovery](/docs/cis?topic=cis-endpoint-management-discovery).

## Endpoint analysis
{: #endpoint-management-analysis}

For each saved endpoint, {{site.data.keyword.cis_short}} tracks the following metrics, viewable for the last 24 hours or seven days:

Request count
:   The total number of requests to the endpoint over time.

Rate limiting recommendation
:   A recommended rate limit per 10 minutes, guided by the observed request count.

Latency
:   The average origin response time in milliseconds, measured from when a request is made to when a response is received from the origin.

Error rate
:   The error rate compared to overall traffic, grouped by 4xx errors, 5xx errors, and their combined sum.

Response size
:   The average size of the response in bytes returned to the request.

Labels
:   The current labels assigned to the endpoint.

Authentication status
:   The session identifiers observed on successful requests to the endpoint.

Sequences
:   The number of Sequence Analytics sequences that contain the endpoint.

## Sensitive data detection
{: #endpoint-management-sensitive-data}

Sensitive Data Detection alerts you when HTTP response bodies from saved endpoints contain personally identifiable information or financial data. {{site.data.keyword.cis_short}} queries WAF events from the last seven days and marks endpoints that have matched sensitive responses.

Sensitive data detection is available to Enterprise customers on the Advanced application security plan. Your zone must also have the Sensitive Data Detection managed ruleset enabled.
{: note}

## Limitations
{: #endpoint-management-limitations}

Certain performance metrics, such as latency, are not supported when a request is handled by a {{site.data.keyword.cis_short}} service in a way that prevents it from being passed directly to your origin server. In these cases, the origin response time cannot be accurately measured and the metric is not populated in the dashboard.

This limitation applies in the following scenarios:

- An Edge Function is running on the URL path.
- A product built on Edge Functions, such as Waiting Room, is active on the application.

## Related resources
{: #endpoint-management-overview-related}

- [Creating and labeling endpoint operations](/docs/cis?topic=cis-endpoint-management-creating)
- [Labeling endpoints](/docs/cis?topic=cis-endpoint-management-labeling)
- [Endpoint discovery](/docs/cis?topic=cis-endpoint-management-discovery)
- [About AI Security for Apps](/docs/cis?topic=cis-ai-security-overview)
