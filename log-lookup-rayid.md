---

copyright:
  years: 2026
lastupdated: "2026-08-24"

keywords: Ray ID, RayID, log lookup, request logs, logpull

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Looking up logs by Ray ID
{: #log-lookup-rayid}

Enterprise accounts can retrieve the log event that is associated with a specific Ray ID. Use the Ray ID from a response to investigate a request that passed through {{site.data.keyword.cis_full_notm}}.
{: shortdesc}

## Before you begin
{: #log-lookup-rayid-prereqs}

1. Install the {{site.data.keyword.cis_short_notm}} CLI plug-in and set the context instance. For more information, see the [{{site.data.keyword.cis_short_notm}} CLI reference](/docs/cis?topic=cis-cis-cli#-cli-prereqs).

1. Enable log retention for the DNS domain. Edge logs are not retained by default.

   ```sh
   ibmcloud cis log-retention-update DNS_DOMAIN_ID --flag on
   ```
   {: pre}

When log retention is enabled, logs are retained for 7 days. For more information, see [Enabling log retention](/docs/cis?topic=cis-logpull#log-retention).

## Finding the Ray ID
{: #log-lookup-rayid-find}

The Ray ID is returned in the `cf-ray` response header for a request that passes through {{site.data.keyword.cis_short_notm}}.

If the Ray ID includes a data center suffix, such as `12ab34cdef567gh8-XXX`, remove the suffix before you look up the log. In this example, use `12ab34cdef567gh8`.
{: note}

## Looking up a log event
{: #log-lookup-rayid-lookup}

Run the following command:

```sh
ibmcloud cis log-lookup-rayid DNS_DOMAIN_ID RAY_ID [--fields FIELDS] [--timestamps FORMAT] [-i, --instance INSTANCE] [--output FORMAT]
```
{: pre}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`RAY_ID`
:   The Ray ID of the request. Required.

`--fields`
:   A comma-separated list of case-sensitive log fields to return. If this option is not specified, the service returns its default fields.

`--timestamps`
:   The format for timestamp fields. Valid values are `unix`, `unixnano`, and `rfc3339`. The default value is `unix`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

For the complete command reference, see [`ibmcloud cis log-lookup-rayid`](/docs/cis?topic=cis-cis-cli#cli-log-lookup-rayid).

### Examples
{: #log-lookup-rayid-examples}

Look up a log event and display the default table output:

```sh
ibmcloud cis log-lookup-rayid DNS_DOMAIN_ID RAY_ID
```
{: pre}

Return selected fields with RFC 3339 timestamps as JSON:

```sh
ibmcloud cis log-lookup-rayid DNS_DOMAIN_ID RAY_ID --fields RayID,ClientIP,EdgeResponseStatus --timestamps rfc3339 --output json
```
{: pre}

The JSON response is similar to the following example:

```json
{
  "ClientIP": "68.278.11.89",
  "EdgeResponseStatus": 403,
  "RayID": "48b371889c489b2c"
}
```
{: codeblock}

If the service returns no log event for the Ray ID, the command reports that the server returned an empty response for that Ray ID.
