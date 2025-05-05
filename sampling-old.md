---

copyright:
  years: 2025
lastupdated: "2025-03-18"

keywords: graphql, metrics, sampling

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Sampling
{: #sampling}

In a small number of cases, the metrics provided in the CIS dashboard and GraphQL API are based on a **sample** — a subset of the dataset. In these cases, CIS metrics returns an estimate derived from the sampled value. For example, suppose that during an attack the sampling rate is 10% and 5,000 events are sampled. CIS will estimate 50,000 total events (5,000 × 10) and report this value.

## Sampled datasets
{: #sampled-datasets}

CIS GraphQL API exposes datasets that powered by adaptive sampling. These nodes have **Adaptive** in the name and can be discovered through [introspection](https://graphql.org/learn/introspection/){: external}.

## Why sampling is applied
{: #why-sampling-is-applied}

The CIS metrics are designed to provide requested data, at the appropriate level of detail, as quickly as possible. Sampling allows CIS to deliver these metrics within seconds, even when datasets scale quickly and unpredictably, such as a burst of firewall events generated during an attack. And because the volume of underlying data is large, the value estimated from the sample should still be statistically significant – meaning you can rely on sampled data with a high degree of confidence. Without sampling, it might take several minutes or longer to answer a query — a long time to wait when validating mitigation efforts.

## Types of sampling
{: #types-of-sampling}

### Adaptive sampling
{: #adaptive-sampling}

CIS almost always uses **adaptive sampling**, which means the sample rate fluctuates depending on the volume of data ingested or queried. If the number of records is relatively small, sampling is not used. However, as the volume of records grows larger, progressively lower sample rates are applied. Security Events (also known as Firewall Events) and the Security Event Log follow this model. Data nodes that use adaptive sampling are easy to identify by the `Adaptive` suffix in the node name, as in `firewallEventsAdaptive`.

### Fixed sampling
{: #fixed-sampling}

The following data nodes are based on fixed sampling, where the sample rate does not vary:

| Dataset | Rate | Notes  |
| ----- | ----- | ----- |  
| Firewall Rules Preview \n \n **Nodes:** `firewallRulePreviewGroups` | 1% | Use with caution. A 1% sample rate does not provide accurate estimates for datasets smaller than a certain threshold, a scenario the CIS dashboard calls out explicitly but the API does not. |
| Network metrics \n \n **Nodes:** \n \n `ipFlows1mGroups` \n `ipFlows1hGroups` \n `ipFlows1dGroups` \n `ipFlows1mAttacksGroups`| 0.012% | Sampling rate is in terms of packet count (1 of every 8,192 packets). |   
{: caption="Fixed sampling" caption-side="bottom"}   

## Access to raw data
{: #access-to-raw-data}

Because sampling is primarily adaptive and automatically adjusts to provide an accurate estimate, the sampling rate cannot be directly controlled. Enterprise customers have access to raw data through [CIS logs](/docs/cis?topic=cis-logpush).
