---

copyright:
  years: 2026
lastupdated: "2026-10-19"

keywords: AI security, firewall for AI, LLM, prompt injection, PII detection, unsafe topics, cf-llm

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# About AI security for apps
{: #ai-security-overview}

Applications that use large language models (LLMs) are exposed to threats specific to how LLMs process input, including prompt injection attacks, PII exposure in prompts, and prompts about unsafe topics. AI Security for Apps complements your existing WAF rules with detections designed for these LLM-specific threats.
{: shortdesc}

[Endpoint Management (all plans) and AI Security for Apps](/docs/cis?topic=cis-release-notes#cis-october-1926) and its mitigation features (Enterprise plans only) are available for evaluation and testing. These features are provided at no additional charge during the beta period. To provide feedback or report issues, open a support case in the [IBM Cloud Support Center](/docs/support?topic=support-open-case&interface=ui). For IBM internal users, post in [#ibmcloud-cis](https://ibm.enterprise.slack.com/archives/C8XKQ9FPB).
{: beta}

AI Security for Apps is model-agnostic — the detections work regardless of which LLM your application uses.

## Detections
{: #ai-security-detections}

AI Security for Apps provides the following detections:

PII detection
:   Detects personally identifiable information (PII) in incoming prompts, such as phone numbers, email addresses, social security numbers, and credit card numbers.

Unsafe and custom topic detection
:   Detects prompts related to unsafe subjects such as violent crimes or hate speech, or custom topics specific to your organization.

Prompt injection detection
:   Detects prompts designed to subvert your LLM's intended behavior, such as attempts to make the model ignore its instructions or reveal its system prompt.

When enabled, AI Security for Apps scans incoming requests to endpoints labeled `cf-llm` for LLM prompts that may contain threats. Currently, detections handle only requests with a JSON content type (`application/json`).

## How AI security for apps works
{: #ai-security-how-it-works}

Based on scan results, {{site.data.keyword.cis_short}} populates AI detection fields that you can use in WAF rule expressions. You can use these fields in the following ways:

Monitor
:   Filter by the `cf-llm` label in Security Analytics to review detection results across your traffic.

Mitigate
:   Use the fields in WAF custom rules or rate-limiting rules to block or challenge requests based on detection results.

To enable AI Security scanning on an endpoint, complete the following steps:

1. Enable AI Security for Apps on your zone in the console.
2. Save the LLM-powered endpoint as an operation in Endpoint Management. See [Creating and labeling endpoint operations](/docs/cis?topic=cis-endpoint-management-creating).
3. Apply the `cf-llm` managed label to the operation so that {{site.data.keyword.cis_short_notm}} can scan its traffic for prompt injection, personally identifiable information (PII), and unsafe topics. See [Labeling endpoints](/docs/cis?topic=cis-endpoint-management-labeling#endpoint-management-cf-llm).

## Availability
{: #ai-security-availability}

AI Security for Apps capabilities are available on CIS Enterprise plans only.

| Capability | Availability |
|---|---|
| LLM endpoint discovery — Automatically identify AI-powered endpoints across your web properties | All Enterprise plans |
| AI Security Log Mode Ruleset — Pre-built ruleset that logs the full request body alongside detection results | Enterprise paid add-on |
| AI detection fields — PII detection, prompt injection scoring, unsafe topic detection, custom topics | Enterprise paid add-on |
{: caption="AI Security for Apps availability" caption-side="bottom"}

To get access to the AI Security Log Mode Ruleset and enable AI detection fields, contact your IBM Cloud account team.

The WAF must be enabled on your zone before AI detection fields can be populated and used in rule expressions.
{: important}

## Related resources
{: #ai-security-related}

- [AI Security for Apps fields](/docs/cis?topic=cis-ai-security-fields)
- [AI Security for Apps example rules](/docs/cis?topic=cis-ai-security-examples)
- [Labeling endpoints](/docs/cis?topic=cis-endpoint-management-labeling)
- [Endpoint Management overview](/docs/cis?topic=cis-endpoint-management-overview)
