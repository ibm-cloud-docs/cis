---

copyright:
  years: 2025
lastupdated: "2025-05-01"

keywords: graphql, metrics, sampling

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# About sampling
{: #about-sampling}

Sampling is a technique used in CIS metrics to analyze a subset of data rather than processing every individual data point. It helps maintain performance and scalability while delivering accurate insights. Given the volume of data CIS handles—over 700 million events per second—sampling is essential for fast, cost-effective metrics at scale.
{: shortdesc}

In some cases, metrics provided in the CIS dashboard and GraphQL API are based on a sample. For example, if during an attack the sampling rate is 10% and 5,000 events are sampled, CIS will estimate the total number of events as 50,000 (5,000 × 10) and report this value.

CIS primarily uses adaptive sampling, including a method called Adaptive Bit Rate (ABR). ABR adjusts the level of detail in the data returned based on query complexity and volume. When the number of records is small or the query is simple, full-resolution data (100%) is used. As the dataset grows or the query becomes more complex, progressively lower sample rates—such as 10% or 1%—are applied to ensure efficient query completion.

This approach prevents large queries from consuming excessive computing resources, ensuring fair distribution and consistent performance for all users. Data is stored at multiple resolutions (100%, 10%, and 1%), allowing the system to select the appropriate resolution based on the query’s complexity and size, helping ABR deliver fast, accurate results.
 
## Why sampling is applied
{: #why-sampling-applied} 

CIS metrics are designed to deliver data at the appropriate level of detail as quickly as possible. Sampling helps achieve this by reducing the amount of data processed, allowing CIS to return metrics within seconds—even during spikes in volume, such as a burst of firewall events during an attack. Without sampling, queries could take minutes or more to complete, which is too long when validating mitigation efforts or troubleshooting issues.

CIS processes over 700 million events per second across its global network. Storing and processing all this data in real-time would be prohibitively expensive and time-consuming. Sampling balances precision with performance, ensuring fast, scalable, and cost-efficient metrics. Given the large scale of the datasets, sampled values are statistically significant, providing reliable and actionable insights.

This approach is similar to other domains:

* Google Maps: Lower-resolution imagery when zoomed out mirrors how CIS adjusts sampling rates to deliver fast, relevant insights based on query size.
* Opinion Polls: A small, representative sample can reflect system-wide trends.
* Movie Frames: Viewing at 30 fps instead of 60 fps still tells the full story—similarly, sampling maintains the key patterns in your data.

While ABR sampling resolution isn’t always visible, the number of rows read is a good indicator: the more rows read, the higher the resolution and reliability of the results.

## Additional considerations
{: #additional-considerations-sampling}
 
When sampling occurs

:   Sampling is typically applied to very high-traffic datasets where full data analysis would be impractical.
    For smaller datasets, full data analysis is often performed without sampling.

Sampling rates

:   Sampling rates vary depending on the dataset and product. CIS ensures that sampling rates are consistent within a single dataset to maintain accuracy across queries.

Impact on metrics

:   While sampling reduces the volume of processed data, aggregated metrics like totals, averages, and percentiles are extrapolated based on the sample size. This ensures the reported metrics represent the entire dataset accurately.

Limitations

:   Sampling might not capture extremely rare events with very low occurrence rates.

Sampling in metrics interfaces

:   GraphQL API: Sampling metadata is included in the query response. For more information, refer to the sampling [GraphQL Analytics API] documentation.
:   Workers Analytics Engine: For more information, refer to the [Workers Analytics Engine] documentation.
:   Dashboard Analytics: Displays an icon with the sampled percentage of data, if sampled data was used for the visualization.

## Sampled datasets
{: #sampled-datasets}

CIS GraphQL API exposes datasets that powered by adaptive sampling. These nodes have **Adaptive** in the name and can be discovered through [introspection](https://graphql.org/learn/introspection/){: external}. 

## Types of sampling
{: #types-of-sampling}

### Adaptive sampling
{: #adaptive-sampling}

CIS metrics primarily relies on **adaptive sampling**, which means the sample rate fluctuates depending on the volume of data ingested or queried. If the number of records is relatively small, sampling is typically not used, allowing full data to be returned. However, as the volume of records increases, progressively lower sample rates are applied to maintain performance and responsiveness.

This model is used in several data sources, including Security Events (also known as Firewall Events) and the Security Event Log. Data nodes that use adaptive sampling are easy to identify by the `Adaptive` suffix in the node name, as in `firewallEventsAdaptive`.

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
