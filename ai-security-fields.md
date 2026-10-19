---

copyright:
  years: 2026
lastupdated: "2026-10-19"

keywords: AI security fields, cf.llm, LLM fields, prompt injection, PII, unsafe topics, WAF expressions

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# AI security for apps fields
{: #ai-security-fields}

AI Security for Apps populates detection fields when an endpoint labeled `cf-llm` receives a request. This topic provides the full field reference, including PII category values and unsafe topic category values that you can use in WAF custom rule expressions.
{: shortdesc}

[Endpoint Management (all plans) and AI Security for Apps](/docs/cis?topic=cis-release-notes#cis-october-1926) and its mitigation features (Enterprise plans only) are available for evaluation and testing. These features are provided at no additional charge during the beta period. To provide feedback or report issues, open a support case in the [IBM Cloud Support Center](/docs/support?topic=support-open-case&interface=ui). For IBM internal users, post in [#ibmcloud-cis](https://ibm.enterprise.slack.com/archives/C8XKQ9FPB).
{: beta}

The fields table summary is also available on the [Using fields, functions, and expressions](/docs/cis?topic=cis-fields-functions-expressions#ai-security-for-apps-fields) page alongside other CIS rule fields.

For example rules that use these fields, see [AI Security for Apps example rules](/docs/cis?topic=cis-ai-security-examples).

## PII categories
{: #ai-security-pii-categories}

The `cf.llm.prompt.pii_categories` field returns one or more of the following category strings:

| Category | Description |
|---|---|
| `BANK_ACCOUNT` | Bank account number |
| `CREDIT_CARD` | Credit card number |
| `DATE_TIME` | Date or time expression |
| `DRIVER_LICENSE` | Driver license number |
| `EMAIL_ADDRESS` | Email address |
| `IP_ADDRESS` | IPv4 address |
| `LOCATION` | Physical location or address |
| `PASSPORT` | Passport number |
| `PERSON` | Full or partial name of an individual |
| `PHONE_NUMBER` | Phone number |
| `TAX_ID` | Tax identification number |
| `URL` | URL |
| `US_SSN` | US Social Security Number |
{: caption="PII categories for cf.llm.prompt.pii_categories" caption-side="bottom"}

## Unsafe topic categories
{: #ai-security-unsafe-topic-categories}

The `cf.llm.prompt.unsafe_topic_categories` field returns one or more of the following category strings:

| Category | Description |
|---|---|
| `CHILD_SAFETY` | Content that sexualizes, exploits, abuses, grooms, or otherwise endangers minors. |
| `HATE_AND_DISCRIMINATION` | Content that attacks, demeans, discriminates against, or incites hatred toward people based on protected characteristics. This category also includes content that promotes dishonesty, manipulation, or professional misconduct. |
| `NON_VIOLENT_CRIME` | Content that encourages or facilitates nonviolent crimes, including fraud, theft, hacking, and the illegal drug trade. |
| `SELF_HARM_AND_SUICIDE` | Content that encourages, glorifies, or provides instructions for self-harm or suicide. |
| `SEXUAL_CONTENT` | Sexually explicit or suggestive content, including sexual exploitation, trafficking, assault, harassment, and other non-consensual sexual acts involving adults. |
| `VIOLENCE_AND_WEAPONS` | Content that promotes, glorifies, threatens, or provides instructions for physical violence or the acquisition, creation, or use of weapons. |
{: caption="Unsafe topic categories for cf.llm.prompt.unsafe_topic_categories" caption-side="bottom"}

## Using fields in WAF custom rules
{: #ai-security-fields-in-rules}

After AI Security for Apps is enabled on your zone and your LLM endpoints are labeled `cf-llm`, you can reference these fields in WAF custom rule expressions.

The following example expression blocks requests where a prompt injection attack is likely and the bot score is low:

```text
(cf.llm.prompt.injection_score lt 25 and cf.bot_management.score lt 10)
```
{: codeblock}

The following example expression blocks requests that contain credit card numbers or bank account numbers from external traffic:

```text
(any(cf.llm.prompt.pii_categories[*] in {"CREDIT_CARD" "BANK_ACCOUNT"}))
```
{: codeblock}

For complete rule examples with actions and response bodies, see [AI Security for Apps example rules](/docs/cis?topic=cis-ai-security-examples).
