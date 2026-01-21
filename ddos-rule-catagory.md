---

copyright:
  years: 2026
lastupdated: "2026-01-21"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Rule categories
{: #rule-categories}

The HTTP DDoS Attack Protection managed rules are grouped into the following categories (tags) based on the type of traffic and mitigation behavior.

| Name | Description |
| ---------- | ------------ |
| `botnets` | Rules that detect requests originating from known botnets. These rules have very high detection accuracy and a low risk of false positives. It is recommended that you keep these rules enabled. |
| `unusual-requests` | Rules that identify requests with suspicious characteristics that are not commonly observed in legitimate traffic. |
| `advanced` | Rules associated with features available to Advanced DDoS Protection customers. |
| `generic` | Rules that detect and mitigate floods of requests. These rules are effective against attacks without known signatures, but they may also trigger during unusually high volumes of legitimate traffic. To reduce the risk of false positives, these rules use a higher requests-per-second (rps) activation threshold. By default, these rules rate limit or challenge traffic, but you can override them to block traffic if required. |
| `read-only` | Highly targeted rules designed to mitigate DDoS attacks with a high confidence rate. These rules are `read-only`. You cannot override their sensitivity level or action. |
| `test` | Rules used to test the detection, mitigation, and alerting capabilities of CIS DDoS protection products. |
{: caption="Available rule catagories" caption-side="bottom"}
