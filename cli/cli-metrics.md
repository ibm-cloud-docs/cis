---

copyright:
  years: 2018
lastupdated: "2018-05-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Metrics

The following `metrics` commands are available:

* Web analytics
* DNS analytics

## Web Analytics
### NAME:
   `web-analytics` - Get analytics of the DNS domain.

### USAGE:
   `ibmcloud cis web-analytics DNS_DOMAIN_ID [-i, --instance INSTANCE_NAME] [-s, --since TIME] [-t, --table requests | bandwidth | uniques | threats | status_code] [-o, --output OUTPUT_FILE]`

### ARGUMENTS:
   `DNS_DOMAIN_ID` is the id of DNS domain.

### OPTIONS:
   `-i, --instance`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `-s, --since `    Since time to now. Valid values are: 6h (6 hours ago), 12h, 1d (1 day ago), 1w (1 week ago), 1m (1 month ago), 3m.

   `-t, --table`     Output table. Valid values are `requests`, `bandwidth`, `uniques`, `threats` and `status_code`. If not set, it outputs all the tables.

   `-o, --output`    Output the result as JSON style to a file. If not set, it outputs the result to terminal.

#### Output Message:

  * Requests table columns
    * since
    * until
    * requests number
  * Bandwidth table columns  
    * since
    * until
    * bandwidth (B)      
  * Uniques table columns
    * since
    * until
    * unique number
  * Threats table columns
    * since
    * until
    * threats number
  * Status codes table columns
    * since
    * until
    * 200
    * 301
    * 400
    * 402
    * 404

## DNS analytics
### NAME:
   `dns-analytics` - Get DNS analytics of the domain.

### USAGE:
   `ibmcloud cis dns-analytics DNS_DOMAIN_ID DIMENSION [-i, --instance INSTANCE_NAME] [-s, --since TIME] [-o, --output OUTPUT_FILE]`

### ARGUMENTS:
   `DNS_DOMAIN_ID` is the ID of DNS domain.

   `DIMENSION` is queried dimension. The valid value is either `queries-by-response-code` or `queries-by-type`.

### OPTIONS:
   `-i, --instance`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `-s, --since` Since time to now. Valid values are: `6h` (6 hours ago), `12h`, `1d` (1 day ago), `1w` (1 week ago)

   `-o, --output`  Output the result as JSON style to a file. If not set, it outputs the result to terminal.


#### Output Message:
   * Table of queried by response code
     * since
     * until
     * queries number

   * Table of queried by query type
     * since
     * until
     * queries number
