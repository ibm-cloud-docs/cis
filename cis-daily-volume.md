---

copyright:
  years: 2020, 2024
lastupdated: "2024-10-29"

keywords: graphql

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Estimating daily volume
{: #volume-estimate}

To estimate the amount of data for a zone per day (the number of log lines and the amount of bytes they take up), request a 1% or 10% sample of data for a 1-hour period (use 10% if your volume is low). 

`start=2018-12-15T00:00:00Z` and `end=2018-12-15T01:00:00Z` span a 1-hour period, and `sample=0.1`.
{: note}

```bash
curl "https://api.cloudflare.com/client/v4/zones/{zone_id}/logs/received?start=2018-12-15T00:00:00Z&end=2018-12-15T01:00:00Z&sample=0.1" \
--header "X-Auth-Email: <EMAIL>" \
--header "X-Auth-Key: <API_KEY>" \
> sample.log
```

```bash
wc -l sample.log
```

```bash output
83 sample.log
```

```bash
ls -lh sample.log
```

```bash output
-rw-r--r-- 1 mik mik 25K Dec 17 15:49 sample.log
```

Based on this information, the approximate number of messages per day is 19,920 (83 × 10 × 24), and the byte size is 6MB (25K × 10 × 24). The size estimate is based on the default response field set. Changing the response field set will change the response size.

For an accurate estimate of daily traffic, you should get at least 30 log lines in your hourly sample. If the response size is too small (or too large), adjust the sample value, not the time range.
{: tip}
