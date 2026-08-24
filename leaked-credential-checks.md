---

copyright:
  years: 2026
lastupdated: "2026-08-24"

keywords: leaked credentials, compromised credentials, credential detection, credential stuffing

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Checking for leaked credentials
{: #leaked-credential-checks}

Enterprise accounts can configure {{site.data.keyword.cis_full_notm}} to check incoming authentication requests for username and password pairs that are known to have been compromised. You can define expressions that identify the username and password fields in your application's login requests.
{: shortdesc}

Unlike the [Exposed Credentials Check ruleset](/docs/cis?topic=cis-exposed-credentials-check-ruleset), leaked credential checks allow you to define which fields in your own login requests are checked.

## Before you begin
{: #leaked-credential-checks-prereqs}

Install the {{site.data.keyword.cis_short_notm}} CLI plug-in, set the context instance, and identify the DNS domain that receives your application's login requests. For more information, see the [{{site.data.keyword.cis_short_notm}} CLI reference](/docs/cis?topic=cis-cis-cli#-cli-prereqs).

The examples use ruleset expressions to extract values from a JSON request body. Adjust the expressions to match the structure of your application's authentication requests.

## Checking and changing the status
{: #leaked-credential-checks-status-settings}

### Checking the status
{: #leaked-credential-checks-status}

Check whether leaked credential checks are enabled for a DNS domain:

```sh
ibmcloud cis leaked-credential-checks status-get DNS_DOMAIN_ID
```
{: pre}

To return the result as JSON, specify `--output json`.

### Enabling or disabling checks
{: #leaked-credential-checks-status-update-workflow}

Enable leaked credential checks:

```sh
ibmcloud cis leaked-credential-checks status-update DNS_DOMAIN_ID --enabled true
```
{: pre}

To disable leaked credential checks, set `--enabled false`.

You can also provide the configuration as a JSON file:

```json
{
  "enabled": true
}
```
{: codeblock}

```sh
ibmcloud cis leaked-credential-checks status-update DNS_DOMAIN_ID --json @status.json
```
{: pre}

## Managing custom detections
{: #leaked-credential-checks-detections}

A custom detection contains ruleset expressions that locate the username and password in an authentication request.

### Creating a detection
{: #leaked-credential-checks-detection-create-workflow}

Create a custom detection by specifying the username and password expressions:

```sh
ibmcloud cis leaked-credential-checks detection-create DNS_DOMAIN_ID --username 'lookup_json_string(http.request.body.raw, "username")' --password 'lookup_json_string(http.request.body.raw, "password")'
```
{: pre}

Both `--username` and `--password` are required when you create a detection by using command options.

You can also provide the detection as a JSON file:

```json
{
  "username": "lookup_json_string(http.request.body.raw, \"username\")",
  "password": "lookup_json_string(http.request.body.raw, \"password\")"
}
```
{: codeblock}

```sh
ibmcloud cis leaked-credential-checks detection-create DNS_DOMAIN_ID --json @detection.json --output json
```
{: pre}

Save the returned detection ID. You need it to retrieve, update, or delete the detection.

### Listing and retrieving detections
{: #leaked-credential-checks-detection-get-workflow}

List all custom detections for a DNS domain:

```sh
ibmcloud cis leaked-credential-checks detection-list DNS_DOMAIN_ID
```
{: pre}

Retrieve a specific detection:

```sh
ibmcloud cis leaked-credential-checks detection-get DNS_DOMAIN_ID DETECTION_ID
```
{: pre}

### Updating a detection
{: #leaked-credential-checks-detection-update-workflow}

Update one or both expressions in an existing detection. The following example changes the username expression:

```sh
ibmcloud cis leaked-credential-checks detection-update DNS_DOMAIN_ID DETECTION_ID --username 'lookup_json_string(http.request.body.raw, "email")'
```
{: pre}

You can also provide the updated fields as a JSON file:

```sh
ibmcloud cis leaked-credential-checks detection-update DNS_DOMAIN_ID DETECTION_ID --json @detection.json
```
{: pre}

### Deleting a detection
{: #leaked-credential-checks-detection-delete-workflow}

Delete a custom detection:

```sh
ibmcloud cis leaked-credential-checks detection-delete DNS_DOMAIN_ID DETECTION_ID
```
{: pre}

The command prompts you to confirm the deletion. To delete the detection without a confirmation prompt, specify `--force`.
