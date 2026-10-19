---

copyright:
  years: 2026
lastupdated: "2026-10-19"

keywords: AI security for apps, getting started, LLM endpoint, cf-llm, PII, WAF custom rule, rate limiting, AI endpoint security

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with AI security for apps
{: #ai-security-getting-started}

Learn how to enable AI security for apps on your {{site.data.keyword.cis_full_notm}} (CIS) instance, add a large language model (LLM) endpoint, and create web application firewall (WAF) custom and rate-limiting rules to protect LLM traffic.
{: shortdesc}

[Endpoint Management (all plans) and AI Security for Apps](/docs/cis?topic=cis-release-notes#cis-october-1926) and its mitigation features (Enterprise plans only) are available for evaluation and testing. These features are provided at no additional charge during the beta period. To provide feedback or report issues, open a support case in the [IBM Cloud Support Center](/docs/support?topic=support-open-case&interface=ui). For IBM internal users, post in [#ibmcloud-cis](https://ibm.enterprise.slack.com/archives/C8XKQ9FPB).
{: beta}

AI security for apps is available only on CIS Enterprise plans. Contact your IBM Cloud account team to enable AI detection fields.
{: important}

## Before you begin
{: #ai-security-gs-prereqs}

- You must have an Enterprise CIS instance with WAF enabled.
- You must have an LLM-powered endpoint that is proxied through CIS.
- You must have Manager or Administrator access to the CIS instance.

## Enabling AI security for apps
{: #ai-security-gs-enable}
{: step}

Enable AI security for apps at the zone level. After you enable it, CIS can scan traffic for endpoints that you label with `cf-llm`.

1. In the {{site.data.keyword.cloud_notm}} console, navigate to the **Security**.
1. Select the **Endpoint management** tab.
1. Verify that **AI Security for Apps** is set to **Enabled**.

   The page displays the following tiles:

   | Tile | Description |
   |------|-------------|
   | **AI Security for Apps** | Shows whether AI security for apps is enabled. |
   | **Endpoint coverage** | Shows the number of LLM endpoints that are protected. |
   | **Custom rules** | Shows the number of LLM-specific custom rules. |
   | **Rate limiting rules** | Shows the number of LLM-specific rate-limiting rules. |
   {: caption="Endpoint management tiles" caption-side="bottom"}

## Adding an LLM endpoint
{: #ai-security-gs-add-endpoint}

Add the LLM-powered API endpoint that you want to protect. CIS might already discover the endpoint. If the endpoint appears in the list, select it. Otherwise, add the endpoint manually.

1. On the **Endpoint management** page, select the **Manage endpoints** tab.
1. Select **Add endpoints**.
1. In the **Add endpoints** panel, enter the endpoint details. To add more endpoints, select **Add**. For example:

   | Field | Example |
   |-------|---------|
   | **Method** | `POST` |
   | **Hostname** | `api.example.com` |
   | **Path** | `/v1/messages` |
   {: caption="Example LLM endpoint details" caption-side="bottom"}

1. Select **Save**. **Save** is enabled only after all rows are valid.

The endpoint appears in the **Manage endpoints** table with a **Pending** protection status.

## Protecting the LLM endpoint
{: #ai-security-gs-label-endpoint}

Apply the `cf-llm` label to the endpoint to enable AI security scanning. CIS does not scan the endpoint for LLM threats until the endpoint is labeled.

1. In the **Manage endpoints** table, find the endpoint that you added.
1. In the **Action** column, select **Protect**.

CIS applies the `cf-llm` managed label to the endpoint. The protection status changes from **Pending** to **Protected**.

After the endpoint is protected, CIS scans incoming requests to the endpoint for supported LLM threats.

## Creating a WAF custom rule to block detected PII
{: #ai-security-gs-create-rule}

Create a WAF custom rule to block requests when CIS detects PII in an LLM prompt. The rule uses AI detection fields that are available in the rule builder.

1. On the **Security** page, select the **Custom rules** tab.
1. Select **Create**.
1. In the **Create a custom rule** panel, enter an optional description, such as `Block LLM PII`.
1. Under **Details**, select **LLM PII detected** from the **Field** list.

   The following LLM fields are available for WAF custom and rate-limiting rules:

   | Field | Description |
   |-------|-------------|
   | **LLM content detected** | Indicates whether CIS detected an LLM threat in the prompt. |
   | **LLM PII categories** | Lists the PII categories that CIS detected in the prompt. |
   | **LLM PII detected** | Indicates whether CIS detected PII in the prompt. |
   | **LLM unsafe topic categories** | Lists the unsafe topic categories that CIS detected in the prompt. |
   {: caption="LLM fields available in WAF custom and rate-limiting rules" caption-side="bottom"}

1. Set **Operator** to **equals** and **Value** to **True**.

   Alternatively, select **Use expression editor** and enter the following expression:

   ```text
   cf.llm.prompt.pii_detected
   ```
   {: codeblock}

1. Set **Action** to **Block**.
1. Select **Save**.

The rule blocks requests to protected LLM endpoints when CIS detects PII in the prompt.

## Creating a rate-limiting rule for LLM traffic
{: #ai-security-gs-rate-limit}

You can also use rate-limiting rules to control LLM traffic. Rate limiting helps protect LLM endpoints from excessive requests and prompt-flood attacks.

1. On the **Security** page, select the **Rate limiting** tab.
1. Select **Create rule**.
1. In the **Create a rate limiting rule** panel, select an LLM field, such as **LLM content detected**, from the **Field** list.
1. Set the operator and value for the condition.
1. Under **When rate exceeds**, specify the request count and time period.
1. Under **Then take action**, select **Block** and specify a response type.
1. Select **Save**.

The rate-limiting rule applies the configured action when LLM traffic exceeds the specified request threshold.
