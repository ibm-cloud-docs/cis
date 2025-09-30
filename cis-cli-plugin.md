---

copyright:
  years: 2018, 2025
lastupdated: "2025-09-30"

keywords:

subcollection: cis

---


{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.cis_short_notm}} CLI reference
{: #cis-cli}

{{site.data.keyword.cis_full}} has several families of commands that are available from the command line interface (CLI). Find the full set of commands for {{site.data.keyword.cis_full_notm}} ({{site.data.keyword.cis_short_notm}}) within each set, such as `Create`, `Delete`, and `Update`.
{: shortdesc}

## Before you begin
{: #-cli-prereqs}

1. Download the [IBM CLI](/docs/cli?topic=cli-getting-started#getting-started).
1. Log in to IBM Cloud.

   ```sh
   ibmcloud login -a
   ```
   {: pre}

1. Install the CIS CLI plug-in.

   ```sh
   ibmcloud plugin install cis
   ```
   {: pre}

1. Set the context instance.

   ```sh
   ibmcloud cis instance-set <instance-name>
   ```
   {: pre}


To see a list of plug-ins and which versions are installed, run this command.

```sh
ibmcloud plugin list
```
{: pre}

The list returns whether the CLI has any updates available. Run the following command to update the CIS CLI plug-in.

```sh
ibmcloud plugin update cis
```
{: pre}

To learn about installing and configuring the IBM Cloud CLI, see [Getting started with the IBM Cloud CLI](/docs/cli?topic=cli-getting-started).

## Access application
{: #access-application-cli-ref}

### `ibmcloud cis access-app-create`
{: #access-app-create}

[Enterprise Plans Only]{: tag-blue}

Create an access application for a DNS domain.

```sh
ibmcloud cis access-app-create DNS_DOMAIN_ID --name NAME --domain DOMAIN [--session-duration SESSION_DURATION] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #command-options-access-app-create}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #command-example-access-app-create}

Create an access application for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis access-app-create 31984fea73a15b45779fa0df4ef62f9b --name exampleCreate --domain example.com --session-duration 12h -i cis-demo
```
{: pre}

### `ibmcloud cis access-apps`
{: #access-apps}

[Enterprise Plans Only]{: tag-blue}

List all access applications for a DNS domain.

```sh
ibmcloud cis access-apps DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #command-options-access-apps}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #command-example-access-apps}

List all access applications for domains `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis access-apps 31984fea73a15b45779fa0df4ef62f9b -i cis-demo
```
{: pre}

### `ibmcloud cis access-app`
{: #access-app}

[Enterprise Plans Only]{: tag-blue}

Show details of an access application.

```sh
ibmcloud cis access-app DNS_DOMAIN_ID ACCESS_APPLICATION_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #command-options-access-app}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`ACCESS_APPLICATION_ID`
:   The ID of the access application. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #command-example-access-app}

Show details of access application `a5836c2a7ea72d2e225890caea70ae32`.

```sh
ibmcloud cis access-app 31984fea73a15b45779fa0df4ef62f9b a5836c2a7ea72d2e225890caea70ae32 -i cis-demo
```
{: pre}

### `ibmcloud cis access-app-update`
{: #access-app-update}

[Enterprise Plans Only]{: tag-blue}

Update an access application.

```sh
ibmcloud cis access-app-update DNS_DOMAIN_ID ACCESS_APPLICATION_ID --name NAME --domain DOMAIN [--session-duration SESSION_DURATION] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #command-options-access-app-update}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`ACCESS_APPLICATION_ID`
:   The ID of the access application. Required.

`--name`
:   The name of the Application. Required.

`--domain`
:   The domain and path that Access blocks. Required.

`--session-duration`
:   Defines the amount of time that the tokens issued for this application are valid. Valid values are `30m`, `6h`, `12h`, `24h`, `168h`, and `730h`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #command-example-access-app-update}

Update access application `a5836c2a7ea72d2e225890caea70ae32`.

```sh
ibmcloud cis access-app-update 31984fea73a15b45779fa0df4ef62f9b a5836c2a7ea72d2e225890caea70ae32 --name exampleUpdate --domain example.com --session-duration 24h -i cis-demo
```
{: pre}

### `ibmcloud cis access-app-delete`
{: #access-app-delete}

[Enterprise Plans Only]{: tag-blue}

Delete an access application.

```sh
ibmcloud cis access-app-delete DNS_DOMAIN_ID ACCESS_APPLICATION_ID [-i, --instance INSTANCE]
```

#### Command options
{: #command-options-access-app-delete}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`ACCESS_APPLICATION_ID`
:   The ID of the access application. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #command-example-access-app-delete}

Delete access application `a5836c2a7ea72d2e225890caea70ae32`.

```sh
ibmcloud cis access-app-delete 31984fea73a15b45779fa0df4ef62f9b a5836c2a7ea72d2e225890caea70ae32 -i cis-demo
```
{: pre}

## Access certificate
{: #access-certificate-cli-ref}

### `ibmcloud cis access-certificate-create`
{: #access-certificate-create}

[Enterprise Plans Only]{: tag-blue}

Create an access certificate for a DNS domain.

```sh
ibmcloud cis access-certificate-create DNS_DOMAIN_ID --name NAME --ca-cert-file CERT_FILE [--associated-hostnames ASSOCIATED_HOSTNAMES] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #options-access-cert-create}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--name`
:   The name of the Certificate. Required.

`--ca-cert-file`
:   The Root CA file for your certificates. Required.

`--associated-hostnames`
:   The hostnames that are prompted for this certificate.

`ACCESS_APPLICATION_ID`
:   The ID of the access application.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #example-access-cert-create}

Create an access certificate for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis access-certificate-create 31984fea73a15b45779fa0df4ef62f9b --name example --ca-cert-file CERT_FILE --associated-hostnames example.com  -i cis-demo
```
{: pre}

### `ibmcloud cis access-certificates`
{: #access-certificates}

[Enterprise Plans Only]{: tag-blue}

List all access certificates for a DNS domain.

```sh
ibmcloud cis access-certificates DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #command-options-access-certificates}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #example-access-certs}

List all access certificates for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis access-certificates 31984fea73a15b45779fa0df4ef62f9b -i cis-demo
```
{: pre}

### `ibmcloud cis access-certificate`
{: #access-certificate}

[Enterprise Plans Only]{: tag-blue}

Show details of an access certificate.

```sh
ibmcloud cis access-certificate DNS_DOMAIN_ID ACCESS_CERTIFICATE_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #command-options-access-certificate}


`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`ACCESS_CERTIFICATE_ID`
:   The ID of the access certificate. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #example-access-cert}

Show details of access certificate `a5836c2a7ea72d2e225890caea70ae32`.

```sh
ibmcloud cis access-certificate 31984fea73a15b45779fa0df4ef62f9b a5836c2a7ea72d2e225890caea70ae32 -i cis-demo
```
{: pre}

### `ibmcloud cis access-certificate-update`
{: #access-certificate-update}

[Enterprise Plans Only]{: tag-blue}

Update an access certificate.

```sh
ibmcloud cis access-certificate-update DNS_DOMAIN_ID ACCESS_CERTIFICATE_ID --name NAME --associated-hostnames ASSOCIATED_HOSTNAMES [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #options-access-cert-update}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`ACCESS_CERTIFICATE_ID`
:   The ID of the access certificate. Required.

`--name`
:   The name of the Certificate. Required.

`--associated-hostnames`
:  The hostnames that are prompted for this certificate. Required.

   The associated hostnames are reset if not specified by `associated-hostnames`.
   {: note}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #example-update-access-cert}

Update the access certificate `a5836c2a7ea72d2e225890caea70ae32`.

```sh
ibmcloud cis access-certificate-update 31984fea73a15b45779fa0df4ef62f9b a5836c2a7ea72d2e225890caea70ae32 --name example  --associated-hostnames example.com -i cis-demo
```
{: pre}

### `ibmcloud cis access-certificate-delete`
{: #access-certificate-delete}

[Enterprise Plans Only]{: tag-blue}

Delete an access certificate.

```sh
ibmcloud cis access-certificate-delete DNS_DOMAIN_ID ACCESS_CERTIFICATE_ID [-i, --instance INSTANCE]
```

Must clear the associated hostnames before you delete the certificate.
{: note}

#### Command options
{: #command-options-access-certificate-delete}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`ACCESS_CERTIFICATE_ID`
:   The ID of the access certificate. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #example-acc-cert-delete}

Delete the access certificate `a5836c2a7ea72d2e225890caea70ae32`.

```sh
ibmcloud cis access-certificate-delete 31984fea73a15b45779fa0df4ef62f9b a5836c2a7ea72d2e225890caea70ae32 -i cis-demo
```
{: pre}

### `ibmcloud cis access-certificates-settings`
{: #access-certificates-settings}

[Enterprise Plans Only]{: tag-blue}

Get access certificates settings for a DNS domain.

```sh
ibmcloud cis access-certificates-settings DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #command-options-access-certificates-settings}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #example-access-certificates-settings}

Get access certificates settings for Domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis access-certificates-settings 31984fea73a15b45779fa0df4ef62f9b -i cis-demo
```
{: pre}

### `ibmcloud cis access-certificates-settings-update`
{: #access-certificates-settings-update}

[Enterprise Plans Only]{: tag-blue}

Update access certificates settings for a DNS domain.

```sh
ibmcloud cis access-certificates-settings-update DNS_DOMAIN_ID (-f, --feature FEATURE) (-v, --value VALUE) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #command-options-access-certificates-settings-update}


`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-f, --feature`
:   Feature of certificates settings. Valid values:

`client_certificate_forwarding`
:   The client certificate payload and its SHA256 signature are forwarded to origin servers through `CF-Client-Cert-DER_BASE64` and `CF-Client-Cert-SHA256` headers.

`-v, --value`
:   The value set to the feature for certificates.

`client_certificate_forwarding`
:   Specify the hostname to forward the client certificate or not. For example, `-v host1=on,host2=on,host3=off`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #example-access-certificates-settings-update}

Update access certificates settings for Domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis access-certificates-settings-update 31984fea73a15b45779fa0df4ef62f9b -f client_certificate_forwarding -v mtls1.example.com=on,mtls2.example.com=off -i cis-demo
```
{: pre}

## Access policy
{: #access-policy-cli-ref}

### `ibmcloud cis access-policy-create`
{: #access-policy-create}

[Enterprise Plans Only]{: tag-blue}

Create an access policy for an access application.

```sh
ibmcloud cis access-policy-create DNS_DOMAIN_ID ACCESS_APPLICATION_ID --name NAME --decision DECISION --include INCLUDE [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #command-options-access-policy-create}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`ACCESS_APPLICATION_ID`
:   The ID of the access application. Required.

`--name`
:   The name of the policy. Required.

`--decision`
:   Defines the action Access takes if the policy matches the user. Valid value is `non_identity`. Required.

`--include`
:   The included rule of the policy. Valid values are `certificate` and `common_name`. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #command-example-access-policy-create}

Create an access policy for access application `a5836c2a7ea72d2e225890caea70ae32`.

```sh
ibmcloud cis access-policy-create 31984fea73a15b45779fa0df4ef62f9b a5836c2a7ea72d2e225890caea70ae32 -name examplePolicy --decision non_identity --include certificate  --include common_name=test -i cis-demo
```
{: pre}

### `ibmcloud cis access-policies`
{: #access-policies}

[Enterprise Plans Only]{: tag-blue}

List all access policies for an access application.

```sh
ibmcloud cis access-policies DNS_DOMAIN_ID ACCESS_APPLICATION_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #command-options-access-policies}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`ACCESS_APPLICATION_ID`
:   The ID of the access application. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #command-example-access-policies}

List all access policies for access application `a5836c2a7ea72d2e225890caea70ae32`.

```sh
ibmcloud cis access-policies 31984fea73a15b45779fa0df4ef62f9b a5836c2a7ea72d2e225890caea70ae32 -i cis-demo
```
{: pre}

### `ibmcloud cis access-policy`
{: #access-policy}

[Enterprise Plans Only]{: tag-blue}

Show details of an access policy.

```sh
ibmcloud cis access-policy DNS_DOMAIN_ID ACCESS_APPLICATION_ID ACCESS_POLICY_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #command-options-access-policy}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`ACCESS_APPLICATION_ID`
:   The ID of the access application. Required.

`ACCESS_POLICY_ID`
:   The ID of access policy. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #command-example-access-policy}

Show details of access policy `a5836c2a7ea72d2e225890caea70ae32`.

```sh
ibmcloud cis access-policy 31984fea73a15b45779fa0df4ef62f9b a5836c2a7ea72d2e225890caea70ae32 65fe21071877669cc69544642bc6c4c4 -i cis-demo
```
{: pre}

### `ibmcloud cis access-policy-delete`
{: #access-policy-delete}

[Enterprise Plans Only]{: tag-blue}

Delete an access policy.

```sh
ibmcloud cis access-policy-delete DNS_DOMAIN_ID ACCESS_APPLICATION_ID ACCESS_POLICY_ID [-i, --instance INSTANCE]
```

#### Command options
{: #command-options-access-policy-delete}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`ACCESS_APPLICATION_ID`
:   The ID of the access application. Required.

`ACCESS_POLICY_ID`
:   The ID of access policy. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #command-example-access-policy-delete}

Delete access policy `65fe21071877669cc69544642bc6c4c4`.

```sh
ibmcloud cis access-policy-delete 31984fea73a15b45779fa0df4ef62f9b a5836c2a7ea72d2e225890caea70ae32 65fe21071877669cc69544642bc6c4c4 -i cis-demo
```
{: pre}

## Cache
{: #cache}

Manipulate how the cache performs by using the following `cache` commands:

### `ibmcloud cis cache-purge`
{: #purge-cache}

Clear the cached assets file by file or entirely for a DNS domain to guarantee that the served assets are updated.

```sh
ibmcloud cis cache-purge DNS_DOMAIN_ID (--all | --file file1 --file file2...｜--tag tag1 --tag tag2...|--host host1 --host host...| --prefix prefix1 --prefix prefix2...) [-f, --force] [-i, --instance INSTANCE_NAME]  [--output FORMAT]
```

#### Command options
{: #purge-cache-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--all`
:   Purging all cached files. This option is mutually exclusive with *--file*.

`--file`
:   Granularly remove one or more files by specifying URLs. This option is mutually exclusive with *--all*.

`--tag`
:   Granularly remove one or more files by the associated Cache-Tag. This option is mutually exclusive with *--all*. [Enterprise Plans Only]{: tag-blue}

`--host`
:   Granularly remove one or more files by specifying the host. This option is mutually exclusive with *--all*. [Enterprise Plans Only]{: tag-blue}

`--prefix`
:   Granularly remove one or more files by a prefix. This option is mutually exclusive with *--all*. [Enterprise Plans Only]{: tag-blue}

`-f, --force`
:   Purging all cached files without prompting for confirmation.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #purge-cache-examples}

Clear all cached assets file for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis cache-purge 31984fea73a15b45779fa0df4ef62f9b --all --force -i "cis-demo"
```
{: pre}

### `ibmcloud cis cache-settings`
{: #show-cache}

Get caching settings for a DNS domain.

```sh
ibmcloud cis cache-settings DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-cache-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-cache-examples}

Get caching settings for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis cache-settings 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis cache-settings-update`
{: #update-cache}

Update cache settings for a give DNS domain.

```sh
ibmcloud cis cache-settings-update DNS_DOMAIN_ID [--caching-level LEVEL][--browser-expiration EXPIRATION] [--development-mode (on | off)] [--serve-stale-content (on | off)] [--query-string-sort (on | off)] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-cache-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--caching-level`
:   Specify under what URL conditions that you want to deliver cached assets to the user. Valid values are `no-query-string`, `query-string-independent`, and `query-string-dependent`.

    - `no-query-string` : Delivers resources from cache only when no query string is present.
    - `query-string-independent` : Delivers the same resource to everyone independent of the query string.
    - `query-string-dependent` : Delivers a different resource each time the query string changes.

`--browser-expiration`
:   Specify how long you want the browser to store cached assets.

   - Valid values are `respect-existing-header`, `30s`, `1M`, `5M`, `20M`, `30M`, `1h`, `2h`, `4h`, `8h`, `16h`, `1d` `3d`, `8d`, `16d`, `1m`, `6m`, and `1y`.
   - `30s`, `1M`, `5M`, and `20M` are only available for an Enterprise or Security plan instance.
   - `30s` means `30 seconds`.
   - `30M` means `30 minutes`.
   - `1h` means `1 hour`.
   - `1d` means `1 day`.
   - `1m` means `1 month`.
   - `1y` means `1 year`.

`--development-mod`
:   Bypass all edge caches and send traffic toward your origin servers.

`--serve-stale-content`
:   Continue serving cached content to users when origin servers are offline, even if the content is expired.

`--query-string-sort`: In the cache, CIS treats files with the same query strings as the same file, regardless of the order of the query strings.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-cache-examples}

Update caching settings for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis cache-settings-update 31984fea73a15b45779fa0df4ef62f9b --caching-level no-query-string --browser-expiration 1h -i "cis-demo"
```
{: pre}

## Custom lists
{: #custom-lists-cmd-ref}

Manipulate how the custom list performs by using the following `custom-lists` commands:

### `ibmcloud cis custom-lists lists`
{: #list-custom-lists}

List the custom lists for your instance.

```sh
ibmcloud cis custom-lists lists [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #custom-list-instance-options}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Example
{: #custom-lists-example}

```sh
ibmcloud cis custom-lists lists -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

### `ibmcloud cis custom-lists list`
{: #get-custom-lists}

Get a custom list for your instance.
```sh
ibmcloud cis custom-lists list LIST_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #get-custom-list-options}

`LIST_ID`
:   The ID of the custom list.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Example
{: #get-custom-list-example}

```sh
ibmcloud cis custom-lists list f93d11a87c4945a0a6bd12820776a66d -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9:: -o json
```
{: pre}

### `ibmcloud cis custom-lists list-create`
{: #create-custom-lists}

Create a custom list for your instance.

```sh
ibmcloud cis custom-lists list-create (--kind KIND) (--name NAME) [--description DESCRIPTION] [-i, --instance INSTANCE]
```

You can also accept JSON input (from a file or directly as a string):

```sh
ibmcloud cis custom-lists list-create (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE]
```

#### Command options
{: #create-custom-lists-options}

`--kind`
:   Custom list kind. Valid values are `ip`, `asn`, and `hostname`.

`--name`
:   The list name.

`--description`
:   Description of the list.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `cis instance-set INSTANCE` is used.

`--json`
:   The JSON file or JSON string that is used to describe a custom list.

:   The required fields in JSON data are:
:   `kind` : Custom list kind. Valid values are `ip`, `asn`, and `hostname`.
:   `name` : The list name.

:   The optional field is:
:   `"description"` : Description of the list.

    Sample JSON data:

    ```json
    {
      "kind": "ip",
      "name": "string",
      "description": "string"
    }
    ```
    {: codeblock}

#### Examples
{: #create-custom-lists-example}

```sh
ibmcloud cis custom-lists list-create --kind ip --name iplistone -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

```sh
ibmcloud cis custom-lists list-create —-json @example.json -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

### `ibmcloud cis custom-lists list-update`
{: #update-custom-list}

Update the description of a custom list.

```sh
ibmcloud cis custom-lists list-update LIST_ID (--description DESCRIPTION) [-i, --instance INSTANCE] [--output FORMAT]
```

```sh
ibmcloud cis custom-lists list-update LIST_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-custom-list-options}

`LIST_ID`
:   The ID of the custom list.

`--description`
:   Briefly describe the list.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

`json`
:   The JSON file or JSON string that is used to describe a custom list.
:   The optional field is:
:   `"description"` : To briefly describe the list.

    Sample JSON data:
    ```json
      {
        "description": "string"
      }
    ```
    {: codeblock}

#### Examples
{: #update-custom-list-example}

```sh
ibmcloud cis custom-lists list-update a46c54444a97431e810c975bf2db4f83 --description "description example" -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

```sh
ibmcloud cis custom-lists list-update a46c54444a97431e810c975bf2db4f83 —-json @example.json -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

### `ibmcloud cis custom-lists list-delete`
{: #delete-custom-list}

Delete a custom list for your instance.

```sh
ibmcloud cis custom-lists list-delete LIST_ID [-f, --force] [-i, --instance INSTANCE]
```

#### Command options
{: #delete-custom-list-options}

`LIST_ID`
:   The ID of the custom list.

`-f, --force`
:   Attempt to delete a custom list without prompting for confirmation.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `cis instance-set INSTANCE` is used.

#### Example
{: #delete-custom-list-example}

```sh
custom-lists list-delete 78277700444f4f69aefef78ea2bef013 -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

### `ibmcloud cis custom-lists items`
{: #get-custom-list-items}

```sh
ibmcloud cis custom-lists items LIST_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #get-custom-list-items-options}

`LIST_ID`
:   The ID of the custom list.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Example
{: #get-custom-list-items-example}

```sh
ibmcloud cis custom-lists items f93d11a87c4945a0a6bd12820776a66d -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

### `ibmcloud cis custom-lists item`
{: #view-custom-list-item}

View a specific item in a custom list.

```sh
ibmcloud cis custom-lists item LIST_ID ITEM_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #view-custom-list-item-options}

`LIST_ID`
:   The ID of the custom list.

`ITEM_ID`
:   The ID of the custom list item.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Example
{: #view-custom-list-item-example}

```sh
ibmcloud cis custom-lists item f93d11a87c4945a0a6bd12820776a66d f550e1d3ede74455bf225a06800bd1be -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

### `ibmcloud cis custom-lists item-create`
{: #create-custom-list-item}

Create a new item in a custom list.

```sh
ibmcloud cis custom-lists item-create LIST_ID (--asn ASN | --ip IP | --hostname HOSTNAME) [--comment COMMENT] [-i, --instance INSTANCE]
```

```sh
ibmcloud cis custom-lists item-create LIST_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE]
```

#### Command options
{: #create-custom-list-item-options}

`LIST_ID`
:   The ID of the custom list.

`--asn`
:   The ASN value.

`--ip`
:   The IPv4 address.

`--hostname`
:   The hostname.

`--comment`
:   To provide a brief comment on the item.

`-i, --instance`
:   Instance name or ID. If instance or ID is not set, the context instance that is specified by `cis instance-set INSTANCE` is used.

`--json`
:   The JSON file or JSON string that is used to describe a custom list.

:   The required fields in JSON data are:
:   `items` : List of custom list items to create.
:   `asn` : The ASN.
:   `hostname` : The hostname.
:   `ip` : The IPv4 address.
:   `comment` : To provide a brief comment on the item.

    Sample JSON data:
    ```json
      [
        {
          "asn": 19604,
          "comment": "My list of developer IPs.",
          "hostname": "cloud.ibm.com",
          "ip": "172.64.0.0/13"
        }
      ]
    ```
    {: codeblock}

#### Command examples
{: #create-custom-list-item-example}

```sh
ibmcloud cis custom-lists item-create f93d11a87c4945a0a6bd12820776a66d --ip 192.0.0.3  -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

```sh
ibmcloud cis custom-lists item-create f93d11a87c4945a0a6bd12820776a66d --json @example.json -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

### `ibmcloud cis custom-lists item-update`
{: #update-custom-list-items}

Update all list items for your custom list.

```sh
ibmcloud cis custom-lists item-update LIST_ID (--json @JSON_FILE | JSON_STRING) [-f, --force] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-custom-list-items-options}

`LIST_ID`
:   The ID of the custom list.

`--json`
:   The JSON file or JSON string that is used to describe a custom list.
:   The required fields in JSON data are:
:   `items` : List of custom list items to create.
:   `asn` : The ASN value.
:   `hostname` : The hostname.
:   `ip` : The IPv4 address.
:   `comment` : To provide a brief comment on the item.

    Sample JSON data:
    ```json
       [
         {
           "asn": 19604,
           "comment": "My list of developer IPs.",
           "hostname": "cloud.ibm.com",
           "ip": "172.64.0.0/13"
         }
       ]
    ```
    {: codeblock}

`-f, --force`
:   Attempt to delete a custom list without prompting for confirmation.

`--output value`
:   The output format. Currently, `json` is the only supported value.

`-i, --instance`
:   Instance name or ID. If instance value or ID is not set, the context instance that is specified by `cis instance-set INSTANCE` is used.

#### Example
{: #update-custom-list-item-options}

```sh
ibmcloud cis custom-lists item-update f93d11a87c4945a0a6bd12820776a66d —json @example.json -f -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}


### `ibmcloud cis custom-lists item-delete`
{: #delete-custom-list-item}

Delete an item from a custom list.

```sh
ibmcloud cis custom-lists item-delete LIST_ID (--item-id CUSTOM_LIST_ITEM_ID) [-f, --force] [-i, --instance INSTANCE]
```

```sh
ibmcloud cis custom-lists item-delete LIST_ID (--json @JSON_FILE | JSON_STRING) [-f, --force] [-i, --instance INSTANCE]
```

#### Command options
{: #delete-custom-list-item-options}

`LIST_ID`
:   The ID of the custom list.

`--item-id`
:   `CUSTOM_LIST_ITEM_ID` is the ID of the custom list item.

`-f, --force`
:   Attempt to delete a custom list without prompting for confirmation.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `cis instance-set INSTANCE` is used.

`--json`
:   The JSON file or JSON string that is used to describe a custom list.
:   The required fields in JSON data are:
:   `items` : List of custom list items to delete by ID.
:   `id` : Unique ID of the custom list item.

    Sample JSON data:
    ```json
      {
        "items": [
          {
            "id": "70c2009751b24ffc9ed1ab462ba957b4"
          }
        ]
      }
    ```
    {: codeblock}

#### Examples
{: #delete-custom-list-item-examples}

```sh
ibmcloud cis custom-lists item-delete f93d11a87c4945a0a6bd12820776a66d --item-id —force 42851cc4589746229552ec5a54f9d623 -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

```sh
ibmcloud cis custom-lists item-delete f93d11a87c4945a0a6bd12820776a66d —json @example.json —-force -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9::
```
{: pre}

### `ibmcloud cis custom-lists operation`
{: #get-status-custom-list-operation}

Get the status for the custom list operation.

```sh
ibmcloud cis custom-lists operation OPERATION_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #get-status-custom-list-operation-options}

`OPERATION_ID`
:   The ID of the custom list operation.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Example
{: #get-status-custom-list-operation-example}

```sh
ibmcloud cis custom-lists operation 04cdb3b267a44ceb895e766fc2affe72 -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9:: -o json
```
{: pre}

## Custom page
{: #custom-pages}

Manipulate how the Custom Page performs by using the following `custom-page` commands:

### `ibmcloud cis custom-page-update`
{: #update-custom-page}

Update a specific custom page.

```sh
ibmcloud cis custom-page-update PAGE_ID PAGE_URL [-d, --domain DNS_DOMAIN_ID] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-custom-page-options}

`PAGE_ID`
:   The name of the Custom Page type. Valid values are `basic_challenge`, `country_challenge`, `ip_block`, `ratelimit_block`, `serve_stale_content`, `under_attack`, `waf_block`, `waf_challenge`, `1000_errors`, `500_errors`. Required.

`PAGE_URL`
:   A URL that is associated with the Custom Page. For example, `http://www.example.com/example.html`. Value `default` means to use the default page. Required.

`-d, --domain`
:   DNS Domain ID.

`-i,- --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-custom-page-examples}

Update `basic_challenge` page for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis custom-page-update "basic_challenge" "http://www.example.com/example.html" -d 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis custom-page`
{: #show-custom-page}

Retrieve a specific custom page.

```sh
ibmcloud cis custom-page PAGE_ID [-d, --domain DNS_DOMAIN_ID] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-custom-page-options}

`PAGE_ID`
:   The name of the Custom Page type. Valid values are `basic_challenge`, `country_challenge`, `ip_block`, `ratelimit_block`, `serve_stale_content`, `under_attack`, `waf_block`, `waf_challenge`, `1000_errors`, and `500_errors`. Required.

`-d, --domain`
:   DNS Domain ID.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-custom-page-examples}

Get `basic_challenge` page for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis custom-page "basic_challenge" -d 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis custom-pages`
{: #list-custom-page}

Retrieve a list of currently existing custom pages.

```sh
ibmcloud cis custom-pages [-d, --domain DNS_DOMAIN_ID] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #list-custom-page-options}

`-d, --domain`
:   DNS Domain ID.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-custom-page-examples}

List existing custom pages for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis custom-pages -d 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

## DNS record
{: #dns-record}

Manipulate how the DNS Record performs by using the following `dns-record` commands:

### `ibmcloud cis dns-record-create`
{: #create-dns-record}

Create a DNS record for a domain of a service instance.

```sh
ibmcloud cis dns-record-create DNS_DOMAIN_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
ibmcloud cis dns-record-create DNS_DOMAIN_ID --type TYPE --name NAME --content CONTENT [--ttl TTL] [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis dns-record-create DNS_DOMAIN_ID --json-str JSON_STR [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis dns-record-create DNS_DOMAIN_ID --json-file JSON_FILE [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #create-dns-record-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--name`
:   DNS record name.

`--type`
:   DNS record type.

`--content`
:   DNS record content.

`--ttl`
:   Time to live for DNS record. A value of 1 is `automatic`. The default value is `1`.

`--proxied`
:   Control whether traffic flows through the security and performance functions on CIS. CIS proxies traffic only for `A`, `AAAA`, and `CNAME` records. Valid values are `true` and `false`.

`--json`
:   The JSON file or JSON string that is used to describe a DNS Record. Supported DNS Record types are: `A`, `AAAA`, `CNAME`, `NS`, `TXT`, `MX`, `LOC`, `SRV`, `CAA`, `PTR`.

    - For type `A`, `AAAA`, `CNAME`, `NS`, `TXT` :
        - The required fields in JSON data are `name`, `type`, `content`.
        - The optional fields are `ttl`, `proxied` :
            - `proxied` Control whether traffic flows through the security and performance functions on CIS. CIS proxies only traffic for `A,` `AAAA`, and `CNAME` records.

Sample JSON data:

```json
{
   "name": "testA",
   "type": "A",
   "content": "127.0.0.1",
   "proxied": true
}

{
   "name": "testAAAA",
   "type": "AAAA",
   "content": "2001:0db8:0012:0001:3c5e:7354:0000:5db1",
   "proxied": false
}

{
   "name": "testCNAME",
   "type": "CNAME",
   "content": "example.com"
}

{
   "name": "testNS",
   "type": "NS",
   "content": "ns1.example.com"
}

{
   "name": "testTXT",
   "type":"TXT",
   "content": "text information"
}

```
{: codeblock}

- For type `PTR` :
   - The required fields in JSON data are `name`, `type`, `content`.
   - The optional field is `ttl`.

Sample JSON data:

```json
{
 "name": "1.2.3.4",
 "type":"PTR",
 "content": "abc.test.com"
}
```
{: codeblock}

- For type `MX` :
   - The required fields in JSON data are `name`, `type`, `content`.
   - The optional fields are `ttl` and `priority`.

Sample JSON data:

```json
{
   "name": "testMX",
   "type": "MX",
   "content": "smtp.example.com",
   "priority": 10
}
```
{: codeblock}

- For type `LOC` :
   - The required fields in JSON data are `name`, `type`, `data`:
      - `data`:
         - `lat_degrees` : Degrees of latitude.
         - `lat_minutes` : Minutes of latitude
         - `lat_seconds` : Seconds of latitude.
         - `lat_direction` : Latitude direction.
         - `long_degrees` : Degrees of longitude.
         - `long_minutes` : Minutes of longitude.
         - `long_seconds` : Seconds of longitude.
         - `long_direction` : Longitude direction.
         - `altitude` : Altitude of location in meters.
         - `size` : Size of location in meters.
         - `precision_horz` : Horizontal precision of location.
         - `precision_vert` : Vertical precision of location.
      - The optional field is `ttl`.

Sample JSON data:

```json
{
   "name": "testLOC",
   "type": "LOC",
   "data": {
         "lat_degrees": 45,
         "lat_minutes": 0,
         "lat_seconds": 0,
         "lat_direction": "N",
         "long_degrees": 45,
         "long_minutes": 0,
         "long_seconds": 0,
         "long_direction": "E",
         "altitude": 20,
         "size": 0,
         "precision_horz": 0,
         "precision_vert": 0
   }
}
```
{: codeblock}

- For type `SRV` :
   - The required fields in JSON data are `type`, `data`:
      - `data`:
            - `service` : A service type, prefixed with an underscore.
            - `proto` : A valid protocol.
            - `priority` : Priority.
            - `weight` : The record weight.
            - `port` : The port of the service.
            - `target` : A valid hostname.
      - The optional field is `ttl`.

Sample JSON data:

```json
{
   "type": "SRV",
   "data": {
         "service": "_ftp",
         "proto": "_tcp",
         "name": "testSRV",
         "priority": 1,
         "weight": 1,
         "port": 21,
         "target": "example.com"
   }
}
```
{: codeblock}

- For type `CAA`:
    - The required fields in JSON data are `name`, `type`, and `data`.
    - The optional field is `ttl`.

Sample JSON data:

```json
{
   "name": "testCAA.yourdomain.com",
   "type": "CAA",
   "data": {
         "tag": "issue",
         "value": "letsencrypt.org"
   }
}
```
{: codeblock}

`-s, --json-str`
:   *Deprecated*. The JSON data used to describe a DNS Record.

`-j, --json-file`
:   *Deprecated*. A file contains input JSON data.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #create-dns-record-examples}

Create a DNS record in the domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis dns-record-create 31984fea73a15b45779fa0df4ef62f9b --json '{"name": "testCNAME", "type": "CNAME", "content": "example.com"}' -i "cis-demo"
ibmcloud cis dns-record-create 31984fea73a15b45779fa0df4ef62f9b --type A --name testA --content "127.0.0.1" -i "cis-demo"
```
{: codeblock}

### `ibmcloud cis dns-record-update`
{: #update-dns-record}

Update a DNS record for a domain of a service instance.

```sh
ibmcloud cis dns-record-update DNS_DOMAIN_ID DNS_RECORD_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
ibmcloud cis dns-record-update DNS_DOMAIN_ID DNS_RECORD_ID [--type TYPE] [--name NAME] [--content CONTENT] [--proxied PROXIED] [--ttl TTL] [--output FORMAT]
[Deprecated] ibmcloud cis dns-record-update DNS_DOMAIN_ID DNS_RECORD_ID --json-str JSON_STR [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis dns-record-update DNS_DOMAIN_ID DNS_RECORD_ID --json-file JSON_FILE [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-dns-record-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`DNS_RECORD_ID`
:   The ID of the DNS record. Required.

`--name`
:   DNS record name.

`--type`
:   DNS record type.

`--content`
:   DNS record content.

`--ttl`
:   Time to live for DNS record. A value of 1 is `automatic`. The default value is `1`.

`--proxied`
:   Control whether traffic flows through the security and performance functions on CIS. CIS proxies traffic only for `A`, `AAAA`, and `CNAME` records. Valid values are `true` and `false`.

`--json`
:   The JSON file or JSON string that is used to describe a DNS Record. Supported DNS Record types are: `A`, `AAAA`, `CNAME`, `NS`, `TXT`, `MX`, `LOC`, `SRV`, `CAA`,`PTR`.

    - For type `A`, `AAAA`, `CNAME`, `NS`, `TXT` :
        - The required fields in JSON data are `name`, `type`, `content`.
        - The optional fields are `ttl` and `proxied` :
            - `proxied` Control whether traffic flows through the security and performance functions on CIS. CIS proxies only traffic for `A`, `AAAA`, and `CNAME` records.

Sample JSON data:

```json
{
   "name": "testA",
   "type": "A",
   "content": "127.0.0.1",
   "proxied": true
}

{
   "name": "testAAAA",
   "type": "AAAA",
   "content": "2001:0db8:0012:0001:3c5e:7354:0000:5db1",
   "proxied": false
}

{
   "name": "testCNAME",
   "type": "CNAME",
   "content": "example.com"
}

{
   "name": "testNS",
   "type": "NS",
   "content": "ns1.example.com"
}

{
   "name": "testTXT",
   "type":"TXT",
   "content": "text information"
}

```
{: codeblock}

- For type `PTR` :
    - The required fields in JSON data are `name`, `type`, `content`.
    - The optional field is `ttl`.

Sample JSON data:

```json
{
 "name": "1.2.3.4",
 "type":"PTR",
 "content": "abc.test.com"
}
```
{: codeblock}

- For type `MX` :
    - The required fields in JSON data are `name`, `type`, `content`.
    - The optional fields are `ttl` and `priority`.

   Sample JSON data:

```json
{
   "name": "testMX",
   "type": "MX",
   "content": "smtp.example.com",
   "priority": 10
}
```
{: codeblock}

- For type `LOC` :
    - The required fields in JSON data are `name`, `type`, `data`:
        - `data`:
            - `lat_degrees` : Degrees of latitude.
            - `lat_minutes` : Minutes of latitude
            - `lat_seconds` : Seconds of latitude.
            - `lat_direction` : Latitude direction.
            - `long_degrees` : Degrees of longitude.
            - `long_minutes` : Minutes of longitude.
            - `long_seconds` : Seconds of longitude.
            - `long_direction` : Longitude direction.
            - `altitude` : Altitude of location in meters.
            - `size` : Size of location in meters.
            - `precision_horz` : Horizontal precision of location.
            - `precision_vert` : Vertical precision of location.
    - The optional field is `ttl`.

   Sample JSON data:

```json
{
   "name": "testLOC",
   "type": "LOC",
   "data": {
         "lat_degrees": 45,
         "lat_minutes": 0,
         "lat_seconds": 0,
         "lat_direction": "N",
         "long_degrees": 45,
         "long_minutes": 0,
         "long_seconds": 0,
         "long_direction": "E",
         "altitude": 20,
         "size": 0,
         "precision_horz": 0,
         "precision_vert": 0
   }
}
```
{: codeblock}

- For type `SRV` :
    - The required fields in JSON data are `type`, `data`:
        - `data`:
            - `service` : A service type, prefixed with an underscore.
            - `proto` : A valid protocol.
            - `priority` : Priority.
            - `weight` : The record weight.
            - `port` : The port of the service.
            - `target` : A valid hostname.
    - The optional field is `ttl`.

   Sample JSON data:

```json
{
   "type": "SRV",
   "data": {
         "service": "_ftp",
         "proto": "_tcp",
         "name": "testSRV",
         "priority": 1,
         "weight": 1,
         "port": 21,
         "target": "example.com"
   }
}
```
{: codeblock}

- For type `CAA` :
     - The required fields in JSON data are `name`, `type`, `data`
     - The optional field is `ttl`.

   Sample JSON data:

```json
{
   "name": "testCAA.yourdomain.com",
   "type": "CAA",
   "data": {
         "tag": "issue",
         "value": "letsencrypt.org"
   }
}
```
{: codeblock}

`-s, --json-str`
:   *Deprecated*. The JSON data used to describe a DNS Record.

`-j, --json-file`
:   *Deprecated*. A file contains input JSON data.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-dns-record-examples}

Update a DNS record in the domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis dns-record-update 31984fea73a15b45779fa0df4ef62f9b 77335b17ce1853d0d76e08a8379a0376 --json '{"name": "testCNAME", "type": "CNAME", "content": "example.com"}' -i "cis-demo"
ibmcloud cis dns-record-update 31984fea73a15b45779fa0df4ef62f9b 417e8605a72d3e085020b82c93cd7f82 --type A --name testA --content "127.0.0.1" -i "cis-demo"
```
{: codeblock}

### `ibmcloud cis dns-record`
{: #get-dns-record}

Get a DNS record details for a domain under a service instance.

```sh
ibmcloud cis dns-record DNS_DOMAIN_ID DNS_RECORD_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #get-dns-record-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`DNS_RECORD_ID`
:   The ID of the DNS record. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #get-dns-record-examples}

Get DNS record details in the domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis dns-record 31984fea73a15b45779fa0df4ef62f9b 77335b17ce1853d0d76e08a8379a0376 -i "cis-demo"
```
{: pre}

### `ibmcloud cis dns-record-delete`
{: #delete-dns-record}

Delete a DNS record for a domain of a service instance.

```sh
ibmcloud cis dns-record-delete DNS_DOMAIN_ID DNS_RECORD_ID [-i, --instance INSTANCE]
```

#### Command options
{: #delete-dns-record-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`DNS_RECORD_ID`
:   The ID of the DNS record. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #delete-dns-record-examples}

Delete a DNS record in the domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis dns-record-delete 31984fea73a15b45779fa0df4ef62f9b 77335b17ce1853d0d76e08a8379a0376 -i "cis-demo"
```
{: pre}

### `ibmcloud cis dns-records`
{: #list-dns-records}

List all DNS records for a domain of a service instance.

```sh
ibmcloud cis dns-records DNS_DOMAIN_ID [--type TYPE] [--name NAME] [--content CONTENT] [--page PAGE] [--per-page PER_PAGE] [--order ORDER] [--direction DIRECTION] [--match MATCH] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #list-dns-records-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--type`
:   Type of DNS records to display.

`--name`
:   Value of name field to filter by.

`--content`
:   Value of content field to filter by.

`--page`
:   Page number of paginated results.

`--per_page`
:   Maximum number of DNS records per page.

`--order`
:   Field by which to order the list of DNS records. Valid values are `type`, `name`, `content`, `ttl`, and `proxied`.

`--direction`
:   Direction in which to order the results (ascending or descending order). Valid values are `asc` and `desc`.

`--match`
:   Whether to match all or at least one search parameter. Valid values are `any` and `all`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-dns-records-examples}

List all DNS records in domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis dns-records 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis dns-records-import`
{: #dns-record-import}

Import your BIND config.

```sh
ibmcloud cis dns-records-import DNS_DOMAIN_ID --file FILE [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #dns-record-import-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--file`
:   BIND config to import. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #dns-record-import-examples}

Import BIND config in the domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis dns-records-import 31984fea73a15b45779fa0df4ef62f9b --file bind_config_file.txt -i "cis-demo"
```
{: pre}

### `ibmcloud cis dns-records-export`
{: #dns-record-export}

Export BIND config.

```sh
ibmcloud cis dns-records-export DNS_DOMAIN_ID [--file FILE] [-i, --instance INSTANCE]
```

#### Command options
{: #dns-record-export-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--file`
:   The BIND config file that saves exported DNS records.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #dns-record-export-examples}

Export BIND config for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis dns-records-export 31984fea73a15b45779fa0df4ef62f9b --file bind_config_file.txt -i "cis-demo"
```
{: pre}

## Domain
{: #domain}

Manipulate domains by using the following `domain` commands.

### `ibmcloud cis domain-add`
{: #add-domain}

Add a domain.

```sh
ibmcloud cis domain-add DNS_DOMAIN_NAME [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #add-domain-options}

`type`
:   Specify the domain type setup. Valid values are `full` and `partial` (default `full`).

    - `full` : A full zone implies that the DNS is hosted.
    - `partial` : A partial zone implies a CNAME setup domain.

`jump-start`
:   Automatically attempt to fetch existing DNS records.

`DNS_DOMAIN_NAME`
:   The FQDN of DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #add-domain-examples}

Add a domain `test.com` in instance `cis-demo`.

```sh
ibmcloud cis domain-add "test.com" -i "cis-demo"
```
{: pre}

### `ibmcloud cis domain-resume`
{: #resume-domain}

Resume the domain.

```sh
ibmcloud cis domain-resume DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #resume-domain-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #resume-domain-examples}

Resume the specified domain.

```sh
ibmcloud cis domain-resume 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis domain-pause`
{: #pause-domain}

Pause the domain.

```sh
ibmcloud cis domain-pause DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #pause-domain-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #pause-domain-examples}

Pause the specified domain.

```sh
ibmcloud cis domain-pause 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis domain`
{: #display-domain}

Display the domain details.

```sh
ibmcloud cis domain DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #display-domain-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #display-domain-examples}

Display the specified domain details.

```sh
ibmcloud cis domain 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis domain-remove`
{: #remove-domain}

Remove a domain.

```sh
ibmcloud cis domain-remove DNS_DOMAIN_ID [-i, --instance INSTANCE]
```

#### Command options
{: #remove-domain-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #remove-domain-examples}

Remove the specified domain.

```sh
ibmcloud cis domain-remove 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis domains`
{: #list-domain}

List domains for a service instance.

```sh
ibmcloud cis domains [--instance INSTANCE_NAME] [--output FORMAT]
```

#### Command options
{: #list-domain-options}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-domain-examples}

List domains for the specified domain `cis-demo`.

```sh
ibmcloud cis domains -i "cis-demo"
```
{: pre}


### `ibmcloud cis domain-activation-check`
{: #check-domain}

Check the activation on the domain.

```sh
ibmcloud cis domain-activation-check DNS_DOMAIN_ID [-i, --instance INSTANCE]
```

#### Command options
{: #check-domain-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #check-domain-examples}

Perform activation check on the specified domain.

```sh
ibmcloud cis domain-activation-check 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

## Domain settings
{: #domain-settings}

Manipulate domain settings by using the following `domain-settings` commands:

### `ibmcloud cis domain-settings`
{: #display-domain-settings}

Get details of a feature for the domain.

```sh
ibmcloud cis domain-settings DNS_DOMAIN_ID [-g, --group GROUP | -f, --feature FEATURE] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #display-domain-settings-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-g, --group`
:   Display features in a same group. Valid values for `group` are `all`, `domain`, `reliability`, `performance`, and `security`. This option is mutually exclusive with *-f, --feature*.

`-f, --feature`
:   Feature of domain settings to check. This option is mutually exclusive with *g, --group*. Valid values are as follows:
    - `always_use_https` : Redirect all requests with scheme `http` to `https`. This setting applies to all HTTP requests to the domain.
    - `automatic_https_rewrites` : Help fix mixed content by changing `http` to `https` for all resources or links on your website that can be served with HTTPS.
    - `bot_management` : Detect and mitigate bot traffic on your domain.
    - `brotli` : When the client that is requesting an asset supports the brotli compression algorithm, CIS serves a brotli compressed version of the asset.
    - `browser_check` : Evaluate HTTP headers from your visitors' browser for threats. If a threat is found, then a block page is delivered.
    - `challenge_ttl` : Specify how long a visitor with a bad IP reputation is allowed access to your website after they complete a challenge.
    - `ciphers` : An allowlist of ciphers for TLS termination in the BoringSSL format. This command lists ciphers that are allowlisted by customers. If no ciphers are allowlisted, the list is empty and the default ciphers are used. See [Edge cipher suites](/docs/cis?topic=cis-set-up-cipher-suites&interface=cli#edge-cipher-suites) and [Origin cipher suites](/docs/cis?topic=cis-set-up-cipher-suites&interface=cli#origin-cipher-suites) for the list of default ciphers.
    - `cname_flattening` : Follow a CNAME to where it points and return that IP address instead of the CNAME record. By default, flatten only the CNAME at the root of your domain.
    - `domain_hold`: Domain holds prevent teams in your organization from adding domains that are already active in another account. [Enterprise Plans Only]{: tag-blue}
    - `email_obfuscation` : Encrypt the email addresses on your web page from bots while it's kept visible to humans.
    - `opportunistic_onion` : Allow legitimate users of the Tor Browser to access your websites.
    - `hotlink_protection` : Protect your images from off-site linking.
    - `http2` : Accelerate your website with HTTP/2.
    - `http3` : Accelerate your website with HTTP/3.
    - `image_load_optimization` : Improve load time for pages that include images on mobile devices with slow network connections.
    - `image_size_optimization` : Improve image load time by optimizing images hosted on your domain.
    - `image_resizing` : Provide on-demand resizing, conversion, and optimization for images served through the CIS network.
    - `ip_geolocation` : Include the country code of the visitor location with all requests to your website.
    - `ipv6` : Enable IPv6 support and gateway.
    - `max_upload` : The number of data visitors who can upload to your website in a single request.
    - `min_tls_version` : Allow only HTTPS connections from visitors that support the selected TLS protocol version or newer.
    - `minify` : Reduce the file size of source code on your website.
    - `mobile_redirect` : Redirect visitors that are using mobile devices to a mobile-optimized website.
    - `opportunistic_encryption` : Opportunistic Encryption allows browsers to benefit from the improved performance of HTTP/2 by letting them know that your site is available over an encrypted connection.
    - `origin_error_page_pass_thru` : When the Origin Error Page is set to `On`, CIS proxies the 502 and 504 error pages directly from the origin. [Enterprise Plans Only]{: tag-blue}
    - `origin_max_http_version` : Configure the HTTP version to Origin.
    - `origin_post_quantum_encryption` : Instructs CIS to use Post-Quantum (PQ) key agreement algorithms when it connects to your origin.
    - `prefetch_preload` : CIS prefetches any URLs included in the prefetch HTTP header. [Enterprise Plans Only]{: tag-blue}
    - `pseudo_ipv4` : Adds an IPv4 header to requests when a client is using IPv6, but the server only supports IPv4.
    - `response_buffering` : Enable or disable buffering of responses from the origin server. [Enterprise Plans Only]{: tag-blue}
    - `script_load_optimization` : Improve the paint time for pages that include JavaScript.
    - `security_header` : Enforce a web security policy for your website.
    - `security_level` : Choose the appropriate security profile for your website.
    - `server_side_exclude` : Automatically hide specific content from suspicious visitors.
    - `tls_client_auth` : TLS client certificate presented for authentication on origin pull. [Enterprise Plans Only]{: tag-blue}
    - `true_client_ip_header` : CIS sends the user’s IP address in the True-Client-IP header. [Enterprise Plans Only]{: tag-blue}
    - `waf` : A Web Application Firewall (WAF) blocks requests that contain malicious content.
    - `websockets` : Allow WebSockets connections to your origin server.
    - `proxy_read_timeout` : Maximum time between two read operations from origin. [Enterprise Plans Only]{: tag-blue}
    - `url_normalization` : Modify the URLs of incoming requests.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #display-domain-settings-example}

Get `ciphers` settings for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis domain-settings -f "ciphers" 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis domain-settings-update`
{: #update-domain-settings}

Update a feature for the domain.

```sh
ibmcloud cis domain-settings-update DNS_DOMAIN_ID (-f, --feature FEATURE) (-v, --value VALUE) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-domain-settings-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-f, --feature`
:   Feature of domain settings to update. Required. Valid values:
    - `always_use_https` : Redirect all requests with scheme `http` to `https`. This redirect applies to all http requests to the domain.
    - `automatic_https_rewrites` : Help fix mixed content by changing `http` to `https` for all resources or links on your website that can be served with HTTPS.
    - `bot_management` : Detect and mitigate bot traffic on your domain.
    - `brotli` : When the client that is requesting an asset supports the brotli compression algorithm, CIS serves a brotli compressed version of the asset.
    - `browser_check` : Evaluate HTTP headers from your visitors' browser for threats. If a threat is found, then a block page is delivered.
    - `challenge_ttl` : Specify how long a visitor with a bad IP reputation is allowed access to your website after they complete a challenge.
    - `ciphers` : An allowlist of ciphers for TLS termination. These ciphers must be in the BoringSSL format.
    - `cname_flattening` : Follow a CNAME to where it points and return that IP address instead of the CNAME record.
       By default, only flatten the CNAME at the root of your domain.
    - `domain_hold`: Domain holds prevent teams in your organization from adding domains that are already active in another account. [Enterprise Plans Only]{: tag-blue}
    - `email_obfuscation` : Encrypt the email addresses on your web page from bots while it's kept visible to humans.
    - `opportunistic_onion` : Allow legitimate users of the Tor Browser to access your websites.
    - `hotlink_protection` : Protect your images from off-site linking.
    - `http2` : Accelerate your website with HTTP/2.
    - `http3` : Accelerate your website with HTTP/3.
    - `image_load_optimization` : Improve load time for pages that include images on mobile devices with slow network connections.
    - `image_size_optimization` : Improve image load time by optimizing images hosted on your domain.
    - `image_resizing` : Provide on-demand resizing, conversion, and optimization for images served through the CIS network.
    - `ip_geolocation` : Include the country code of the visitor location with all requests to your website.
    - `ipv6` : Enable IPv6 support and gateway.
    - `max_upload` : The number of data visitors who can upload to your website in a single request.
    - `min_tls_version`: Allow only HTTPS connections from visitors that support the selected TLS protocol version or newer.
    - `minify` : Reduce the file size of source code on your website.
    - `mobile_redirect` : Redirect visitors that are using mobile devices to a mobile-optimized website.
    - `opportunistic_encryption` : Opportunistic Encryption allows browsers to benefit from the improved performance of HTTP/2 by letting them know that your site is available over an encrypted connection.
    - `origin_error_page_pass_thru` : When Origin Error Page is set to `On`, CIS proxies the 502 and 504 error pages directly from the origin. [Enterprise Plans Only]{: tag-blue}
    - `origin_max_http_version` : Configure the HTTP version to Origin.
    - `origin_post_quantum_encryption` : Instructs CIS to use Post-Quantum (PQ) key agreement algorithms when it connects to your origin.
    - `prefetch_preload` : CIS prefetches any URLs included in the prefetch HTTP header. [Enterprise Plans Only]{: tag-blue}
    - `pseudo_ipv4` : Adds an IPv4 header to requests when a client is using IPv6, but the server supports IPv4 only.
    - `response_buffering` : Enable or disable buffering of responses from the origin server. [Enterprise Plans Only]{: tag-blue}
    - `script_load_optimization` : Improve the paint time for pages that include JavaScript.
    - `security_header` : Enforce a web security policy for your website.
    - `security_level` : Choose the appropriate security profile for your website.
    - `server_side_exclude` : Automatically hide specific content from suspicious visitors.
    - `tls_client_auth` : TLS client certificate presented for authentication on origin pull. [Enterprise Plans Only]{: tag-blue}
    - `true_client_ip_header` : CIS sends the user’s IP address in the True-Client-IP header. [Enterprise Plans Only]{: tag-blue}
    - `waf` : A Web Application Firewall (WAF) blocks requests that contain malicious content.
    - `websockets` : Allow WebSockets connections to your origin server.
    - `proxy_read_timeout` : Maximum time between two read operations from origin.
    - `url_normalization` : Modify the URLs of incoming requests.

`-v, --value`
:   The value set to the feature for domain. Required.
    - Valid values for `always_use_https` are `on` and `off`.
    - Valid values for `automatic_https_rewrites` are `on` and `off`.
    - Valid values for `bot_management` are "use_latest_model", "fight_mode", "session_score", "enable_js". For example, `-v fight_mode=true,session_score=true`
         - `use_latest_model` : Whether to enable the latest model version. Valid values for `use_latest_model` are `true` and `false`.
         - `fight_mode` : Whether to enable the fight mode. Valid values for `fight_mode` are `true` and `false`.
         - `session_score` : Whether to enable the session score. Valid values for `session_score` are `true` and `false`.
         - `enable_js` : Whether to enable JavaScript detections. Valid values for `enable_js` are `true` and `false`.
    - Valid values for `browser_check` are `on` and `off`.
    - Valid values for `challenge_ttl` are `300, 900, 1800, 2700, 3600, 7200, 10800, 14400, 28800, 57600, 86400, 604800, 2592000, 31536000`.
    - Valid values for `cname_flattening` are `flatten_at_root`, `flatten_all`.
        - `flatten_at_root` : Flatten CNAME at the root domain. This value is the default value.
        - `flatten_all` : Flatten all CNAME records under your domain.
    - Valid values for `domain_hold` are `hold`, `include_subdomains` and `hold_after`.
        - `hold` : Whether to enable the domain hold. Valid values for `hold` are `true` and `false`.
        - `include_subdomains`: Whether to enable the domain hold. Valid values for `include_subdomains` are `true` and `false`.
        - `hold_after` : If `hold_after` is provided, the hold is temporarily disabled, then automatically re-enabled by the system at the time specified.

        For enable domain and subdomains hold: `-v hold=true,include_subdomains=true`.
        For disable domain hold: `-v hold=false,hold_after=2023-05-31T15:56:36+00:00`.
    - Valid values for `hotlink_protection` are `on`, `off`.
    - Valid values for `email_obfuscation` are `on`, `off`.
    - Valid values for `opportunistic_onion` are `on`, `off`.
    - Valid values for `http2` are `on`, `off`.
    - Valid values for `http3` are `on`, `off`.
    - Valid values for `image_load_optimization` are `on`, `off`.
    - Valid values for `image_resizing` are `on`, `off`.
    - Valid values for `image_size_optimization` are `off`, `lossless`, `lossy`.
        - `off`: Disable Image Size Optimization.
        - `lossless` : Reduce the size of image files without impacting visual quality.
        - `lossy` : The file size of JPEG images is reduced by using lossy compression, which might reduce visual quality.
    - Valid values for `ip_geolocation` are `on`, `off`.
    - Valid values for `ipv6` are `on`, `off`.
    - Valid values(in MB) for `max_upload` are:
        `100, 125, 150, 175, 200 and 225, 250, 275, 300, 325, 350, 375, 400, 425, 450, 475, 500`. [Enterprise Plans Only]{: tag-blue}
    - Valid values for `min_tls_version` are `1.0`, `1.1`, `1.2`, `1,3`.
    - Valid values for `minify` are `css`, `html`, `js`. For example, -v css=on,html=off,js=on
        - `css` : Automatically minify all CSS for your website. Valid values for `css` are `on`, `off`.
        - `html` : Automatically minify all HTML for your website. Valid values for `html` are `on`, `off`.
        - `js` : Automatically minify all JS for your website. Valid values for `js` are `on`, `off`.
    - Valid values for `mobile_redirect` are `status`, `mobile_subdomain`, `strip_uri`. For example, `-v status=on,mobile_subdomain=m,strip_uri=true`
        - `status` : Whether the mobile redirection is enabled. Valid values for `status` are `on` and `off`.
        - `mobile_subdomain`: Which subdomain prefix you want to redirect visitors on mobile devices to (subdomain must exist).
        - `strip_uri` : Whether to drop the current page path and redirect to the mobile subdomain URL root. Valid values for `strip_uri` are `true`, `false`.
    - Valid values for `opportunistic_encryption` are `on`, `off`.
    - Valid values for `origin_error_page_pass_thru` are `1`, `2`.
    - Valid values for `origin_max_http_version` are `supported`, `preferred`, `off`.
        - `supported` : Post-Quantum algorithms are advertised but only used when requested by the origin.
        - `preferred` : Preferred instructs CIS to opportunistically send a Post-Quantum (PQ) keyshare in the first message to the origin (for fastest connections when the origin supports and prefers PQ).
        - `off`: Post-Quantum algorithms are not advertised.
    - Valid values for `origin_post_quantum_encryption` are `on`, `off`.
    - Valid values for `brotli` are `on`, `off`.
    - Valid values for `prefetch_preload` are `on`, `off`.
    - Valid values for `pseudo_ipv4` are `off`, `add_header`, `overwrite_header`.
        - `off`: Disable Pseudo IPv4.
        - `add_header` : Add an additional Cf-Pseudo-IPv4 header only.
        - `overwrite_header`: Overwrite the existing Cf-Connecting-IP and X-Forwarded-For headers with a pseudo IPv4 address.
    - Valid values for `response_buffering` are `on`, `off`.
    - Valid values for `script_load_optimization` are `on`, `off`.
    - Valid values for `security_header` are `enabled`, `max_age`, `include_subdomains`, `preload`, `nosniff`. For example, -v enabled=true,max_age=100,include_subdomains=true,preload=true,nosniff=true
        - `enabled` : Whether the security_header is enabled. Valid values for `enabled` are `true`, `false`.
        - `max_age` : Specify the duration(in seconds) security_header are cached in browsers.
        - `include_subdomains`: Every domain below the domain inherits the same security_header. Valid values for `include_subdomains` are `true`, `false`.
        - `preload` : Whether to permit browsers to preload security_header config. Valid values for `enabled` are `true`, `false`.
        - `nosniff` : Whether to send `X-Content-Type-Options: nosniff` header. Valid values for `nosniff` are `true`, `false`.
    - Valid values for `server_level` are `off`, `essentially_off`, `low`, `medium`, `high`, `under_attack`.
    - Valid values for `server_side_exclude` are `on`, `off`.
    - Valid values for `tls_client_auth` are `on`, `off`.
    - Valid values for `true_client_ip_header` are `on`, `off`.
    - Valid values for `waf` are `on`, `off`.
    - Valid values for `websockets` are `on`, `off`.
    - Valid values for `proxy_read_timeout`, 1-6000, default: 100.
    - Valid values for `ciphers` are `ECDHE-ECDSA-AES128-GCM-SHA256`, `ECDHE-ECDSA-CHACHA20-POLY1305`, `ECDHE-RSA-AES128-GCM-SHA256`, `ECDHE-RSA-CHACHA20-POLY1305`, `ECDHE-ECDSA-AES128-SHA256`, `ECDHE-ECDSA-AES128-SHA`, `ECDHE-RSA-AES128-SHA256`, `ECDHE-RSA-AES128-SHA`, `AES128-GCM-SHA256`, `AES128-SHA256`, `AES128-SHA`, `ECDHE-ECDSA-AES256-GCM-SHA384`, `ECDHE-ECDSA-AES256-SHA384`, `ECDHE-RSA-AES256-GCM-SHA384`, `ECDHE-RSA-AES256-SHA384`, `ECDHE-RSA-AES256-SHA`, `AES256-GCM-SHA384`, `AES256-SHA256`, `AES256-SHA`, `DES-CBC3-SHA`, `default`. For example, `-v AES256-SHA256,AES256-SHA`, using `-v default` to reset configured cipher suites to the default value.
    - Valid values for `url_normalization` are "type", "scope". For example, -v type=cis,scope=both
         - `type` : Selects the type of URL normalization that is performed by CIS. Valid values for `type` are `cis`, `rfc3986`.
         - `scope` : Configures the scope of the URL normalization. Valid values for `scope` are `both`, `incoming`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-domain-settings-example}

Enable `tls_client_auth` for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis domain-settings-update -f tls_client_auth -v on 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

## Edge functions
{: #edge-functions}

Manipulate how Edge Functions perform by using the following `edge-functions` commands:

### `ibmcloud cis edge-functions-actions`
{: #list-edge-functions-actions}

List all Edge Functions actions of a service instance.

```sh
ibmcloud cis edge-functions-actions [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #list-edge-functions-actions-options}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-edge-functions-actions-examples}

List all Edge Functions actions in instance `cis-demo`.

```sh
ibmcloud cis edge-functions-actions -i "cis-demo"
```
{: pre}

### `ibmcloud cis edge-functions-action`
{: #show-an-edge-functions-action}

Show an Edge Functions action of a service instance.

```sh
ibmcloud cis edge-functions-action [--name ACTION_NAME] [-i, --instance INSTANCE]
```

#### Command options
{: #show-an-edge-functions-action-options}

`--name`
:   Action name. [Enterprise Plans Only]{: tag-blue}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #show-an-edge-functions-action-examples}

Show details of Edge Functions action `action-demo`.

```sh
ibmcloud cis edge-functions-action --name "action-demo" -i "cis-demo"
```
{: pre}

### `ibmcloud cis edge-functions-action-create`
{: #create-an-edge-functions-action}

Create an Edge Functions action for a service instance.

```sh
ibmcloud cis edge-functions-action-create [--name ACTION_NAME] (--javascript-str JAVASCRIPT_STR | --javascript-file JAVASCRIPT_FILE) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #create-an-edge-functions-action-options}

`--name`
:   Action name. [Enterprise Plans Only]{: tag-blue}

`--javascript-str`
:   JavaScript string. For example, `addEventListener('fetch', event => { event.respondWith(fetch(event.request))})`

`--javascript-file`
:   JavaScript file.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #create-an-edge-functions-action-examples}

Create an Edge Functions action for instance `action-demo`.

```sh
ibmcloud cis edge-functions-action-create --javascript-str "addEventListener('fetch', event => { event.respondWith(fetch(event.request)) })" --name "action-demo" -i "cis-demo"
```
{: pre}

### `ibmcloud cis edge-functions-action-update`
{: #update-an-edge-functions-action}

Update an Edge Functions action of a service instance.

```sh
ibmcloud cis edge-functions-action-update (--javascript-str JAVASCRIPT_STR | --javascript-file JAVASCRIPT_FILE) [--name ACTION_NAME] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-an-edge-functions-action-options}

`--name`
:   Action name. [Enterprise Plans Only]{: tag-blue}

`--javascript-str`
:   JavaScript string. For example, `addEventListener('fetch', event => { event.respondWith(fetch(event.request))})`

`--javascript-file`
:   JavaScript file.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-an-edge-functions-action-examples}

Update an Edge Functions action for instance `action-demo`.

```sh
ibmcloud cis edge-functions-action-update --javascript-str "addEventListener('fetch', event => { event.respondWith(fetch(event.request)) })" --name "action-demo" -i "cis-demo"
```
{: pre}

### `ibmcloud cis edge-functions-action-delete`
{: #delete-an-edge-functions-action}

Delete an Edge Functions action of a service instance.

```sh
ibmcloud cis edge-functions-action-delete [--name ACTION_NAME] [-i, --instance INSTANCE]
```

#### Command options
{: #delete-an-edge-functions-action-options}

`--name`
:   Action name. [Enterprise Plans Only]{: tag-blue}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #delete-an-edge-functions-action-examples}

Delete Edge Functions action `action-demo`.

```sh
ibmcloud cis edge-functions-action-delete --name "action-demo" -i "cis-demo"
```
{: pre}

### `ibmcloud cis edge-functions-triggers`
{: #list-edge-functions-triggers}

List all Edge Functions triggers for a domain of a service instance.

```sh
ibmcloud cis edge-functions-triggers DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #list-edge-functions-triggers-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-edge-functions-triggers-examples}

List all Edge Functions triggers for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis edge-functions-triggers 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis edge-functions-trigger`
{: #show-an-edge-functions-trigger}

Show an Edge Functions trigger for a domain of a service instance.

```sh
ibmcloud cis edge-functions-trigger DNS_DOMAIN_ID TRIGGER_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-edge-functions-trigger-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`TRIGGER_ID`
:   The ID of the trigger. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-edge-functions-trigger-examples}

Show details of Edge Functions trigger `9a7806061c88ada191ed06f989cc3dac`.

```sh
ibmcloud cis edge-functions-trigger 31984fea73a15b45779fa0df4ef62f9b 9a7806061c88ada191ed06f989cc3dac -i "cis-demo"
```
{: pre}

### `ibmcloud cis edge-functions-trigger-create`
{: #create-an-edge-functions-trigger}

Create an Edge Functions trigger for a domain of a service instance.

```sh
ibmcloud cis edge-functions-trigger-create DNS_DOMAIN_ID PATTERN_URL [--name ACTION_NAME] [--disable] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #create-edge-functions-trigger-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`PATTERN_URL`
:   The request URL, which triggers the action. Required.

`name`
:   The action name to which the created trigger is attached. [Enterprise Plans Only]{: tag-blue}

`disable`
:   Disable an Edge Functions trigger.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #create-edge-functions-trigger-examples}

Create an Edge Functions trigger for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis edge-functions-trigger 31984fea73a15b45779fa0df4ef62f9b "example.net/*" --name "demo-action" -i "cis-demo"
```
{: pre}

### `ibmcloud cis edge-functions-trigger-update`
{: #update-an-edge-functions-trigger}

Update an Edge Functions trigger for a domain of a service instance.

```sh
ibmcloud cis edge-functions-trigger-update DNS_DOMAIN_ID TRIGGER_ID PATTERN_URL [--name ACTION_NAME] [--disable] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-edge-functions-trigger-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`TRIGGER_ID`
:   The ID of the trigger. Required.

`PATTERN_URL`
:   The request URL, which triggers the action. Required.

`name`
:   The action name, which the created trigger is attached to. [Enterprise Plans Only]{: tag-blue}

`disable`
:   Disable an Edge Functions trigger.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-edge-functions-trigger-examples}

Update Edge Functions trigger `9a7806061c88ada191ed06f989cc3dac`.

```sh
ibmcloud cis edge-functions-trigger 31984fea73a15b45779fa0df4ef62f9b 9a7806061c88ada191ed06f989cc3dac "example.net/*" --name "demo-action" -i "cis-demo"
```
{: pre}

### `ibmcloud cis edge-functions-trigger-delete`
{: #delete-an-edge-functions-trigger}

Delete an Edge Functions trigger for a domain of a service instance.

```sh
ibmcloud cis edge-functions-trigger-delete DNS_DOMAIN_ID TRIGGER_ID [-i, --instance INSTANCE]
```

#### Command options
{: #delete-edge-functions-trigger-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`TRIGGER_ID`
:   The ID of the trigger. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #delete-edge-functions-trigger-examples}

Delete Edge Functions trigger `9a7806061c88ada191ed06f989cc3dac`.

```sh
ibmcloud cis edge-functions-trigger-delete 31984fea73a15b45779fa0df4ef62f9b 9a7806061c88ada191ed06f989cc3dac -i "cis-demo"
```
{: pre}

## Firewall
{: #firewall}

Manipulate firewalls by using the following `firewall` commands.

### `ibmcloud cis firewall-create`
{: #create-firewall}

Create a new firewall rule.

```sh
ibmcloud cis firewall-create (-t, --type Type) (--json @JSON_FILE | JSON_STRING) [-d, --domain DNS_DOMAIN_ID] [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis firewall-create (-t, --type Type) (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-d, --domain DNS_DOMAIN_ID] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #create-firewall-options}

`-t, --type`
:   Type of firewall rules to create. Valid values: `access-rules`, `ua-rules`, `lockdowns`. Required.
    - `access-rules`: Access Rules are a way to allow, challenge, or block requests to your website. You can apply access rules to one domain only or all domains in the same service instance.
    - `ua-rules`: Perform access control when matching the exact UserAgent reported by the client. The access control mechanisms can be defined within a rule to help manage traffic from particular clients. This option enables you to customize the access to your site.
    - `lockdowns`: Lock access to URLs in this domain to only permitted addresses or address ranges.

`-d, --domain`
:   DNS Domain ID. For `ua-rules` and `lockdowns` type rule, it is a required parameter.

`--json`
:   The JSON file or JSON string that is used to describe a firewall rule. Required.
    - For `--type access-rules` : The JSON data that describes a firewall access rule as follows.
        - Required fields are `mode`, `configuration`.
            - `mode` : The type of action to perform. Valid values are `block`, `challenge`, `whitelist`, and `js_challenge`.
            - `configuration` : Target/Value pair to use for this rule.
                - `target` : The request property to target. Valid values are `ip`, `ip_range`, `asn`, and `country`.
                - `value` : The value for the selected target.
                    - For ip, the value is a valid IP address.
                    - For ip_range, the value specifies an ip range that is limited to `/16` and `/24`.
                    - For asn, the value is an AS number.
                    - For a country, the value is a country code for the country.
        -   Option fields are `notes`.
            - `notes` : Some useful information about this rule to help identify the purpose of it.

Sample JSON data:

```json
{
   "mode": "block",
   "notes": "This rule is added because of event X that occurred on date xyz",
   "configuration": {
      "target": "ip",
      "value": "127.0.0.1"
   }
}
```
{: codeblock}

- For `--type ua-rules` : The JSON data that describes a user-agent rule as follows.
    - Required fields are `mode`, `configuration`.
        - `mode` : The type of action to perform. Valid values are `block`, `challenge`, and `js_challenge`.
        - `configuration` : Target/Value pair to use for this rule.
            - `target` : The request property to target. Valid value is `ua`.
            - `value` : The exact UserAgent string to match with this rule.
    - Option fields are `paused`, `description`.
        - `paused` : Whether this rule is currently disabled.
        - `description` : Some useful information about this rule to help identify the purpose of it.

Sample JSON data:

```json
{
   "mode": "block",
   "configuration": {
      "target": "ua",
      "value": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/603.2.4 (KHTML, like Gecko) Version/10.1.1 Safari/603.2.4"
   }
}
```
{: codeblock}

- For `--type lockdowns` : The JSON data that describes a lockdown rule is as follows.
    - Required fields are `urls`, `configurations`.
        - `urls` : URLs to be included in this rule definition.
            - Wildcards are permitted.
            - The URL pattern entered here is escaped before use.
            - This field limits the URL to simple wildcard patterns.
        - `configurations` : List of IP addresses or CIDR ranges to use for this rule.
            - This field can include any number of ip or ip_range configurations that can access the provided URLs.
            - `target` : The request property to target. Valid values are `ip`, and `ip_range`.
            - `value` : IP addresses or CIDR. If target is `ip`, then value must be an IP address, otherwise CIDR.
    - Option fields are `paused`, `description`.
        - `paused` : Whether this rule is currently disabled.
        - `description` : Some useful information about this rule to help identify the purpose of it.

Sample JSON data:

```json
{
   "urls": [
      "api.mysite.com/some/endpoint*"
   ],
   "configurations": [
      {
         "target": "ip",
         "value": "127.0.0.1"
      },
      {
         "target": "ip_range",
         "value": " 2.2.2.0/24"
      }
   ]
}
```
{: codeblock}

`-s, --json-str`
:   *Deprecated*. The JSON data describing a firewall rule.

`-j, --json-file`
:   *Deprecated*. A file contains input JSON data.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #create-firewall-examples}

Create firewall rules.

```sh
ibmcloud cis firewall-create -t access-rules --json '{"mode": "block", "notes": "This rule is added because of event X that occurred on date xyz", "configuration": {"target": "ip", "value": "127.0.0.1"}}' -i "cis-demo"
ibmcloud cis firewall-create -t ua-rules -d 31984fea73a15b45779fa0df4ef62f9b --json '{"mode": "block", "configuration": {"target": "ua", "value": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/603.2.4 (KHTML, like Gecko) Version/10.1.1 Safari/603.2.4"}}' -i "cis-demo"
ibmcloud cis firewall-create -t lockdowns -d 31984fea73a15b45779fa0df4ef62f9b --json '{"urls": ["api.mysite.com/some/endpoint*"], "configurations": [{"target": "ip", "value": "127.0.0.1"}, {"target": "ip_range", "value": "2.2.2.0/24"}]}' -i "cis-demo"
```
{: codeblock}

### `ibmcloud cis firewall-update`
{: #update-firewall}

Update a firewall rule.

```sh
ibmcloud cis firewall-update FIREWALL_RULE_ID (-t, --type Type) (--json @JSON_FILE | JSON_STRING) [-d, --domain DNS_DOMAIN_ID] [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis firewall-update FIREWALL_RULE_ID (-t, --type Type) (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-d, --domain DNS_DOMAIN_ID] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-firewall-options}

- **FIREWALL_RULE_ID**: The ID of firewall rule. Required.

`-t, --type`
:   The type of firewall rule to create. Valid values are `access-rules`, `ua-rules`, and `lockdowns`. Required.
    - `access-rules` : Access Rules are a way to allow, challenge, or block requests to your website. You can apply access rules to one domain only or all domains in the same service instance.
    - `ua-rules` : Perform access control when matching the exact UserAgent reported by the client. The access control mechanisms can be defined within a rule to help manage traffic from particular clients. This enables you to customize the access to your site.
    - `lockdowns` : Lock access to URLs in this domain to only permitted addresses or address ranges.

`-d, --domain`
:   DNS Domain ID. For `ua-rules` and `lockdowns` type rule, it is a required parameter.

`--json`
:   The JSON file or JSON string that is used to describe a firewall rule. Required.
    - For `--type access-rules`: The JSON data that describes a firewall access rule is as follows.
        - Option fields are `mode`, `notes`.
            - `mode` : The type of action to perform. Valid values are `block`, `challenge`, `whitelist`, and `js_challenge`.
            - `notes` : Some useful information about this rule to help identify the purpose of it.

    Sample JSON data:

```json
{
   "mode": "challenge",
   "notes": "This rule is added because of event X that occurred on date xyz",
}
```
{: codeblock}

- For `--type ua-rules` : The JSON data that describes a user-agent rule is as follows.
    - Required fields are `mode`, `configuration`.
        - `mode` : The type of action to perform. Valid values are `block`, `challenge`, and `js_challenge`.
        - `configuration` : Target/Value pair to use for this rule.
            - `target` : The request property to target. Valid value is `ua`.
            - `value` : The exact UserAgent string to match with this rule.
    - Option fields are `paused`, `description`.
        - `paused` : Whether this rule is currently disabled.
        - `description` : Some useful information about this rule to help identify the purpose of it.

    Sample JSON data:

```json
{
   "mode": "block",
   "configuration": {
      "target": "ua",
      "value": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/603.2.4 (KHTML, like Gecko) Version/10.1.1 Safari/603.2.4"
   }
}
```
{: codeblock}

- For `--type lockdowns` : The JSON data that describes a lockdown rule is as follows.
    - Required fields are `urls`, `configurations`.
        - `urls` : URLs to be included in this rule definition.
            - Wildcards are permitted.
            - The URL pattern entered here is escaped before use.
            - This field limits the URL to simple wildcard patterns.
        - `configurations` : List of IP addresses or CIDR ranges to use for this rule.
             - This field can include any number of ip or ip_range configurations that can access the provided URLs.
             - `target` : The request property to target. Valid values are `ip` and `ip_range`.
             - `value` : IP addresses or CIDR. If the target is `ip`, then the value must be an IP addresses, otherwise CIDR.
    - Option fields are `paused`, `description`.
        - `paused` : Whether this rule is currently disabled.
        - `description` : Some useful information about this rule to help identify the purpose of it.

Sample JSON data:

```json
{
   "urls": [
      "api.mysite.com/some/endpoint*"
   ],
   "configurations": [
      {
         "target": "ip",
         "value": "127.0.0.1"
      },
      {
         "target": "ip_range",
         "value": " 2.2.2.0/24"
      }
   ]
}
```
{: codeblock}

`-s, --json-str`
:   *Deprecated*. The JSON data that describes a firewall rule.

`-j, --json-file`
:   *Deprecated*. A file contains input JSON data.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-firewall-examples}

Update firewall rules.

```sh
ibmcloud cis firewall-update bc014906ccce4e7ea2e28be7df70d0d2 -t access-rules --json '{"mode": "challenge", "notes": "This rule is added because of event X that occurred on date xyz"}' -i "cis-demo"
ibmcloud cis firewall-update 4af47b1518be478aa2c8f024af1c0bad -t ua-rules -d 31984fea73a15b45779fa0df4ef62f9b --json '{"mode": "block", "configuration": {"target": "ua", "value": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/603.2.4 (KHTML, like Gecko) Version/10.1.1 Safari/603.2.4"}}' -i -i "cis-demo"
ibmcloud cis firewall-update e6106d7ec58e47ebb2fa053dedcd7dcb -t lockdowns -d 31984fea73a15b45779fa0df4ef62f9b --json '{"urls": ["api.mysite.com/some/endpoint*"], "configurations": [{"target": "ip", "value": "127.0.0.1"}, {"target": "ip_range", "value": "2.2.2.0/24"}]}' -i "cis-demo"
```
{: codeblock}


### `ibmcloud cis firewalls`
{: #list-firewall}

List firewall rules.

```sh
ibmcloud cis firewalls (-t, --type Type) [-d, --domain DNS_DOMAIN_ID] [--page PAGE] [--per-page PER_PAGE ] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #list-firewall-options}

`-t, --type`
:   The type of firewall rule to create. Valid values are `access-rules`, `ua-rules`, and `lockdowns`. Required.
    - `access-rules` : Access Rules are a way to allow, challenge, or block requests to your website. You can apply access rules to one domain only or all domains in the same service instance.
    - `ua-rules` : Perform access control when matching the exact UserAgent reported by the client. The access control mechanisms can be defined within a rule to help manage traffic from particular clients. This action enables you to customize the access to your site.
    - `lockdowns` : Lock access to URLs in this domain to only permitted addresses or address ranges.

`-d, --domain`
:   DNS Domain ID. For `ua-rules` and `lockdowns` type rule, it is a required parameter.

`--page`
:   Page number of paginated results. The default value is `0`.

`--per-page`
:   Maximum number of access rules per page. The minimum value is `5`. The default value is `20`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-firewall-examples}

List firewall rules.

```sh
ibmcloud cis firewalls -t access-rules -i "cis-demo"
ibmcloud cis firewalls -t ua-rules -d 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
ibmcloud cis firewalls -t lockdown -d 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: codeblock}


### `ibmcloud cis firewall`
{: #get-firewall-detail}

Get details of a firewall rule.

```sh
ibmcloud cis firewall FIREWALL_RULE_ID (-t, --type Type) [-d, --domain DNS_DOMAIN_ID] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #get-firewall-detail-options}

`FIREWALL_RULE_ID`
:   The ID of firewall rule. Required.

`-t, --type`
:   Type of firewall rule to create. Valid values are `access-rules`, `ua-rules`, and `lockdowns`.
    - `access-rules` : Access Rules are a way to allow, challenge, or block requests to your website. You can apply access rules to one domain only or all domains in the same service instance.
    - `ua-rules` : Perform access control when matching the exact UserAgent reported by the client. The access control mechanisms can be defined within a rule to help manage traffic from particular clients. This enables you to customize the access to your site.
    - `lockdowns` : Lock access to URLs in this domain to only permitted addresses or address ranges.

`-d, --domain`
:   DNS Domain ID. For `ua-rules` and `lockdowns` type rule, it is a required parameter.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #get-firewall-detail-examples}

Get firewall rule details.

```sh
ibmcloud cis firewall dc014906ccce4e7ea2e28be7df70d0d2 -t access-rules -i "cis-demo"
ibmcloud cis firewall bc014906ccce4e7ea2e28be7df70d0d2 -t access-rules -d 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
ibmcloud cis firewall 4af47b1518be478aa2c8f024af1c0bad -t ua-rules -d 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
ibmcloud cis firewall e6106d7ec58e47ebb2fa053dedcd7dcb -t lockdown -d 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: codeblock}


### `ibmcloud cis firewall-delete`
{: #delete-firewall}

Delete a firewall rule by ID.

```sh
ibmcloud cis firewall-delete FIREWALL_RULE_ID (-t, --type Type) [-d, --domain DNS_DOMAIN_ID] [-i, --instance INSTANCE]
```

#### Command options
{: #delete-firewall-options}

`FIREWALL_RULE_ID`
:   The ID of firewall rule. Required.

`-t, --type`
:   Type of firewall rule to create. Valid values are `access-rules`, `ua-rules`, and `lockdowns`. Required.
    - `access-rules` : Access Rules are a way to allow, challenge, or block requests to your website. You can apply access rules to one domain only or all domains in the same service instance.
    - `ua-rules` : Perform access control when matching the exact UserAgent reported by the client. The access control mechanisms can be defined within a rule to help manage traffic from particular clients. This field enables you to customize the access to your site.
    - `lockdowns` : Lock access to URLs in this domain to only permitted addresses or address ranges.

`-d, --domain`
:   DNS Domain ID. For `ua-rules` and `lockdowns` type rule, it is a required parameter.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #delete-firewall-examples}

Delete a firewall rule.

```sh
ibmcloud cis firewall-delete dc014906ccce4e7ea2e28be7df70d0d2 -t access-rules -i "cis-demo"
ibmcloud cis firewall-delete bc014906ccce4e7ea2e28be7df70d0d2 -t access-rules -d 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
ibmcloud cis firewall-delete 4af47b1518be478aa2c8f024af1c0bad -t ua-rules -d 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
ibmcloud cis firewall-delete e6106d7ec58e47ebb2fa053dedcd7dcb -t lockdown -d 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

## Firewall rules
{: #firewall-rules}

Manipulate how firewall rules perform by using the following `firewall-rules` commands:

### `ibmcloud cis firewall-rules`
{: #list-firewall-rules}

Retrieve a list of currently existing firewall-rules for a DNS domain.

```sh
ibmcloud cis firewall-rules DNS_DOMAIN_ID [--page PAGE] [--per-page PER_PAGE] [-i, --instance INSTANCE] [--output FORMAT
```

#### Command options
{: #list-firewall-rules-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--page`
:   Page number of paginated results. The default value is `1`.

`--per-page`
:   Number of firewall rules per page. The minimum value is `5` and the maximum value is `100`. The default value is `25`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-firewall-rules-examples}

List existing firewall-rules in the domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis firewall-rules 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis firewall-rule`
{: #show-a-firewall-rule}

Retrieve a specific firewall-rule for a DNS domain.

```sh
ibmcloud cis firewall-rule DNS_DOMAIN_ID FIREWALL_RULE_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-a-firewall-rule-options}


`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`FIREWALL_RULE_ID`
:   The ID of firewall-rule. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-a-firewall-rule-examples}

Get the details of firewall-rule `372e67954025e0ba6aaa6d586b9e0b60`.

```sh
ibmcloud cis firewall-rule 31984fea73a15b45779fa0df4ef62f9b 372e67954025e0ba6aaa6d586b9e0b60 -i "cis-demo"
```
{: pre}

### `ibmcloud cis firewall-rule-create`
{: #create-a-firewall-rule}

Create a firewall-rule for a DNS domain.

```sh
ibmcloud cis firewall-rule-create DNS_DOMAIN_ID --expression EXPRESSION --action ACTION [--priority PRIORITY] [--paused on|off] [--products PRODUCTS][--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
ibmcloud cis firewall-rule-create DNS_DOMAIN_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis firewall-rule-create DNS_DOMAIN_ID (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #create-a-firewall-rule-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--expression`
:   A filter expression. For example, `ip.src eq 93.184.216.0`.

`--action`
:   The rule action to perform. Valid values are `log`, `allow`, `challenge`, `js_challenge`, `block`, and `bypass`.

`--priority`
:   The rule's priority. Valid values range from `0` to `2147483647`. The value `0` means to set to the default value.

`--description`
:   To briefly describe the rule.

`--paused`
:   Indicates whether the rule is active or not. Valid values are `on` and `off`. The default value is `off`.

`--products`
:   The list of security products to be bypassed. Valid values are `zoneLockdown`, `uaBlock`, `bic`, `hot`, `securityLevel`, `rateLimit`, and `waf`.

`--json`
:   The JSON file or JSON strin that isused to describe a firewall-rule.
    - The required fields in JSON data are `expression` and `action`.
        - `expression` : A filter expression. For example, `ip.src eq 93.184.216.0`
        - `action` : The rule action to perform. Valid values are `log`, `allow`, `challenge`, `js_challenge`, `block`, and `bypass`.
    - The optional fields are `description`, `priority`, `paused`, `products`.
        - `description` : To briefly describe the rule.
        - `priority` : The rule's priority. Valid values range from `0` to `2147483647`. The value `0` means to set to the default value.
        - `paused` : Indicates whether the rule is active or not. Valid values are `on` and `off`. The default value is `off`.
        - `products` : The list of security products to be bypassed. Valid values are `zoneLockdown`, `uaBlock`, `bic`, `hot`, `securityLevel`, `rateLimit`, and `waf` For example, --products zoneLockdown, rateLimit

   Sample JSON data:

```json
{
   "expression": "ip.src eq 93.184.216.1 and http.request.uri.path ~ \"^.*/wp-login.php$\"",
   "action": "allow",
   "priority": 100,
   "paused": false,
   "description": "do not challenge login from office"
}
```
{: codeblock}

`-s, --json-str`
:    *Deprecated*. The JSON data that describes a firewall-rule.

`-j, --json-file`
:   *Deprecated*. A file contains input JSON data.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #create-a-firewall-rule-examples}

Create a firewall-rule in the domain `372e67954025e0ba6aaa6d586b9e0b60`.

```sh
ibmcloud cis firewall-rule-create 31984fea73a15b45779fa0df4ef62f9b --expression "ip.src eq 93.184.216.1 and http.request.uri.path ~ \"^.*/wp-login.php$\""  --action allow --priority 200 --paused off --description "do not challenge login from office" -i "cis-demo"

ibmcloud cis firewall-rule-create 31984fea73a15b45779fa0df4ef62f9b --json '{"expression": "ip.src eq 93.184.216.1 and http.request.uri.path ~ \"^.*/wp-login.php$\"", "action": "allow", "priority": 100, "paused": false, "description": "do not challenge login from office"}' -i "cis-demo"
```
{: codeblock}

### `ibmcloud cis firewall-rule-update`
{: #update-a-firewall-rule}

Update a specific firewall-rule for a DNS domain.

```sh
ibmcloud cis firewall-rule-update DNS_DOMAIN_ID FIREWALL_RULE_ID [--expression EXPRESSION] [--action ACTION] [--priority PRIORITY] [--paused on|off] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
ibmcloud cis firewall-rule-update DNS_DOMAIN_ID FIREWALL_RULE_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis firewall-rule-update DNS_DOMAIN_ID FIREWALL_RULE_ID (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-a-firewall-rule-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`FIREWALL_RULE_ID`
:   The ID of firewall-rule. Required.

`--expression`
:   A filter expression. For example, `ip.src eq 93.184.216.0`.

`--action`
:   The rule action to perform. Valid values are `log`, `allow`, `challenge`, `js_challenge`, `block`, and `bypass`.

`--priority`
:   The rule's priority. Valid values range from `0` to `2147483647`. The value `0` means to set to the default value.

`--description`
:   To briefly describe the rule.

`--paused`
:   Indicates whether the rule is active or not. Valid values are `on` and `off`. The default value is `off`.

`--products`
:   The list of security products to be bypassed. Valid values are `zoneLockdown`, `uaBlock`, `bic`, `hot`, `securityLevel`, `rateLimit`, and `waf`.

`--json`
:   The JSON file or JSON string that is used to describe a firewall-rule.
    - The required fields in JSON data are `expression`, and `action`.
        - `expression` : A filter expression. For example, `ip.src eq 93.184.216.0`
        - `action` : The rule action to perform. Valid values are `log`, `allow`, `challenge`, `js_challenge`, `block`, and `bypass`.
    - The optional fields are `description`, `priority`, `paused`, `products`.
        - `description` : To briefly describe the rule.
        - `priority` : The rule's priority. Valid values range from `0` to `2147483647`. The value `0` means to set to the default value.
        - `paused` : Indicates whether the rule is active or not. Valid values are `on` and `off`. The default value is `off`.
        - `products` : The list of security products to be bypassed. Valid values are `zoneLockdown`, `uaBlock`, `bic`, `hot`, `securityLevel`, `rateLimit`, and `waf` For example, --products zoneLockdown, rateLimit
    - Note: Fields `description`, `priority`, `paused`, which aren't explicitly set in JSON data are overwritten by the default value.

Sample JSON data:

```json
{
   "expression": "ip.src eq 93.184.216.1 and http.request.uri.path ~ \"^.*/wp-login.php$\"",
   "action": "allow",
   "priority": 100,
   "paused": false,
   "description": "do not challenge login from office"
}
```
{: codeblock}

`-s, --json-str`
:   *Deprecated*. The JSON data that describes a firewall-rule.

`-j, --json-file`
:   *Deprecated*. A file contains input JSON data.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-a-firewall-rule-examples}

Update firewall-rule `372e67954025e0ba6aaa6d586b9e0b60`.

```sh
ibmcloud cis firewall-rule-update 31984fea73a15b45779fa0df4ef62f9b 372e67954025e0ba6aaa6d586b9e0b60 --expression "ip.src eq 93.184.216.1 and http.request.uri.path ~ \"^.*/wp-login.php$\""  --action allow --priority 200 --paused off --description "do not challenge login from office" -i "cis-demo"

ibmcloud cis firewall-rule-update 31984fea73a15b45779fa0df4ef62f9b 372e67954025e0ba6aaa6d586b9e0b60 --json '{"expression": "ip.src eq 93.184.216.1 and http.request.uri.path ~ \"^.*/wp-login.php$\"", "action": "allow", "priority": 100, "paused": false, "description": "do not challenge login from office"}' -i "cis-demo"
```
{: pre}

### `ibmcloud cis firewall-rule-delete`
{: #delete-a-Firewall-rule}

Delete a specific firewall-rule for a DNS domain.

```sh
ibmcloud cis firewall-rule-delete DNS_DOMAIN_ID FIREWALL_RULE_ID [-i, --instance INSTANCE]
```

#### Command options
{: #delete-a-firewall-rule-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`FIREWALL_RULE_ID`
:   The ID of firewall-rule. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #delete-a-firewall-rule-examples}

Delete firewall-rule `372e67954025e0ba6aaa6d586b9e0b60`.

```sh
ibmcloud cis firewall-rule-delete 31984fea73a15b45779fa0df4ef62f9b 372e67954025e0ba6aaa6d586b9e0b60 -i "cis-demo"
```
{: pre}

### `ibmcloud cis firewall-rule-validate`
{: #validate-a-firewall-rule-expression}

Validate a firewall-rule expression.

```sh
ibmcloud cis firewall-rule-validate DNS_DOMAIN_ID EXPRESSION [-i, --instance INSTANCE]
```

#### Command options
{: #validate-a-firewall-rule-expression-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`EXPRESSION`
:   The filter expression. For example, `ip.src eq 93.184.216.0`. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #validate-a-firewall-rule-expression-examples}

Validate firewall-rule expression `ip.src eq 93.184.216.0`.

```sh
ibmcloud cis firewall-rule-validate 31984fea73a15b45779fa0df4ef62f9b "ip.src eq 93.184.216.0" -i "cis-demo"
```
{: pre}

## Global load balancer
{: #glb}

Manipulate global load balancers by using the following `glb` commands.

### `ibmcloud cis glb-create`
{: #create-glb}

Create a global load balancer under a DNS domain.

```sh
ibmcloud cis glb-create DNS_DOMAIN_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis glb-create DNS_DOMAIN_ID (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #create-glb-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--json`
:   The JSON file or JSON string that is used to describe a global load balancer. Required.
    - The required fields in JSON data are `name`, `fallback_pool` and `default_pools` :
        - `name` : The DNS hostname to associate with your load balancer.
        - `fallback_pool` : The pool ID to use when all other pools are detected as unhealthy.
        - `default_pools` : A list of pool IDs ordered by their failover priority.
    - The optional fields are `description`, `ttl`, `region_pools`, `proxied`, `enabled`, `session_affinity`,  `session_affinity_ttl`, `steering_policy`:
        - `description` : The description of your load balancer.
        - `ttl`: Time to live (TTL) of the DNS entry for the IP address returned by this load balancer.
        - `region_pools` : A mapping of region and country codes to a list of pool IDs (ordered by their failover priority) for the region.
        - `proxied` : Control whether traffic should flow through the security and performance functions on CIS.
        - `enabled` : Whether to enable (the default) this load balancer.
        - `session_affinity` : Ensures that a user's requests are consistently directed to the same backend server during a session. Valid values are `cookie` and `none`.
        - `session_affinity_ttl` : Time, in seconds, until this load balancers session affinity cookie expires after it is created. Valid value is between `[1800, 604800]`. The default value is `82800`.
        - `steering_policy` : Valid values for `steering_policy` are `off`, `geo`, `random`, `dynamic_latency`.
             - `off` : Use `default_pools`.
             - `geo` : Use `region_pools/pop_pools`.
             - `random` : Select a pool randomly.
             - `dynamic_latency` : Use round-trip time to select the closest pool in `default_pools` (requires pool health checks).

Sample JSON data:

```json
{
      "name": "www.example.com",
      "fallback_pool": "17b5962d775c646f3f9725cbc7a53df4",
      "default_pools": [
         "17b5962d775c646f3f9725cbc7a53df4",
         "9290f38c5d07c2e2f4df57b1f61d4196"
      ],
      "description": "Example global load balancer.",
      "ttl": 60,
      "region_pools": {
         "WNAM": [
               "de90f38ced07c2e2f4df50b1f61d4194",
               "9290f38c5d07c2e2f4df57b1f61d4196"
         ],
         "ENAM": [
               "00920f38ce07c2e2f4df50b1f61d4194"
         ]
      }
}
```
{: codeblock}

`-s, --json-str`
:   *Deprecated*. The JSON data describing a global load balancer.

`-j, --json-file`
:   *Deprecated*. A file contains input JSON data.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #create-glb-examples}

Create a global load balancer in the domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis glb-create 31984fea73a15b45779fa0df4ef62f9b --json '{"description":"Example global load balancer.","name":"www.example.com","ttl":60,"fallback_pool":"17b5962d775c646f3f9725cbc7a53df4","default_pools":["17b5962d775c646f3f9725cbc7a53df4","9290f38c5d07c2e2f4df57b1f61d4196"],"region_pools":{"WNAM":["de90f38ced07c2e2f4df50b1f61d4194","9290f38c5d07c2e2f4df57b1f61d4196"],"ENAM":["00920f38ce07c2e2f4df50b1f61d4194"]}}' -i "cis-demo"
```
{: pre}

### `ibmcloud cis glb-update`
{: #update-glb}

Update a global load balancer under a DNS domain.

```sh
ibmcloud cis glb-update DNS_DOMAIN_ID GLB_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis glb-update DNS_DOMAIN_ID GLB_ID (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-glb-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`GLB_ID`
:   The ID of the global load balancer. Required.

`--json`
:   The JSON file or JSON string that is used to describe a global load balancer. Required.
    - The required fields in JSON data are `name`, `fallback_pool`, and `default_pools` :
        - `name` : The DNS hostname to associate with your load balancer.
        - `fallback_pool` : The pool ID to use when all other pools are detected as unhealthy.
        - `default_pools` : A list of pool IDs ordered by their failover priority.
    - The optional fields are `description`, `ttl`, `region_pools`, `proxied`, `enabled`, `session_affinity`, `session_affinity_ttl`, `steering_policy`:
        - `description` : The description of your Load Balancer.
        - `ttl` : Time to live (TTL) of the DNS entry for the IP address returned by this load balancer.
        - `region_pools` : A mapping of region and country codes to a list of pool IDs (ordered by their failover priority) for the region.
        - `proxied` : Control whether traffic must flow through the security and performance functions on CIS.
        - `enabled` : Whether to enable (the default) this load balancer.
        - `session_affinity` : Ensures that a user's requests are consistently directed to the same backend server during a session. Valid values are `cookie` and `none`.
        - `session_affinity_ttl` : Time, in seconds, until this load balancers session affinity cookie expires it is created. Valid value is between `[1800, 604800]`. The default value is `82800`.
        - `steering_policy` : Valid values for `steering_policy` are `off`, `geo`, `random`, `dynamic_latency`.
             - `off` : Use `default_pools`.
             - `geo` : Use `region_pools/pop_pools`.
             - `random` : Select a pool randomly.
             - `dynamic_latency` : Use round-trip time to select the closest pool in `default_pools` (requires pool health checks).

Sample JSON data:

```json
{
      "name": "www.example.com",
      "fallback_pool": "17b5962d775c646f3f9725cbc7a53df4",
      "default_pools": [
         "17b5962d775c646f3f9725cbc7a53df4",
         "9290f38c5d07c2e2f4df57b1f61d4196"
      ],
      "description": "Example global load balancer.",
      "ttl": 60,
      "region_pools": {
         "WNAM": [
               "de90f38ced07c2e2f4df50b1f61d4194",
               "9290f38c5d07c2e2f4df57b1f61d4196"
         ],
         "ENAM": [
               "00920f38ce07c2e2f4df50b1f61d4194"
         ]
      }
}
```
{: codeblock}

`-s, --json-str`
:   *Deprecated*. The JSON data describing a global load balancer.

`-j, --json-file`
:   *Deprecated*. A file contains input JSON data.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-glb-examples}

Update the global load balancer `699d98642c564d2e855e9661899b7252` in the domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis glb-update 31984fea73a15b45779fa0df4ef62f9b 699d98642c564d2e855e9661899b7252 --json '{"description":"Example global load balancer.","name":"www.example.com","ttl":60,"fallback_pool":"17b5962d775c646f3f9725cbc7a53df4","default_pools":["17b5962d775c646f3f9725cbc7a53df4","9290f38c5d07c2e2f4df57b1f61d4196"],"region_pools":{"WNAM":["de90f38ced07c2e2f4df50b1f61d4194","9290f38c5d07c2e2f4df57b1f61d4196"],"ENAM":["00920f38ce07c2e2f4df50b1f61d4194"]}}' -i "cis-demo"
```
{: pre}


### `ibmcloud cis glb`
{: #show-glb}

Show a global load balancer under a DNS domain.

```sh
ibmcloud cis glb DNS_DOMAIN_ID GLB_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-glb-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`GLB_ID`
:   The ID of the global load balancer. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-glb-examples}

Show global load balancer `699d98642c564d2e855e9661899b7252` in domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis glb 31984fea73a15b45779fa0df4ef62f9b 699d98642c564d2e855e9661899b7252 -i "cis-demo"
```
{: pre}


### `ibmcloud cis glb-delete`
{: #delete-glb}

Delete a global load balancer under a DNS domain.

```sh
ibmcloud cis glb-delete DNS_DOMAIN_ID GLB_ID [-i, --instance INSTANCE]
```

#### Command options
{: #delete-glb-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`GLB_ID`
:   The ID of the global load balancer. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #delete-glb-examples}

Delete global load balancer `699d98642c564d2e855e9661899b7252` in domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis glb-delete 31984fea73a15b45779fa0df4ef62f9b 699d98642c564d2e855e9661899b7252 -i "cis-demo"
```
{: pre}


### `ibmcloud cis glbs`
{: #list-glb}

List all load balancers for the domain.

```sh
ibmcloud cis glbs DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #list-glb-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-glb-examples}

List load balancers for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis glbs 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis glb-pools`
{: #list-glb-pools}

List all GLB pools for a service instance.

```sh
ibmcloud cis glb-pools [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #list-glb-pools-options}

`-i, --instance`
:  Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   Specify the output format. Only JSON is supported.

#### Examples
{: #list-glb-pools-examples}

List all GLB pools for instance `cis-demo`.

```sh
ibmcloud cis glb-pools -i "cis-demo"
```
{: pre}

### `ibmcloud cis glb-pool-create`
{: #create-glb-pool}

Create a GLB pool for a service instance.

```sh
ibmcloud cis glb-pool-create (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis glb-pool-create (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #create-glb-pool-options}

`--json`
:    The JSON file or JSON string that is used to describe a GLB pool. Required.
    - The required fields in JSON data are `name`, `origins` and `check_regions` :
        - `name` : A short name (tag) for the pool.
        - `origins` : A list of origins within this pool.
        - `check_regions` : A list of geographic region code.
    - The optional fields are `description`, `minimum_origins`, `enabled`, `monitor`.

Sample JSON data:

```json
{
   "name": "us-pool",
   "description": "application server pool in US",
   "origins": [
      {
            "name": "us-app-dal01",
            "address": "1.1.1.1",
            "enabled": true,
            "header": {
               "host": ["test.com"]
            }
      },
      {
            "name": "us-app-dal02",
            "address": "2.2.2.2",
            "enabled": true,
            "header": {
               "host": ["example.com"]
            }
      }
   ],
   "minimum_origins": 1,
   "check_regions": [ "WNAM" ],
   "monitor": "f1aba936b94213e5b8dca0c0dbf1f9cc",
   "enabled": true
}
```
{: codeblock}

`-s, --json-str`
:    *Deprecated*. The JSON data used to describe a GLB pool.

`-j, --json-file`
:   *Deprecated*. A file contains input JSON data.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #create-glb-pool-examples}

Create a GLB pool for instance `cis-demo`.

```sh
ibmcloud cis glb-pool-create --json '{"description":"application server pool in US", "name":"us-pool", "enabled":true, "check_regions":["WNAM"], "minimum_origins":1,"monitor":"f1aba936b94213e5b8dca0c0dbf1f9cc", "origins":[{"name":"us-app-dal01","address":"1.1.1.1","enabled":true,"header":{"host":["test.com"]}}, {"name":"us-app-dal02","address":"2.2.2.2","enabled":true,"header":{"host":["example.com"]}}]}'-i "cis-demo"
```
{: pre}

### `ibmcloud cis glb-pool`
{: #show-glb-pool}

Show the details of a GLB pool.

```sh
ibmcloud cis glb-pool GLB_POOL_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-glb-pool-options}

`GLB_POOL_ID`
:   The ID of the global load balancer pool. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-glb-pool-examples}

Show the details of the GLB pool `17b5962d775c646f3f9725cbc7a53df4`.

```sh
ibmcloud cis glb-pool 17b5962d775c646f3f9725cbc7a53df4 -i "cis-demo"
```
{: pre}

### `ibmcloud cis glb-pool-delete`
{: #delete-glb-pool}

Delete a GLB pool.

```sh
ibmcloud cis glb-pool-delete GLB_POOL_ID [-i, --instance INSTANCE]
```

#### Command options
{: #delete-glb-pool-options}

`GLB_POOL_ID`
:   The ID of the global load balancer pool. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #delete-glb-pool-examples}

Delete GLB pool `17b5962d775c646f3f9725cbc7a53df4`.

```sh
ibmcloud cis glb-pool-delete 17b5962d775c646f3f9725cbc7a53df4 -i "cis-demo"
```
{: pre}


### `ibmcloud cis glb-pool-update`
{: #update-glb-pool}

Update a GLB pool.

```sh
ibmcloud cis glb-pool-update GLB_POOL_ID [--enable-origin ORIGIN_NAME --enable-origin ORIGIN_NAME ...] [--disable-origin ORIGIN_NAME --disable-origin ORIGIN_NAME ...] [--add-origin ORIGIN_PARAMETER --add-origin ORIGIN_PARAMETER ...] [--remove-origin ORIGIN_NAME --remove-origin ORIGIN_NAME ...]  [-i, --instance INSTANCE] [--output FORMAT]
ibmcloud cis glb-pool-update GLB_POOL_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis glb-pool-update GLB_POOL_ID (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-glb-pool-options}

`GLB_POOL_ID`
:   The ID of the global load balancer pool. Required.

`--json`
:   The JSON file or JSON string that is used to describe a GLB pool.
    - The required fields in JSON data are `name`, `origins` and `check_regions` :
        - `name` : A short name (tag) for the pool.
        - `origins` : A list of origins within this pool.
        - `check_regions` : A list of geographic region code.
    - The optional fields are `description`, `minimum_origins`, `enabled`, `monitor`.

Sample JSON data:

```json
{
   "name": "us-pool",
   "description": "application server pool in US",
   "origins": [
      {
            "name": "us-app-dal01",
            "address": "1.1.1.1",
            "enabled": true,
            "header": {
               "host": ["example.com"]
            }
      },
      {
            "name": "us-app-dal02",
            "address": "2.2.2.2",
            "enabled": true
      }
   ],
   "minimum_origins": 1,
   "check_regions": [ "WNAM" ],
   "monitor": "f1aba936b94213e5b8dca0c0dbf1f9cc",
   "enabled": true
}
```
{: codeblock}

`--enable-origin`
:   Enable the origin within the Pool. The value can be ORIGIN_NAME or ORIGIN_ADDRESS.

`--disable-origin`
:   Disable the origin within the Pool. The value can be ORIGIN_NAME or ORIGIN_ADDRESS.

`--add-origin`
:   Add an origin into the Pool. ORIGIN_NAME and ORIGIN_ADDRESS are required. For example, --add-origin name=us-app-dal01,address=1.1.1.1,enabled=true,weight=0.5,host=example.com

`--remove-origin`
:   Remove an origin from the Pool. The value can be ORIGIN_NAME or ORIGIN_ADDRESS.

`-s, --json-str`
:   *Deprecated*. The JSON data used to describe a GLB pool.

`-j, --json-file`
:   *Deprecated*. A file contains input JSON data.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-glb-pool-examples}

Update GLB pool `17b5962d775c646f3f9725cbc7a53df4`.

```sh
ibmcloud cis glb-pool-update 17b5962d775c646f3f9725cbc7a53df4 --json '{"description":"application server pool in US", "name":"us-pool", "enabled":true, "check_regions":["WNAM"], "minimum_origins":1,"monitor":"f1aba936b94213e5b8dca0c0dbf1f9cc", "origins":[{"name":"us-app-dal01","address":"1.1.1.1","enabled":true,"header":{"host":["example.com"]}}, {"name":"us-app-dal02","address":"2.2.2.2","enabled":true}]}'-i "cis-demo"
```
{: pre}


### `ibmcloud cis glb-monitors`
{: #list-glb-monitors}

List GLB monitors for a service instance.

```sh
ibmcloud cis glb-monitors [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #list-glb-monitors-options}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-glb-monitors-examples}

List all GLB monitors for instance `cis-demo`.

```sh
ibmcloud cis glb-monitors -i "cis-demo"
```
{: pre}

### `ibmcloud cis glb-monitor-create`
{: #create-glb-monitor}

Create a GLB monitor for a service instance.

```sh
ibmcloud cis glb-monitor-create (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis glb-monitor-create (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #create-glb-monitors-options}

`--json`
:   The JSON file or JSON string that is used to describe a GLB monitor. Required.
    - The required fields in JSON data are `type`.
        - `type` : The protocol to use for the healthcheck. Valid values are `HTTP`, `HTTPS`, and `TCP`.
    - The optional fields are `description`, `timeout`, `retries`, `interval`.
        - `description` : Description.
        - `timeout` : The timeout (in seconds) before marking the health check as failed.
        - `retries` : The number of retries to attempt in case of a timeout before marking the origin as unhealthy.
        - `interval` : The interval between each health check.
    - For `TCP` type health check. Extra required fields are `port`.
        - `port` : The TCP port to use for the health check.
    - For `HTTP/HTTPS` type health check. Extra option fields are `port`, `expected_body`, `expected_codes`, `method`, `path`, `header`, `follow_redirects`, `allow_insecure`.
        - `port` : The TCP port to use for the health check.
        - `expected_body` : A case-insensitive substring to look for in the response body.
        - `expected_codes` : The expected HTTP response code or code range of the health check.
        - `method` : The HTTP method to use for the health check.
        - `path` : The endpoint path to health check against.
        - `header` : The HTTP request headers to send in the health check.
        - `follow_redirects` : Follow redirects if returned by the origin.
        - `allow_insecure` : Do not validate the certificate when monitor use HTTPS.
        - `probe_zone` : Assign this monitor to emulate the specified zone while probing.

   Sample JSON data:

   For HTTP/HTTPS:

```json
{
      "description": "Health monitor of web service",
      "type": "https",
      "method": "GET",
      "path": "/health",
      "header": {
         "Host": [
            "example.com"
         ],
         "X-App-ID": [
            "abc123"
         ]
      },
      "timeout": 5,
      "retries": 2,
      "interval": 90,
      "follow_redirects": true,
      "allow_insecure": false,
      "expected_codes": "2xx",
      "expected_body": "alive",
      "probe_zone": "example.com"
}
```
{: codeblock}

For TCP:

```json
{
      "description": "Health monitor of TCP",
      "type": "tcp",
      "port": 80,
      "timeout": 5,
      "retries": 2,
      "interval": 90
}
```
{: codeblock}

`-s, --json-str`
:   *Deprecated*. The JSON data used to describe a GLB monitor.

`-j, --json-file`
:   *Deprecated*. A file contains input JSON data.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #create-glb-monitors-examples}

Create a GLB monitors under instance `cis-demo`.

```sh
ibmcloud cis glb-monitor-create --json '{"type":"https", "description":"Health monitor of web service", "method":"GET", "path":"/health", "header":{"Host":["example.com"],"X-App-ID":["abc123"]}, "port":8080, "timeout":5, "retries":2, "interval":90, "expected_body":"alive", "expected_codes":"2xx", "follow_redirects":true, "allow_insecure":true}' -i "cis-demo"
```
{: pre}

### `ibmcloud cis glb-monitor`
{: #show-glb-monitor}

Show the details of a GLB monitor.

```sh
ibmcloud cis glb-monitor GLB_MON_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-glb-monitor-options}

`GLB_MON_ID`
:   The ID of the global load balancer monitor. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-glb-monitor-examples}

Show the details of the GLB monitor `f1aba936b94213e5b8dca0c0dbf1f9cc`.

```sh
ibmcloud cis glb-monitor f1aba936b94213e5b8dca0c0dbf1f9cc -i "cis-demo"
```
{: pre}

### `ibmcloud cis glb-monitor-delete`
{: #delete-glb-monitor}

Delete the GLB monitor for a service instance.

```sh
ibmcloud cis glb-monitor-delete GLB_MON_ID [-i, --instance INSTANCE]
```

#### Command options
{: #delete-glb-monitor-options}

`GLB_MON_ID`
:   The ID of global load balancer monitor. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #delete-glb-monitor-examples}

Delete the GLB monitor `f1aba936b94213e5b8dca0c0dbf1f9cc`.

```sh
ibmcloud cis glb-monitor-delete f1aba936b94213e5b8dca0c0dbf1f9cc -i "cis-demo"
```
{: pre}


### `ibmcloud cis glb-monitor-update`
{: #update-glb-monitor}

Update the GLB monitor for a service instance.

```sh
ibmcloud cis glb-monitor-update GLB_MON_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis glb-monitor-update GLB_MON_ID (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-glb-monitor-options}

`GLB_MON_ID`
:   The ID of the global load balancer monitor. Required.

`--json`
:   The JSON file or JSON string that is used to describe a GLB monitor. Required.
    - The required fields in JSON data are `type`.
        - `type` : The protocol to use for the healthcheck. Valid values are `HTTP`, `HTTPS`, and `TCP`.
    - The optional fields are `description`, `timeout`, `retries`, `interval`.
        - `description` : Description.
        - `timeout` : The timeout (in seconds) before marking the health check as failed.
        - `retries` : The number of retries to attempt in case of a timeout before marking the origin as unhealthy.
        - `interval` : The interval between each health check.
    - For `TCP` type health check. Extra required fields are `port`.
        - `port` : The TCP port to use for the health check.
    - For `HTTP/HTTPS` type health check. Extra option fields are `port`, `expected_body`, `expected_codes`, `method`, `path`, `header`, `follow_redirects`, `allow_insecure`.
        - `port` : The TCP port to use for the health check.
        - `expected_body` : A case-insensitive substring to look for in the response body.
        - `expected_codes` : The expected HTTP response code or code range of the health check.
        - `method` : The HTTP method to use for the health check.
        - `path` : The endpoint path to health check against.
        - `header` : The HTTP request headers to send in the health check.
        - `follow_redirects` : Follow redirects if returned by the origin.
        - `allow_insecure` : Do not validate the certificate when monitor use HTTPS.
        - `probe_zone` : Assign this monitor to emulate the specified zone while probing.

   Sample JSON data:

   For HTTP/HTTPS:

```json
{
      "description": "Health monitor of web service",
      "type": "https",
      "method": "GET",
      "path": "/health",
      "header": {
         "Host": [
            "example.com"
         ],
         "X-App-ID": [
            "abc123"
         ]
      },
      "timeout": 5,
      "retries": 2,
      "interval": 90,
      "follow_redirects": true,
      "allow_insecure": false,
      "expected_codes": "2xx",
      "expected_body": "alive",
      "probe_zone": "example.com"
}
```
{: codeblock}

For TCP:

```json
{
      "description": "Health monitor of TCP",
      "type": "tcp",
      "port": 80,
      "timeout": 5,
      "retries": 2,
      "interval": 90
}
```
{: codeblock}

`-s, --json-str`
:   *Deprecated*. The JSON data used to describe a GLB monitor.

`-j, --json-file`
:   *Deprecated*. A file contains input JSON data.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-glb-monitors-examples}

Update GLB monitors `f1aba936b94213e5b8dca0c0dbf1f9cc` under instance `cis-demo`.

```sh
ibmcloud cis glb-monitor-update f1aba936b94213e5b8dca0c0dbf1f9cc --json '{"type":"https", "description":"Health monitor of web service", "method":"GET", "path":"/health", "header":{"Host":["example.com"],"X-App-ID":["abc123"]}, "port":8080, "timeout":5, "retries":2, "interval":90, "expected_body":"alive", "expected_codes":"2xx", "follow_redirects":true, "allow_insecure":true}' -i "cis-demo"
```
{: pre}

### `ibmcloud cis glb-events`
{: #get-glb-events}

List status changes from origins that are connected to a GLB monitor.

```sh
ibmcloud cis glb-events [-s, --since START_DATE] [-u, --until END_DATE] [--origin-name ORIGIN_NAME] [--pool-name POOL_NAME]
                        [--origin-healthy (true | false)] [--pool-healthy (true | false)]
                        [-i, --instance INSTANCE]  [--output FORMAT]
```

#### Command options
{: #get-glb-events-options}

`-s, --since`
:   Start date requesting data period in the ISO8601 format. For example `2018-11-26`.

`-u, --until`
:   End date requesting data period in the ISO8601 format. For example `2018-11-28`.

`--origin-name`
:   The name for the origin to filter for.

`--pool-name`
:   The name for the pool to filter for.

`--origin-healthy`
:   If true, filter events where the origin status is healthy, if false, filter events where the origin status is unhealthy. The default value is `true` and valid values are `true` and `false`.

`--pool-healthy`
:   If true, filter events where the pool status is healthy, if false, filter events where the pool status is unhealthy. The default value is `true` and valid values are `true` and `false`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #get-glb-events-examples}

Get glb events in instance `cis-demo`.

```sh
ibmcloud cis glb-events -s "2020-05-20" -u "2020-05-22" --origin-name "dal09" --origin-healthy true -i "cis-demo"
```
{: pre}

## Instant Logs
{: #instant-logs}

Create and get logs of serverless functions instantly by using the following `instant-log` commands.

### `instant-log-create`
{: #create-instant-log}

Creates an instant logs job for a domain. The command returns a `Destination`, which is valid for 60 minutes.

```sh
cis instant-log-create DNS_DOMAIN_ID [--fields FIELD1,FIELD2,FIELD3|all] [--filter FILTER] [--sample SAMPLE] [-i, --instance INSTANCE] [--output FORMAT] [-h, --help HELP]
```

You can have only one active Instant Logs session per domain and the maximum session time is 60 minutes.
{: note}

#### Command options
{: #create-instant-logs-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--fields`
:   Define the field set in return.

    - This field must be specified as a comma-separated list without any whitespaces, and all fields must exist.
    - The order in which fields are specified doesn't matter, and the order of fields in the response is not specified.
    - The fields are expected to be case-sensitive.

`--filter`
:    Filters to drill down into specific events. Filters consist of three parts: key, operator, and value. For information about supported operators, see [Using fields, functions, and expressions](/docs/cis?topic=cis-fields-and-expressions).

`--sample`
:    The sample rate of the records set by the client: `sample`: 1 is 100% of records.

`-i, --instance`
:    Instance name or ID. If instance name or ID is not set, the context instance that is specified by `cis instance-set INSTANCE` is used.

`--output`
:    The output format. Currently, `json` is the only supported value.

`-h, --help`
:    Get help on this command.

#### Examples
{: #examples-instant-logs-create}

Create an instant log for `dns-domain`:

```sh
cis instant-log-create dns-domain [--fields all] [--filter FILTER] [--sample 1] [-i cis-demo]
```

The following are three examples of filters:

* Filter when client IP country is not Canada:

   `"filter": "{\"where\":{\"and\":[{\"key\":\"ClientCountry\",\"operator\":\"neq\",\"value\":\"ca\"}]}}"`
   {: pre}

* Filter when the status code returned from CIS is either 200 or 201:

   `"filter": "{\"where\":{\"and\":[{\"key\":\"EdgeResponseStatus\",\"operator\":\"in\",\"value\":\"200,201\"}]}}"`
   {: pre}

* Filter when the request path contains "/static" and the request hostname is "example.com":

   `"filter": "{\"where\":{\"and\":[{\"key\":\"ClientRequestPath\",\"operator\":\"contains\",\"value\":\"/static\"}, {\"where\":{\"and\":[{\"key\":\"ClientRequestHost\",\"operator\":\"eq\",\"value\":\"example.com\"}]}}"`
   {: pre}

### `instant-log-get`
{: #get-instant-log}

Get the instant logs job for a domain.

```sh
cis instant-log-get DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT] [-h, --help HELP]
```

#### Command options
{: #get-instant-logs-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

`-h, --help`
:   Help on this command.

#### Example
{: #examples-instant-logs-get}

Get the instant logs job for `dns-domain`:

```sh
cis instant-log-get dns-domain [-i cis-demo]
```
{: codeblock}

## Logpull
{: #logpull-section}

### `ibmcloud cis logpull`
{: #cli-logpull}

Manipulate Logpull services by using the following `logpull` commands.

```sh
ibmcloud cis logpull DNS_DOMAIN_ID --available-fields [--output FORMAT]
```

#### Command options
{: #command-options-logpull}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--available-fields`
:   List of all available fields.

`--ray-id`
:   Lookup logs by specific Ray ID.

`--fields`
:   Define the field set in return. This field must be specified as a comma-separated list without any spaces, and all fields must exist. The order in which fields are specified doesn't matter, and the order of fields in the response is not specified. Note that fields are expected to be case sensitive.

`--start`
:   The (inclusive) beginning of the requested time frame. This can be a unix timestamp (in seconds or nanoseconds), or an absolute timestamp that conforms to RFC 3339. Currently, it cannot exceed a time in the past greater than 7 days. Default is 65 minutes earlier.

`--end`
: The (exclusive) end of the requested time frame. This value can be a unix timestamp (in seconds or nanoseconds), or an absolute timestamp that conforms to RFC 3339. The `end` must be at least 5 minutes earlier than now and must be later than `start`. The difference between `start` and `end` must be not greater than 1h. The default is 5 minutes earlier.

`--count`
:   Number of logs to retrieve. The default value is `-1`.

`--sample`
:   Percentage of sampling. When a sample is provided, a sample of matching records is returned. If `sample=0.1` then 10% of records are returned. The sampling is random: repeated calls not only return different records, but likely also vary slightly in the number of returned records. When count is also specified, count is applied to the number of returned records, not the sampled records. So, with `sample=0.05` and `count=7`, when there is a total of 100 records available, approximately 5 records are returned. When there are 1000 records, 7 records are returned. When there are 10,000 records, 7 records are returned. The default value is `1`.

`--timestamps`
:   Set the format in which response timestamps are returned. Valid values are `unix`, `unixnano` and `rfc3339`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #examples-logpull}

```sh
ibmcloud cis logpull 31984fea73a15b45779fa0df4ef62f9b --available-fields
ibmcloud cis logpull 31984fea73a15b45779fa0df4ef62f9b --ray-id 59348abde87afe50 --all-fields --timestamps rfc3339 --output JSON
ibmcloud cis logpull 31984fea73a15b45779fa0df4ef62f9b --start 2020-05-18T12:14:58Z --end 2020-05-18T13:14:58Z --fields ClientIP,EdgeServerIP,ClientRequestHost --count 10 --sample 1 --timestamps rfc3339 --output JSON
```
{: codeblock}

## Log push
{: #log-push-cli-ref}

[Enterprise Plans Only]{: tag-blue}

### `ibmcloud cis logpush-job-create`
{: #logpush-job-create}

[Enterprise Plans Only]{: tag-blue}

Create a new log push job for a domain. Before using this command grant write access to your IBM Cloud Object Storage bucket to the IBM Cloud account cislogp@us.ibm.com.

```sh
ibmcloud cis logpush-job-create DNS_DOMAIN_ID --destination DESTINATION_URL --name NAME [--enable true|false] [--fields FIELDS | all] [--timestamps format][--dataset DATASET] [--frequency FREQUENCY] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #command-options-logpush-job-create}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--destination`
:   Specify a Cloud Object Storage bucket path or a LogDNA path where data is pushed.
    - Syntax for LogDNA Path: `https://{LOGS_REGION_URL}?hostname={DOMAIN}&apikey={LOGDNA_INGRESS_KEY}`

      Example: `'https://logs.eu-de.logging.cloud.ibm.com/logs/ingest?hostname=testv2_logpush&apikey=xxxxxx'`
      Syntax for Cloud Object Storage Path: `cos://<BUCKET_OBJECT_PATH>?region=<REGION>&instance-id=<IBM_ClOUD_OBJECT_STORAGE_INSTANCE_ID>`
      Example: `'cos://cis-test-bucket/logs?region=us&instance-id=f75e6d90-4212-4026-851c-d572071146cd'`
      To separate logs in to daily subfolders, use the special string `{DATE}` in the bucket path.
      It is substituted with the date in `YYYYMMDD` format, for example '20190423'.
      Subfolders are created as appropriate, for example:
      `'cos://cis-test-bucket/logs/{DATE}?region=us&instance-id=f75e6d90-4212-4026-851c-d572071146cd'`

`--name`
:   Job name. Required.

`--enable`
:   Enable the job. The job is disabled by default.

`--fields`
:   Define the list of log fields to be included in log files. Multiple fields can be separated by commas and use command [`ibmcloud cis logpush-available-fields DNS_DOMAIN_ID`] to get the comprehensive list of available log fields, or use `all` to include all available fields in log files. Note that fields are expected to be case sensitive.

`--timestamps`
:   Set the format in which response timestamps are returned. Valid values are `unix`, `unixnano` and `rfc3339`.

`--dataset`
:   The category of logs you want to receive. This value cannot be changed after the job is created. Valid values are `http_requests`, `range_events`, `firewall_events`, `dns_logs`. The default value is `http_requests`.

`--frequency`
:   The frequency at which CIS sends batches of logs to your destination. Setting the frequency to high sends your logs in larger quantities of smaller files. Setting the frequency to low sends logs in smaller quantities of larger files. Valid values are `high`, `low`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #command-example-logpush-job-create}

Create a log push job for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis logpush-job-create 31984fea73a15b45779fa0df4ef62f9b --destination cos://cis-test-bucket/logs?region=us&instance-id=f75e6d90-4212-4026-851c-d572071146cd --name logpushcreate --enable true --fields all --timestamps rfc3339 --dataset http_requests --frequency low -i cis-demo --output JSON
```
{: pre}

### `ibmcloud cis logpush-job-update`
{: #logpush-job-update}

[Enterprise Plans Only]{: tag-blue}

Update a log push job for a domain.

```sh
ibmcloud cis logpush-job-update DNS_DOMAIN_ID [--destination DESTINATION_URL] [--enable true|false] [--fields FIELDS | all] [--timestamps format] [--dataset DATASET] [--jobid JOB_ID] [--frequency FREQUENCY] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #command-options-logpush-job-update}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--destination`
:   Specify a Cloud Object Storage bucket path or a LogDNA path where data is pushed.
    Syntax for LogDNA Path: `https://{LOGS_REGION_URL}?hostname={DOMAIN}&apikey={LOGDNA_INGRESS_KEY}`
    Example: `'https://logs.eu-de.logging.cloud.ibm.com/logs/ingest?hostname=testv2_logpush&apikey=xxxxxx'`
    Syntax for Cloud Object Storage Path: `cos://<BUCKET_OBJECT_PATH>?region=<REGION>&instance-id=<IBM_ClOUD_OBJECT_STORAGE_INSTANCE_ID>`
    Example: `'cos://cis-test-bucket/logs?region=us&instance-id=f75e6d90-4212-4026-851c-d572071146cd'`
    To separate logs into daily subfolders, use the special string `{DATE}` in the bucket path.
    It is to be substituted with the date in `YYYYMMDD` format, for example '20190423'.
    Subfolders are created as appropriate, for example:
    `'cos://cis-test-bucket/logs/{DATE}?region=us&instance-id=f75e6d90-4212-4026-851c-d572071146cd'`

`--enable`
:   Enable the job. The job is disabled by default.

`--fields`
:   Define the list of log fields to be included in log files. Multiple fields can be separated by commas and use command `ibmcloud cis logpush-available-fields DNS_DOMAIN_ID` to get the comprehensive list of available log fields, or use `all` to include all available fields in log files. Note that fields are expected to be case sensitive.

`--timestamps`
:   Set the format in which response timestamps are returned. Valid values are `unix`, `unixnano`, `rfc3339`.

`--dataset`
:   The category of logs you want to receive. This value cannot be changed after the job is created. Valid values are `http_requests`, `range_events`, `firewall_events`,`dns_logs`. The default value is `http_requests`.

`--jobid`
:   JOB_ID is the ID of the logpush job.

`--frequency`
:   The frequency at which CIS sends batches of logs to your destination. Setting the frequency to high sends your logs in larger quantities of smaller files. Setting the frequency to low sends logs in smaller quantities of larger files. Valid values are `high` and `low`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #command-example-logpush-job-update}

Update `range_events` log push job for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis logpush-job-update 31984fea73a15b45779fa0df4ef62f9b --destination cos://cis-test-bucket/logs?region=us&instance-id=f75e6d90-4212-4026-851c-d572071146cd --enable true --fields all --timestamps rfc3339 --dataset range_events --frequency high -i cis-demo --output JSON
```
{: pre}

### `ibmcloud cis logpush-jobs`
{: #logpush-jobs}

[Enterprise Plans Only]{: tag-blue}

Get all log push jobs for a domain.

```sh
ibmcloud cis logpush-jobs DNS_DOMAIN_ID  [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #command-options-logpush-jobs}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`-output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #command-example-logpush-jobs}

Get all log push jobs for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis logpush-jobs 31984fea73a15b45779fa0df4ef62f9b -i cis-demo --output JSON
```
{: pre}

### `ibmcloud cis logpush-job`
{: #logpush-job}

[Enterprise Plans Only]{: tag-blue}

Get the details of a log push job for a domain.

```sh
ibmcloud cis logpush-job DNS_DOMAIN_ID [--dataset DATASET] [--jobid JOB_ID] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #command-options-logpush-job}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--dataset`
:   The category of logs you want to receive. This value cannot be changed after the job is created. Valid values are `http_requests`, `range_events`, `firewall_events`,`dns_logs`. The default value is `http_requests`.

`--jobid`
:   JOB_ID is the ID of the logpush job.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #command-example-logpush-job}

Get details of `http_requests` log push job.

```sh
ibmcloud cis logpush-job 31984fea73a15b45779fa0df4ef62f9b --dataset http_requests -i cis-demo --output JSON
```
{: pre}

### `ibmcloud cis logpush-job-delete`
{: #logpush-job-delete}

[Enterprise Plans Only]{: tag-blue}

Delete a log push job for a domain.

```sh
ibmcloud cis logpush-job-delete DNS_DOMAIN_ID [--dataset DATASET] [--jobid JOB_ID] [-f, --force] [-i, --instance INSTANCE]
```

#### Command options
{: #command-options-logpush-job-delete}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--dataset`
:   The category of logs you want to receive. This value cannot be changed after the job is created. Valid values are `http_requests`, `range_events`, `firewall_events`,`dns_logs`. The default value is `http_requests`.

`--jobid`
:   JOB_ID is the ID of the logpush job.

`-f, --force`
:   Delete log push job without prompting for confirmation.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #command-example-logpush-job-delete}

Delete `http_requests` log push job for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis logpush-job-delete 31984fea73a15b45779fa0df4ef62f9b --dataset http_requests -i cis-demo --force
```
{: pre}

### `ibmcloud cis logpush-available-fields`
{: #get-log-push-available-fields}

[Enterprise Plans Only]{: tag-blue}

Get all available fields for a data set.

```sh
ibmcloud cis logpush-available-fields DNS_DOMAIN_ID [--dataset DATASET] [-i, --instance INSTANCE]
```

#### Command options
{: #command-options-logpush-available-fields}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--dataset`
:   The category of logs you want to receive. This value cannot be changed after the job is created. Valid values are `http_requests`, `range_events`, `firewall_events`,`dns_logs`. The default value is `http_requests`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #command-example-logpush-available-fields}

Get all available fields for `http_requests` logs.

```sh
ibmcloud cis logpush-available-fields 31984fea73a15b45779fa0df4ef62f9b --dataset http_requests -i cis-demo
```
{: pre}

## Log retention
{: #log-retention-cli-ref}

[Enterprise Plans Only]{: tag-blue}

### `ibmcloud cis log-retention`
{: #cli-log-retention}

Get a log retention setting for the domain.

```sh
ibmcloud cis log-retention DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #command-options-log-retention}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #examples-log-retention}

Get a log retention setting for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis log-retention 31984fea73a15b45779fa0df4ef62f9b -i cis-demo --output JSON
```
{: pre}

### ibmcloud cis log-retention-update
{: #log-retention-update}

Update the log retention setting for the domain.

```sh
ibmcloud cis log-retention-update DNS_DOMAIN_ID (--flag on|off) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #command-options-log-retention-update}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--flag`
:   Whether to turn log retention on or off. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #examples-logpull-update}

Enable log retention for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis log-retention-update 31984fea73a15b45779fa0df4ef62f9b --flag on -i cis-demo --output JSON
```
{: pre}

## Managed lists
{: #managed-lists}

Manipulate managed lists by using the following `managed-lists` commands.

### `cis managed-lists`
{: #list-managed-lists}

List managed lists in an instance.

```sh
cis managed-lists [-i, --instance INSTANCE] [--output FORMAT]
```

### Command options
{: #list-managed-lists-options}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

### Example
{: #list-managed-lists-example}

```sh
ibmcloud cis managed-lists -i crn:v1:staging:public:internet-svcs-ci:global:a/c987fg3e4h278745690dp435683568rp:eg7kb437-4893-56yl-4wn9-c595j8t78gr9:: -o json
```
{: pre}

## Metrics
{: #metrics}

Manipulate metrics by using the following `metrics` commands.

### `ibmcloud cis firewall-event-analytics`
{: #firewall-event-analytics}

Retrieve a full log of firewall events.

```sh
ibmcloud cis firewall-event-analytics DNS_DOMAIN_ID [--dataset DATA_SET] [--filter FILTER] [--order FILTER_ORDER] [--limit LIMIT_NUMBER] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #firewall-event-analytics-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--dataset`
:   Requested dataset. The default value is `firewallEventsAdaptiveGroups`.

   Use the following table to identify which datasets are included in your plan and the range of historical data you can query.

   | Dataset                        | Trial / Standard / Standard-Next | Enterprise / Security / GLB |
   | ------------------------------ | ---------------------------------| --------------------------- |
   | firewallEventsAdaptiveGroups   |     30 days                      |         30 days             |
   | firewallEventsAdaptive         |     30 days                      |         30 days             |
   {: caption="Datasets included in your plan" caption-side="bottom"}


`--filter`
:   Filter events. The default value is the last 6 hours of data.

   The following operators are supported for all filter options:

   | Operator | Comparison          |
   | -------- | ------------------- |
   | gt       | greater than        |
   | lt       | less than           |
   | geq      | greater or equal to |
   | leq      | less or equal to    |
   | neq      | not equal           |
   | in       | in                  |
   {: caption="Operators supported for filter options" caption-side="bottom"}

    - `firewallEventsAdaptiveGroups` filter options.
        - `datetime`
        - `datetimeFifteenMinutes`
        - `datetimeHour`
        - `datetimeFiveMinutes`
        - `datetimeMinute`
        - `matchIndex`
        - `sampleInterval`
    - The following filter options support `like` and `notlike` operators.
        - `action`
        - `clientASNDescription`
        - `clientAsn`
        - `clientCountryName`
        - `clientIP`
        - `clientRefererHost`
        - `clientRefererPath`
        - `clientRefererQuery`
        - `clientRefererScheme`
        - `clientRequestHTTPHost`
        - `clientRequestHTTPMethodName`
        - `clientRequestHTTPProtocol`
        - `clientRequestPath`
        - `clientRequestQuery`
        - `clientRequestScheme`
        - `edgeColoName`
        - `edgeResponseStatus`
        - `kind`
        - `originResponseStatus`
        - `originatorRayName`
        - `rayName`
        - `ref`
        - `ruleId`
        - `source`
        - `userAgent`

`--order`
:   Output order. (The default value is `datetime_ASC`)

    The following list is usable order options for corresponding dataset and all of order options support ASC and DESC action. Combine these filter options and action with `_`.

    For example, `datetime_ASC` orders by datetime ascending.

    - `firewallEventsAdaptiveGroups` order options.
        - `datetime`
        - `datetimeFifteenMinutes`
        - `datetimeHour`
        - `datetimeFiveMinutes`
        - `datetimeMinute`
        - `action`
        - `avg_sampleInterval`
        - `clientASNDescription`
        - `clientAsn`
        - `clientCountryName`
        - `clientIPClass`
        - `clientIP`
        - `clientRefererHost`
        - `clientRefererPath`
        - `clientRefererQuery`
        - `clientRefererScheme`
        - `clientRequestHTTPHost`
        - `clientRequestHTTPMethodName`
        - `clientRequestHTTPProtocol`
        - `clientRequestPath`
        - `clientRequestQuery`
        - `clientRequestScheme`
        - `count`
        - `edgeColoName`
        - `edgeResponseStatus`
        - `kind`
        - `matchIndex`
        - `originResponseStatus`
        - `originatorRayName`
        - `rayName`
        - `ref`
        - `ruleId`
        - `sampleInterval`
        - `source`
        - `userAgent`
        - `visibility`

`--limit`
:   The number of events to return. (minimum: `1`, maximum: `10000`, default: `10000`)

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #firewall-event-analytics-examples}

Get firewall event analytics for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis firewall-event-analytics 31984fea73a15b45779fa0df4ef62f9b --order datetime_ASC \
     --filter "datetime_geq:2020-06-28T00:00:00Z"  --filter "datetime_leq:2020-06-29T00:00:00Z" --output json
```
{: pre}

### `ibmcloud cis http-request-analytics`
{: #http-request-analytics}

Retrieve a full log of http request events.

```sh
ibmcloud cis http-request-analytics DNS_DOMAIN_ID [--dataset DATA_SET] [--filter FILTER] [--order FILTER_ORDER] [--limit LIMIT_NUMBER] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #http-request-analytics-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--dataset`
:   Requested dataset. The default value is `httpRequests1dGroups`.
    Use the following table to identify which datasets are included in your plan and the range of historical data you can query.

    | Dataset                     | Trial / Standard / Standard-next | Enterprise / Security / GLB |
    | --------------------------- | -------------------------------- | --------------------------- |
    | httpRequests1dGroups        | 365 days                         | 365 days                    |
    | httpRequests1hGroups        | 30 days                          | 90 days                     |
    | httpRequests1mGroups        | 3 days                           | 7 days                      |
    {: caption="Identify datasets included in your plan" caption-side="bottom"}

`--filter`
:   Filter events. The default value is the last 7 days data.
    The following operators are supported for all filter options:

    | Operator | Comparison          |
    | -------- | ------------------- |
    | gt       | greater than        |
    | lt       | less than           |
    | geq      | greater or equal to |
    | leq      | less or equal to    |
    | neq      | not equal           |
    | in       | in                  |
    {: caption="Operators supported for filter options" caption-side="bottom"}

    - `httpRequests1dGroups` and `httpRequests1hGroups` filter options.
        - `date`

    - `httpRequests1mGroups` filter options.
        - `datetime`
        - `datetimeFifteenMinutes`
        - `datetimeHour`
        - `datetimeDay`

`--order`
:   Output order. (The default value is `datetime_ASC`)

    The following list is usable order options for corresponding dataset and all of order options support ASC and DESC action. Combine these order options and action with `_`.

    For example, `date_ASC` orders by date ascending.
    - Common order options for every http dataset.
        - `orderByParams`
        - `date`
        - `sum_bytes`
        - `sum_cachedBytes`
        - `sum_cachedRequests`
        - `sum_requests`
    - `httpRequests1dGroups` order options.
        - `avg_bytes`
        - `sum_encryptedBytes`
        - `sum_encryptedRequests`
        - `sum_pageViews`
        - `sum_threats`
        - `uniq_uniques`
    - `httpRequests1hGroups` order options.
        - `avg_bytes`
        - `sum_encryptedBytes`
        - `sum_encryptedRequests`
        - `sum_pageViews`
        - `sum_threats`
        - `uniq_uniques`
        - `datetime`
    - `httpRequests1mGroups` order options.
        - `avg_bytes`
        - `sum_encryptedBytes`
        - `sum_encryptedRequests`
        - `sum_pageViews`
        - `sum_threats`
        - `uniq_uniques`
        - `datetime`
        - `datetimeFifteenMinutes`
        - `datetimeHour`
        - `datetimeFifteenMinutes`
        - `datetimeHour`
        - `datetimeDay`

`--limit`
:   The number of events to return. (minimum: `1`, maximum: `10000`, default: `10000`)

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #http-request-analytics-examples}

Get http request analytics for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis http-request-analytics 31984fea73a15b45779fa0df4ef62f9b --order date_ASC \
     --dataset httpRequests1dGroups --limit 500 \
     --filter "date_geq:2020-06-28"  --filter "date_leq:2020-06-29" --output json
```
{: pre}

### `ibmcloud cis web-analytics` (Deprecated)
{: #web-analytics}

Web analytics are deprecated on 2 November 2020. Use [`ibmcloud cis http-request-analytics`](#http-request-analytics) instead. Get analytics of the DNS domain.

```sh
ibmcloud cis web-analytics DNS_DOMAIN_ID [--recent DURATION] [-t, --table requests | bandwidth | uniques | threats | status_code] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #web-analytics-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--recent`
:   The beginning of the requested time frame. Valid values are `6h` (6 hours ago), `12h`, `1d` (1 day ago), `1w` (1 week ago), `1m` (1 month ago), `2m`, `3m`. The default value is `1w`.

`-t, --table`
:   Output table. Valid values are `requests`, `bandwidth`, `uniques`, `threats` and, `status_code`. If this field is not set, it outputs all the tables.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #web-analytics-examples}

Get web analytics for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis web-analytics 31984fea73a15b45779fa0df4ef62f9b --recent 1d -t requests -i "cis-demo"
```
{: pre}

### `ibmcloud cis dns-analytics`
{: #dns-analytics}

Get DNS analytics of the domain.

```sh
ibmcloud cis dns-analytics DNS_DOMAIN_ID DIMENSION [-s, --since TIME] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #dns-analytics-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`DIMENSION`
:   The queried dimension. Valid values are `queries-by-response-code`, `queries-by-type`, `queries-by-name`. Required.

`-s, --since`
:   Since time to now. Valid values are `6h` (6 hours ago), `12h`, `1d` (1 day ago), `1w` (1 week ago).

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #dns-analytics-examples}

Get DNS analytics for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis dns-analytics 31984fea73a15b45779fa0df4ef62f9b queries-by-response-code -s 6h -i "cis-demo" --output json
```
{: pre}

### `ibmcloud cis ratelimit-analytics`
{: #ratelimit-analytics}

Get rate limit analytics for a DNS domain.

```sh
ibmcloud cis ratelimit-analytics DNS_DOMAIN_ID [--recent DURATION] [--time-delta SECONDS] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #ratelimit-analytics-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--recent`
:   The beginning of the requested time frame. Valid values are `6h` (6 hours ago), `12h`, `1d` (1 day ago), `1w` (1 week ago), `1m` (1 month ago), `2m`, `3m`. The default value is `1w`.

`--time-delta`
:   The time interval (seconds) of each analytic's record. Valid values are `60`, `3600`, `86400`, `2592000`. The default value is `3600`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #ratelimit-analytics-examples}

Get rate limit analytics for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis ratelimit-analytics 31984fea73a15b45779fa0df4ef62f9b --recent 6h --time-delta 3600 -i "cis-demo" --output json
```
{: pre}

## MTLS enable
{: #mtls-enable-cli-ref}

### `ibmcloud cis access-enable`
{: #access-enable}

[Enterprise Plans Only]{: tag-blue}

Enable Mutual TLS for a service instance.

```sh
ibmcloud cis access-enable [-i, --instance INSTANCE]
```

#### Command options
{: #command-options-access-enable}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #command-example-access-enable}

Enable Mutual TLS for instance `cis-demo`.

```sh
ibmcloud cis access-enable -i cis-demo
```
{: pre}

## Origin certificates
{: #origin-certificates-cli-ref}

### `ibmcloud cis origin-certificates`
{: #origin-certificates}

List all origin certificates for a DNS domain.

```sh
ibmcloud cis origin-certificates DNS_DOMAIN_ID [--instance INSTANCE_NAME] [--output FORMAT]
```

#### Command options
{: #command-options-origin-certificates}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #command-example-origin-certificates}

List all origin certificates for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis origin-certificates 31984fea73a15b45779fa0df4ef62f9b -i cis-demo --output JSON
```
{: pre}

### `ibmcloud cis origin-certificate-create`
{: #origin-certificate-create}

Create a CIS-signed certificate.

```sh
ibmcloud cis origin-certificate-create DNS_DOMAIN_ID [--request-type REQUEST_TYPE] [--hostnames HOST_NAME1] [--hostnames HOST_NAME2] [--requested-validity DAYS] [--csr CSR] [--instance INSTANCE_NAME] [--output FORMAT]
ibmcloud cis origin-certificate-create DNS_DOMAIN_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis origin-certificate-create DNS_DOMAIN_ID --json-str JSON_STR [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis origin-certificate-create DNS_DOMAIN_ID --json-file JSON_FILE [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #command-options-origin-certificate-create}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--request-type REQUEST_TYPE`
:   Signature type that you want on the certificate. Valid values are `origin-rsa` and `origin-ecc`.

`--hostnames HOSTNAME`
:   hostname or wildcard name that is bound to the certificate.

`--requested-validity DAYS`
:   The number of days for which the certificate must be valid. The default value is `5475`.

`--csr CSR`
:   The Certificate Signing Request (CSR). If this field is not set, CIS generates one.

`--json value*`
:   The JSON file or JSON string that is used to describe an origin certificate.
    - The required fields in JSON data are `request_type`, `hostnames`.
        - `request_type` : Signature type that you want on the certificate. Valid values are `origin-rsa`, `origin-ecc`.
        - `hostnames` : An array of hostnames or wildcard names that are bound to the certificate.
    - The optional fields are `requested_validity`, `csr`.
        - `requested_validity` : The number of days for which the certificate must be valid. Valid values are `0`, `7`, `30`, `90`, `365`, `730`, `1095`, `5475`.
        - `csr` : The Certificate Signing Request (CSR). If this field is not set, CIS generates one.

   Sample JSON data:

```json
{
   "request_type": "origin-rsa",
   "hostnames": [
      "*.example.com",
      "example.com",
],
   "requested_validity": 5475,
   "csr": "your_csr"
}
```
{: codeblock}

`-s, --json-str`
:   *Deprecated*. The JSON data that describes an origin certificate.

`-j, --json-file`
:   *Deprecated*. A file contains input JSON data.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #command-example-origin-certificate-create}

Create a CIS-signed certificate for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis origin-certificate-create 31984fea73a15b45779fa0df4ef62f9b --request-type origin-rsa --hostnames "*.example.com" --hostnames "example.com" --requested-validity 5475 --csr your_csr -i cis-demo --output JSON

ibmcloud cis origin-certificate-create 31984fea73a15b45779fa0df4ef62f9b --json '{"hostnames":["example.com","*.example.com"], "requested_validity":5475,"request_type": "origin-rsa","csr":"-----BEGIN CERTIFICATE REQUEST-----\nMIICxzCCAa8CAQAwSDELMAkGA1UEBhMCVVMxFjAUBgNVBAgTDVNhbiBGcmFuY2lz\nY28xCzAJBgNVBAcTAkNBMRQwEgYDVQQDEwtleGFtcGxlLm5ldDCCASIwDQYJKoZI\nhvcNAQEBBQADggEPADCCAQoCggEBALxejtu4b+jPdFeFi6OUsye8TYJQBm3WfCvL\nHu5EvijMO/4Z2TImwASbwUF7Ir8OLgH+mGlQZeqyNvGoSOMEaZVXcYfpR1hlVak8\n4GGVr+04IGfOCqaBokaBFIwzclGZbzKmLGwIQioNxGfqFm6RGYGA3be2Je2iseBc\nN8GV1wYmvYE0RR+yWweJCTJ157exyRzu7sVxaEW9F87zBQLyOnwXc64rflXslRqi\ng7F7w5IaQYOl8yvmk/jEPCAha7fkiUfEpj4N12+oPRiMvleJF98chxjD4MH39c5I\nuOslULhrWunfh7GB1jwWNA9y44H0snrf+xvoy2TcHmxvma9Eln8CAwEAAaA6MDgG\nCSqGSIb3DQEJDjErMCkwJwYDVR0RBCAwHoILZXhhbXBsZS5uZXSCD3d3dy5leGFt\ncGxlLm5ldDANBgkqhkiG9w0BAQsFAAOCAQEAcBaX6dOnI8ncARrI9ZSF2AJX+8mx\npTHY2+Y2C0VvrVDGMtbBRH8R9yMbqWtlxeeNGf//LeMkSKSFa4kbpdx226lfui8/\nauRDBTJGx2R1ccUxmLZXx4my0W5iIMxunu+kez+BDlu7bTT2io0uXMRHue4i6quH\nyc5ibxvbJMjR7dqbcanVE10/34oprzXQsJ/VmSuZNXtjbtSKDlmcpw6To/eeAJ+J\nhXykcUihvHyG4A1m2R6qpANBjnA0pHexfwM/SgfzvpbvUg0T1ubmer8BgTwCKIWs\ndcWYTthM51JIqRBfNqy4QcBnX+GY05yltEEswQI55wdiS3CjTTA67sdbcQ==\n-----END CERTIFICATE REQUEST-----"}' -i cis-demo --output JSON
```
{: codeblock}

### `ibmcloud cis origin-certificate`
{: #origin-certificate}

Get details of an origin certificate.

```sh
ibmcloud cis origin-certificate DNS_DOMAIN_ID CERT_ID [--instance INSTANCE_NAME] [--output FORMAT]
```

#### Command options
{: #command-options-origin-certificate}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`CERT_ID`
:   The ID of the Origin Certificate. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #command-example-origin-certificate}

Get details of origin certificate `a5836c2a7ea72d2e225890caea70ae32`.

```sh
ibmcloud cis origin-certificate 31984fea73a15b45779fa0df4ef62f9b a5836c2a7ea72d2e225890caea70ae32 -i cis-demo --output JSON
```
{: pre}

### `ibmcloud cis origin-certificate-delete`
{: #origin-certificate-delete}

Delete an origin certificate.

```sh
ibmcloud cis origin-certificate-delete DNS_DOMAIN_ID CERT_ID [--instance INSTANCE_NAME]
```

#### Command options
{: #command-options-origin-certificate-delete}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`CERT_ID`
:   The ID of Origin Certificate. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #command-example-origin-certificate-delete}

Delete origin certificate `a5836c2a7ea72d2e225890caea70ae32`.

```sh
ibmcloud cis origin-certificate-delete 31984fea73a15b45779fa0df4ef62f9b a5836c2a7ea72d2e225890caea70ae32 -i cis-demo
```
{: pre}

## Overview
{: #overview}

View the overview information for a domain.

### `ibmcloud cis overview`
{: #get-overview}

Show the overview information for a domain.

```sh
ibmcloud cis overview DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #get-overview-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #get-overview-examples}

Show the overview information for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis overview 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

## Page rules
{: #page-rule-cli-ref}

Manipulate page rules by using the following `pagerule` commmands.

### `ibmcloud cis page-rule-create`
{: #page-rule-create}

Create a page rule of the DNS domain.

```sh
ibmcloud cis page-rule-create DNS_DOMAIN_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis page-rule-create DNS_DOMAIN_ID (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #command-options-page-rule-create}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--json`
:   The JSON file or JSON string that is used to describe a page rule. Required.
    - The required fields in JSON data are targets, actions :
        - `targets` : The target URL pattern to evaluate on a request.
        - `actions` : An array of actions to perform if the targets of this rule match the request. Available actions are:
            - `disable_security`
            - `always_use_https`
            - `ssl`
            - `browser_cache_ttl`
            - `security_level`
            - `cache_level`
            - `edge_cache_ttl`
            - `bypass_cache_on_cookie`
            - `browser_check`
            - `server_side_exclude`
            - `email_obfuscation`
            - `automatic_https_rewrites`
            - `opportunistic_encryption`
            - `ip_geolocation`
            - `explicit_cache_control`
            - `cache_deception_armor`
            - `waf`
            - `forwarding_url`
            - `image_load_optimization`
            - `image_size_optimization`
            - `script_load_optimization`
            - `host_header_override`
            - `resolve_override`
            - Some actions are limited to Enterprise plans:
                - `cache_on_cookie`
                - `disable_apps`
                - `disable_performance`
                - `minify`
                - `origin_error_page_pass_thru`
                - `response_buffering`
                - `true_client_ip_header`
                - `sort_query_string_for_cache`
                - `respect_strong_etag`
    - The optional fields are `priority` and `status` :
        - `priority`: A number that indicates the preference for a page rule over another. The default value is `1`.
        - `status`: Status of the page rule. The valid values are `active` and `disabled` (default).

Sample JSON data:

```json
   {
   "targets": [
      {
            "target": "url",
            "constraint": {
               "operator": "matches",
               "value": "*example.com/images/*"
            }
      }
   ],
   "actions": [
      {
            "id": "ssl",
            "value": "flexible"
      },
      {
            "id": "browser_cache_ttl",
            "value": 14400
      },
      {
            "id": "security_level",
            "value": "medium"
      },
      {
            "id": "cache_level",
            "value": "basic"
      },
      {
            "id": "edge_cache_ttl",
            "value": 7200
      },
      {
            "id": "bypass_cache_on_cookie",
            "value": "wp-.*|wordpress.*|comment_.*"
      }
   ]
}
```
{: codeblock}

`-s, --json-str`
:   *Deprecated*. The JSON data describing a page rule.

`-j, --json-file`
:   *Deprecated*. A file contains input JSON data.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #command-examples-page-rule-create}

Create a page rule for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis page-rule-create 31984fea73a15b45779fa0df4ef62f9b --json '{"targets":[{"target":"url", "constraint":{"operator": "matches", "value":"*example.com/images/*"}}], "actions":[{"id":"always_online", "value":"on"}], "priority":1, "status": "active"}' cis-demo --output JSON
```
{: pre}

### `ibmcloud cis page-rule-update`
{: #page-rule-update}

Update the page rule of the DNS domain.

```sh
ibmcloud cis page-rule-update DNS_DOMAIN_ID PAGE_RULE_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis page-rule-update DNS_DOMAIN_ID PAGE_RULE_ID (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #command-options-page-rule-update}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`PAGE_RULE_ID`
:   The ID of page rule. Required.

`--json VALUE`
:   The JSON file or JSON string that is used to describe a page rule. Required.
    - The required fields in JSON data are `targets` and `actions` :
        - `targets` : The target URL pattern to evaluate on a request.
        - `actions` : An array of actions to perform if the targets of this rule match the request. Available actions are:
            - `disable_security`
            - `always_use_https`
            - `ssl`
            - `browser_cache_ttl`
            - `security_level`
            - `cache_level`
            - `edge_cache_ttl`
            - `bypass_cache_on_cookie`
            - `browser_check`
            - `server_side_exclude`
            - `email_obfuscation`
            - `automatic_https_rewrites`
            - `opportunistic_encryption`
            - `ip_geolocation`
            - `explicit_cache_control`
            - `cache_deception_armor`
            - `waf`
            - `forwarding_url`
            - `image_load_optimization`
            - `image_size_optimization`
            - `script_load_optimization`
            - `host_header_override`
            - `resolve_override`
            - Some actions are limited to Enterprise plans:
                - `cache_on_cookie`
                - `disable_apps`
                - `disable_performance`
                - `minify`
                - `origin_error_page_pass_thru`
                - `response_buffering`
                - `true_client_ip_header`
                - `sort_query_string_for_cache`
                - `respect_strong_etag`
    - The optional fields are `priority` and `status` :
        - `priority` : A number that indicates the preference for a page rule over another. The default value is `1`.
        - `status` : Status of the page rule. Valid values are `active` and `disabled`. The default value is `disabled`.

Sample JSON data:

```json
{
   "targets": [
      {
            "target": "url",
            "constraint": {
               "operator": "matches",
               "value": "*example.com/images/*"
            }
      }
   ],
   "actions": [
      {
            "id": "ssl",
            "value": "flexible"
      },
      {
            "id": "browser_cache_ttl",
            "value": 14400
      },
      {
            "id": "security_level",
            "value": "medium"
      },
      {
            "id": "cache_level",
            "value": "basic"
      },
      {
            "id": "edge_cache_ttl",
            "value": 7200
      },
      {
            "id": "bypass_cache_on_cookie",
            "value": "wp-.*|wordpress.*|comment_.*"
      }
   ]
}
```
{: codeblock}

`-s, --json-str`
:   *Deprecated*. The JSON data describing a page rule.

`-j, --json-file`
:   *Deprecated*. A file contains input JSON data.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #command-examples-page-rule-update}

Update page rule `a5836c2a7ea72d2e225890caea70ae32`.

```sh
ibmcloud cis page-rule-update 31984fea73a15b45779fa0df4ef62f9b a5836c2a7ea72d2e225890caea70ae32 --json '{"targets":[{"target":"url", "constraint":{"operator":"matches", "value":"*example.com/images/*"}}], "actions":[{"id":"always_online", "value":"on"}],"priority":1, "status":"active"}' -i cis-demo --output JSON
```
{: pre}

### `ibmcloud cis page-rule-delete`
{: #page-rule-delete}

Delete a page rule of the DNS domain.

```sh
ibmcloud cis page-rule-delete DNS_DOMAIN_ID PAGE_RULE_ID [-i, --instance INSTANCE]
```

#### Command options
{: #command-options-page-rule-delete}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`PAGE_RULE_ID`
:   The ID of page rule. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #command-examples-page-rule-delete}

Delete page rule `a5836c2a7ea72d2e225890caea70ae32`.

```sh
ibmcloud cis page-rule-update 31984fea73a15b45779fa0df4ef62f9b a5836c2a7ea72d2e225890caea70ae32 -i cis-demo
```
{: pre}

### `ibmcloud cis page-rules`
{: #page-rules}

List page rules of the DNS domain.

```sh
ibmcloud cis page-rules DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #command-options-page-rules}


`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #command-examples-page-rules}

List all page rules in domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis page-rules 31984fea73a15b45779fa0df4ef62f9b -i cis-demo --output JSON
```
{: pre}

### `ibmcloud cis page-rule`
{: #page-rule}

Get details of a page rule.

```sh
ibmcloud cis page-rule DNS_DOMAIN_ID PAGE_RULE_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #command-options-page-rule}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`PAGE_RULE_ID`
:   The ID of page rule. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #command-examples-page-rule}

Get details of page rule `a5836c2a7ea72d2e225890caea70ae32`.

```sh
ibmcloud cis page-rule 31984fea73a15b45779fa0df4ef62f9b a5836c2a7ea72d2e225890caea70ae32 -i cis-demo --output JSON
```
{: pre}

## Range app
{: #range-app}

Manipulate how the Range App performs by using the following `range-app` commands:

### `ibmcloud cis range-app-create`
{: #cli-create-range-app}

[Enterprise Plans Only]{: tag-blue}

Create a new range application.

```sh
ibmcloud cis range-app-create DNS_DOMAIN_ID --name NAME --edge-port EDGE_PORT --origin-direct ORIGIN_DIRECT [--origin-direct ORIGIN_DIRECT] [--proxy-protocol on|off] [--ip-firewall on|off] [--edge-connectivity all|ipv4|ipv6] [--edge-tls off|flexible|full|strict] [--traffic-type direct/http/https] [-i, --instance INSTANCE] [--output FORMAT]

ibmcloud cis range-app-create DNS_DOMAIN_ID --name NAME --edge-port EDGE_PORT --origin-lb-name ORIGIN_LB_NAME --origin-lb-port ORIGIN_LB_PORT [--proxy-protocol on|off] [--ip-firewall on|off] [--edge-connectivity all|ipv4|ipv6] [--edge-tls off|flexible|full|strict] [--traffic-type direct/http/https] [-i, --instance INSTANCE] [--output FORMAT]

ibmcloud cis range-app-create DNS_DOMAIN_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]

[Deprecated] ibmcloud cis range-app-create DNS_DOMAIN_ID -s JSON_STR [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis range-app-create DNS_DOMAIN_ID -j JSON_FILE [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #create-range-app-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--name`
:   The name of the DNS record for the range application.

`--edge-port`
:   Port configuration at CIS's edge. The default value is `22`.

`--origin-direct`
:   Destination addresses to the origin.

`--origin-lb-name`
:   The Load Balancer name associated with the range application.

`--origin-lb-port`
:   The Load Balancer port associated with the range application. The default value is `22`.

`--protocol`
:   Protocol type. Valid values are `tcp` and `udp`. UDP protocol support is in early access, request custom UDP from CIS dashboard before creating range UDP app. The default value is `tcp`.

`--proxy-protocol`
:   Enable Proxy Protocol to the origin. Valid values are `on`, `off`, `v1`, `v2`, `simple`. The default value is `off`.
    *Deprecated*. The value `on` is equivalent to `v1`.

`--ip-firewall`
:   Control whether the IP Firewall for this application is enabled. Valid values are `on` and `off`. The default value is `off`.

`--edge-connectivity`
:   The IP versions supported for inbound connections on a range of anycast IPs. Valid values are `all`, `ipv4`, `ipv6`. The default value is `all`.

`--edge-tls`
:   The type of TLS termination associated with the application. Valid values are `off`, `flexible`, `full`, `strict`. The default value is `off`.

`--traffic-type`
:   Determines how data travels from the edge to your origin. Valid values are `direct`, `http`, `https`. The default value is `direct`.

`--json`
:   The JSON file or JSON string that is used to describe a range application.
    - The required fields in JSON data are `protocol` and `dns`.
        - `protocol` : Port configuration at CIS's edge.
        - `dns` : The name and type of the DNS record for the range application.
            - `name` : The name of the DNS record for the range application.
            - `type` : The type of the DNS record associated with the application. Valid value is `CNAME`.
    - The optional fields are `origin_direct`, `origin_dns`, `origin_port`, `proxy_protocol`, `ip_firewall`, `edge_ips`, `tls`, and `traffic_type`.
        - `origin_direct` : A list of destination addresses to the origin.
        - `origin_dns` : Method and parameters that are used to discover the origin server address via DNS.
            - `name` : DNS record name.
        - `origin_port` : The destination port at the origin.
        - `proxy_protocol` : Enable the Proxy Protocol to the origin. Valid values are `on`, `off`, `v1`, `v2`, `simple`. The default value is `off`.
            *Deprecated*. The value `on` is equivalent to `v1`.
        - `ip_firewall` : Control whether the IP Firewall for this application is enabled. Valid values are `on` and `off`.
        - `edge_ips` : The anycast edge IP configuration for the hostname of this application.
            - `type` : The type of edge IP configuration specified. Dynamically allocated edge IPs use range anycast IPs in accordance with the connectivity you specify. Valid value is `dynamic`.
            - `connectivity` : The IP versions supported for inbound connections on a range of anycast IPs. Valid values: `all`, `ipv4`, `ipv6`.
        - `tls`: The type of TLS termination associated with the application. Valid values are `off`, `flexible`, `full`, and `strict`.
        - `traffic_type` : Determines how data travels from the edge to your origin. When set to `direct`, range sends traffic directly to your origin, and the application's type is derived from the protocol. When set to `http` or `https`, range applies CIS's HTTP/HTTPS features as it sends traffic to your origin, and the application type matches this property exactly. Valid values are `direct`, `http`, and `https`. The default value is `direct`.

Sample JSON data:

```json
{
   "protocol": "tcp/22",
   "dns": {
      "type": "CNAME",
      "name": "ssh.example.com"
   },
   "origin_direct": [
      "tcp://1.2.3.4:22",
      "tcp://1.2.3.4:23",
      "tcp://1.2.3.4:24"
   ],
   "proxy_protocol": false,
   "ip_firewall": false,
   "edge_ips": {
      "type": "dynamic",
      "connectivity": "all"
   },
   "tls": "full",
   "traffic_type": "direct"
}

{
   "protocol": "tcp/22",
   "dns": {
      "type": "CNAME",
      "name": "glb.example.com"
   },
   "origin_dns": {
      "name": "name-to-glb.example.com"
   },
   "origin_port": 22,
   "proxy_protocol": false,
   "ip_firewall": false,
   "edge_ips": {
      "type": "dynamic",
      "connectivity": "all"
   },
   "tls": "full",
   "traffic_type": "direct"
}
```
{: codeblock}

`-s, --json-str`
:   *Deprecated*. The JSON data describing a range application.

`-j, --json-file`
:   *Deprecated*. A file contains input JSON data.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #create-range-app-examples}

Create a range app for the domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis range-app-create 31984fea73a15b45779fa0df4ef62f9b --json '{"protocol":"tcp/22", "dns":{"type":"CNAME","name":"ssh.example.com"}, "origin_direct":["tcp://1.2.3.4:22"], "proxy_protocol":"off", "ip_firewall":true, "tls":"full", "edge_ips":{"type":"dynamic", "connectivity":"all"}, "traffic_type":"direct"}' -i "cis-demo"
```
{: pre}

### `ibmcloud cis range-app-update`
{: #update-range-app}

[Enterprise Plans Only]{: tag-blue}

Update a previously existing application's configuration.

```sh
ibmcloud cis range-app-update DNS_DOMAIN_ID APP_ID --origin-direct ORIGIN_DIRECT [-i, --instance INSTANCE] [--output FORMAT]
ibmcloud cis range-app-update DNS_DOMAIN_ID APP_ID [--add-origin-direct ORIGIN_DIRECT] [--remove-origin-direct ORIGIN_DIRECT] [-i, --instance INSTANCE] [--output FORMAT]
ibmcloud cis range-app-update DNS_DOMAIN_ID APP_ID [--origin-lb-name ORIGIN_LB_NAME] [--origin-lb-port ORIGIN_LB_PORT] [-i, --instance INSTANCE] [--output FORMAT]
ibmcloud cis range-app-update DNS_DOMAIN_ID APP_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis range-app-update DNS_DOMAIN_ID APP_ID -s JSON_STR [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis range-app-update DNS_DOMAIN_ID APP_ID -j JSON_FILE [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-range-app-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`APP_ID`
:   The ID of the range application. Required.

`--name`
:   The name of the DNS record for the range application.

`--add-origin-direct`
:   Add new destination addresses to the origin.

`--remove-origin-direct`
:   Remove destination addresses from origin.

`--origin-direct`
:   Destination addresses to the origin.

`--origin-lb-name`
:   The Load Balancer name associated with the range application.

`--origin-lb-port`
:   The Load Balancer port associated with the range application. The default value is `22`.

`--proxy-protocol`
:   Enable the Proxy Protocol to the origin. Valid values are `on`, `off`, `v1`, `v2`, `simple`. The default value is `off`.
    *Deprecated*. The value `on` is equivalent to `v1`.

`--ip-firewall`
:   Control whether the IP Firewall for this application is enabled. Valid values are `on` and `off`. The default value is `off`.

`--edge-connectivity`
:   The IP versions supported for inbound connections on a range of anycast IPs. Valid values are `all`, `ipv4`, `ipv6`. The default value is `all`.

`--edge-tls`
:   The type of TLS termination associated with the application. Valid values are `off`, `flexible`, `full`, `strict`. The default value is `off`.

`--traffic-type`
:   Determines how data travels from the edge to your origin. Valid values are `direct`, `http`, `https`. The default value is `direct`.

`--json`
:   The JSON file or JSON string that is used to describe a range application.
    - The required fields in JSON data are `protocol` and `dns`.
        - `protocol` : Port configuration at CIS's edge.
        - `dns` : The name and type of the DNS record for the range application.
            - `name` : The name of the DNS record for the range application.
            - `type` : The type of the DNS record associated with the application. Valid value is `CNAME`.
    - The optional fields are `origin_direct`, `origin_dns`, `origin_port`, `proxy_protocol`, `ip_firewall`, `edge_ips`, `tls`, and `traffic_type`.
        - `origin_direct` : A list of destination addresses to the origin.
        - `origin_dns` : Method and parameters that are used to discover the origin server address via DNS.
            - `name` : DNS record name.
        - `origin_port` : The destination port at the origin.
        - `proxy_protocol` : Enable Proxy Protocol to the origin. Valid values are `on`, `off`, `v1`, `v2`, `simple`. The default value is `off`.
            *Deprecated*. The value `on` is equivalent to `v1`.
        - `ip_firewall` : Control whether the IP Firewall for this application is enabled. Valid values are `on` and `off`.
        - `edge_ips` : The anycast edge IP configuration for the hostname of this application.
            - `type` : The type of edge IP configuration specified. Dynamically allocated edge IPs use range anycast IPs in accordance with the connectivity you specify. Valid value is `dynamic`.
            - `connectivity`: The IP versions supported for inbound connections on range anycast IPs. Valid values are `all`, `ipv4`, `ipv6`.
        - `tls`: The type of TLS termination associated with the application. Valid values are `off`, `flexible`, `full`, `strict`.
        - `traffic_type` : Determines how data travels from the edge to your origin. When set to `direct`, range sends traffic directly to your origin, and the application's type is derived from the protocol. When set to `http` or `https`, range applies CIS's HTTP/HTTPS features as it sends traffic to your origin, and the application type matches this property exactly. Valid values are `direct`, `http`, and `https`. The default value is `direct`.

Sample JSON data:

```json
{
   "protocol": "tcp/22",
   "dns": {
      "type": "CNAME",
      "name": "ssh.example.com"
   },
   "origin_direct": [
      "tcp://1.2.3.4:22",
      "tcp://1.2.3.4:23",
      "tcp://1.2.3.4:24"
   ],
   "proxy_protocol": false,
   "ip_firewall": false,
   "edge_ips": {
      "type": "dynamic",
      "connectivity": "all"
   },
   "tls": "full",
   "traffic_type": "direct"
}

{
   "protocol": "tcp/22",
   "dns": {
      "type": "CNAME",
      "name": "glb.example.com"
   },
   "origin_dns": {
      "name": "name-to-glb.example.com"
   },
   "origin_port": 22,
   "proxy_protocol": false,
   "ip_firewall": false,
   "edge_ips": {
      "type": "dynamic",
      "connectivity": "all"
   },
   "tls": "full",
   "traffic_type": "direct"
}
```
{: codeblock}

`-s, --json-str`
:   *Deprecated*. The JSON data describing a range application.

`-j, --json-file`
:   *Deprecated*. A file contains input JSON data.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-range-app-examples}

Update range app `ea95132c15732412d22c1476fa83f27a`.

```sh
ibmcloud cis range-app-update 31984fea73a15b45779fa0df4ef62f9b ea95132c15732412d22c1476fa83f27a --json '{"protocol":"tcp/22", "dns":{"type":"CNAME","name":"ssh.example.com"}, "origin_direct":["tcp://1.2.3.4:22"], "proxy_protocol":"off", "ip_firewall":true, "tls":"full", "edge_ips":{"type":"dynamic", "connectivity":"all"}, "traffic_type":"direct"}' -i "cis-demo"
```
{: pre}

### `ibmcloud cis range-app-delete`
{: #delete-range-app}

[Enterprise Plans Only]{: tag-blue}

Delete a previously existing application.

```sh
ibmcloud cis range-app-delete DNS_DOMAIN_ID APP_ID [--instance INSTANCE]
```

#### Command options
{: #delete-range-app-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`APP_ID`
:   The ID of range application. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #delete-range-app-examples}

Delete range application `ea95132c15732412d22c1476fa83f27a`.

```sh
ibmcloud cis range-app-delete 31984fea73a15b45779fa0df4ef62f9b ea95132c15732412d22c1476fa83f27a -i "cis-demo"
```
{: pre}

### `ibmcloud cis range-app`
{: #show-range-app}

[Enterprise Plans Only]{: tag-blue}

Get the application configuration of a specific application.

```sh
ibmcloud cis range-app DNS_DOMAIN_ID APP_ID [--instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-range-app-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`APP_ID`
:   The ID of range application. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-range-app-examples}

Show details of range application `ea95132c15732412d22c1476fa83f27a`.

```sh
ibmcloud cis range-app 31984fea73a15b45779fa0df4ef62f9b ea95132c15732412d22c1476fa83f27a -i "cis-demo"
```
{: pre}

### `ibmcloud cis range-apps`
{: #list-range-app}

[Enterprise Plans Only]{: tag-blue}

Retrieve a list of currently existing range applications for a DNS domain.

```sh
ibmcloud cis range-apps DNS_DOMAIN_ID [--instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #list-range-app-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-range-app-examples}

List all range applications in the domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis range-apps 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis range-analytics`
{: #get-analytics-range-app}

[Enterprise Plans Only]{: tag-blue}

Get analytics data for range applications.

```sh
ibmcloud cis range-analytics DNS_DOMAIN_ID [--metrics METRICS] [--dimensions DIMENSION] [--filters FILTERS] [--sort SORT] [--since SINCE] [--until UNTIL]
ibmcloud cis range-analytics DNS_DOMAIN_ID --bytime [--time_delta DELTA] [--metrics METRICS] [--dimensions DIMENSION] [--filters FILTERS] [--sort SORT] [--since SINCE] [--until UNTIL]
```

#### Command options
{: #get-analytics-range-app-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--metrics`
:   One or more metrics to compute.
    To get all metrics, set metrics to `count,bytesIngress,bytesEgress,durationAvg,durationMedian,duration90th,duration99th`.

`--dimension`
:   Can be used to break down the data by attributes. To get all dimensions, set dimensions to `event,appID,coloName,ipVersion`.
`--filters`
:   Used to filter rows by one or more dimensions.
    Filters can be combined by using OR and AND Boolean logic. AND takes precedence over OR in all the expressions.
    The OR operator is defined by using a comma (,) or OR keyword that is surrounded by whitespace.
    The AND operator is defined by using a semicolon (;) or AND keyword that is surrounded by whitespace.
    Comparison options are: `==`, `!=`, `>`, `<`, `>=`, `<=`.
    An example value for filters is: `event==connect AND coloName!=SFO`.

`--sort`
:   The sort order for the result set. Sort fields must be included in metrics or dimensions.
    An example value for sort is: `+count,-bytesIngress`.

`--since`
:   Start of time interval to query, defaults to until - 6 hours.
    This value must be an absolute timestamp that conforms to RFC 3339.

`--until`
:   End of time interval to query, defaults to current time.
    This value must be an absolute timestamp that conforms to RFC 3339.

`--bytime`
:   Analytics data for range applications grouped by time interval.

`--time-delta`
:   Used to select time series resolution. Valid values are `year`, `quarter`, `month`, `week`, `day`, `hour`, `dekaminute`, `minute`. Only valid when `--bytime` is given.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #get-analytics-range-app-examples}

Get analytics data for range applications in the domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis range-analytics 31984fea73a15b45779fa0df4ef62f9b --metrics "count,bytesIngress" --dimensions "event,appID" --since "2020-05-22T02:20:00Z"
--until "2020-05-23T02:20:00Z" -i "cis-demo"
```
{: pre}


## Rate limiting
{: #ratelimit}

Manipulate rate limits by using the following `ratelimit` commands.

### `ibmcloud cis ratelimit-rule-create`
{: #create-ratelimit}

[Enterprise Plans Only]{: tag-blue}

Create a new rate limiting rule for a DNS domain.

```sh
ibmcloud cis ratelimit-rule-create DNS_DOMAIN_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
ibmcloud cis ratelimit-rule-create DNS_DOMAIN_ID --url URL [--description DESCRIPTION] [--threshold NUM] [--period SECONDS] [...]
[Deprecated] ibmcloud cis ratelimit-rule-create DNS_DOMAIN_ID --json-str JSON_STR [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis ratelimit-rule-create DNS_DOMAIN_ID --json-file JSON_FILE [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #create-ratelimit-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--json`
:   The JSON file or JSON string that is used to describe a rate limiting rule.
    - The required fields in JSON data are `match`, `threshold`, `period` and `action` :
        - `match` : Determines which traffic the rate limiting rule counts toward the threshold.
            - `request` : Matches HTTP requests.
                - `methods` :  HTTP Methods, can be a subset `[POST,PUT]` or all `[_ALL_]`. This field is not required to create a rate limit rule. Valid values are `GET`, `POST`, `PUT`, `DELETE`, `PATCH`, `HEAD`, `_ALL_`.
                - `schemes` :  HTTP Schemes, can be one `[HTTPS]`, both `[HTTP`,`HTTPS]` or all `[_ALL_]`. This field is not required.
                - `url` : The URL pattern to match composed of the host and path, for instance, `example.org/path`. Wildcards are expanded to match applicable traffic, query strings are not matched. Use `*` for all traffic to your zone. The max length is `1024`.
            - `response` : Matches HTTP responses before they are returned to the client. If this is defined, then the entire counting of traffic occurs at this stage.
                - `status` : HTTP Status codes, can be one `[403]`, many `[401,403]` or indicate all by not providing this value. This field is not required. The min value is `100`and the max value is `999`.
                - `headers` : Array of response headers to match. If a response does not meet the header criteria, then the request is not counted towards the rate limiting rule. The header matching criteria includes the following properties.
                    - `name` : The name of the response header to match.
                    - `op` : The operator when matching, eq means equals, ne means not equals. Valid values are `eq` and `ne`.
                    - `value` : The value of the header, which is exactly matched.
        - `threshold` : The threshold that triggers the rate limit mitigations, which are combined with a period. For example, the threshold per period. The min value is `2`and the max value is`1000000`.
        - `period` : The time, in seconds, to count matching traffic. If the count exceeds the threshold within this period, the action is performed. The min value is `10` and the max value is `86400`.
        - `action` : The action performed when the threshold of matched traffic within the period defined is exceeded.
            - `mode` : The type of action performed. Valid values are: `simulate`, `ban`, `challenge`, `js_challenge`.
            - `timeout` : The time in seconds, as an integer to perform the mitigation action. The timeout can be the same or greater than the period. This field is valid only when the mode is `simulate` or `ban`. The min value is `10` and the max value is `86400`.
            - `response` : Custom content-type and body to return. This overrides the custom error for the zone. This field is not required. Omission results in the default HTML error page. This field is valid only when mode is `simulate` or `ban`.
                - `content_type` : The content-type of the body, which must be one of the following: `text/plain`, `text/xml`, `application/json`.
                - `body` : The body to return. The content here must conform to the `content_type`. The max length is `10240`.
    - The optional fields are `id`, `disabled`, `description`, `correlate` and `bypass`:
        - `id` : Identifier of the rate limiting rule.
        - `disabled` : Whether this rate limiting rule is currently disabled.
        - `description` : A note that you can use to describe the reason for a rate limiting rule.
        - `correlate` : Whether to enable NAT-based rate limiting.
            - `by` : Valid value is `nat`.
        - `bypass` : Criteria that allow the rate limit to be bypassed. For example, to express that you shouldn’t apply a rate limit to a set of URLs.
            - `name` : Valid value is `url`.
            - `value` : The url to bypass.

Sample JSON data:

```json
{
   "id": "92f17202ed8bd63d69a66b86a49a8f6b",
   "disabled": false,
   "description": "Prevent multiple login failures to mitigate brute force attacks",
   "bypass": [
      {
         "name": "url",
         "value": "api.example.com/*"
      }
   ],
   "threshold": 60,
   "period": 900,
   "correlate": {
      "by": "nat"
   },
   "action": [
      {
         "mode": "simulate",
         "timeout": 86400,
         "response": {
            "content_type": "text/plain",
            "body": "<error>This request has been rate-limited.</error>"
         }
      }
   ],
   "match": {
      "request": {
               "methods": [
                  "GET"
               ],
               "schemes": [
                  "HTTP",
                  "HTTPS"
               ],
               "url": "*.example.org/path*"
      },
      "response": {
         "status": [
               403, 401
         ],
         "headers": [
            {
               "name": "Cf-Cache-Status",
               "op": "eq",
               "value": "HIT"
            }
         ]
      }
   }
}
```
{: codeblock}

`-s, --json-st`
:   *Deprecated*. The JSON data describing a rate limiting rule.

`-j, --json-file`
:   *Deprecated*. A file contains input JSON data.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #create-ratelimit-examples}

Create a rate limiting rule for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis ratelimit-rule-create 31984fea73a15b45779fa0df4ef62f9b --json '{"id":"372e67954025e0ba6aaa6d586b9e0b59","disabled":false,"description":"Prevent multiple login failures to mitigate brute force attacks","match":{"request":{"methods":["GET","POST"],"schemes":["HTTP","HTTPS"],"url":"*.example.org/path*"},"response":{"status": [403, 401],"headers":[{"name":"Cf-Cache-Status","op":"ne","value":"HIT"}]}},"bypass":[{"name":"url","value":"api.example.com/*"}],"threshold":60,"period":900,"action":{"mode":"challenge","timeout":86400,"response":{"content_type":"text/xml","body":"<error>This request has been rate-limited.</error>"}}}' -i "cis-demo"
```
{: pre}

### `ibmcloud cis ratelimit-rule-update`
{: #update-ratelimit}

Update a rate limiting rule of a DNS domain.

```sh
ibmcloud cis ratelimit-rule-update DNS_DOMAIN_ID RATELIMIT_RULE_ID  (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
ibmcloud cis ratelimit-rule-update DNS_DOMAIN_ID RATELIMIT_RULE_ID [--url URL] [--description DESCRIPTION] [--threshold NUM] [--period SECONDS] [...]
[Deprecated] ibmcloud cis ratelimit-rule-update DNS_DOMAIN_ID RATELIMIT_RULE_ID --json-str JSON_STR [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis ratelimit-rule-update DNS_DOMAIN_ID RATELIMIT_RULE_ID --json-file JSON_FILE [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-ratelimit-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`RATELIMIT_RULE_ID`
:   The ID of rate limiting rule. Required.

`--json`
:   The JSON file or JSON strinthat is used to describe a rate limiting rule.
    - The required fields in JSON data are `match`, `threshold`, `period` and `action` :
        - `match` : Determines which traffic the rate limiting rule counts towards the threshold.
            - `request` : Matches HTTP requests.
                - `methods` :  HTTP Methods, can be a subset `[POST,PUT]` or all `[ALL]`. This field is not required to create a rate limit rule. Valid values are `GET`, `POST`, `PUT`, `DELETE`, `PATCH`, `HEAD`, `ALL`.
                - `schemes` :  HTTP Schemes, can be one `[HTTPS]`, both `[HTTP,HTTPS]` or all `[_ALL_]`. This field is not required.
                - `url` : The URL pattern to match consisted of the host and path, for instance, `example.org/path`. Wildcards are expanded to match applicable traffic, query strings are not matched. Use `*` for all traffic to your zone. The max length is `1024`.
            - `response` : Matches HTTP responses before they are returned to the client. If this field is defined, then the entire counting of traffic occurs at this stage.
                - `status` : HTTP Status codes, can be one `[403]`, many `[401,403]` or indicate all by not providing this value. This field is not required. The min value is `100` and the max value is `999`.
                - `headers` : Array of response headers to match. If a response does not meet the header criteria, then the request is not counted towards the rate limiting rule. An array of header matching criteria includes the following properties.
                    - `name` : The name of the response header to match.
                    - `op` : The operator when matching, eq means equals, ne means not equals. Valid values are `eq` and `ne`.
                    - `value` : The value of the header, which is exactly matched.
        - `threshold` : The threshold that triggers the rate limit mitigations, which are combined with period. For example, the threshold per period. The min value is `2` and the max value is `1000000`.
        - `period` : The time, in seconds, to count matching traffic. If the count exceeds the threshold within this period the action is performed. The min value is `1` and the max value is `3600`.
        - `action` : The action is performed when the threshold of matched traffic within the defined period is exceeded.
            - `mode` : The type of action performed. Valid values are `simulate`, `ban`, `challenge`, `js_challenge`.
            - `timeout` : The time, in seconds, as an integer to perform the mitigation action. Timeout is the same or greater than the period. This field is valid only when mode is `simulate` or `ban`. The min value is `10` and the max value is `86400`.
            - `response` : Custom content-type and body to return. This overrides the custom error for the zone. This field is not required. Omission results in the default HTML error page. This field is valid only when mode is `simulate` or `ban`.
                - `content_type` : The content-type of the body, which must be one of the following: `text/plain`, `text/xml`, `application/json`.
                - `body` : The body to return. The content here must conform to the `content_type`. The max length is `10240`.
    - The optional fields are `disabled`, `description`, `correlate` and `bypass`:
        - `disabled` : Whether this rate limiting rule is currently disabled.
        - `description` : A note that you can use to describe the reason for a rate limiting rule.
        - `correlate` : Whether to enable NAT-based rate limiting.
            - `by` : Valid value is `nat`.
        - `bypass` : Criteria that allow the rate limit to be bypassed. For example, to express that you shouldn’t apply a rate limit to a set of URLs.
            - `name` : Valid value is `url`.
            - `value` : The url to bypass.

Sample JSON data:

```json
{
   "disabled": false,
   "description": "Prevent multiple login failures to mitigate brute force attacks",
   "bypass": [
      {
         "name": "url",
         "value": "api.example.com/*"
      }
   ],
   "threshold": 60,
   "period": 900,
   "correlate": {
      "by": "nat"
   },
   "action": [
      {
         "mode": "simulate",
         "timeout": 86400,
         "response": {
            "content_type": "text/plain",
            "body": "<error>This request has been rate-limited.</error>"
         }
      }
   ],
   "match": {
      "request": {
               "methods": [
                  "GET"
               ],
               "schemes": [
                  "HTTP",
                  "HTTPS"
               ],
               "url": "*.example.org/path*"
      },
      "response": {
         "status": [
               403, 401
         ],
         "headers": [
            {
               "name": "Cf-Cache-Status",
               "op": "eq",
               "value": "HIT"
            }
         ]
      }
   }
}
```
{: codeblock}

`-s, --json-str`
:   *Deprecated*. The JSON data describing a rate limiting rule.

`-j, --json-file`
:   *Deprecated*. A file contains input JSON data.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-ratelimit-examples}

Update rate limiting rule for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis ratelimit-rule-update 31984fea73a15b45779fa0df4ef62f9b 372e67954025e0ba6aaa6d586b9e0b59 --json '{"disabled":false,"description":"Prevent multiple login failures to mitigate brute force attacks","match":{"request":{"methods":["GET","POST"],"schemes":["HTTP","HTTPS"],"url":"*.example.org/path*"},"response":{"status": [403, 401],"headers":[{"name":"Cf-Cache-Status","op":"ne","value":"HIT"}]}},"bypass":[{"name":"url","value":"api.example.com/*"}],"threshold":60,"period":900,"action":{"mode":"challenge","timeout":86400,"response":{"content_type":"text/xml","body":"<error>This request has been rate-limited.</error>"}}}' -i "cis-demo"
```
{: pre}

### `ibmcloud cis ratelimit-rules`
{: #list-ratelimit-rules}

List rate limiting rules of a DNS domain.

```sh
ibmcloud cis ratelimit-rules DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #list-ratelimit-rules-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #llist-ratelimit-rules-examples}

List rate limiting rules in domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis ratelimit-rules 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis ratelimit-rule`
{: #show-ratelimit-rule}

Get details of a rate limiting rule by ID.

```sh
ibmcloud cis ratelimit-rule DNS_DOMAIN_ID  RATELIMIT_RULE_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-ratelimit-rule-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`RATELIMIT_RULE_ID`
:   The ID of rate limit rule. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-ratelimit-rule-examples}


Get the details of rate limiting rule `372e67954025e0ba6aaa6d586b9e0b59`.

```sh
ibmcloud cis ratelimit-rule 31984fea73a15b45779fa0df4ef62f9b 372e67954025e0ba6aaa6d586b9e0b59 -i "cis-demo"
```
{: pre}

### `ibmcloud cis ratelimit-rule-delete`
{: #delete-ratelimit-rule}

Delete a rate limiting rule by ID.

```sh
ibmcloud cis ratelimit-rule-delete DNS_DOMAIN_ID RATELIMIT_RULE_ID [--instance INSTANCE]
```

#### Command options
{: #delete-ratelimit-rule-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`RATELIMIT_RULE_ID`
:   The ID of rate limit rule. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #delete-ratelimit-rule-examples}

Delete rate limiting rule `372e67954025e0ba6aaa6d586b9e0b60`.

```sh
ibmcloud cis ratelimit-rule-delete 31984fea73a15b45779fa0df4ef62f9b 372e67954025e0ba6aaa6d586b9e0b60 -i "cis-demo"
```
{: pre}

## Resource instance
{: #resource-instance}

Manipulate CIS Service instances by using the following `instance` commands.

### `ibmcloud cis instances`
{: #list-cis-service-instances}

List all CIS service instances.

```sh
ibmcloud cis instances [--output FORMAT]
```

#### Command options
{: #list-service-instances-options}

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-cis-service-instances-examples}

List all CIS instance in current account.

```sh
ibmcloud cis instances
```
{: pre}

### `ibmcloud cis instance-set`
{: #set-context-cis-service-instance}

Set the context service instance to operate.

```sh
ibmcloud cis instance-set [INSTANCE_NAME] [--unset]
```

#### Command options
{: #set-service-instances-options}

`INSTANCE_NAME`
:   The name of the CIS service instance. If it is presented, set the context instance to operate, if not, show the current context instance.

`--unset`
:   Unset context instance.

#### Examples
{: #set-context-cis-service-examples}

Set the context service instance to `cis-demo`

```sh
ibmcloud cis instance-set cis-demo
```
{: pre}

### `ibmcloud cis instance-create`
{: #create-cis-service-instance}

Create a CIS service instance.

```sh
ibmcloud cis instance-create INSTANCE_NAME PLAN [--output FORMAT]
```

#### Command options
{: #create-cis-service-instance-options}

`INSTANCE_NAME`
:   The name of CIS service instance. Required.

`PLAN`
:   The name or ID of a service plan. Required.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #create-cis-service-instance-examples}

Create a standard-next plan CIS instance `cis-demo`

```sh
ibmcloud cis instance-create cis-demo standard-next
```
{: pre}

### `ibmcloud cis instance-delete`
{: #delete-cis-service-instance}

Delete a CIS service instance.

```sh
ibmcloud cis instance-delete INSTANCE [-f, --force]
```

#### Command options
{: #delete-cis-service-instance-options}

`INSTANCE`
:   The name or ID of a CIS service instance. Required.

`-f, --force`
:   Delete instance without prompting for confirmation.

#### Examples
{: #delete-cis-service-instance-examples}

Delete CIS instance `cis-demo`

```sh
ibmcloud cis instance-delete cis-demo -f
```
{: pre}

### `ibmcloud cis instance-update`
{: #update-cis-service-instance}

Update a CIS service instance.

```sh
ibmcloud cis instance-update INSTANCE [--name NAME] [--plan PLAN]  [--output FORMAT]
```

#### Command options
{: #update-cis-service-instance-options}

`INSTANCE`
:   The name or ID of a CIS service instance. Required.

`NAME`
:   The name of CIS service instance.

`PLAN`
:   The name or ID of a service plan.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-cis-service-instance-examples}

Update cis instance `cis-demo` to enterprise-usage plan.

```sh
ibmcloud cis instance-update cis-demo --plan enterprise-usage
```
{: pre}

### `ibmcloud cis instance`
{: #get-cis-service-instance}

Show details of a CIS service instance.

```sh
ibmcloud cis instance INSTANCE [--output FORMAT]
```

#### Command options
{: #get-cis-service-instance-options}

`INSTANCE`
:   The name or ID of a CIS service instance. Required.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #get-cis-service-instance-examples}

Show details of cis instance `cis-demo`.

```sh
ibmcloud cis instance cis-demo
```
{: pre}

### `ibmcloud cis plans`
{: #list-cis-service-plans}

List all CIS service plans.

```sh
ibmcloud cis plans [--refresh] [--output FORMAT]
```

#### Command options
{: #list-cis-service-plans-options}

`--refresh`
:   Force refresh from catalog.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-cis-service-plans-examples}

List CIS services plans.

```sh
ibmcloud cis plans --refresh
```
{: pre}

## Routing
{: #routing}

Manipulate routing by using the following `routing` commands.

### `ibmcloud cis routing`
{: #show-routing}

[Enterprise Plans Only]{: tag-blue}

Get details of Routing settings.

```sh
ibmcloud cis routing DNS_DOMAIN_ID (--smart-routing | --tiered-caching) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-routinge-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--smart-routing`
:   Uses real-time network intelligence to route traffic across paths from the origin to a CIS data center.

`--tiered-caching`
:   Uses regional Tier 1 CIS data centers to accelerate content delivery.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-routing-examples}

Get the details of routing settings for domain `372e67954025e0ba6aaa6d586b9e0b60`.

```sh
ibmcloud cis routing 31984fea73a15b45779fa0df4ef62f9b --smart-routing -i "cis-demo"
```
{: pre}

### `ibmcloud cis routing-update`
{: #update-routing}

[Enterprise Plans Only]{: tag-blue}

Update Routing setting.

```sh
ibmcloud cis routing-update DNS_DOMAIN_ID (--smart-routing (on|off) | --tiered-caching (on|off)) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-routinge-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--smart-routing`
:   Uses real-time network intelligence to route traffic across paths from the origin to a CIS data center. Valid values: `on`, `off`.

`--tiered-caching`
:   Uses regional Tier 1 CIS data centers to accelerate content delivery. Valid values are `on` and `off`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-routing-examples}

Update routing settings for domain `372e67954025e0ba6aaa6d586b9e0b60`.

```sh
ibmcloud cis routing-update 31984fea73a15b45779fa0df4ef62f9b --smart-routing on --tiered-caching on -i "cis-demo"
```
{: pre}

### `ibmcloud cis routing-analytics`
{: #display-routing-analytics}

[Enterprise Plans Only]{: tag-blue}

Get analytics of smart-routing latency.

```sh
ibmcloud cis routing-analytics DNS_DOMAIN_ID [--colos] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #display-routing-analytics-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--colos`
:   Analytics of smart-routing latency colos.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #display-routing-analytics-examples}

Get analytics of smart-routing latency for domain `372e67954025e0ba6aaa6d586b9e0b60`.

```sh
ibmcloud cis routing-analytics 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

## Security events (Deprecated)
{: #security-events}

Security events are deprecated on 26 October 2020. Use [`ibmcloud cis firewall-event-analytics`](#firewall-event-analytics) instead. Manage how the Security Events performs by using the following `security-events` command:

### `ibmcloud cis security-events`
{: #list-security-event}

The `security-events` command is replacing the `firewall-events` command. It can pull up to 30 days of security events which might be triggered from a wider variety of sources (other than firewall) such as rate-limiting, L7 DDoS, and browser-integrity-check. With the new `security-events` command, you are able to list only firewall events by specifying the `--source` options.

Retrieve a full log of security events include Firewall Rules, Rate Limiting, Security Level, Access Rules, WAF, User Agent Blocking, Zone Lockdown, and Advanced DDoS Protection.

```sh
ibmcloud cis security-events DNS_DOMAIN_ID [--ip-class IP_CLASS] [--method METHOD] [--scheme SCHEME] [--ip IP_ADDR] [--host HOSTNAME] [--protocol PROTOCOL] [--uri URI] [--ua USER_AGENT] [--colo COLO] [--ray-id RAY_ID] [--kind KIND] [--action ACTION] [--cursor CURSOR] [--country COUNTRY] [--since START_DATE] [--until END_DATE] [--source SOURCE] [--limit LIMIT] [--rule_id RULE_ID] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #list-security-event-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--ip-class`
:   IP class is a map of client IP to visitor classification. Valid values are `unknown`, `clean`, `badHost`, `searchEngine`, `whitelist`, `greylist`, `monitoringService`, `securityScanner`, `noRecord`, `scan`, `backupService`, `mobilePlatform`, `tor`.

`--method`
:   The HTTP method of the request. Valid values are `GET`, `POST`, `DELETE`, `PUT`, `HEAD`, `PURGE`, `OPTIONS`, `PROPFIND`, `MKCOL`, `PATCH`, `ACL`, `BCOPY`, `BDELETE`, `BMOVE`, `BPROPFIND`, `BPROPPATCH`, `CHECKIN`, `CHECKOUT`, `CONNECT`, `COPY`, `LABEL`, `LOCK`, `MERGE`, `MKACTIVITY`, `MKWORKSPACE`, `MOVE`, `NOTIFY`, `ORDERPATCH`, `POLL`, `PROPPATCH`, `REPORT`, `SEARCH`, `SUBSCRIBE`, `TRACE`, `UNCHECKOUT`, `UNLOCK`, `UNSUBSCRIBE`, `UPDATE`, `VERSION-CONTROL`, `BASELINE-CONTROL`, `X-MS-ENUMATTS`, `RPC_OUT_DATA`, `RPC_IN_DATA`, `JSON`, `COOK`, `TRACK`.

`--scheme`
:   The scheme of the URI. Valid values are `unknown`, `http` and `https`.

`--ip`
:   The IPv4 or IPv6 address from which the request originated.

`--host`
:   The hostname the request attempted to access.

`--protocol`
:   The protocol of the request. Valid values are `UNK`, `HTTP/1.0`, `HTTP/1.1`, `HTTP/1.2`, `HTTP/2` and `SPDY/3.1`.

`--uri`
:   The URI requested from the hostname.

`--ua`
:   The client user agent that initiated the request.

`--colo`
:   The 3-letter airport code of the Cloudflare data center that handled the request. For example, `SJC`.

`--ray-id`
:   Ray ID of the request.

`--action`
:   What type of action was taken. Valid values are `unknown`, `allow`, `drop`, `challenge`, `jschallenge`, `simulate`, `connectionClose` and `log`.

`--cursor`
:   Cursor position and direction for requesting the next set of records when the number of results are limited by the limit parameter. A valid value for the cursor can be obtained from the cursors object in the result_info structure.

`--country`
:   The 2-digit country code in which the request originated. For example, `US`.

`--since`
:   Start date and time of requesting data period in the ISO8601 format. Can't go back more than a year. For example, `2016-11-11T12:00:00Z`.

`--until`
:   End date and time of requesting data period in the ISO8601 format. For example, `2016-11-11T12:00:00Z`.

`--source`
:   Source of the event. Valid values are `unknown`, `asn`, `country`, `ip`, `ipRange`, `securityLevel`, `zoneLockdown`, `waf`, `uaBlock`, `rateLimit`, `firewallRules`, `bic`, `hot`, and `l7ddos`.

`--limit`
:   The number of events to return. The cursor attribute can be used to iterate over the next batch of events, if there are more events in the queried time range. Note that the `scanned_range` parameter in the `result_info` structure gives an indication of when events were considered in the current resultset if a limit was applied. Valid values are from 10 to 1000. Default value: 50.

`--rule-id`
:   The ID of the rule that triggered the event, which must be considered in the context of source.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-security-event-examples}

Get security events for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis security-events 31984fea73a15b45779fa0df4ef62f9b --action challenge --colo SJC --country US --host "www.example.com" --ip-class clean
--method POST --ray-id 187d944c61940c77 --cursor "6yDGxLKVeeHZZmORS_8XeSuhz9SjIJRaSa2lnsF01tQOHrfTGAP3R5X1Kv5iVUuMbNKhWNAXHOl6ePB0TUL8nw" -i "cis-demo"
```
{: pre}

## TLS
{: #tls}

Manipulate TLS by using the following `tls` commands.

### `ibmcloud cis tls-settings`
{: #show-tls-setting}

Get TLS settings for a domain.

```sh
ibmcloud cis tls-settings DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-tls-setting-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-tls-setting-examples}

Get TLS settings for domain `372e67954025e0ba6aaa6d586b9e0b60`.

```sh
ibmcloud cis tls-settings 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis tls-settings-update`
{: #update-tls-settings}

Update TLS settings for a DNS domain.

```sh
ibmcloud cis tls-settings-update DNS_DOMAIN_ID [--mode MODE] [--universal (true|false)] [--tls-1-2-only (on|off)] [--tls-1-3 (on|off)] [-i, --instance INSTANCE][--output FORMAT]
```

#### Command options
{: #update-tls-settings-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--mode`
:   Specify whether visitors can browse your website over a secure connection, and when they do, how CIS connects to your origin server.
    Valid values are `off`, `client-to-edge`, `end-to-end-flexible`, `end-to-end-ca-signed`, `https-only-origin-pull`.
    See the following documentation link for detailed [TLS mode description](/docs/cis?topic=cis-cis-tls-options).

`--universal`
:   Specify whether universal ssl is enabled for your domain. Valid values are `true` and `false`.

`--tls-1-2-only`
:   Specify whether Crypto TLS 1.2 feature is enable for your domain. Enabling this feature prevents use of previous versions. Valid values are `on` and `off`.

`--tls-1-3`
:   Specify whether Crypto TLS 1.3 feature is enabled for your domain. Valid values are `on`, `off`.

`--min-tls-version`
:   Only accept HTTPS requests that use at least the TLS protocol version specified.  Valid values are `1.0`, `1.1`, `1.2`, `1.3`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-tls-settings-examples}

Update TLS settings for the domain `372e67954025e0ba6aaa6d586b9e0b60`.

```sh
ibmcloud cis tls-settings-update 31984fea73a15b45779fa0df4ef62f9b --mode end-to-end-ca-signed --tls-1-2-only on -i "cis-demo"
```
{: pre}

### `ibmcloud cis certificates`
{: #list-cert}

List all certificates for a DNS domain, including shared, dedicated, and custom certificates.

```sh
ibmcloud cis certificates DNS_DOMAIN_ID [--keyless] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #list-cert-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--keyless`
:   List all keyless certificates.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-cert-examples}

List all certificates for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis certificates 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis certificate`
{: #show-cert}

Get the details of a shared, dedicated, or custom certificate.

```sh
ibmcloud cis certificate DNS_DOMAIN_ID (--cert-id CERT_ID | --universal) [--keyless] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-cert-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--cert-id`
:   ID of the dedicated or custom certificate.

`--universal`
:   Show universal certificate details.

`--keyless`
:   Show keyless certificate details.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-cert-examples}

Show details for a certificate.

```sh
ibmcloud cis certificate 31984fea73a15b45779fa0df4ef62f9b --universal -i "cis-demo"
ibmcloud cis certificate 31984fea73a15b45779fa0df4ef62f9b --cert-id 5a7805061c76ada191ed06f989cc3dac -i "cis-demo"
ibmcloud cis certificate 31984fea73a15b45779fa0df4ef62f9b --cert-id 5a7805061c76ada191ed06f989cc3dac --keyless -i "cis-demo"
```
{: codeblock}

### `ibmcloud cis certificate-order`
{: #order-dedicated-cert}

Order a certificate pack with an optional list of hostnames for a DNS domain.

```sh
ibmcloud cis certificate-order DNS_DOMAIN_ID [--hostnames host1 --hostnames host2 ...] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #order-dedicated-cert-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--hostnames`
:   Valid host names for the certificate packs. Add up to 50 custom hostnames - Can affect the price.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #order-dedicated-cert-examples}

Order a certificate pack for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis certificate-order 31984fea73a15b45779fa0df4ef62f9b --hostnames www.example.com --hostnames api.example.com -i "cis-demo"
```
{: pre}

### `ibmcloud cis certificate-upload`
{: #upload-cert}

Upload a custom certificate for a DNS domain.

```sh
ibmcloud cis certificate-upload DNS_DOMAIN_ID [--keyless] (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis certificate-upload DNS_DOMAIN_ID [--keyless] (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #upload-cert-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--keyless`
:   Upload a keyless certificate.

`--json`
:   The JSON file or JSON string that is used to describe a custom certificate. Required.
    - The required fields in JSON data are `certificate`, `private_key`,`host` and `port` :
        - `certificate` : SSL certificate or certificate and one or more intermediates for the domain.
        - `private_key` : Private key for the domain.
        - `host` : The keyless SSL host name.
        - `port` : The keyless SSL port used to communicate between CIS and the client's Keyless SSL server.
    - The optional fields are `bundle_method` and `name` :
        - `bundle_method` : Bundle method, default value is `compatible`, valid values are `compatible`, `modern` and `user-defined`.
        - `name` : The keyless SSL name.

Sample JSON data:

```json
{
   "certificate": "xxx",
   "private_key": "xxx",
   "bundle_method": "compatible"
}

For keyless ssl
{
    "host":"www.example.com",
    "port":8000,
    "certificate": "xxx",
    "bundle_method": "user-defined",
   "name": "test"
}
```
{: codeblock}

`-s, --json-str`
:   *Deprecated*. The JSON data used to upload a custom certificate.

`-j, --json-file`
:   *Deprecated*. A file contains input JSON data.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #upload-cert-examples}

Upload a custom certificate for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis certificate-upload 31984fea73a15b45779fa0df4ef62f9b --json '{"certificate": "-----BEGIN CERTIFICATE-----\nMIIDtTCCAp2gAwIBAgIJAMHAwfXZ5/PWMA0GCSqGSIb3DQEBCwUAMEUxCzAJBgNV\nBAYTAkFVMRMwEQYDVQQIEwpTb21lLVN0YXRlMSEwHwYDVQQKExhJbnRlcm5ldCBX\naWRnaXRzIFB0eSBMdGQwHhcNMTYwODI0MTY0MzAxWhcNMTYxMTIyMTY0MzAxWjBF\nMQswCQYDVQQGEwJBVTETMBEGA1UECBMKU29tZS1TdGF0ZTEhMB8GA1UEChMYSW50\nZXJuZXQgV2lkZ2l0cyBQdHkgTHRkMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIB\nCgKCAQEAwQHoetcl9+5ikGzV6cMzWtWPJHqXT3wpbEkRU9Yz7lgvddmGdtcGbg/1\nCGZu0jJGkMoppoUo4c3dts3iwqRYmBikUP77wwY2QGmDZw2FvkJCJlKnabIRuGvB\nKwzESIXgKk2016aTP6/dAjEHyo6SeoK8lkIySUvK0fyOVlsiEsCmOpidtnKX/a+5\n0GjB79CJH4ER2lLVZnhePFR/zUOyPxZQQ4naHf7yu/b5jhO0f8fwt+pyFxIXjbEI\ndZliWRkRMtzrHOJIhrmJ2A1J7iOrirbbwillwjjNVUWPf3IJ3M12S9pEewooaeO2\nizNTERcG9HzAacbVRn2Y2SWIyT/18QIDAQABo4GnMIGkMB0GA1UdDgQWBBT/LbE4\n9rWf288N6sJA5BRb6FJIGDB1BgNVHSMEbjBsgBT/LbE49rWf288N6sJA5BRb6FJI\nGKFJpEcwRTELMAkGA1UEBhMCQVUxEzARBgNVBAgTClNvbWUtU3RhdGUxITAfBgNV\nBAoTGEludGVybmV0IFdpZGdpdHMgUHR5IEx0ZIIJAMHAwfXZ5/PWMAwGA1UdEwQF\nMAMBAf8wDQYJKoZIhvcNAQELBQADggEBAHHFwl0tH0quUYZYO0dZYt4R7SJ0pCm2\n2satiyzHl4OnXcHDpekAo7/a09c6Lz6AU83cKy/+x3/djYHXWba7HpEu0dR3ugQP\nMlr4zrhd9xKZ0KZKiYmtJH+ak4OM4L3FbT0owUZPyjLSlhMtJVcoRp5CJsjAMBUG\nSvD8RX+T01wzox/Qb+lnnNnOlaWpqu8eoOenybxKp1a9ULzIVvN/LAcc+14vioFq\n2swRWtmocBAs8QR9n4uvbpiYvS8eYueDCWMM4fvFfBhaDZ3N9IbtySh3SpFdQDhw\nYbjM2rxXiyLGxB4Bol7QTv4zHif7Zt89FReT/NBy4rzaskDJY5L6xmY=\n-----END CERTIFICATE-----\n", "private_key": "-----BEGIN RSA PRIVATE KEY-----\nMIIEowIBAAKCAQEAwQHoetcl9+5ikGzV6cMzWtWPJHqXT3wpbEkRU9Yz7lgvddmG\ndtcGbg/1CGZu0jJGkMoppoUo4c3dts3iwqRYmBikUP77wwY2QGmDZw2FvkJCJlKn\nabIRuGvBKwzESIXgKk2016aTP6/dAjEHyo6SeoK8lkIySUvK0fyOVlsiEsCmOpid\ntnKX/a+50GjB79CJH4ER2lLVZnhePFR/zUOyPxZQQ4naHf7yu/b5jhO0f8fwt+py\nFxIXjbEIdZliWRkRMtzrHOJIhrmJ2A1J7iOrirbbwillwjjNVUWPf3IJ3M12S9pE\newooaeO2izNTERcG9HzAacbVRn2Y2SWIyT/18QIDAQABAoIBACbhTYXBZYKmYPCb\nHBR1IBlCQA2nLGf0qRuJNJZg5iEzXows/6tc8YymZkQE7nolapWsQ+upk2y5Xdp/\naxiuprIs9JzkYK8Ox0r+dlwCG1kSW+UAbX0bQ/qUqlsTvU6muVuMP8vZYHxJ3wmb\n+ufRBKztPTQ/rYWaYQcgC0RWI20HTFBMxlTAyNxYNWzX7RKFkGVVyB9RsAtmcc8g\n+j4OdosbfNoJPS0HeIfNpAznDfHKdxDk2Yc1tV6RHBrC1ynyLE9+TaflIAdo2MVv\nKLMLq51GqYKtgJFIlBRPQqKoyXdz3fGvXrTkf/WY9QNq0J1Vk5ERePZ54mN8iZB7\n9lwy/AkCgYEA6FXzosxswaJ2wQLeoYc7ceaweX/SwTvxHgXzRyJIIT0eJWgx13Wo\n/WA3Iziimsjf6qE+SI/8laxPp2A86VMaIt3Z3mJN/CqSVGw8LK2AQst+OwdPyDMu\niacE8lj/IFGC8mwNUAb9CzGU3JpU4PxxGFjS/eMtGeRXCWkK4NE+G08CgYEA1Kp9\nN2JrVlqUz+gAX+LPmE9OEMAS9WQSQsfCHGogIFDGGcNf7+uwBM7GAaSJIP01zcoe\nVAgWdzXCv3FLhsaZoJ6RyLOLay5phbu1iaTr4UNYm5WtYTzMzqh8l1+MFFDl9xDB\nvULuCIIrglM5MeS/qnSg1uMoH2oVPj9TVst/ir8CgYEAxrI7Ws9Zc4Bt70N1As+U\nlySjaEVZCMkqvHJ6TCuVZFfQoE0r0whdLdRLU2PsLFP+q7qaeZQqgBaNSKeVcDYR\n9B+nY/jOmQoPewPVsp/vQTCnE/R81spu0mp0YI6cIheT1Z9zAy322svcc43JaWB7\nmEbeqyLOP4Z4qSOcmghZBSECgYACvR9Xs0DGn+wCsW4vze/2ei77MD4OQvepPIFX\ndFZtlBy5ADcgE9z0cuVB6CiL8DbdK5kwY9pGNr8HUCI03iHkW6Zs+0L0YmihfEVe\nPG19PSzK9CaDdhD9KFZSbLyVFmWfxOt50H7YRTTiPMgjyFpfi5j2q348yVT0tEQS\nfhRqaQKBgAcWPokmJ7EbYQGeMbS7HC8eWO/RyamlnSffdCdSc7ue3zdVJxpAkQ8W\nqu80pEIF6raIQfAf8MXiiZ7auFOSnHQTXUbhCpvDLKi0Mwq3G8Pl07l+2s6dQG6T\nlv6XTQaMyf6n1yjzL+fzDrH3qXMxHMO/b13EePXpDMpY7HQpoLDi\n-----END RSA PRIVATE KEY-----\n", "bundle_method": "compatible"}' -i "cis-demo"
```
{: pre}

### `ibmcloud cis certificate-update`
{: #update-cert}

Update a custom certificate for a DNS domain.

```sh
ibmcloud cis certificate-update DNS_DOMAIN_ID CERT_ID [--keyless] (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis certificate-update DNS_DOMAIN_ID CERT_ID [--keyless] [-s, --json-str JSON_STR | -j, --json-file JSON_FILE] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-cert-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`CERT_ID`
:   The ID of the custom certificate. Required.

`--keyless`
:   Update a keyless certificate.

`--json`
:   The JSON file or JSON string that is used to describe a custom certificate. Required.
    - The required fields in JSON data are `certificate`, `private_key`,`host` and `port` :
        - `certificate` : SSL certificate or certificate and one or more intermediates for the domain.
        - `private_key` : Private key for the domain.
        - `host` : The keyless SSL host name.
        - `port` : The keyless SSL port used to communicate between CIS and the client's Keyless SSL server.
    - The optional fields are `bundle_method` :
        - `bundle_method` : Bundle method, default value is `compatible`, valid values are `compatible`, `modern` and `user-defined`.
        - `name` : The keyless SSL name.

Sample JSON data:

```json
{
   "certificate": "xxx",
   "private_key": "xxx",
   "bundle_method": "compatible"
}

For keyless ssl
{
    "host":"www.example.com",
    "port":8000,
    "certificate": "xxx",
    "bundle_method": "user-defined",
   "name": "test"
}
```
{: codeblock}

`-s, --json-str`
:   *Deprecated*. The JSON data used to update a custom certificate.

`-j, --json-file`
:   *Deprecated*. A file contains input JSON data.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-cert-examples}

Update the custom certificate `5a7805061c76ada191ed06f989cc3dac`.

```sh
ibmcloud cis certificate-update 31984fea73a15b45779fa0df4ef62f9b 5a7805061c76ada191ed06f989cc3dac --json '{"certificate": "-----BEGIN CERTIFICATE-----\nMIIDtTCCAp2gAwIBAgIJAMHAwfXZ5/PWMA0GCSqGSIb3DQEBCwUAMEUxCzAJBgNV\nBAYTAkFVMRMwEQYDVQQIEwpTb21lLVN0YXRlMSEwHwYDVQQKExhJbnRlcm5ldCBX\naWRnaXRzIFB0eSBMdGQwHhcNMTYwODI0MTY0MzAxWhcNMTYxMTIyMTY0MzAxWjBF\nMQswCQYDVQQGEwJBVTETMBEGA1UECBMKU29tZS1TdGF0ZTEhMB8GA1UEChMYSW50\nZXJuZXQgV2lkZ2l0cyBQdHkgTHRkMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIB\nCgKCAQEAwQHoetcl9+5ikGzV6cMzWtWPJHqXT3wpbEkRU9Yz7lgvddmGdtcGbg/1\nCGZu0jJGkMoppoUo4c3dts3iwqRYmBikUP77wwY2QGmDZw2FvkJCJlKnabIRuGvB\nKwzESIXgKk2016aTP6/dAjEHyo6SeoK8lkIySUvK0fyOVlsiEsCmOpidtnKX/a+5\n0GjB79CJH4ER2lLVZnhePFR/zUOyPxZQQ4naHf7yu/b5jhO0f8fwt+pyFxIXjbEI\ndZliWRkRMtzrHOJIhrmJ2A1J7iOrirbbwillwjjNVUWPf3IJ3M12S9pEewooaeO2\nizNTERcG9HzAacbVRn2Y2SWIyT/18QIDAQABo4GnMIGkMB0GA1UdDgQWBBT/LbE4\n9rWf288N6sJA5BRb6FJIGDB1BgNVHSMEbjBsgBT/LbE49rWf288N6sJA5BRb6FJI\nGKFJpEcwRTELMAkGA1UEBhMCQVUxEzARBgNVBAgTClNvbWUtU3RhdGUxITAfBgNV\nBAoTGEludGVybmV0IFdpZGdpdHMgUHR5IEx0ZIIJAMHAwfXZ5/PWMAwGA1UdEwQF\nMAMBAf8wDQYJKoZIhvcNAQELBQADggEBAHHFwl0tH0quUYZYO0dZYt4R7SJ0pCm2\n2satiyzHl4OnXcHDpekAo7/a09c6Lz6AU83cKy/+x3/djYHXWba7HpEu0dR3ugQP\nMlr4zrhd9xKZ0KZKiYmtJH+ak4OM4L3FbT0owUZPyjLSlhMtJVcoRp5CJsjAMBUG\nSvD8RX+T01wzox/Qb+lnnNnOlaWpqu8eoOenybxKp1a9ULzIVvN/LAcc+14vioFq\n2swRWtmocBAs8QR9n4uvbpiYvS8eYueDCWMM4fvFfBhaDZ3N9IbtySh3SpFdQDhw\nYbjM2rxXiyLGxB4Bol7QTv4zHif7Zt89FReT/NBy4rzaskDJY5L6xmY=\n-----END CERTIFICATE-----\n", "private_key": "-----BEGIN RSA PRIVATE KEY-----\nMIIEowIBAAKCAQEAwQHoetcl9+5ikGzV6cMzWtWPJHqXT3wpbEkRU9Yz7lgvddmG\ndtcGbg/1CGZu0jJGkMoppoUo4c3dts3iwqRYmBikUP77wwY2QGmDZw2FvkJCJlKn\nabIRuGvBKwzESIXgKk2016aTP6/dAjEHyo6SeoK8lkIySUvK0fyOVlsiEsCmOpid\ntnKX/a+50GjB79CJH4ER2lLVZnhePFR/zUOyPxZQQ4naHf7yu/b5jhO0f8fwt+py\nFxIXjbEIdZliWRkRMtzrHOJIhrmJ2A1J7iOrirbbwillwjjNVUWPf3IJ3M12S9pE\newooaeO2izNTERcG9HzAacbVRn2Y2SWIyT/18QIDAQABAoIBACbhTYXBZYKmYPCb\nHBR1IBlCQA2nLGf0qRuJNJZg5iEzXows/6tc8YymZkQE7nolapWsQ+upk2y5Xdp/\naxiuprIs9JzkYK8Ox0r+dlwCG1kSW+UAbX0bQ/qUqlsTvU6muVuMP8vZYHxJ3wmb\n+ufRBKztPTQ/rYWaYQcgC0RWI20HTFBMxlTAyNxYNWzX7RKFkGVVyB9RsAtmcc8g\n+j4OdosbfNoJPS0HeIfNpAznDfHKdxDk2Yc1tV6RHBrC1ynyLE9+TaflIAdo2MVv\nKLMLq51GqYKtgJFIlBRPQqKoyXdz3fGvXrTkf/WY9QNq0J1Vk5ERePZ54mN8iZB7\n9lwy/AkCgYEA6FXzosxswaJ2wQLeoYc7ceaweX/SwTvxHgXzRyJIIT0eJWgx13Wo\n/WA3Iziimsjf6qE+SI/8laxPp2A86VMaIt3Z3mJN/CqSVGw8LK2AQst+OwdPyDMu\niacE8lj/IFGC8mwNUAb9CzGU3JpU4PxxGFjS/eMtGeRXCWkK4NE+G08CgYEA1Kp9\nN2JrVlqUz+gAX+LPmE9OEMAS9WQSQsfCHGogIFDGGcNf7+uwBM7GAaSJIP01zcoe\nVAgWdzXCv3FLhsaZoJ6RyLOLay5phbu1iaTr4UNYm5WtYTzMzqh8l1+MFFDl9xDB\nvULuCIIrglM5MeS/qnSg1uMoH2oVPj9TVst/ir8CgYEAxrI7Ws9Zc4Bt70N1As+U\nlySjaEVZCMkqvHJ6TCuVZFfQoE0r0whdLdRLU2PsLFP+q7qaeZQqgBaNSKeVcDYR\n9B+nY/jOmQoPewPVsp/vQTCnE/R81spu0mp0YI6cIheT1Z9zAy322svcc43JaWB7\nmEbeqyLOP4Z4qSOcmghZBSECgYACvR9Xs0DGn+wCsW4vze/2ei77MD4OQvepPIFX\ndFZtlBy5ADcgE9z0cuVB6CiL8DbdK5kwY9pGNr8HUCI03iHkW6Zs+0L0YmihfEVe\nPG19PSzK9CaDdhD9KFZSbLyVFmWfxOt50H7YRTTiPMgjyFpfi5j2q348yVT0tEQS\nfhRqaQKBgAcWPokmJ7EbYQGeMbS7HC8eWO/RyamlnSffdCdSc7ue3zdVJxpAkQ8W\nqu80pEIF6raIQfAf8MXiiZ7auFOSnHQTXUbhCpvDLKi0Mwq3G8Pl07l+2s6dQG6T\nlv6XTQaMyf6n1yjzL+fzDrH3qXMxHMO/b13EePXpDMpY7HQpoLDi\n-----END RSA PRIVATE KEY-----\n", "bundle_method": "compatible"}' -i "cis-demo"
```
{: pre}

### `ibmcloud cis certificate-priority-change`
{: #change-priority-custom-cert}

Change custom certificates' priority for a DNS domain.

```sh
ibmcloud cis certificate-priority-change DNS_DOMAIN_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
[Deprecated] ibmcloud cis certificate-priority-change DNS_DOMAIN_ID (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #change-priority-custom-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--json`
:   The JSON file or JSON string that is used to describe the custom certificates' priority. Required.
    - The required fields in JSON data are `certificates`:
        - `certificates` : An array of objects with the following fields.
            - `id`: Custom certificate identifier.
            - `priority` : The order or priority in which the certificate is used in a request. Higher numbers are tried first.

Sample JSON data:

```json
{
"certificates":[
   {
      "id":"5a7805061c76ada191ed06f989cc3dac",
      "priority":2
   },
   {
      "id":"da534493b38266b17fea74f3312be21c",
   "priority":1
   }
]
}
```
{: codeblock}

`-s, --json-str`
:   *Deprecated*. The JSON data used to change the custom certificates' priority.

`-j, --json-file`
:   *Deprecated*. A file contains input JSON data.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #change-priority-custom-examples}

Change custom certificates' priority for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis certificate-priority-change 31984fea73a15b45779fa0df4ef62f9b --json '{"certificates": [{"id":"5a7805061c76ada191ed06f989cc3dac", "priority":2},{"id":"9a7806061c88ada191ed06f989cc3dac","priority":1}]}' -i "cis-demo"
```
{: pre}

### `ibmcloud cis certificate-delete`
{: #delete-cert}

Delete a dedicated or custom certificate.

```sh
ibmcloud cis certificate-delete DNS_DOMAIN_ID CERT_ID [--keyless][-i, --instance INSTANCE]
```

#### Command options
{: #delete-cert-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`CERT_ID`
:   The ID of the dedicated or custom certificate. Required.

`--keyless`
:   Delete a keyless certificate.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

#### Examples
{: #delete-cert-examples}

Delete the custom certificate `5a7805061c76ada191ed06f989cc3dac`.

```sh
ibmcloud cis certificate-delete 31984fea73a15b45779fa0df4ef62f9b 5a7805061c76ada191ed06f989cc3dac -i "cis-demo"
```
{: pre}

## Web application firewall (WAF)
{: #waf}

Manage Web Application Firewalls by using the following `waf` commands.

### `ibmcloud cis waf-setting`
{: #show-waf-setting}

Show WAF setting.

```sh
ibmcloud cis waf-setting DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-waf-setting-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-waf-setting-examples}

Show WAF settings for domain `372e67954025e0ba6aaa6d586b9e0b60`.

```sh
ibmcloud cis waf-setting 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis waf-setting-update`
{: #update-waf-setting}

Update the WAF setting.

```sh
ibmcloud cis waf-setting-update DNS_DOMAIN_ID WAF_MODE [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-waf-setting-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`WAF_MODE`
:   The mode of WAF setting. Valid values are `waf-enable` and `waf-disable`. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-waf-setting-examples}

Enable WAF for domain `372e67954025e0ba6aaa6d586b9e0b60`.

```sh
ibmcloud cis waf-setting-update 31984fea73a15b45779fa0df4ef62f9b waf-enable -i "cis-demo"
```
{: pre}

### `ibmcloud cis waf-packages`
{: #list-waf-packages}

List all WAF packages.

```sh
ibmcloud cis waf-packages DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #list-waf-packages-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-waf-packages-examples}

List all WAF packages for domain `372e67954025e0ba6aaa6d586b9e0b60`.

```sh
ibmcloud cis waf-packages 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis waf-package`
{: #show-waf-package}

Get detail of a WAF package.

```sh
ibmcloud cis waf-package DNS_DOMAIN_ID WAF_PACKAGE_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-waf-package-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`WAF_PACKAGE_ID`
:   The ID of the WAF package. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-waf-package-examples}

Get detail of a WAF package `a25a9a7e9c00afc1fb2e0245519d725b`.

```sh
ibmcloud cis waf-package 31984fea73a15b45779fa0df4ef62f9b a25a9a7e9c00afc1fb2e0245519d725b -i "cis-demo"
```
{: pre}

### `ibmcloud cis waf-package-set`
{: #update-waf-owasp-package}

Update OWASP Package setting.

```sh
ibmcloud cis waf-package-set DNS_DOMAIN_ID OWASP_PACKAGE_ID [--sensitivity SENSITIVITY] [--action-mode ACTION_MODE] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-waf-owasp-package-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`OWASP_PACKAGE_ID`
:   The ID of the WAF package. Required.

`--sensitivity`
:   The sensitivity of the firewall package. Valid values are `high`, `medium`, `low`, and `off`.

`--action-mode`
:   The default action that is taken for rules under the firewall package. Valid values are `simulate` and `block`, `challenge`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-waf-owasp-package-examples}

Update the OWASP setting for package `a25a9a7e9c00afc1fb2e0245519d725b`.

```sh
ibmcloud cis waf-package-set 31984fea73a15b45779fa0df4ef62f9b a25a9a7e9c00afc1fb2e0245519d725b --sensitivity medium --action-mode simulate -i "cis-demo"
```
{: pre}

### `ibmcloud cis waf-groups`
{: #list-waf-groups}

List the WAF groups in a WAF package.

```sh
ibmcloud cis waf-groups DNS_DOMAIN_ID WAF_PACKAGE_ID [--page PAGE] [--per-page NUM] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #list-waf-groups-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`WAF_PACKAGE_ID`
:   The ID of the WAF package. Required.

`--page`
:   The page number of paginated results. The default value is `1`.

`--per-page`
:   The number of groups per page. The min value is `5` and the max value is `1000`. The default value is `50`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-waf-groups-examples}

List the WAF groups in a WAF package `a25a9a7e9c00afc1fb2e0245519d725b`.

```sh
ibmcloud cis waf-groups 31984fea73a15b45779fa0df4ef62f9b a25a9a7e9c00afc1fb2e0245519d725b --page 1 --per-page 100 -i "cis-demo"
```
{: pre}

### `ibmcloud cis waf-group`
{: #show-waf-group}

Get detail of a WAF group.

```sh
ibmcloud cis waf-group DNS_DOMAIN_ID WAF_PACKAGE_ID WAF_GROUP_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-waf-group-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`WAF_PACKAGE_ID`
:   The ID of the WAF package. Required.

`WAF_GROUP_ID`
:   The ID of the WAF group.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-waf-group-examples}

Get details of WAF group `de677e5818985db1285d0e80225f06e5` in WAF package `a25a9a7e9c00afc1fb2e0245519d725b`.

```sh
ibmcloud cis waf-group 31984fea73a15b45779fa0df4ef62f9b a25a9a7e9c00afc1fb2e0245519d725b de677e5818985db1285d0e80225f06e5 -i "cis-demo"
```
{: pre}

### `ibmcloud cis waf-group-mode-set`
{: #update-waf-group}

Set the mode of a WAF group.

```sh
ibmcloud cis waf-group-mode-set DNS_DOMAIN_ID WAF_PACKAGE_ID WAF_GROUP_ID WAF_GROUP_MODE [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-waf-group-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`WAF_PACKAGE_ID`
:   The ID of the WAF package. Required.

`WAF_GROUP_ID`
:   The ID of the WAF group. Required.

`WAF_GROUP_MODE`
:   The mode of WAF group. Valid values are `on` and `off`. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-waf-group-examples}

Enable the WAF group `de677e5818985db1285d0e80225f06e5` in the WAF package `a25a9a7e9c00afc1fb2e0245519d725b`.

```sh
ibmcloud cis waf-group-mode-set 31984fea73a15b45779fa0df4ef62f9b a25a9a7e9c00afc1fb2e0245519d725b de677e5818985db1285d0e80225f06e5 on -i "cis-demo"
```
{: pre}

### `ibmcloud cis waf-rules`
{: #list-waf-rules}

List all WAF rules of a WAF package.

```sh
ibmcloud cis waf-rules DNS_DOMAIN_ID WAF_PACKAGE_ID [--page PAGE] [--per-page NUM] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #list-waf-rules-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`WAF_PACKAGE_ID`
:   The ID of the WAF package. Required.

`--page`
:   Page number of the paginated results. The default value is `1`.

`--per-page`
:   Number of rules per page. The default value is `50`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-waf-rules-examples}

List all WAF rules in the WAF package `a25a9a7e9c00afc1fb2e0245519d725b`.

```sh
ibmcloud cis waf-rules 31984fea73a15b45779fa0df4ef62f9b a25a9a7e9c00afc1fb2e0245519d725b --page 1 --per-page 100 -i "cis-demo"
```
{: pre}

### `ibmcloud cis waf-rule`
{: #show-waf-rule}

Get detail of a WAF rule.

```sh
ibmcloud cis waf-rule DNS_DOMAIN_ID WAF_PACKAGE_ID WAF_RULE_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-waf-rule-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`WAF_PACKAGE_ID`
:   The ID of WAF package. Required.

`WAF_RULE_ID`
:   The ID of WAF rule. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-waf-rule-examples}

Get details of WAF rule `f939de3be84e66e757adcdcb87908023` in WAF package `a25a9a7e9c00afc1fb2e0245519d725b`.

```sh
ibmcloud cis waf-rule 31984fea73a15b45779fa0df4ef62f9b a25a9a7e9c00afc1fb2e0245519d725b f939de3be84e66e757adcdcb87908023 -i "cis-demo"
```
{: pre}

### `ibmcloud cis waf-rule-mode-set`
{: #update-waf-rule}

Set the mode of a WAF rule.

```sh
ibmcloud cis waf-rule-mode-set DNS_DOMAIN_ID WAF_PACKAGE_ID WAF_RULE_ID WAF_RULE_MODE [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-waf-rule-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`WAF_PACKAGE_ID`
:   The ID of the WAF package. Required.

`WAF_RULE_ID`
:   The ID of the WAF rule. Required.

`WAF_RULE_MODE`
:   The mode of WAF rule. Valid values are `on`, `off`, `default`, `disable`, `simulate`, `block`, and `challenge`. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-waf-rule-examples}

Disable WAF rule `f939de3be84e66e757adcdcb87908023` in WAF package `a25a9a7e9c00afc1fb2e0245519d725b`.

```sh
ibmcloud cis waf-rule-mode-set 31984fea73a15b45779fa0df4ef62f9b a25a9a7e9c00afc1fb2e0245519d725b f939de3be84e66e757adcdcb87908023 disable -i "cis-demo"
```
{: pre}

### `ibmcloud cis cis waf-override-create`
{: #create-waf-override}

Create a URL-based Web Application Firewall (WAF) rule.

```sh
ibmcloud cis waf-override-create DNS_DOMAIN_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #create-waf-override-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--json`
:   The JSON file or JSON string that is used to describe an override WAF rule. Required.
    - The required fields in JSON data are `urls` and `rules`.
        - `urls` : URLs to be included in this rule definition. Wildcards are permitted.
        - `rules` : Change the action that is assigned to a WAF rule. The keys of this object are WAF rule IDs and the values must be a valid WAF action. Unless disabling the rule, ensure that you also enable the rule group that this WAF rule belongs to. The max length is `1024`.
    - The optional fields are `paused`, `description`, `priority`, `groups`, and `rewrite_action`.
        - `paused` : Whether this package is currently paused. Valid values are `true` and `false`.
        - `description` : A note that you can use to describe the purpose of this rule.
        - `priority` : Relative priority of this configuration when multiple configurations match a single URL. Higher priority configurations might overwrite values set by lower priority configurations. The min value is `-1000000000` and the max value is `1000000000`.
        - `groups` Enable or disable WAF rule groups. The keys of this object are WAF rule group IDs and the values must be a valid WAF action (usually `default` or `disable`).
        - `rewrite_action` : When a WAF rule matches, substitute its configured action for a different action that is specified by this object.

Sample JSON data:

```json
   {
      "description": "Enable IBM Magento ruleset for www.example.com",
      "urls": [
         "www.example.com/*"
      ],
      "priority": 1,
      "groups": {
         "ea8687e59929c1fd05ba97574ad43f77": "default"
      },
      "rules": {
         "100015": "disable"
      },
      "rewrite_action": {
         "default": "block",
         "challenge": "block",
         "simulate": "disable"
      }
   }
```
{: codeblock}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #create-waf-override-examples}

Create a WAF override rule under instance `cis-demo`.

```sh
ibmcloud cis waf-override-create 31984fea73a15b45779fa0df4ef62f9b --json '{"description":"Enable IBM Magento ruleset for www.example.com","urls":["www.example.com/*"],"priority":1,"groups":{"ea8687e59929c1fd05ba97574ad43f77":"default"},"rules":{"100015":"disable"},"rewrite_action":{"default":"block","challenge":"block","simulate":"disable"}}' -i "cis-demo"
```
{: pre}

### `ibmcloud cis cis waf-override-update`
{: #update-waf-override}

Update a URL-based Web Application Firewall (WAF) rules.

```sh
ibmcloud cis waf-override-update DNS_DOMAIN_ID OVERRIDE_WAF_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-waf-override-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`OVERRIDE_WAF_ID`
:   The ID of the override WAF rule. Required.

`--json`
:   The JSON file or JSON string that is used to describe a override WAF rule. Required.
    - The required fields in JSON data are `urls` and `rules`.
        - `urls` : URLs to be included in this rule definition. Wildcards are permitted.
        - `rules` : Change the action that is assigned to a WAF rule. The keys of this object are WAF rule IDs and the values must be a valid WAF action. Unless you disable the rule, ensure that you also enable the rule group that this WAF rule belongs to. The max length is `1024`.
    - The optional fields are `paused`, `description`, `priority`, `groups`, and `rewrite_action`.
        - `paused` : Whether this package is currently paused. Valid values are `true` and `false`.
        - `description` : A note that you can use to describe the purpose of this rule.
        - `priority` : Relative priority of this configuration when multiple configurations match a single URL. Higher priority configurations might overwrite values set by lower priority configurations. The min value is`-1000000000` and the max value is `1000000000`.
        - `groups` Enable or disable WAF rule groups. The keys of this object are WAF rule group IDs and the values must be a valid WAF action (usually `default` or `disable`).
        - `rewrite_action` : When a WAF rule matches, substitute its configured action for a different action that is specified by this object.

Sample JSON data:

   ```json
   {
      "description": "Enable IBM Magento ruleset for www.example.com",
      "urls": [
         "www.example.com/*"
      ],
      "priority": 1,
      "groups": {
         "ea8687e59929c1fd05ba97574ad43f77": "default"
      },
      "rules": {
         "100015": "disable"
      },
      "rewrite_action": {
         "default": "block",
         "challenge": "block",
         "simulate": "disable"
      }
   }
   ```
   {: codeblock}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-waf-override-examples}

Update a WAF override rule under instance `cis-demo`.

```sh
ibmcloud cis waf-override-update 31984fea73a15b45779fa0df4ef62f9b a5836c2a7ea72d2e225890caea70ae32 --json '{"description":"Enable IBM Magento ruleset for www.example.com","urls":["www.example.com/*"],"priority":1,"groups":{"ea8687e59929c1fd05ba97574ad43f77":"default"},"rules":{"100015":"disable"},"rewrite_action":{"default":"block","challenge":"block","simulate":"disable"}}' -i "cis-demo"
```
{: pre}

### `ibmcloud cis cis waf-overrides`
{: #list-waf-overrides}

List all URL-based Web Application Firewall (WAF) rules.

```sh
ibmcloud cis waf-overrides DNS_DOMAIN_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #list-waf-overrides-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--page`
:   Page number of paginated results. The default value is `1`.

`--per-page`
:   Number of rules per page. The default value is `50`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-waf-override-examples}

List WAF override rules under instance `cis-demo`.

```sh
ibmcloud cis  waf-overrides 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis cis waf-override`
{: #get-waf-override}

Get a URL-based Web Application Firewall (WAF) rule.

```sh
ibmcloud cis waf-override DNS_DOMAIN_ID OVERRIDE_WAF_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #get-waf-overrides-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`OVERRIDE_WAF_ID`
:   The ID of override WAF rule.  Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #get-waf-override-examples}

Get a WAF override rule under instance `cis-demo`.

```sh
ibmcloud cis waf-override 31984fea73a15b45779fa0df4ef62f9b a5836c2a7ea72d2e225890caea70ae32 -i "cis-demo"
```
{: pre}

### `ibmcloud cis cis waf-override-delete`
{: #delete-waf-override}

Delete a URL-based Web Application Firewall (WAF) rule.

```sh
ibmcloud cis waf-override-delete DNS_DOMAIN_ID OVERRIDE_WAF_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #delete-waf-overrides-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`OVERRIDE_WAF_ID`
:   The ID of override WAF rule.  Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`-f, --force`
:   Attempt to delete the URL-based WAF rule without prompting for confirmation.

#### Examples
{: #delete-waf-override-examples}

Delete a WAF override rule under instance `cis-demo`.

```sh
ibmcloud cis waf-override-delete 31984fea73a15b45779fa0df4ef62f9b a5836c2a7ea72d2e225890caea70ae32 -i "cis-demo"
```
{: pre}

## Authenticated Origin Pull
{: #cli-authenticated-origin-pull}

Manage Authenticated Origin Pull by using the following `authenticated-origin-pull` commands.

### `ibmcloud cis authenticated-origin-pull-settings`
{: #show-authenticated-origin-pull-settings}

Get authenticated origin pull settings for a domain.

```sh
ibmcloud cis authenticated-origin-pull-settings DNS_DOMAIN_ID [--level zone|hostname] [--hostname HOSTNAME] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-authenticated-origin-pull-settings-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`----level`
:   Specify the authenticated origin pull certificate or settings per zone or hostname level. Valid values are `zone` and `hostname`. The default value is `zone`.

`--hostname`
:   The authenticated origin pull settings on a hostname. (hostname level only)

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-authenticated-origin-pull-settings-examples}

List authenticated origin pull settings on zone level for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis authenticated-origin-pull-settings 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis authenticated-origin-pull-setting-update`
{: #update-authenticated-origin-pull-setting}

Update authenticated origin pull settings for a domain.

```sh
ibmcloud cis authenticated-origin-pull-settings-update DNS_DOMAIN_ID [--level zone|hostname] [--hostname HOSTNAME] [--cert_id CERT_ID] (--enabled on|off) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-authenticated-origin-pull-settings-option}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`----level`
:   Specify the authenticated origin pull certificate or settings per zone or hostname level. Valid values are `zone` and `hostname`. The default value is `zone`.

`--hostname`
:   The authenticated origin pull settings on a hostname. (hostname level only)

`----cert_id`
:   The certificate id, which the hostname is bundled to. (hostname level only)

`----enabled`
:   Enable authenticated origin pull. Valid values are `on` and `off`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-authenticated-origin-pull-setting-examples}

Update authenticated origin pull setting on zone level for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis authenticated-origin-pull-settings-update 31984fea73a15b45779fa0df4ef62f9b --enabled on -i "cis-demo"
```
{: pre}

### `ibmcloud cis authenticated-origin-pull-certificates`
{: #show-authenticated-origin-pull-certificates}

List zone-level authenticated origin pull certificates for a domain.

```sh
ibmcloud cis authenticated-origin-pull-certificates DNS_DOMAIN_ID [--level zone|hostname][-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-authenticated-origin-pull-certificates-option}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`----level`
:   Specify the authenticated origin pull certificate or settings per zone or hostname level. Valid values are `zone` and `hostname`. The default value is `zone`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-authenticated-origin-pull-certificates-examples}

Show authenticated origin pull certificates on zone level for domain `31984fea73a15b45779fa0df4ef62f9b`.

```sh
ibmcloud cis authenticated-origin-pull-certificates 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis authenticated-origin-pull-certificate`
{: #show-authenticated-origin-pull-certificate}

Get an authenticated origin pull certificate for a domain.

```sh
ibmcloud cis authenticated-origin-pull-certificate DNS_DOMAIN_ID CERT_ID [--level zone|hostname] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-authenticated-origin-pull-certificate-option}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`CERT_ID`
:   The ID of the certificate. Required.

`----level`
:   Specify the authenticated origin pull certificate or settings per zone or hostname level. Valid values are `zone` and `hostname`. The default value is `zone`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-authenticated-origin-pull-certificate-examples}

Get an authenticated origin pull certificate `5a7805061c76ada191ed06f989cc3dac` on zone level for domain `31984fea73a15b45779fa0df4ef62f9b` .

```sh
ibmcloud cis authenticated-origin-pull-certificate 31984fea73a15b45779fa0df4ef62f9b 5a7805061c76ada191ed06f989cc3dac -i "cis-demo"
```
{: pre}

### `ibmcloud cis authenticated-origin-pull-certificate-upload`
{: #upload-authenticated-origin-pull-certificate}

Upload an authenticated origin pull certificate for a domain.

```sh
ibmcloud cis authenticated-origin-pull-certificate-upload DNS_DOMAIN_ID [--level zone|hostname] (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #upload-authenticated-origin-pull-certificate-option}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`--level`
:   Specify the authenticated origin pull certificate or settings per zone or hostname level. Valid values are `zone` and `hostname`. The default value is `zone`.

`--json`
:   The JSON file or JSON string that is used to describe a custom certificate.
    - The required fields in JSON data are `certificate` and `private_key` :
        - `certificate` : SSL certificate or certificate and one or more intermediates for the domain.
        - `private_key` : Private key for the domain.

   Sample JSON data:

```json
{
  "certificate": "-----BEGIN CERTIFICATE-----\n...-----END CERTIFICATE-----\n",
  "private_key": "-----BEGIN PRIVATE KEY-----\n...-----END PRIVATE KEY-----\n"
}
```
{: codeblock}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #upload-authenticated-origin-pull-certificate-examples}

Upload an authenticated origin pull certificate on zone level for domain `31984fea73a15b45779fa0df4ef62f9b` .

```sh
ibmcloud cis authenticated-origin-pull-certificate-upload 31984fea73a15b45779fa0df4ef62f9b --json '{"certificate": "-----BEGIN CERTIFICATE-----\nMIIDtTCCAp2gAwIBAgIJAMHAwfXZ5/PWMA0GCSqGSIb3DQEBCwUAMEUxCzAJBgNV\nBAYTAkFVMRMwEQYDVQQIEwpTb21lLVN0YXRlMSEwHwYDVQQKExhJbnRlcm5ldCBX\naWRnaXRzIFB0eSBMdGQwHhcNMTYwODI0MTY0MzAxWhcNMTYxMTIyMTY0MzAxWjBF\nMQswCQYDVQQGEwJBVTETMBEGA1UECBMKU29tZS1TdGF0ZTEhMB8GA1UEChMYSW50\nZXJuZXQgV2lkZ2l0cyBQdHkgTHRkMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIB\nCgKCAQEAwQHoetcl9+5ikGzV6cMzWtWPJHqXT3wpbEkRU9Yz7lgvddmGdtcGbg/1\nCGZu0jJGkMoppoUo4c3dts3iwqRYmBikUP77wwY2QGmDZw2FvkJCJlKnabIRuGvB\nKwzESIXgKk2016aTP6/dAjEHyo6SeoK8lkIySUvK0fyOVlsiEsCmOpidtnKX/a+5\n0GjB79CJH4ER2lLVZnhePFR/zUOyPxZQQ4naHf7yu/b5jhO0f8fwt+pyFxIXjbEI\ndZliWRkRMtzrHOJIhrmJ2A1J7iOrirbbwillwjjNVUWPf3IJ3M12S9pEewooaeO2\nizNTERcG9HzAacbVRn2Y2SWIyT/18QIDAQABo4GnMIGkMB0GA1UdDgQWBBT/LbE4\n9rWf288N6sJA5BRb6FJIGDB1BgNVHSMEbjBsgBT/LbE49rWf288N6sJA5BRb6FJI\nGKFJpEcwRTELMAkGA1UEBhMCQVUxEzARBgNVBAgTClNvbWUtU3RhdGUxITAfBgNV\nBAoTGEludGVybmV0IFdpZGdpdHMgUHR5IEx0ZIIJAMHAwfXZ5/PWMAwGA1UdEwQF\nMAMBAf8wDQYJKoZIhvcNAQELBQADggEBAHHFwl0tH0quUYZYO0dZYt4R7SJ0pCm2\n2satiyzHl4OnXcHDpekAo7/a09c6Lz6AU83cKy/+x3/djYHXWba7HpEu0dR3ugQP\nMlr4zrhd9xKZ0KZKiYmtJH+ak4OM4L3FbT0owUZPyjLSlhMtJVcoRp5CJsjAMBUG\nSvD8RX+T01wzox/Qb+lnnNnOlaWpqu8eoOenybxKp1a9ULzIVvN/LAcc+14vioFq\n2swRWtmocBAs8QR9n4uvbpiYvS8eYueDCWMM4fvFfBhaDZ3N9IbtySh3SpFdQDhw\nYbjM2rxXiyLGxB4Bol7QTv4zHif7Zt89FReT/NBy4rzaskDJY5L6xmY=\n-----END CERTIFICATE-----\n", "private_key": "-----BEGIN RSA PRIVATE KEY-----\nMIIEowIBAAKCAQEAwQHoetcl9+5ikGzV6cMzWtWPJHqXT3wpbEkRU9Yz7lgvddmG\ndtcGbg/1CGZu0jJGkMoppoUo4c3dts3iwqRYmBikUP77wwY2QGmDZw2FvkJCJlKn\nabIRuGvBKwzESIXgKk2016aTP6/dAjEHyo6SeoK8lkIySUvK0fyOVlsiEsCmOpid\ntnKX/a+50GjB79CJH4ER2lLVZnhePFR/zUOyPxZQQ4naHf7yu/b5jhO0f8fwt+py\nFxIXjbEIdZliWRkRMtzrHOJIhrmJ2A1J7iOrirbbwillwjjNVUWPf3IJ3M12S9pE\newooaeO2izNTERcG9HzAacbVRn2Y2SWIyT/18QIDAQABAoIBACbhTYXBZYKmYPCb\nHBR1IBlCQA2nLGf0qRuJNJZg5iEzXows/6tc8YymZkQE7nolapWsQ+upk2y5Xdp/\naxiuprIs9JzkYK8Ox0r+dlwCG1kSW+UAbX0bQ/qUqlsTvU6muVuMP8vZYHxJ3wmb\n+ufRBKztPTQ/rYWaYQcgC0RWI20HTFBMxlTAyNxYNWzX7RKFkGVVyB9RsAtmcc8g\n+j4OdosbfNoJPS0HeIfNpAznDfHKdxDk2Yc1tV6RHBrC1ynyLE9+TaflIAdo2MVv\nKLMLq51GqYKtgJFIlBRPQqKoyXdz3fGvXrTkf/WY9QNq0J1Vk5ERePZ54mN8iZB7\n9lwy/AkCgYEA6FXzosxswaJ2wQLeoYc7ceaweX/SwTvxHgXzRyJIIT0eJWgx13Wo\n/WA3Iziimsjf6qE+SI/8laxPp2A86VMaIt3Z3mJN/CqSVGw8LK2AQst+OwdPyDMu\niacE8lj/IFGC8mwNUAb9CzGU3JpU4PxxGFjS/eMtGeRXCWkK4NE+G08CgYEA1Kp9\nN2JrVlqUz+gAX+LPmE9OEMAS9WQSQsfCHGogIFDGGcNf7+uwBM7GAaSJIP01zcoe\nVAgWdzXCv3FLhsaZoJ6RyLOLay5phbu1iaTr4UNYm5WtYTzMzqh8l1+MFFDl9xDB\nvULuCIIrglM5MeS/qnSg1uMoH2oVPj9TVst/ir8CgYEAxrI7Ws9Zc4Bt70N1As+U\nlySjaEVZCMkqvHJ6TCuVZFfQoE0r0whdLdRLU2PsLFP+q7qaeZQqgBaNSKeVcDYR\n9B+nY/jOmQoPewPVsp/vQTCnE/R81spu0mp0YI6cIheT1Z9zAy322svcc43JaWB7\nmEbeqyLOP4Z4qSOcmghZBSECgYACvR9Xs0DGn+wCsW4vze/2ei77MD4OQvepPIFX\ndFZtlBy5ADcgE9z0cuVB6CiL8DbdK5kwY9pGNr8HUCI03iHkW6Zs+0L0YmihfEVe\nPG19PSzK9CaDdhD9KFZSbLyVFmWfxOt50H7YRTTiPMgjyFpfi5j2q348yVT0tEQS\nfhRqaQKBgAcWPokmJ7EbYQGeMbS7HC8eWO/RyamlnSffdCdSc7ue3zdVJxpAkQ8W\nqu80pEIF6raIQfAf8MXiiZ7auFOSnHQTXUbhCpvDLKi0Mwq3G8Pl07l+2s6dQG6T\nlv6XTQaMyf6n1yjzL+fzDrH3qXMxHMO/b13EePXpDMpY7HQpoLDi\n-----END RSA PRIVATE KEY-----\n"}'-i "cis-demo"
```
{: pre}

### `ibmcloud cis authenticated-origin-pull-certificate-delete`
{: #delete-authenticated-origin-pull-certificate}

Delete the authenticated origin pull certificate for a domain.

```sh
ibmcloud cis authenticated-origin-pull-certificate-delete DNS_DOMAIN_ID CERT_ID [--level zone|hostname] [-i, --instance INSTANCE] [--output FORMAT] [-f, --force]
```

#### Command options
{: #delete-authenticated-origin-pull-certificate-option}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain. Required.

`CERT_ID`
:   The ID of certificate. Required.

`--level`
:   Specify the authenticated origin pull certificate or settings per zone or hostname level. Valid values are `zone` and `hostname`. The default value is `zone`.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #delete-authenticated-origin-pull-certificate-examples}

Delete authenticated origin pull certificate `5a7805061c76ada191ed06f989cc3dac` on zone level for domain `31984fea73a15b45779fa0df4ef62f9b` .

```sh
ibmcloud cis authenticated-origin-pull-certificate-delete 31984fea73a15b45779fa0df4ef62f9b 5a7805061c76ada191ed06f989cc3dac -i "cis-demo"
```
{: pre}

## Alert policy
{: #alert-policy}

Manage alert policies.

### `ibmcloud cis alert-policy list` (List)
{: #list-alert-policies}

List all alert policies.

```sh
ibmcloud cis alert-policy list [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #opt-list-alert-policies}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-alert-policies-examples}

List all policies for instance `cis-demo`

```sh
ibmcloud cis alert-policy list -i "cis-demo"
```
{: pre}

### `ibmcloud cis alert-policy get` (Show)
{: #show-alert-policy}

Show the details of a policy.

```sh
ibmcloud cis alert-policy get POLICY_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-alert-policy-options}

`POLICY_ID`
:   The ID of alert policy. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-alert-policy-examples}

Show the details of the alert policy `a2633e68-1a64-2512-a321-b64a17c7db7a`.

```sh
ibmcloud cis alert-policy get a2633e68-1a64-2512-a321-b64a17c7db7a -i "cis-demo"
```
{: pre}

### `ibmcloud cis alert-policy ddos-attack-l7-alert-create`
{: #create-ddos-attack-l7-alert}

 Create an alert policy for DDoS attack l7.

```sh
ibmcloud cis alert-policy ddos-attack-l7-alert-create --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #opt-create-ddos-attack-l7-alert}

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`

`--webhooks`
:   The webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`

`--enabled`
:   Whether the alert policy is enabled.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #create-ddos-attack-l7-alert-examples}

Create a DDoS attack alert policy for instance `cis-demo`.

```sh
ibmcloud cis alert-policy ddos-attack-l7-alert-create --name test1 --emails test1@cn.ibm.com --webhooks b2633e68-9a64-4519-b361-a64a67c8db8e --enabled true  -i "cis-demo"
```
{: pre}

### `ibmcloud cis alert-policy ddos-attack-l3-l4-alert-create`
{: #create-ddos-attack-l3/l4-alert}

 Create an alert policy for DDoS attack L3/L4.

```sh
ibmcloud cis alert-policy ddos-attack-l3-l4-alert-create --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #opt-create-ddos-attack-l3-l4-alert}

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`

`--webhooks`
:   The webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`

`--enabled`
:   Whether the alert policy is enabled.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #create-ddos-attack-l3-l4-alert-examples}

Create a DDoS L3/L4 attack alert policy for instance `cis-demo`.

```sh
ibmcloud cis alert-policy ddos-attack-l3-l4-alert-create --name test1 --emails test1@cn.ibm.com --webhooks b2633e68-9a64-4519-b361-a64a67c8db8e --enabled true  -i "cis-demo"
```
{: pre}

### `ibmcloud cis alert-policy failing-logpush-job-alert-create`
{: #create-failing-logpush-job-alert-create}

 Create an alert policy when logpush job did not complete at least one successful push in the last 24 hours.

```sh
ibmcloud cis alert-policy failing-logpush-job-alert-create --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #opt-failing-logpush-job-alert-create}

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`

`--webhooks`
:   The webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`

`--enabled`
:   Whether the alert policy is enabled.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #create-failing-logpush-job-alert-examples}

Create a failing logpush job disabled alert policy for instance `cis-demo`.

```sh
ibmcloud cis alert-policy failing-logpush-job-alert-create --name test1 --emails test1@cn.ibm.com --webhooks b2633e68-9a64-4519-b361-a64a67c8db8e --enabled true  -i "cis-demo"
```
{: pre}

### `ibmcloud cis alert-policy pool-toggle-alert-create` (Pool toggle alert)
{: #create-pool-toggle-alert}

 Create an alert policy for pool toogle alert.

```sh
ibmcloud cis alert-policy pool-toggle-alert-create --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) --pools POOLS --trigger-condition (enabled | disabled | either) [--include-future-pools (true | false)] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #opt-create-pool-toggle-alert}

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`

`--webhooks`
:   The webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`

`--enabled`
:   Whether the alert policy is enabled.

`--pools`
:   The IDs of the origin pool, if set to all, the all pool IDs are used.

`--trigger-condition`
:   The condition of the pool toggle status.

`--include-future-pools`
:   Whether to include the future pools.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #create-pool-toggle-alert-examples}

Create a pool toggle alert policy for instance `cis-demo`.

```sh
ibmcloud cis alert-policy pool-toggle-alert-create --name test1 --emails test1@cn.ibm.com --enabled true --pools all --trigger-condition enabled --include-future-pools true -i "cis-demo"
```
{: pre}

### `ibmcloud cis alert-policy firewall-events-alert-create`
{: #firewall-events-alert}

Create an alert policy about spikes in firewall events. Firewall events alerts use a [z-score] (https://en.m.wikipedia.org/wiki/Standard_score) calculation over the last six hours and five-minute buckets of events. An alert is triggered whenever the z-score is above the threshold of 3.5. You will not receive duplicate alerts within the same two-hour time frame.

```sh
ibmcloud cis alert-policy firewall-events-alert-create --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) --domains DOMAINS [--services SERVICES] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #opt-firewall-events-alert}

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`

`--webhooks`
:   The webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`

`--enabled`
:   Whether the alert policy is enabled.

`--domains`
:   The domain IDs that for the alert policy. For example, `--domains domainID1,domainID2`

`--services`
:   Specify which services the alert should monitor. Valid values are `country-access-rules`, `waf`, `firewall-rules`, `ratelimit`, `securitylevel`, `ip-access-rules`, `browser-integrity-check`, `ua-rules`, `lockdowns`, `iprange-access-rules`, `asn-access-rules`, `Managed-firewall` [Enterprise Plans Only]{: tag-blue}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #firewall-events-alert-examples}

Create a firewall-events alert for instance `cis-demo`.

```sh
ibmcloud cis alert-policy firewall-events-alert-create --name test1 --emails test1@cn.ibm.com --enabled true  --domains d2633e61-1b61-2512-1321-b61a17c3db7e --service waf,ratelimit -i "cis-demo"
```
{: pre}

### `ibmcloud cis alert-policy certificate-alert-create`
{: #certificate-alert}

Create an alert policy for certificate events.

```sh
ibmcloud cis alert-policy certificate-alert-create --type (universal | dedicated | mtls ) --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #opt-certificate-alert}

`--type`
:   The type of the certificate.

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`

`--webhooks`
:   The webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`

`--enabled`
:   Whether the alert policy is enabled.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #certificate-alert-examples}

Create a certificate alert for instance `cis-demo`.

```sh
ibmcloud cis alert-policy certificate-alert-create --type universal --name test1 --emails test1@cn.ibm.com --enabled true -i "cis-demo"
```
{: pre}

### `ibmcloud cis alert-policy glb-healthcheck-alert-create`
{: #create-glb-healthcheck-alert}

 Create an alert policy for changes in health status for global load balancer, pools, and origins.

```sh
ibmcloud cis alert-policy glb-healthcheck-alert-create --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) --pools POOLS [--include-future-pools (true | false)] [--health-status-trigger (healthy | unhealthy | either)] [--event-source-trigger (pool | origin | either)] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #opt-create-glb-healthcheck-alert}

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`

`--webhooks`
:   The webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`

`--enabled`
:   Whether the alert policy is enabled.

`--pools`
:   The IDs of origin pool. If set to `all`, all pool IDs are used.

`--include-future-pools`
:   Whether to include the future pools. (The default value is `false`)

`--health-status-trigger`
:   The trigger condition to fire the notification. Valid values are `healthy`, `unhealthy`, and `either`. (The default value is `either`)

`--event-source-trigger`
:   The event source of trigger to fire the notification. Valid values are `pool`, `origin`, and `either`. (The default value is `either`)

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #create-glb-healthcheck-alert-examples}

Create a glb healthcheck alert policy for instance `cis-demo`.

```sh
ibmcloud cis alert-policy glb-healthcheck-alert-create --name test1 --emails test1@cn.ibm.com --enabled true --pools all --include-future-pools true -i "cis-demo"
```
{: pre}


### `ibmcloud cis alert-policy web-analytics-alert-create`
{: #create-web-analytics-alert}

 Create an alert policy for web metrics report.

```sh
ibmcloud cis alert-policy web-analytics-alert-create --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #opt-create-web-analytics-alert}

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`

`--webhooks`
:   The webhook ID for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`

`--enabled`
:   Whether the alert policy is enabled.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #create-web-analytics-alert-examples}

Create a web metrics report alert policy for instance `cis-demo`.

```sh
ibmcloud cis alert-policy web-analytics-alert-create --name test1 --emails test1@cn.ibm.com --webhooks b2633e68-9a64-4519-b361-a64a67c8db8e --enabled true  -i "cis-demo"
```
{: pre}

### `ibmcloud cis alert-policy maintenance-event-alert-create`
{: #create-maintenance-event-alert}

 Create an alert policy for maintenance event.

```sh
ibmcloud cis alert-policy maintenance-event-alert-create --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) --event-type TYPE [--airport-code AIRPORT_CODE] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #opt-create-maintenance-event-alert}

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`

`--webhooks`
:   The webhook ID for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`

`--enabled`
:   Whether the alert policy is enabled.

`--event-type`
:   The type of the maintenance event. Valid values are `scheduled`, `changed`, and `canceled`.

`--airport-code`
:   Comma-separated three-letter IATA Codes.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #create-maintenance-event-alert-examples}

Create a maintenance event alert policy for instance `cis-demo`.

```sh
ibmcloud cis alert-policy maintenance-event-alert-create --name test1 --emails test1@cn.ibm.com --webhooks b2633e68-9a64-4519-b361-a64a67c8db8e --event-type  scheduled,changed,canceled --airport-code IAD,AUS  --enabled true  -i "cis-demo"
```
{: pre}

### `ibmcloud cis alert-policy ddos-attack-l7-alert-update`
{: #update-ddos-attack-l7-alert}

 Update an alert policy for DDos attack l7.

```sh
ibmcloud cis alert-policy ddos-attack-l7-alert-update POLICY_ID [--name NAME] [--emails EMAILS] [--webhooks WEBHOOKS] [--enabled (true | false)] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #opt-update-ddos-attack-l7-alert}

`POLICY_ID`
:   The ID of alert policy. Required.

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`

`--webhooks`
:   The webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`

`--enabled`
:   Whether the alert policy is enabled.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-ddos-attack-l7-alert-examples}

Update a DDoS attack alert policy `a2633e68-1a64-2512-a321-b64a17c7db7a`.

```sh
ibmcloud cis alert-policy ddos-attack-l7-alert-update a2633e68-1a64-2512-a321-b64a17c7db7a --name test1 --emails test1@cn.ibm.com --webhooks b2633e68-9a64-4519-b361-a64a67c8db8e --enabled true  -i "cis-demo"
```
{: pre}

### `ibmcloud cis alert-policy ddos-attack-l3-l4-alert-update`
{: #update-ddos-attack-l3-l4-alert}

 Update an alert policy for DDoS attack L3/L4.

```sh
ibmcloud cis alert-policy ddos-attack-l3-l4-alert-update POLICY_ID [--name NAME] [--emails EMAILS] [--webhooks WEBHOOKS] [--enabled (true | false)] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #opt-update-ddos-attack-l3-l4-alert}

`POLICY_ID`
:   The ID of alert policy. Required.

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`

`--webhooks`
:   The webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`

`--enabled`
:   Whether the alert policy is enabled.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-ddos-attack-l3-l4-alert-examples}

Update a DDoS attack alert policy `a2633e68-1a64-2512-a321-b64a17c7db7a`.

```sh
ibmcloud cis alert-policy ddos-attack-l3-l4-alert-update a2633e68-1a64-2512-a321-b64a17c7db7a --name test1 --emails test1@cn.ibm.com --webhooks b2633e68-9a64-4519-b361-a64a67c8db8e --enabled true  -i "cis-demo"
```
{: pre}


### `ibmcloud cis alert-policy failing-logpush-job-alert-update`
{: #update-failing-logpush-job-alert}

Update an alert policy when logpush job did not complete at least one successful push in the last 24 hours.

```sh
ibmcloud cis alert-policy failing-logpush-job-alert-update POLICY_ID [--name NAME] [--emails EMAILS] [--webhooks WEBHOOKS] [--enabled (true | false)] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #opt-update-failing-logpush-job-alert}

`POLICY_ID`
:   The ID of alert policy. Required.

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`

`--webhooks`
:   The webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`

`--enabled`
:   Whether the alert policy is enabled.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-failing-logpush-job-alert-examples}

Update a failing logpush job alert policy `a2633e68-1a64-2512-a321-b64a17c7db7a`.

```sh
ibmcloud cis alert-policy failing-logpush-job-alert-update a2633e68-1a64-2512-a321-b64a17c7db7a --name test1 --emails test1@cn.ibm.com --webhooks b2633e68-9a64-4519-b361-a64a67c8db8e --enabled true  -i "cis-demo"
```
{: pre}


### `ibmcloud cis alert-policy pool-toggle-alert-update`
{: #update-pool-toggle-alert}

 Update an alert policy for pool toogle alert.

```sh
ibmcloud cis alert-policy pool-toggle-alert-update POLICY_ID --name NAME (--emails EMAILS | --webhooks WEBHOOKS) --enabled (true | false) --pools POOLS --trigger-condition (enabled | disabled | either) [--include-future-pools (true | false)] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #opt-update-pool-toggle-alert}

`POLICY_ID`
:   The ID of alert policy. Required.

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`

`--webhooks`
:   The webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`

`--enabled`
:   Whether the alert policy is enabled.

`--pools`
:   The IDs of the origin pool. If set to `all`, all pool IDs are used.

`--trigger-condition`
:   The condition of the pool toggle status.

`--include-future-pools`
:   Whether to include the future pools.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-pool-toggle-alert-examples}

Update a pool toggle alert policy for instance `cis-demo`.

```sh
ibmcloud cis alert-policy pool-toggle-alert-update a2633e68-1a64-2512-a321-b64a17c7db7a --name test1 --emails test1@cn.ibm.com --enabled true --pools all --trigger-condition enabled --include-future-pools true -i "cis-demo"
```
{: pre}

### `ibmcloud cis alert-policy firewall-events-alert-update`
{: #update-firewall-events-alert}

 Update an alert policy about spikes in firewall events.

```sh
ibmcloud cis alert-policy firewall-events-alert-update POLICY_ID [--name NAME] [--emails EMAILS] [--webhooks WEBHOOKS] [--enabled (true | false)] [--domains DOMAINS] [--services SERVICES] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #opt-update-firewall-events-alert}

`POLICY_ID`
:   The ID of alert policy. Required.

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`

`--webhooks`
:   The webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`

`--enabled`
:   Whether the alert policy is enabled.

`--domains`
:   The domain IDs that for the alert policy. For example, `--domains domainID1,domainID2`

`--services`
:   Specify which services the alert must monitor. Valid values are `country-access-rules`, `waf`, `firewall-rules`, `ratelimit`, `securitylevel`, `ip-access-rules`, `browser-integrity-check`, `ua-rules`, `lockdowns`, `iprange-access-rules`, `asn-access-rules`, `Managed-firewall` [Enterprise Plans Only]{: tag-blue}

   The 'SERVICES' is only used for advanced waf alert. If the alert policy you wanted to update is created without services that are specified, create a new one with sevices specified instead of updating.
   {: note}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-firewall-events-alert-examples}

Update a firewall-events-alert policy `a2633e68-1a64-2512-a321-b64a17c7db7a`.

```sh
ibmcloud cis alert-policy firewall-events-alert-update a2633e68-1a64-2512-a321-b64a17c7db7a --name test1 --emails test1@cn.ibm.com --webhooks b2633e68-9a64-4519-b361-a64a67c8db8e --enabled true --domains d2633e61-1b61-2512-1321-b61a17c3db7e  -i "cis-demo"
```
{: pre}

### `ibmcloud cis alert-policy certificate-alert-update`
{: #update-certificate-alert}

 Update an alert policy for certificate events.

```sh
ibmcloud cis alert-policy certificate-alert-update POLICY_ID [--name NAME] [--emails EMAILS] [--webhooks WEBHOOKS] [--enabled (true | false)] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #opt-update-certificate-alert}

`POLICY_ID`
:   The ID of alert policy. Required.

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`

`--webhooks`
:   The webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`

`--enabled`
:   Whether the alert policy is enabled.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-certificate-alert-examples}

Update a certificate alert policy `a2633e68-1a64-2512-a321-b64a17c7db7a`.

```sh
ibmcloud cis alert-policy certificate-alert-update a2633e68-1a64-2512-a321-b64a17c7db7a --name test1 --emails test1@cn.ibm.com --webhooks b2633e68-9a64-4519-b361-a64a67c8db8e --enabled true  -i "cis-demo"
```
{: pre}

### `ibmcloud cis alert-policy glb-healthcheck-alert-update`
{: #update-glb-healthcheck-alert}

 Update an alert policy for changes in health status for global load balancer, pools, and origins.

```sh
ibmcloud cis alert-policy glb-healthcheck-alert-update POLICY_ID [--name NAME] [--emails EMAILS] [--webhooks WEBHOOKS] [--enabled (true | false)] [--pools POOLS] [--include-future-pools (true | false)] [--health-status-trigger (healthy | unhealthy | either)] [--event-source-trigger (pool | origin | either)] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #opt-update-glb-healthcheck-alert}

`POLICY_ID`
:   The ID of alert policy. Required.

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`

`--webhooks`
:   The webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`

`--enabled`
:   Whether the alert policy is enabled.

`--pools`
:   The IDs of origin pool. If set to `all`, all pool IDs are used.

`--include-future-pools`
:   Whether to include the future pools. (The default value is `false`)

`--health-status-trigger`
:   The trigger condition to send the notification. Valid values are `healthy`, `unhealthy`, and `either`. (The default value is `either`)

`--event-source-trigger`
:   The event source of trigger to send the notification. Valid values are `pool`, `origin`, and `either`. (The default value is `either`)

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-glb-healthcheck-alert-examples}

Update a certificate alert policy `a2633e68-1a64-2512-a321-b64a17c7db7a`.

```sh
ibmcloud cis alert-policy glb-healthcheck-alert-update  a2633e68-1a64-2512-a321-b64a17c7db7a --name test1 --emails test1@cn.ibm.com --enabled true --pools all --include-future-pools true -i "cis-demo"
```
{: pre}

### `ibmcloud cis alert-policy web-analytics-alert-update`
{: #update-web-analytics-alert}

 Update an alert policy for web metric report.

```sh
ibmcloud cis alert-policy web-analytics-alert-update POLICY_ID [--name NAME] [--emails EMAILS] [--webhooks WEBHOOKS] [--enabled (true | false)] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #opt-update-web-analytics-alert}

`POLICY_ID`
:   The ID of alert policy. Required.

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`

`--webhooks`
:   The webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`

`--enabled`
:   Whether the alert policy is enabled.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-web-analytics-alert-examples}

Update a web metric report alert policy `a2633e68-1a64-2512-a321-b64a17c7db7a`.

```sh
ibmcloud cis alert-policy web-analytics-alert-update a2633e68-1a64-2512-a321-b64a17c7db7a --name test1 --emails test1@cn.ibm.com --webhooks b2633e68-9a64-4519-b361-a64a67c8db8e --enabled true  -i "cis-demo"
```
{: pre}

### `ibmcloud cis alert-policy maintenance-event-alert-update`
{: #update-maintenance-event-alert}

 Update an alert policy for maintenance event.

```sh
ibmcloud cis alert-policy maintenance-event-alert-update POLICY_ID [--name NAME] [--emails EMAILS] [--webhooks WEBHOOKS] [--enabled (true | false)] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #opt-update-maintenance-event-alert}

`POLICY_ID`
:   The ID of alert policy. Required.

`--name`
:   The name of the alert policy.

`--description`
:   The description for the alert policy.

`--emails`
:   The email addresses for dispatching an alert notification. For example, `--emails test1@cn.ibm.com,test2@cn.ibm.com`

`--webhooks`
:   The webhook ID that for dispatching an alert notification. For example, `--webhook webhookID1,webhookID2`

`--enabled`
:   Whether the alert policy is enabled.

`--event-type`
:   The type of the maintenance event. Valid values are `scheduled`, `changed`, and `canceled`.

`--airport-code`
:   Comma-separated three-letter IATA Codes.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-maintenance-event-alert-examples}

Update a maintenance event alert policy `a2633e68-1a64-2512-a321-b64a17c7db7a`.

```sh
ibmcloud cis alert-policy maintenance-event-alert-update a2633e68-1a64-2512-a321-b64a17c7db7a --name test1 --emails test1@cn.ibm.com --webhooks b2633e68-9a64-4519-b361-a64a67c8db8e --enabled true --event-type  scheduled,changed,canceled --airport-code IAD,AUS -i "cis-demo"
```
{: pre}

### `ibmcloud cis alert-policy delete`
{: #delete-alert-policy}

Delete an alert policy.

```sh
cis alert-policy delete POLICY_ID [-i, --instance INSTANCE] [-f, --force]
```

#### Command options
{: #delete-alert-policy-options}

`POLICY_ID`
:   The ID of alert policy. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`-f, --force`
:   Attempt to delete the policy without prompting for confirmation.

#### Examples
{: #delete-alert-policy-examples}

Delete an alert policy `a2633e68-1a64-2512-a321-b64a17c7db7a`.

```sh
ibmcloud cis alert-policy delete  a2633e68-1a64-2512-a321-b64a17c7db7a -f -i "cis-demo"
```
{: pre}

### `ibmcloud cis alert-policy test`
{: #test-alert-policy}

Send a test alert for an alert policy.

```sh
cis alert-policy test POLICY_ID [-i, --instance INSTANCE] [-f, --force]
```

#### Command options
{: #test-alert-policy-options}

`POLICY_ID`
:   The ID of alert policy. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`-f, --force`
:   Attempt to send a test alert without prompting for confirmation.

#### Examples
{: #test-alert-policy-examples}

Send a test notification for an alert policy `a2633e68-1a64-2512-a321-b64a17c7db7a`.

```sh
ibmcloud cis alert-policy test a2633e68-1a64-2512-a321-b64a17c7db7a -f -i "cis-demo"
```
{: pre}

## Alert Webhook
{: #alert-webhook}

### `ibmcloud cis alert-webhooks`
{: #list-alert-webhooks}

List all alert webhooks.

```sh
ibmcloud cis alert-webhooks [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #opt-list-alert-webhooks}

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-alert-webhooks-examples}

List all webhooks for instance `cis-demo`

```sh
ibmcloud cis alert-webhooks -i "cis-demo"
```
{: pre}

### `ibmcloud cis alert-webhook`
{: #show-alert-webhook}

Show the details of a webhook.

```sh
ibmcloud cis alert-webhook WEBHOOK_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-alert-webhook-options}

`WEBHOOK_ID`
:   The ID of the alert webhook. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-alert-webhook-examples}

Show the details of the alert webhook `b2633e68-9a64-4519-b361-a64a67c8db8e`.

```sh
ibmcloud cis alert-webhook b2633e68-9a64-4519-b361-a64a67c8db8e -i "cis-demo"
```
{: pre}

### `ibmcloud cis alert-webhook-create`
{: #create-alert-webhook}

Create an alert webhook for an instance.

```sh
ibmcloud cis alert-webhook-create --name NAME --url URL [--secret SECRET] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #create-alert-webhook-options}

`--name`
:   The name of the webhook. Required.

`--url`
:   The POST endpoint to call when dispatching an alert. Required.

`--secret`
:   The secret that is passed in the webhook auth header when dispatching a webhook alert.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #create-alert-webhook-examples}

Create an alert webhook for instance `cis-demo`.

```sh
ibmcloud cis alert-webhook-create --name testwebhook --url https://hooks.slack.com/services/Ds3fdBFbV/1234568 --secret 007  -i "cis-demo"
```
{: pre}

### `ibmcloud cis alert-webhook-update`
{: #update-alert-webhook}

Update an alert webhook.

```sh
cis alert-webhook-update WEBHOOK_ID [--name NAME] [--url URL] [--secret SECRET] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-alert-webhook-options}

`WEBHOOK_ID`
:   The ID of the alert webhook. Required.

`--name`
:   The name of the webhook.

`--url`
:   The POST endpoint to call when dispatching an alert.

`--secret`
:   The secret that is passed in the webhook auth header when dispatching a webhook alert.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-alert-webhook-examples}

Update an alert webhook `b2633e68-9a64-4519-b361-a64a67c8db8e`.

```sh
ibmcloud cis alert-webhook-update b2633e68-9a64-4519-b361-a64a67c8db8e --name testwebhook --url https://hooks.slack.com/services/Ds3fdBFbV/1234568 -i "cis-demo"
```
{: pre}

### `ibmcloud cis alert-webhook-delete`
{: #delete-alert-webhook}

Delete an alert webhook.

```sh
ibmcloud cis alert-webhook-delete WEBHOOK_ID [-i, --instance INSTANCE] [-f, --force]
```

#### Command options
{: #delete-alert-webhook-options}

`WEBHOOK_ID`
:   The ID of the alert webhook. Required.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`-f, --force`
:   Attempt to delete the webhook without prompting for confirmation.

#### Examples
{: #delete-alert-webhook-examples}

Delete an alert webhook `b2633e68-9a64-4519-b361-a64a67c8db8e`.

```sh
ibmcloud cis alert-webhook-delete  b2633e68-9a64-4519-b361-a64a67c8db8e -f -i "cis-demo"
```
{: pre}

## Advanced Rate Limiting Rules
{: #advanced-ratelimiting-rules}

Manage the advanced rate limiting rules by using the following `advanced-rate-limiting` commands.

### `ibmcloud cis advanced-rate-limiting rules`
{: #list-rules}

List all advanced rate limiting rules.

```sh
ibmcloud cis advanced-rate-limiting rules DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #list-rules-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-rules-examples}

List all advanced rate limiting rules for domain `31984fea73a15b45779fa0df4ef62f9b` under instance `cis-demo`.

```sh
ibmcloud cis advanced-rate-limiting rules 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis advanced-rate-limiting rule`
{: #show-rule}

Get details of an advanced rate limiting rule.

```sh
ibmcloud cis advanced-rate-limiting rule DNS_DOMAIN_ID RULE_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-rule-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain.

`RULE_ID`
:   RULE_ID is the id of the advanced rate limiting rule.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-rule-examples}

Show a rule `c2e184081120413c86c3ab7e14069605` for domain `31984fea73a15b45779fa0df4ef62f9b` under instance `cis-demo`.

```sh
ibmcloud cis advanced-rate-limiting rule 31984fea73a15b45779fa0df4ef62f9b  c2e184081120413c86c3ab7e14069605 -i "cis-demo"
```
{: pre}

### `ibmcloud cis advanced-rate-limiting rule-create`
{: #create-rule}

Create an advanced rate limiting rule.

```sh
ibmcloud cis advanced-rate-limiting rule-create DNS_DOMAIN_ID --name NAME --match EXPRESSION --action ACTION --same-characteristics CHARACTERSTICS --requests REQUEST_PER_PERIOD --period PERIOD [--timeout TIMEOUT] [--enabled true|false] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #create-rule-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain.

`--name`
:  The rule name.

`--match`
:  Specifies the conditions that must be matched for the rule to run. For match value, see [Using fields, functions, and expressions](/docs/cis?topic=cis-fields-and-expressions).

`--action`
:  Action to perform when the rate that is specified in the rule is reached. Valid values are `block`, `challenge`, `js_challenge`, `managed_challenge`, and `log`.

`--same-characteristics`
:  A set of parameters defining how CIS tracks the request rate for the rule. Use one or more of the characteristics: `ip`, `ip_nat`, `host`, `path`, `country`, `asnum`. For complex characteristics, use JSON file or JSON string instead.

`--requests`
:  The number of requests over the period of time that triggers the rule. Valid values range from `1-1000000`

`--period`
:  The period of time to consider (in seconds) when evaluating the request rate. Valid values are `10`, `60`, `120`, `300`, `600`, and `3600`.

`--timeout`
: The rate limiting rule applies the rule action to further requests for the period of time. Valid values are `0`, `10`, `60`, `120`, `300`, `600`, `3600`, and `86400`.

`--enabled`
: Indicates whether the rule is active or not. Valid values for "enabled" are `true` and `false`. (The default value is `false`)

`--json`
:  The JSON file or JSON string that is used to describe an advanced rate limiting rule.

   - The required fields in JSON data are `expression`, `ratelimit` and `action`.

      - `expression` : Defines the criteria for the advanced rate limiting rule to match a request.
      - `ratelimit` : Define the rate-limit parameters.
        - `characteristics` : A set of parameters defining how CIS tracks the request rate for the rule.
        - `requests_per_period` : The number of requests over the period of time that triggers the rule.
        - `period` : The period of time to consider (in seconds) when evaluating the request rate. Valid values are `10`, `60`, `120`, `300`, `600`, and `3600`.
        - `requests_to_origin` : Apply the rate limiting to cached assets or not.
        - `mitigation_timeout` : The rate limiting rule applies the rule action to further requests for the period of time. Valid values are `0`, `10`, `60`, `120`, `300`, `600`, `3600`, and `86400`.
        - `counting_expression` : Defines the criteria that are used for determining the request rate.
      - `action` : Action to perform when the rate that is specified in the rule is reached. Valid values are `block`, `challenge`, `js_challenge`, `managed_challenge`, and `log`.

   - The optional fields are `description`, `action_parameters`, and `enabled`.

      - `description` : The descriptive name of your rule.
      - `action_parameters` : Define the action parameters.
         - `response` : Define a custom response for block action.
         - `status_code` : Defines the HTTP status code that is returned to the visitor when blocking the request due to rate limiting. Only available when the rule action is Block. Valid values range from `400-499`. The default value is `429`.
         - `content_type` : Defines the content type of a custom response when blocking a request due to rate limiting. Only available when the rule action is Block.
         - `content` : Defines the body of the returned HTTP response when the request is blocked due to rate limiting. Only available when the rule action is Block.
      - `enabled` : Whether enable this rule or not.

      ```json
         Sample JSON data:

            {

               "description": "description",
               "expression": "(http.request.method eq \"POST\")",
               "ratelimit": {
                  "characteristics": [
                     "cf.unique_visitor_id",
                     "cf.colo.id"
                  ],
                  "requests_to_origin": false,
                  "counting_expression": "(ip.geoip.continent in {\"AN\"})",
                  "requests_per_period": 10,
                  "period": 10,
                  "mitigation_timeout": 120
               },
               "action": "block",
               "action_parameters": {
                  "response": {
                     "status_code": 429,
                     "content_type": "text/xml",
                     "content": "reject"
                  }
               },
               "enabled": false
            }
      ```

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #create-rule-examples}

Create an advanced rate limiting rule for domain `31984fea73a15b45779fa0df4ef62f9b` under instance `cis-demo`.

```sh
ibmcloud cis advanced-rate-limiting rule-create 31984fea73a15b45779fa0df4ef62f9b --name rule-name --match "(http.request.method eq \"POST\")" --action log --same-characteristics ip,ip_nat --requests 100 --period 10 -i "cis-demo"
```
{: pre}


### `ibmcloud cis advanced-rate-limiting rule-update`
{: #update-rule}

Update an advanced rate limiting rule.

```sh
ibmcloud cis advanced-rate-limiting rule-update DNS_DOMAIN_ID RULE_ID --name NAME --match EXPRESSION --action ACTION --same-characteristics CHARACTERSTICS --requests REQUEST_PER_PERIOD --period PERIOD [--timeout TIMEOUT] [--enabled true|false] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #update-rule-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain.

`RULE_ID`
:   RULE_ID is the id of the advanced rate limiting rule.

`--name`
:  The rule name.

`--match`
:  Specifies the conditions that must be matched for the rule to run. For match value, see [Using fields, functions, and expressions](/docs/cis?topic=cis-fields-and-expressions).

`--action`
:  Action to perform when the rate that is specified in the rule is reached. Valid values are `block`, `challenge`, `js_challenge`, `managed_challenge`, and `log`.

`--same-characteristics`
:  A set of parameters defining how CIS tracks the request rate for the rule. Use one or more of the characteristics: `ip`, `ip_nat`, `host`, `path`, `country`, `asnum`. For complex characteristics, use JSON file or JSON string instead.

`--requests`
:  The number of requests over the period of time that triggers the rule. Valid values range from `1-1000000`

`--period`
:  The period of time to consider (in seconds) when evaluating the request rate. Valid values are `10`, `60`, `120`, `300`, `600`, and `3600`.

`--timeout`
: The rate limiting rule applies the rule action to further requests for the period of time. Valid values are `0`, `10`, `60`, `120`, `300`, `600`, `3600` and `86400`.

`--enabled`
: Indicates whether the rule is active or not. Valid values for "enabled" are `true` and `false`. (The default value is `false`)

`--json`
:  The JSON file or JSON string that is used to describe an advanced rate limiting rule.

   - The required fields in JSON data are `expression`, `ratelimit` and `action`.

      - `expression` : Defines the criteria for the advanced rate limiting rule to match a request.
      - `ratelimit` : Define the ratelimit parameters.
        - `characteristics` : A set of parameters defining how CIS tracks the request rate for the rule.
        - `requests_per_period` : The number of requests over the period of time that triggers the rule.
        - `period` : The period of time to consider (in seconds) when evaluating the request rate. Valid values are `10`, `60`, `120`, `300`, `600`, and `3600`.
        - `requests_to_origin` : Apply the rate limiting to cached assets or not.
        - `mitigation_timeout` : The rate limiting rule applies the rule action to further requests for the period of time. Valid values are `0`, `10`, `60`, `120`, `300`, `600`, `3600`, and `86400`.
        - `counting_expression` : Defines the criteria that are used for determining the request rate.
      - `action` : Action to perform when the rate that is specified in the rule is reached. Valid values are `block`, `challenge`, `js_challenge`, `managed_challenge`, and `log`.

   - The optional fields are `description`, `action_parameters`, and `enabled`.

      - `description` : The descriptive name of your rule.
      - `action_parameters` : Define the action parameters.
         - `response` : Define a custom response for block action.
         - `status_code` : Defines the HTTP status code that is returned to the visitor when blocking the request due to rate limiting. Only available when the rule action is Block. Valid values range from `400-499`. The default value is `429`.
         - `content_type` : Defines the content type of a custom response when blocking a request due to rate limiting. Only available when the rule action is Block.
         - `content` : Defines the body of the returned HTTP response when the request is blocked due to rate limiting. Only available when the rule action is Block.
      - `enabled` : Whether enable this rule or not.

      ```json
         Sample JSON data:

            {

               "description": "description",
               "expression": "(http.request.method eq \"POST\")",
               "ratelimit": {
                  "characteristics": [
                     "cf.unique_visitor_id",
                     "cf.colo.id"
                  ],
                  "requests_to_origin": false,
                  "counting_expression": "(ip.geoip.continent in {\"AN\"})",
                  "requests_per_period": 10,
                  "period": 10,
                  "mitigation_timeout": 120
               },
               "action": "block",
               "action_parameters": {
                  "response": {
                     "status_code": 429,
                     "content_type": "text/xml",
                     "content": "reject"
                  }
               },
               "enabled": false
            }
      ```

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #update-rule-examples}

Update an advanced rate limiting rule `c2e184081120413c86c3ab7e14069605` for domain `31984fea73a15b45779fa0df4ef62f9b` under instance `cis-demo`.

```sh
ibmcloud cis advanced-rate-limiting rule-update 31984fea73a15b45779fa0df4ef62f9b c2e184081120413c86c3ab7e14069605 --name rule-name --match "(http.request.method eq \"POST\")" --action log --same-characteristics ip,ip_nat --requests 100 --period 10 -i "cis-demo"
```
{: pre}

### `ibmcloud cis advanced-rate-limiting rule-delete`
{: #show-rule-delete}

Delete an advanced rate limiting rule by id.

```sh
ibmcloud cis advanced-rate-limiting rule-delete DNS_DOMAIN_ID RULE_ID [-f, --force] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #delete-rule-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain.

`RULE_ID`
:   RULE_ID is the id of the advanced rate limiting rule.

`-f, --force`
:   Attempt to delete an advanced rate limiting rule without prompting for confirmation.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #delete-rule-examples}

Delete a rule `c2e184081120413c86c3ab7e14069605` for domain `31984fea73a15b45779fa0df4ef62f9b` under instance `cis-demo`.

```sh
ibmcloud cis advanced-rate-limiting rule-delete 31984fea73a15b45779fa0df4ef62f9b  c2e184081120413c86c3ab7e14069605 -i "cis-demo"
```
{: pre}

## WAF managed rules
{: #waf-managed-rules}

Manage the WAF-managed rulesets and rules by using the following `managed-waf` commands. Migrate to a new WAF by API or GUI first before you use managed WAF commands. Keep in mind that the previous version of WAF commands stops working after you migrate.

### `ibmcloud cis managed-waf rulesets`
{: #list-rulesets}

List all managed WAF rulesets.

```sh
ibmcloud cis managed-waf rulesets DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #list-rulesets-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-rulesets-examples}

List all managed WAF rulesets for domain `31984fea73a15b45779fa0df4ef62f9b` under instance `cis-demo`.

```sh
ibmcloud cis managed-waf rulesets 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis managed-waf ruleset`
{: #show-ruleset}

Get details of a managed WAF ruleset.

```sh
ibmcloud cis managed-waf ruleset DNS_DOMAIN_ID RULESET_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-ruleset-options}

`DNS_DOMAIN_ID`
:   The ID of DNS domain.

`RULESET_ID`
:   The ID of the ruleset.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-ruleset-examples}

Show a ruleset `c2e184081120413c86c3ab7e14069605` for domain `31984fea73a15b45779fa0df4ef62f9b` under instance `cis-demo`.

```sh
ibmcloud cis managed-waf ruleset 31984fea73a15b45779fa0df4ef62f9b  c2e184081120413c86c3ab7e14069605 -i "cis-demo"
```
{: pre}

### `ibmcloud cis managed-waf deployment`
{: #show-deployment}

Get details of a deployed managed WAF rule.

```sh
ibmcloud cis managed-waf deployment DNS_DOMAIN_ID RULE_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-deployment-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain.

`RULE_ID`
:   The ID of the rule.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-deployment-examples}

Show a deployment rule `a2121e23-9e68-1218-a356-b78e23a8ec8a` for domain `31984fea73a15b45779fa0df4ef62f9b` under instance `cis-demo`.

```sh
ibmcloud cis managed-waf deployment 31984fea73a15b45779fa0df4ef62f9b  a2121e23-9e68-1218-a356-b78e23a8ec8a -i "cis-demo"
```
{: pre}

### `ibmcloud cis managed-waf deployments`
{: #list-deployments}

List all deployed managed WAF rules.

```sh
ibmcloud cis managed-waf deployments DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #list-deployments-options}

`DNS_DOMAIN_ID`
:   The ID of DNS domain.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-deployments-examples}

List all deployment rules for domain `31984fea73a15b45779fa0df4ef62f9b` under instance `cis-demo`.

```sh
ibmcloud cis managed-waf deployments 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis managed-waf deployment-add-exception`
{: #deployment-add-exception}

Create an exception rule to skip execution of specified managed WAF rules.

```sh
ibmcloud cis managed-waf deployment-add-exception DNS_DOMAIN_ID --match EXPRESSION [--skip-rules RULES] [--enabled true|false] [--logging true|false] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
ibmcloud cis managed-waf deployment-add-exception DNS_DOMAIN_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #deployment-add-exception-options}

`DNS_DOMAIN_ID`
:   The ID of DNS domain.

`--match`
:   Specifies the conditions that must be matched for the rule to run. For match value, see [Using fields, functions, and expressions](/docs/cis?topic=cis-fields-and-expressions).

`--skip-rules`
:  Skip all remaining rules, WAF managed rulesets, or rules of WAF managed rulesets. For example, `--skip-rules RULESETID-1:RULEID-a,RULEID-b;RULESETID-2:RULEID-x,RULEID-y.`. Set `current` to skip all remaining rules. The default value is `current`.

`--enabled`
:  Indicates whether the rule is active or not. The default value is `true`.

`--logging`
:  Log requests matching the skip rule. The default value is `true`.

`--description`
:  A brief description of the rule.

`--json`
:  The JSON file or JSON string that is used to describe a managed WAF.

   - The required fields in JSON data are `expression`, `action` and `action_parameters`.

      `expression` : The rule expression.
      `action` : The rule action to perform. Valid value is `skip`.
      `action_parameters` : The rule action parameters.
        `ruleset` : Skip all remaining rules or one or more WAF-managed rulesets.
        `rules` : Skip one or more rules of WAF-managed rulesets.

   - The optional fields are `description`, `enabled`, and `logging`.
      `description` : Briefly describes the rule.
      `enabled` : Indicates whether the rule is active or not.
      `logging` : Log requests matching the skip rule.
         - `enabled` : When disabled, matched requests don't appear in firewall events.

   Sample JSON data:
      ```json
         {
            "action": "skip",
            "expression": "(http.cookie eq \"example.com/contact?page=1234\")",
            "description": "rule name",
            "enabled": true,
            "logging": {
                   "enabled": true
            },
            "action_parameters": {
               "rules": {
                  "efb7b8c949ac4650a09736fc376e9aee": [
                     "5de7edfa648c4d6891dc3e7f84534ffa",
                     "e3a567afc347477d9702d9047e97d760"
                  ],
                  "c2e184081120413c86c3ab7e14069605": [
                     "ef21b0a932ae422790f9249d213b85e6"
                  ]
               }
            }
         }
      ```

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #deployment-add-exception-examples}

Create exception rule for domain `31984fea73a15b45779fa0df4ef62f9b` under instance `cis-demo`.

```sh
ibmcloud cis managed-waf deployment-add-exception 31984fea73a15b45779fa0df4ef62f9b --match "(http.cookie eq \"example.com/contact?page=1234\")" --skip-rules 'efb7b8c949ac4650a09736fc376e9aee:5de7edfa648c4d6891dc3e7f84534ffa' --enabled false --logging true -i "cis-demo"
```
{: pre}

### `ibmcloud cis managed-waf deployment-update-exception`
{: #deployment-update-exception}

Update an exception rule in the deployed managed WAF rules.

```sh
ibmcloud cis managed-waf deployment-update-exception DNS_DOMAIN_ID RULE_ID [--match MATCH] [--skip-rules RULES] [--enabled true|false] [--logging true|false] [--description DESCRIPTION] [-i, --instance INSTANCE] [--output FORMAT]
ibmcloud cis managed-waf deployment-update-exception DNS_DOMAIN_ID RULE_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #deployment-update-exception-options}

`DNS_DOMAIN_ID`
:   The ID of DNS domain.

`RULE_ID`
:   The ID of rule.

`--match`
:   Specifies the conditions that must be matched for the rule to run. For match value, see [Using fields, functions, and expressions](/docs/cis?topic=cis-fields-and-expressions).

`--skip-rules`
:  Skip all remaining rules, WAF managed rulesets, or rules of WAF managed rulesets. For example, `--skip-rules RULESETID-1:RULEID-a,RULEID-b;RULESETID-2:RULEID-x,RULEID-y.`. Set `current` to skip all remaining rules. The default value is `current`.

`--enabled`
:  Indicates whether the rule is active or not. The default value is `true`.

`--logging`
:  Log requests matching the skip rule. The default value is `true`.

`--description`
:  To briefly describe the rule.

`--json`
:  The JSON file or JSON string that is used to describe a managed WAF.

   - The required fields in JSON data are `expression`, `action`, and `action_parameters`.

      `expression` : The rule expression.
      `action` : The rule action to perform. Valid value is `skip`.
      `action_parameters` : The rule action parameters.
        `ruleset` : Skip all remaining rules or one or more WAF-managed rulesets.
        `rules` : Skip one or more rules of WAF-managed rulesets.

   - The optional fields are `description`, `enabled`, and `logging`.
      `description` : Briefly describes the rule.
      `enabled` : Indicates whether the rule is active or not.
      `logging` : Log requests matching the skip rule.
         - `enabled` : When disabled, matched requests don't appear in firewall events.

Sample JSON data:
   ```json
         {
            "action": "skip",
            "expression": "(http.cookie eq \"example.com/contact?page=1234\")",
            "description": "rule name",
            "enabled": true,
            "logging": {
                   "enabled": true
            },
            "action_parameters": {
               "rules": {
                  "efb7b8c949ac4650a09736fc376e9aee": [
                     "5de7edfa648c4d6891dc3e7f84534ffa",
                     "e3a567afc347477d9702d9047e97d760"
                  ],
                  "c2e184081120413c86c3ab7e14069605": [
                     "ef21b0a932ae422790f9249d213b85e6"
                  ]
               }
            }
         }
   ```

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #deployment-update-exception-examples}

Update an exception rule `e7ead74deb2b4c30a91c793f502f5e14` for domain `31984fea73a15b45779fa0df4ef62f9b` under instance `cis-demo`.

```sh
ibmcloud cis managed-waf deployment-add-exception 31984fea73a15b45779fa0df4ef62f9b e7ead74deb2b4c30a91c793f502f5e14 --match "(http.cookie eq \"example.com/contact?page=1234\")" --skip-rules 'efb7b8c949ac4650a09736fc376e9aee:5de7edfa648c4d6891dc3e7f84534ffa' --enabled false --logging true -i "cis-demo"
```
{: pre}

### `ibmcloud cis managed-waf deployment-add-ruleset`
{: #deployment-add-ruleset}

Add a managed ruleset to the deployed managed WAF rules.

```sh
ibmcloud cis managed-waf deployment-add-ruleset DNS_DOMAIN_ID RULESET_ID [--match EXPRESSION] [--enabled true|false] [--override-action ACTION] [--override-status STATUS] [--paranoia-level LEVEL] [--override-rules RULE] [-i, --instance INSTANCE] [--output FORMAT]
ibmcloud cis managed-waf deployment-add-ruleset DNS_DOMAIN_ID RULESET_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #deployment-add-ruleset-options}

`DNS_DOMAIN_ID`
:   The ID of DNS domain.

`RULESET_ID`
:   The ID of managed ruleset.

`--match`
:   Specifies the conditions that must be matched for the rule to run. For match value, see [Using fields, functions, and expressions](/docs/cis?topic=cis-fields-and-expressions).

`--enabled`
:  Indicates whether the rule is active or not. The default value is `true`.

`--override-action`
:  The ruleset action of the overrides. Valid values are `managed_challenge`, `block`, `js_challenge`, `log`, and `challenge`.

`--override-status`
:  The ruleset status of the overrides. Valid values are `true` and `false`.

`--paranoia-level`
:  OWASP paranoia level, higher paranoia levels activate more aggressive rules. Valid values are `PL1`, `PL2`, `PL3`, `PL4` and it's only available for `CIS OWASP Core Ruleset`.

`--override-rules`
:  The rules options of the overrides. For example `--override-rules rule=RULE_ID,action=ACTION,enabled=STATUS`. For OWASP Core Ruleset, you can also override the Score Threshold. For example, `--override-rules rule=6179ae15870a4bb7b2d480d4843b323c,score-threshold=25`.

`--json`
:  The JSON file or JSON string that is used to describe a managed WAF rule.

   - The required fields in JSON data are `expression`, `action`, and `action_parameters`.

      `expression` : The rule expression.
      `action` : The rule action to perform. Valid value is `skip`.
      `action_parameters` : The rule action parameters.
         `id` : The ruleset ID of the overrides.
         `overrides` : The rules options of the overrides.
            `action` : The ruleset action of the overrides. Valid values are `managed_challenge`, `block`, and `js_challenge`, "log", "challenge".
            `enabled` : The ruleset status of the overrides. Valid values are `true` and `false`.
            `rules`: The rules options of the overrides.
               `id`: The rule ID of the overrides.
               `action`: The rule action of the overrides. Valid values are `managed_challenge`, `block`, `js_challenge`, `log`, and `challenge`.
               `enabled`: The rule status of the overrides.
               `score_threshold`: OWASP Anomaly Score Threshold. Set the score threshold, which triggers the Firewall.
            `categories`: Define OWASP Paranoia Level and only valid for `CIS OWASP core ruleset`
               `category`: OWASP paranoia level, higher paranoia levels activate more aggressive rules.
               `enabled`: Whether this OWASP Paranoia Level is enabled.

   - The optional fields are `description` and `enabled`.
      `description` : Briefly describes the rule.
      `enabled` : Indicates whether the rule is active or not.

Sample JSON data:
   ```json
         {
            "action": "execute",
            "description": "CIS Managed Ruleset",
            "enabled": true,
            "expression": "(http.cookie eq \"example.com/contact?page=1234\")",
            "action_parameters": {
               "id": "efb7b8c949ac4650a09736fc376e9aee",
               "overrides": {
                  "action": "block",
                  "enabled": false,
                  "rules": [
                     {
                        "id": "5de7edfa648c4d6891dc3e7f84534ffa",
                        "action": "managed_challenge"
                     },
                     {
                        "id": "e3a567afc347477d9702d9047e97d760",
                        "action": "log",
                        "enabled": true
                     }
                  ]
               }
         }
   ```

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #deployment-add-ruleset-examples}

Deploy a managed ruleset for domain `31984fea73a15b45779fa0df4ef62f9b` under instance `cis-demo`.

```sh
ibmcloud cis managed-waf deployment-add-ruleset 31984fea73a15b45779fa0df4ef62f9b efb7b8c949ac4650a09736fc376e9aee --match true --enabled true --override-action block --override-status true --override-rules rule=5de7edfa648c4d6891dc3e7f84534ffa,action=managed_challenge --override-rules rule=e3a567afc347477d9702d9047e97d760,action=action,enabled=true -i "cis-demo"
```
{: pre}

### `ibmcloud cis managed-waf deployment-update-ruleset`
{: #deployment-update-ruleset}

Update a managed ruleset in the deployed managed WAF rules.

```sh
ibmcloud cis managed-waf deployment-update-ruleset DNS_DOMAIN_ID RULE_ID [--match EXPRESSION] [--enabled true|false] [--override-action ACTION] [--override-status STATUS] [--paranoia-level LEVEL] [--override-rules RULE] [--reset-all] [-i, --instance INSTANCE] [--output FORMAT]
ibmcloud cis managed-waf deployment-update-ruleset DNS_DOMAIN_ID RULE_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #deployment-update-ruleset-options}

`DNS_DOMAIN_ID`
:   The ID of DNS domain.

`RULE_ID`
:   The ID of deployed managed rule.

`--match`
:   Specifies the conditions that must be matched for the rule to run. For match value, see [Using fields, functions, and expressions](/docs/cis?topic=cis-fields-and-expressions).

`--enabled`
:  Indicates whether the rule is active or not. The default value is `true`.

`--override-action`
:  The ruleset action of the overrides. Valid values are `managed_challenge`, `block`, `js_challenge`, `log`, and `challenge`.

`--override-status`
:  The ruleset status of the overrides. Valid values are `true` and `false`.

`--paranoia-level`
:  OWASP paranoia level, higher paranoia levels activate more aggressive rules. Valid values are `PL1`, `PL2`, `PL3`, `PL4` and it's only available for `CIS OWASP Core Ruleset`.

`--override-rules`
:  The rules options of the overrides. For example, `--override-rules rule=RULE_ID,action=ACTION,enabled=STATUS`. For OWASP Core Ruleset, you can also override the Score Threshold. For example, `--override-rules rule=6179ae15870a4bb7b2d480d4843b323c,score-threshold=25`.

`--reset-all`
:  Reset all the overrides rules to the default settings.

`--json`
:  The JSON file or JSON string that is used to describe a managed waf rule.

   - The required fields in JSON data are `expression`, `action`, and `action_parameters`.

      `expression` : The rule expression.
      `action` : The rule action to perform. Valid value is `skip`.
      `action_parameters` : The rule action parameters.
         `id` : The ruleset id of the overrides.
         `overrides` : The rules options of the overrides.
            `action` : The ruleset action of the overrides. Valid values are `managed_challenge`, `block`, and `js_challenge`, `log`, `challenge`.
            `enabled` : The ruleset status of the overrides. Valid values are `true` and `false`.
            `rules` : The rules options of the overrides.
               `id` : The rule ID of the overrides.
               `action` : The rule action of the overrides. Valid values are `managed_challenge`, `block`, `js_challenge`, `log`, and `challenge`.
               `enabled` : The rule status of the overrides.
               `score_threshold` : OWASP Anomaly Score Threshold. Set the score threshold, which triggers the Firewall.
            `categories` : Define OWASP Paranoia Level and only valid for `CIS OWASP core ruleset`
               `category` : OWASP paranoia level, higher paranoia levels activate more aggressive rules.
               `enabled` : Whether this OWASP Paranoia Level enabled.

   - The optional fields are `description` and `enabled`.
      `description`: Briefly describes the rule.
      `enabled`: Indicates whether the rule is active or not.

Sample JSON data:
   ```json
         {
            "action": "execute",
            "description": "CIS Managed Ruleset",
            "enabled": true,
            "expression": "(http.cookie eq \"example.com/contact?page=1234\")",
            "action_parameters": {
               "id": "efb7b8c949ac4650a09736fc376e9aee",
               "overrides": {
                  "action": "block",
                  "enabled": false,
                  "rules": [
                     {
                        "id": "5de7edfa648c4d6891dc3e7f84534ffa",
                        "action": "managed_challenge"
                     },
                     {
                        "id": "e3a567afc347477d9702d9047e97d760",
                        "action": "log",
                        "enabled": true
                     }
                  ]
               }
         }
   ```
`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #deployment-update-ruleset-examples}

Update a managed ruleset rule `1a18a1ea7fc043c68761bc69adcbb11c` for domain `31984fea73a15b45779fa0df4ef62f9b` under instance `cis-demo`.

```sh
ibmcloud cis managed-waf deployment-update-ruleset 31984fea73a15b45779fa0df4ef62f9b 1a18a1ea7fc043c68761bc69adcbb11c --match true --enabled true --override-action block --override-status true --override-rules rule=5de7edfa648c4d6891dc3e7f84534ffa,action=managed_challenge --override-rules rule=e3a567afc347477d9702d9047e97d760,action=action,enabled=true -i "cis-demo"
```
{: pre}

## WAF custom rules
{: #waf-custom-rules}

Manage the WAF custom rules by using the following `custom-waf` commands. Firewall rules are now managed by WAF custom rules.

### `ibmcloud cis custom-waf rules`
{: #list-custom-rules}

List all custom rules.

```sh
ibmcloud cis custom-waf rules DNS_DOMAIN_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #list-custom-rules-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #list-custom-rules-examples}

List all custom rules for domain `31984fea73a15b45779fa0df4ef62f9b` under instance `cis-demo`.

```sh
ibmcloud cis custom-waf rules 31984fea73a15b45779fa0df4ef62f9b -i "cis-demo"
```
{: pre}

### `ibmcloud cis custom-waf rule`
{: #show-custom-rule}

Get details of a custom rule.

```sh
ibmcloud cis custom-waf rule DNS_DOMAIN_ID RULE_ID [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #show-custom-rule-options}

`DNS_DOMAIN_ID`
:   The ID of DNS domain.

`RULE_ID`
:   The ID of the rule.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #show-custom-rule-examples}

Show a custom rule `b94632a4cd5a49ed830544d91417a98c` for domain `9343630b9bd5c6e6899834d77f9e50ff` under instance `cis-demo`.

```sh
ibmcloud cis custom-waf rule 9343630b9bd5c6e6899834d77f9e50ff  b94632a4cd5a49ed830544d91417a98c -i "cis-demo"
```
{: pre}

### `ibmcloud cis custom-waf rule-create`
{: #rule-create}

Create a custom rule.

```sh
ibmcloud cis custom-waf rule-create DNS_DOMAIN_ID --match EXPRESSION --action ACTION [--description DESCRIPTION] [--enabled true|false] [-i, --instance INSTANCE] [--output FORMAT]

ibmcloud cis custom-waf rule-create DNS_DOMAIN_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #rule-create-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain.

`--match`
:   Specifies the conditions that must be matched for the rule to run. For match value, see [Using fields, functions, and expressions](/docs/cis?topic=cis-fields-and-expressions).

`--action`
:   The rule action to perform. Valid values are `block`, `challenge`, `js_challenge`, `managed_challenge`, `log`, and `skip`. For 'block' and 'skip' actions, use JSON file or JSON string instead.

`--enabled`
:  Indicates whether the rule is active or not. The default value is `false`.

`--description`
:  A brief description of the rule.

`--json`
:  The JSON file or JSON string that is used to describe a custom rule.

   - The required fields in JSON data are `expression` and `action`.

      - `expression` : Specifies the conditions that must be matched for the rule to run.
      - `action` : The rule action to perform. Valid values are `block`, `challenge`, `js_challenge`, `managed_challenge`, `log`, and `skip`.

   - The optional fields are `description`, `enabled`, `logging`, and `action_parameters`.

      - `action_parameters` : The rule action parameters.
      - `ruleset` : Skip all remaining rules or one or more WAF managed rulesets. Valid value is `current`.
      - `phases` : Skips WAF components for matching requests. Valid values are `http_ratelimit`, `http_request_firewall_managed`, and `http_request_sbfm`.
      - `products` : Skips specific security products for matching requests. Valid values are `waf`, `rateLimit`, `securityLevel`, `hot`, `bic`, `uaBlock`, and `zoneLockdown`.
      - `response` :  Define a custom response for `block` action.
         - `status_code` :  Choose an HTTP status code for the response in the range `400-499`.
         - `content_type` : The content type of a custom response. Valid response types are :`text/html`, `text/plain`, `application/json`, `text/xml`.
         - `content` : The response body.
      - `description` : Briefly describes the rule.
      - `enabled` : Indicates whether the rule is active or not. When this field is disabled, matched requests don't appear in firewall requests.
      - `logging` : Log requests matching the skip rule. This field is only available for 'skip' action.

   Sample JSON data:
   ```json
         {
           "description": "test-custom-rule",
           "expression": "(http.cookie contains \"test\")",
           "action": "skip",
           "logging": {
                   "enabled": true
               },
           "action_parameters": {
             "ruleset": "current",
               "phases": [
                       "http_ratelimit",
                       "http_request_firewall_managed",
                       "http_request_sbfm"
                   ],
                   "products": [
                       "waf",
                       "rateLimit",
                       "securityLevel",
                       "hot",
                       "bic",
                       "uaBlock",
                       "zoneLockdown"
                   ]
           },
           "enabled": true
         }
   ```
`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #rule-create-example}

Create a custom rule for domain `9343630b9bd5c6e6899834d77f9e50ff` under instance `cis-demo`.

```sh
ibmcloud cis custom-waf rule-create 9343630b9bd5c6e6899834d77f9e50ff  --action challenge --description "rule 1" --enabled true --match "(http.host eq \"www.example.com\")" -i "cis-demo"
```
{: pre}

### `ibmcloud cis custom-waf rule-update`
{: #rule-update}

Update a custom rule.

```sh
ibmcloud cis custom-waf rule-update DNS_DOMAIN_ID [--match EXPRESSION] [--action ACTION] [--description DESCRIPTION] [--enabled true|false] [-i, --instance INSTANCE] [--output FORMAT]

ibmcloud cis custom-waf rule-update DNS_DOMAIN_ID (--json @JSON_FILE | JSON_STRING) [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #rule-update-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain.

`RULE_ID`
:  The ID of the rule.

`--match`
:   Specifies the conditions that must be matched for the rule to run. For match value, see [Using fields, functions, and expressions](/docs/cis?topic=cis-fields-and-expressions).

`--action`
:   The rule action to perform. Valid values are `block`, `challenge`, `js_challenge`, `managed_challenge`, `log`, and `skip`. For 'block' and 'skip' actions, use JSON file or JSON string instead.

`--enabled`
:  Indicates whether the rule is active or not. The default value is `false`.

`--description`
:  A brief description of the rule.

`--json`
:  The JSON file or JSON string that is used to describe a custom rule.

   - The required fields in JSON data are `expression` and `action`.

      - `expression` : Specifies the conditions that must be matched for the rule to run.
      - `action` : The rule action to perform. Valid values are `block`, `challenge`, `js_challenge`, `managed_challenge`, `log`, and `skip`.

   - The optional fields are `description`, `enabled`, `logging`, and `action_parameters`.

      - `action_parameters` : The rule action parameters.
        - `ruleset` : Skip all remaining rules or one or more WAF managed rulesets. Valid value is `current`
        - `phases` : Skips WAF components for matching requests. Valid values are `http_ratelimit`, `http_request_firewall_managed`, and `http_request_sbfm`.
        - `products` : Skips specific security products for matching requests. Valid values are `waf`, `rateLimit`, `securityLevel`, `hot`, `bic`, `uaBlock`, and `zoneLockdown`.
        - `response` :  Define a custom response for 'block' action.
            - `status_code` :  Choose an HTTP status code for the response in the range `400-499`.
            - `content_type` : The content type of a custom response. Valid response types are `text/html`, `text/plain`, `application/json`, and `text/xml`.
            - `content` : The response body.
      - `description` : Briefly describes the rule.
      - `enabled` : Indicates whether the rule is active or not. When this field is disabled, matched requests don't appear in firewall requests.
      - `logging` : Log requests matching the skip rule. This field is only available for 'skip' action.

   Sample JSON data:
   ```json
         {
           "description": "test-custom-rule",
           "expression": "(http.cookie contains \"test\")",
           "action": "block",
           "action_parameters": {
             "response": {
             "status_code": 429,
             "content_type": "text/xml",
             "content": "reject"
             }
           },
           "enabled": true
         }
   ```

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #rule-update-example}

Update a custom rule `b94632a4cd5a49ed830544d91417a98c` for the domain `9343630b9bd5c6e6899834d77f9e50ff` under instance `cis-demo`.

```sh
ibmcloud cis custom-waf rule-update 9343630b9bd5c6e6899834d77f9e50ff b94632a4cd5a49ed830544d91417a98c --enabled false --description rule-updateion "rule 1" --enabled true --match "(http.host eq \"www.example.com\")" -i "cis-demo"
```
{: pre}

### `ibmcloud cis custom-waf rule-order-update`
{: #rule-order-update}

Change the execution order of the custom rule.

```sh
ibmcloud cis custom-waf rule-order-update DNS_DOMAIN_ID RULE_ID [--before RULE_ID] [--after RULE_ID] [--index INDEX] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #rule-order-update-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain.

`RULE_ID`
:  The ID of the custom rule.

`--before`
:  Places the rule before rule `<RULE_ID>`.

`--after`
:  Places the rule after rule `<RULE_ID>`.

`--index`
:  Places the rule in the exact position that is specified by the integer number.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #rule-order-update-example}

Put custom rule `4eae81b170f644f795da017001383de7` before rule `2ed2dd160cb745feb415414544d97c70` for domain `9343630b9bd5c6e6899834d77f9e50ff` under instance `cis-demo`.

```sh
ibmcloud cis custom-waf rule-order-update 9343630b9bd5c6e6899834d77f9e50ff 4eae81b170f644f795da017001383de7 --before 2ed2dd160cb745feb415414544d97c70 -i "cis-demo"
```
{: pre}

### `ibmcloud cis custom-waf rule-delete`
{: #rule-delete}

Delete a custom rule by ID.

```sh
ibmcloud cis custom-waf rule-delete DNS_DOMAIN_ID RULE_ID [-f, --force] [-i, --instance INSTANCE] [--output FORMAT]
```

#### Command options
{: #rule-delete-options}

`DNS_DOMAIN_ID`
:   The ID of the DNS domain.

`RULE_ID`
:  The ID of the custom rule.

`-i, --instance`
:   Instance name or ID. If instance name or ID is not set, the context instance that is specified by `ibmcloud cis instance-set INSTANCE` is used.

`-f, --force`
:   Attempt to delete a custom rule without prompting for confirmation.

`--output`
:   The output format. Currently, `json` is the only supported value.

#### Examples
{: #rule-delete-example}

Delete custom rule `e9fad806880c4c42bd7ebeec8dcba4e6` for domain `9343630b9bd5c6e6899834d77f9e50ff` under instance `cis-demo`.

```sh
ibmcloud cis custom-waf rule-delete  9343630b9bd5c6e6899834d77f9e50ff e9fad806880c4c42bd7ebeec8dcba4e6 -i "cis-demo"
```
{: pre}

## Private endpoint support
{: #private-endpoint-support}

To ensure that you have enhanced control and security over your data when you use the CIS CLI, you have the option of using private routes to CIS endpoints. Private routes are not accessible or reachable over the internet. By using CIS private endpoints, you can protect your data from threats from the public network and logically extend your private network.

Regional support is provided for a limited number of CLI commands. The following regions support private endpoints:

- us-south
- us-east

### Logging in to the CLI with a private endpoint
{: #logging-in-cli-private-endpoint}

Use the following command to log in to a private endpoint by using the CLI:

```sh
ibmcloud login -a private.cloud.ibm.com
```
{: pre}

### Targeting a supported region
{: #targeting-supported-region}

A region must be targeted when a private endpoint is set.
Use the following command to target a supported region:

```sh
ibmcloud target -r [region]
```
{: pre}

### Using CIS CLI with private endpoints
{: #using-cli-private-endpoints}

All the commands support private endpoints, for example:

```sh
ibmcloud cis domains -i cis-demo
```
{: pre}
