---

copyright:
  years: 2026
lastupdated: "2026-10-19"

keywords: AI security examples, prompt injection rule, PII rule, unsafe topics rule, cf.llm, WAF custom rules

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# AI Security for apps example rules
{: #ai-security-examples}

The following examples show how to use AI Security for Apps detection fields in WAF custom rules to block, challenge, or log requests based on LLM threat detections.
{: shortdesc}

[Endpoint Management (all plans) and AI Security for Apps](/docs/cis?topic=cis-release-notes#cis-october-1926) and its mitigation features (Enterprise plans only) are available for evaluation and testing. These features are provided at no additional charge during the beta period. To provide feedback or report issues, open a support case in the [IBM Cloud Support Center](/docs/support?topic=support-open-case&interface=ui). For IBM internal users, post in [#ibmcloud-cis](https://ibm.enterprise.slack.com/archives/C8XKQ9FPB).
{: beta}

Before you use these fields, make sure that AI Security for Apps is enabled on your zone and that the relevant endpoints are labeled `cf-llm`. For more information, see [About AI Security for Apps](/docs/cis?topic=cis-ai-security-overview) and [Labeling endpoints](/docs/cis?topic=cis-endpoint-management-labeling).

## Block requests about violent or hateful content
{: #ai-security-example-unsafe-topics}

This rule blocks requests where the LLM prompt contains content about violent crimes or hate speech and returns a custom JSON error that your application can parse and display to the user.

Expression:

```text
(any(cf.llm.prompt.unsafe_topic_categories[*] in {"CHILD_SAFETY" "HATE_AND_DISCRIMINATION"}))
```
{: codeblock}

- Action: **Block**
- Response type: **Custom JSON**

Custom response body:

```json
{
  "error": "content_policy",
  "message": "Your message could not be processed because it touches on a topic outside this assistant's scope. Please rephrase your question."
}
```
{: codeblock}

Your application can check for a non-200 response and display the `message` field to the user, keeping the experience conversational instead of showing a raw block page.

## Block prompt injection from automated sources
{: #ai-security-example-prompt-injection}

This rule combines the AI Security injection score with Bot Management and the request's country to focus on high-confidence attacks from automated sources. This layered approach reduces false positives compared to using any single signal alone.

Expression:

```text
(cf.llm.prompt.injection_score lt 25 and cf.bot_management.score lt 10 and ip.src.country ne "US")
```
{: codeblock}

- Action: **Block**

The rule targets requests that are simultaneously:

- Likely prompt injection attempts (injection score below 25, where lower scores indicate higher risk)
- Coming from automated tooling, not a real browser (bot score below 10)
- Originating from outside the US — adjust the country code to match where your users are

Adjust the country code (`"US"`) to match the primary geography of your users.

## Allow financial PII only from your internal network
{: #ai-security-example-pii-internal}

A financial services application might legitimately handle credit card and bank account numbers from internal agents, but should block those PII types from external users. This rule uses the request's autonomous system number (ASN) to distinguish internal traffic from public traffic.

Expression:

```text
(any(cf.llm.prompt.pii_categories[*] in {"CREDIT_CARD" "BANK_ACCOUNT"}) and ip.src.asnum ne 13335)
```
{: codeblock}

Replace `13335` with your organization's ASN.

- Action: **Block**
- Response type: **Custom JSON**

Custom response body:

```json
{
  "error": "pii_blocked",
  "message": "Financial account information cannot be submitted from external networks. If you are an internal agent, connect to the corporate network and try again."
}
```
{: codeblock}

Internal agents on your corporate network (identified by ASN) can submit financial PII to the AI assistant as part of their workflow, while external users are blocked.

## Handle block responses in your application
{: #ai-security-example-app-error-handling}

When a WAF rule blocks a request, {{site.data.keyword.cis_short}} sends the block response back to your application, not to the end user. Your application must handle that response and decide what to display. Without error handling, users might see a raw HTML error page or a broken UI.

### Set a fallback message
{: #ai-security-example-fallback}

Define a default message that your application displays whenever it receives a non-successful response. This works regardless of how the block rule is configured.

```javascript
const FALLBACK = "Sorry, I can't process that request. Please try rephrasing.";

const resp = await fetch("/api/chat", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ prompt: userMessage }),
});

if (!resp.ok) {
  await resp.text();
  showError(FALLBACK);
  return;
}

const data = await resp.json();
showMessage(data.message);
```
{: codeblock}

### Display custom error messages from the WAF
{: #ai-security-example-custom-error}

For more control, configure your block rules with a custom JSON response. Your application can then parse the response and show the custom message when available, falling back to the default when it is not.

```javascript
const FALLBACK = "Sorry, I can't process that request. Please try rephrasing.";

const resp = await fetch("/api/chat", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ prompt: userMessage }),
});

if (!resp.ok) {
  const ct = (resp.headers.get("content-type") || "").toLowerCase();

  if (ct.includes("application/json")) {
    const data = await resp.json();
    showError(data.message || FALLBACK);
  } else {
    await resp.text();
    showError(FALLBACK);
  }
  return;
}

const data = await resp.json();
showMessage(data.message);
```
{: codeblock}

The content-type check distinguishes a custom JSON block response from the default {{site.data.keyword.cis_short}} HTML block page, which would break a JSON-based chat UI if parsed as JSON.
