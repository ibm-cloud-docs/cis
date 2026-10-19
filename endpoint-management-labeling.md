---

copyright:
  years: 2026
lastupdated: "2026-10-19"

keywords: endpoint labeling, cf-llm, managed labels, user-defined labels, API gateway labels, LLM endpoint

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Labeling endpoints
{: #endpoint-management-labeling}

The Endpoint Management labeling service helps you organize your API endpoints and identify security risks. Labels can be managed labels provided by {{site.data.keyword.cis_short}}, or user-defined labels that you create.
{: shortdesc}

[Endpoint Management (all plans) and AI Security for Apps](/docs/cis?topic=cis-release-notes#cis-october-1926) and its mitigation features (Enterprise plans only) are available for evaluation and testing. These features are provided at no additional charge during the beta period. To provide feedback or report issues, open a support case in the [IBM Cloud Support Center](/docs/support?topic=support-open-case&interface=ui). For IBM internal users, post in [#ibmcloud-cis](https://ibm.enterprise.slack.com/archives/C8XKQ9FPB).
{: beta}

## The cf-llm label and AI Security for Apps
{: #endpoint-management-cf-llm}

The `cf-llm` managed label is the critical link between Endpoint Management and AI Security for Apps. You must apply the `cf-llm` label to a saved endpoint before AI Security for Apps can scan traffic to that endpoint.

When an endpoint carries the `cf-llm` label, {{site.data.keyword.cis_short}} scans incoming requests to that endpoint for:

- Prompt injection attacks
- Personally identifiable information (PII) in prompts
- Unsafe topics such as violent crimes or hate speech

Before you apply the `cf-llm` label, you must complete the following steps:

1. Enable AI Security for Apps on your zone. For more information, see [Managing AI Security for Apps settings](/docs/cis?topic=cis-ai-security-settings).
1. Save the LLM-powered endpoint in Endpoint Management. For more information, see [About endpoint management](/docs/cis?topic=cis-endpoint-management-overview).
1. Apply the `cf-llm` label to the endpoint, as described in [Applying labels to endpoints](#endpoint-management-applying-labels).

After the label is applied, you can use `cf.llm.prompt.*` fields in WAF custom rule expressions to monitor or block LLM-specific threats. For more information, see [AI Security for Apps fields](/docs/cis?topic=cis-ai-security-fields).

## Managed labels
{: #endpoint-management-managed-labels}

Managed labels identify endpoints by use case. The following managed labels are available:

| Label | Description |
|---|---|
| `cf-llm` | **Required for AI Security for Apps.** Endpoints that are fully or partially powered by a large language model (LLM). Applying this label enables AI Security for Apps scanning on the endpoint for prompt injection, PII, and unsafe topics. |
| `cf-log-in` | Endpoints that accept user credentials. |
| `cf-sign-up` | Endpoints that are the final step in creating user accounts. |
| `cf-content` | Endpoints that provide unique content such as product details or pricing. |
| `cf-purchase` | Endpoints that are the final step in purchasing goods or services. |
| `cf-password-reset` | Endpoints that participate in the user password reset process. |
| `cf-add-cart` | Endpoints that add items to a user's shopping cart or verify item availability. |
| `cf-add-payment` | Endpoints that accept credit card or bank account details. |
| `cf-check-value` | Endpoints that check the balance of rewards points, in-game currency, or other stored value products. |
| `cf-add-post` | Endpoints that post messages in a communication forum, or product or merchant reviews. |
| `cf-account-update` | Endpoints that participate in user account or profile updates. |
| `cf-mcp` | Endpoints that implement the Model Context Protocol (MCP) for AI tool and data access. |
| `cf-rss-feed` | Endpoints that expect traffic from RSS clients. Bot Fight Mode and Super Bot Fight Mode rules do not match or challenge requests labeled `cf-rss-feed`. |
| `cf-web-page` | Endpoints that serve HTML pages. |
| `cf-contains-ads` | Endpoints that serve web pages containing advertisements. |
{: caption="Managed labels" caption-side="bottom"}

## Risk labels
{: #endpoint-management-risk-labels}

{{site.data.keyword.cis_short}} automatically runs risk scans every 24 hours on your saved endpoints and applies risk labels when a scan finds security risks. A corresponding Security Center insight is also raised when risks are found.

| Label | Description |
|---|---|
| `cf-risk-missing-auth` | All successful requests lack a session identifier. |
| `cf-risk-mixed-auth` | Some successful requests contain a session identifier and some do not. |
| `cf-risk-sensitive` | HTTP responses match the WAF Sensitive Data Detection ruleset. |
| `cf-risk-missing-schema` | A learned schema is available for an endpoint that has no active schema. |
| `cf-risk-error-anomaly` | An endpoint experienced a recent increase in response errors over the last 24 hours. |
| `cf-risk-latency-anomaly` | An endpoint experienced a recent increase in response latency over the last 24 hours. |
| `cf-risk-size-anomaly` | An endpoint experienced a spike in response body size over the last 24 hours. |
| `cf-risk-zombie` | A saved endpoint has not received traffic in 32 days. |
{: caption="Risk labels" caption-side="bottom"}

## Applying labels to endpoints
{: #endpoint-management-applying-labels}

### Apply a label to a single endpoint
{: #endpoint-management-apply-single}

1. In the {{site.data.keyword.cis_short}} console, go to **Security** > **Endpoint management**.
1. Select the **Manage endpoints** tab.
1. Choose the endpoint that you want to label.
1. Select **Edit endpoint labels**.
1. Add the labels that you want from the list of managed and user-defined labels.
1. Select **Save labels**.

## Related resources
{: #endpoint-management-labeling-related}

- [About AI Security for Apps](/docs/cis?topic=cis-ai-security-overview)
- [About endpoint management](/docs/cis?topic=cis-endpoint-management-overview)
- [Creating and labeling endpoint operations](/docs/cis?topic=cis-endpoint-management-creating)
- [Endpoint discovery](/docs/cis?topic=cis-endpoint-management-discovery)
