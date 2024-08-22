---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-22"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.cis_short_notm}} DNS zone CNAME (partial) setup
{: #cname-setup}



The following table shows the recommended setup configurations for a child zone (subdomain).


|Parent domain setup |Recommended child subdomain setup|
|:--|:--|
|Parent domain on {{site.data.keyword.cis_short_notm}} through a Full setup |Full setup only|
|Parent domain on {{site.data.keyword.cis_short_notm}} through a CNAME setup |CNAME setup only|
|The parent domain is not on {{site.data.keyword.cis_short_notm}} |Can choose Full or CNAME setup|
{: caption="Table 1. Parent and child domain setup" caption-side="bottom"}

## Setting up a CNAME zone
{: #cname-step-one}

To set up a CNAME, take the following steps.

1. Create the `partial` type zone by using the {{site.data.keyword.cis_short_notm}} API or CLI.
    * Create `partial` type zone with {{site.data.keyword.cis_short_notm}} API

        POST `https://{{api}}/v1/{{crn}}/zones`

        ```sh
        data:  {
                "name":       "ibmnetworkdemo.com",
                "jump_start": false,
                "type":       "partial"
            }
        ```
        {: codeblock}

    * Create `partial` type zone with {{site.data.keyword.cis_short_notm}} CLI

        ```sh
            ibmcloud cis domain-add ibmnetworkdemo.com --type partial --output JSON
        ```
        {: pre}

    If you encounter the error message: "Partial zone signup not allowed", contact Support.

1. Get the txt record `verification_key` and `cname_suffix` from the response:

    ```sh
    {
        "result": {
            "id": "1df93abfb59849abd3e34fde156a4c21",
            "name": "ibmnetworkdemo.com",
            "status": "active",
            "paused": false,
            "verification_key": "476754457-428595283",
             "cname_suffix": "cdn.cloudflare.net",
            "original_name_servers": [
                "ns1.softlayer.com",
                "ns2.softlayer.com"
            ],
            "original_registrar": "everyones internet, ltd. dba s (id: 925)",
            "original_dnshost": null,
            "modified_on": "2021-05-07T06:46:19.326826Z",
            "created_on": "2021-05-07T01:57:53.163247Z",
            "account": {
                "id": "b0c53e3f037b8cdc62b5cb373b8c55e6",
                "name": "57aea3aa-a38e-4760-ada5-a698bca56171"
            }
        },
        "success": true,
        "errors": [],
        "messages": []
    }
    ```
    {: codeblock}

1. Add the record `cloudflare-verify` to the parent DNS zone indicated by the `verification-key` (in this example, `ibmnetworkdemo.com`).

    ```sh
    txt cloudflare-verify.ibmnetworkdemo.com  476754457-428595283
    ```
    {: pre}

1. After {{site.data.keyword.cis_short_notm}} verifies the record, the zone will be activated. This process might take several hours.

## Verify the CNAME
{: #verification}

To verify your CNAME setup, take the following steps.

1. Add an A record in {{site.data.keyword.cis_short_notm}} and enable proxy:

    ```sh
    www.ibmnetworkdemo.com   A      169.48.151.44   true      1
    ```
    {: pre}

1. Add the CNAME record in the authoritative DNS:

    ```sh
    www.ibmnetworkdemo.com  www.ibmnetworkdemo.com.cdn.cloudflare.net
    ```
    {: pre}

    The response should look like the following example.

    ```text
    check::
       dig www.ibmnetworkdemo.com a

    ; <<>> DiG 9.10.6 <<>> www.ibmnetworkdemo.com a
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 13528
    ;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 1

    ;; OPT PSEUDOSECTION:
    ; EDNS: version: 0, flags:; udp: 512
    ;; QUESTION SECTION:
    ;www.ibmnetworkdemo.com.                IN        A

    ;; ANSWER SECTION:
    www.ibmnetworkdemo.com.        899        IN        CNAME        www.ibmnetworkdemo.com.cdn.cloudflare.net.
    www.ibmnetworkdemo.com.cdn.cloudflare.net. 299 IN A 104.18.8.216
    www.ibmnetworkdemo.com.cdn.cloudflare.net. 299 IN A 104.18.9.216
    ```
    {: codeblock}
