---

copyright:
  years: 2018
lastupdated: "2019-1-4"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Domain

The following `log` commands are available:

* Retrieve edge http logs

## Retrieve edge http logs
**NAME**

   `logpull` - Retrieve edge http logs for a given DNS domain. (enterprise plan only)

**USAGE**

   `ibmcloud cis logpull DNS_DOMAIN_ID --available-fields`

   `ibmcloud cis logpull DNS_DOMAIN_ID --ray-id  RAY_ID [--fields FIELD1,FIELD2,FIELD3...]`

   `ibmcloud cis logpull DNS_DOMAIN_ID [--start START] [--end END] [--fields FIELD1,FIELD2,FIELD3...] [--count COUNT] [--sample SAMPLE]`


**ARGUMENTS**

   `DNS_DOMAIN_ID` is the id of DNS domain.

**OPTIONS**

   `--available-fields`          List of all available fields.

   `--ray-id value`              Lookup logs by specific Ray ID.

   `--fields value`              Define field set in return.
                              This must be specified as a comma separated list without any whitespaces, and all fields must exist.
                               The order in which fields are specified doesn't matter, and the order of fields in the response is not specified.
                               Note that fields are expected to be case sensitive.

   `--start value`               The (inclusive) beginning of the requested time frame.
                               This can be a unix timestamp (in seconds or nanoseconds), or an absolute timestamp that conforms to RFC 3339.
                               At this point in time, it cannot exceed a time in the past greater than 7 days.
                               Default is 65 minutes earlier.

   `--end value`                 The (exclusive) end of the requested time frame.
                               This can be a unix timestamp (in seconds or nanoseconds), or an absolute timestamp that conforms to RFC 3339.
                               The `end` must be at least 5 minutes earlier than now and must be later than `start`.
                               Difference between 'start' and 'end' must be not greater than 1h.
                               Default is 5 minutes earlier.

  `--count value`               Number of logs to retrieve. (default: -1)
  
   `--sample value`              Percentage of sampling. When sample is provided, a sample of matching records is returned.
                               If sample=0.1 then 10% of records will be returned.
                               Sampling is random: repeated calls will not only return different records, but likely will also vary slightly in number of returned records.
                               When count is also specified, count is applied to the number of returned records, not the sampled records.
                               So, with sample=0.05 and count=7, when there is a total of 100 records available, approximately 5 will be returned.
                               When there are 1000 records, 7 will be returned. When there are 10,000 records, 7 will be returned. (default: 1)

   `-i, --instance INSTANCE_NAME`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
