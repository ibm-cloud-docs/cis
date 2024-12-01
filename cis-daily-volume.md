---

copyright:
  years: 2020, 2024
lastupdated: "2024-12-01"

keywords: graphql

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Estimating daily volume
{: #volume-estimate}

To estimate your daily log volume, you can look at the relevant count of metrics for your logged datasets and fields.
{: shortdesc}

You can configure a Logpush job to analyze a single log to get the average amount of data per log. To do so, make a GraphQL query with an HTTP dataset (such as `httpRequestsAdaptiveGroups`). Then, multiply the average data per log by the average number of requests per day to get the number of requests per day. For example:

```sh
echo -n '{"ClientIP":"123.45.67.89","ClientRequestHost":"example.cis.com","ClientRequestMethod":"GET","ClientRequestURI":"/shark/sl-12345","EdgeEndTimestamp":1724947703387000000,"EdgeResponseBytes":495,"EdgeResponseStatus":200,"EdgeStartTimestamp":1724947703256000000,"RayID":"ffadcca953ea3908"}' | \
wc -c
```
{: codeblock}

The output indicates the log file is 286 bytes in size:

```
286
```
{: screen}

If the domain receives 100 KB requests daily, then the daily log volume calculation would be about 28.6 MB (286 bytes multiplied by 10,0000 requests is 28.6 MB).
