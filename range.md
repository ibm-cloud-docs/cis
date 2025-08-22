---

copyright:
  years: 2018, 2025
lastupdated: "2025-08-22"

keywords: range application, tls encryption, global tcp proxy

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Creating Range applications
{: #cis-range}

Creating a Range application involves configuring how traffic is routed to your origin servers, with support for specifying protocols, origin settings, and advanced features like TLS termination and custom rules. You can add a Range application by using the CIS console or API.
{: shortdesc}

Range is only available to Enterprise customers for an additional cost, and is priced per bandwidth usage.
{: note}

## Before you begin
{: #range-limitations}

Review the following planning considerations:

* You can create up to 10 Range applications, each with a unique origin. Every Range application with a unique origin requires a unique IP address, which are a limited resource. If you need more than 10 Range applications, submit a support case to IBM. Requests to increase the limit require a use case review and may take several days

   You can create more than 10 applications if they share an existing origin, but use different ports.
   {: tip}

* For TCP Range applications, only custom IP rules apply because these rules operate at OSI Layer 3 and 4. HTTP(S) Range applications support both firewall rules and IP rules. Generally, firewall rules are designed for Layer 7 (HTTP) properties, such as request headers and body content.

For more information, see [Range applications](/docs/cis?topic=cis-range-concept).
{: note}

## Creating a Range application in the console
{: #range-add-an-application}
{: ui}

To add a Range application in the console, follow these steps: 

1. In the CIS console, navigate to the **Security** section.
1. Select the **Range** tab, then click **Create**.
1. Select an application type from the list: TCP, UDP, HTTP, HTTPS, RDP, SSH, or Minecraft. For more information, see [Protocols and use cases](/docs/cis?topic=cis-range-concept#choosing-protocol-on).
1. Enter the application name. This name associates your application with a DNS name on your {{site.data.keyword.cis_short_notm}} domain.
1. Enter the edge port. {{site.data.keyword.cis_short_notm}} listens for incoming connections on these ports and proxies them to your origin. Connections to these addresses are proxied to your origin.

   You can enter a port range for example, (`8080-8090`), but the origin must have an equal number of consecutive ports matching the range.
   {: note}
   
1. Select the edge IP connectivity.
1. In the Origin section, enter the origin IP and port of your TCP application, or select an existing load balancer and port.
1. Optionally, enable custom rules. When enabled, rules with a "block" or "allowlist" action are enforced for the application.
1. Optionally, enable edge TLS termination. When enabled, select the type of TLS termination you want to use from the list.
1. Optionally, select a [PROXY Protocol](/docs/cis?topic=cis-enable-proxy-protocol) if you have a proxy inline that supports it. This is useful if you are running a service that requires knowledge of the true client IP. Usually, this setting remains `off`. 
1. Click **Create**.

Provisioning a Range application incurs additional costs, based on the amount of bandwidth used per application.
{: attention}

### Viewing metrics
{: #range-view-metrics}

Your application is now ready to proxy TCP traffic through {{site.data.keyword.cis_short_notm}} (Cloudflare).

Navigate to **Metrics > Range** to view your number of connections to applications and throughput traffic.

The graphs show metrics for up to 10 applications.
{: note}

To toggle application metrics, use the Chart key or click **Select applications**. To change the Metrics data timeframe, use the list menu.

## API usage examples
{: #range-api-usage-examples}
{: api}

Use the following examples to create and list the Range applications.

### Creating Range applications
{: #create-range-app}

You can designate an origin in two ways in Range applications:

1. Origin IP - Use the `origin_direct`parameter.
2. Load balancer - Use the `origin_dns` and `origin_port` parameters. 

For the origin IP request:

```sh
curl --request POST \
  --url https://api-int.cis.dev.cloud.ibm.com/v1/crn:v1:staging:public:internet-svcs-ci:global:a/ce12845bf2914ca18db35bedcd9aefa2:e04e7ccd-9197-4b6d-bf98-933de5074fe6::/zones/2566bebb17f5c0b559a9873a692ccab5/range/apps \
  --header 'Content-Type: application/json' \
  --header 'X-AUTH-USER-TOKEN: Bearer XXXX' \
  --data '{"protocol":"tcp/22","dns":{"type":"CNAME","name":"origin.entdemo5.batflare.com"},"origin_direct":
["tcp://8.8.8.8:22"],"proxy_protocol":"off","ip_firewall":true}'
```
{: codeblock}

Example response:

```sh
{
    "result": {
        "id": "de4d336aea6f4f56b998ffdec9a0f00c",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "origin.entdemo5.batflare.com"
        },
        "origin_direct": [
            "tcp://8.8.8.8:22"
        ],
        "ip_firewall": true,
        "proxy_protocol": "off",
        "tls": "off",
        "traffic_type": "direct",
        "edge_ips": {
            "type": "dynamic",
            "connectivity": "all"
        },
        "created_on": "2025-08-13T07:39:54.175727Z",
        "modified_on": "2025-08-13T07:39:54.175727Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}
```
{: codeblock}

Example request using a load balancer:

```sh
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps \
  -H 'X-Auth-User-Token: <token>' \
  -d '{"protocol":"tcp/22","dns":{"type":"CNAME","name":"ssh.example.com"},"origin_dns": {"name": "test"},"proxy_protocol":true,"ip_firewall":true, "origin_port": 43}'
```
{: codeblock}

Example response:

```sh
{
    "result": {
        "id": "4f70c3d4f20576b79135b898295e8093",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_dns": {
          "name": "test"
        },
        "origin_port": 43,
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-09T17:39:09.190606Z",
        "modified_on": "2019-01-09T17:39:09.190606Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}
```
{: codeblock}

DNS Name
:    The DNS name associated with your application on your domain.

Protocol/Edge port
:   The port your application listens on; incoming connections are proxied to your origin.

Origin direct
:    The IP and port where your application runs, specifying traffic flow from edge to origin.

IP Firewall
:    If enabled, CIS enforces custom rule criteria, such as allowing, blocking, or challenging specific IPs or ranges, replacing legacy IP firewall behavior to provide more granular access control.

PROXY Protocol
:    Enable only if you have an inline proxy supporting PROXY Protocol v1; usually disabled.

Origin DNS
:    The load balancer name used as your origin.

Origin Port
:    The port of your origin service.

For more information, see [Creating Range applications](/apidocs/cis#create-range-app).

### Listing all Range applications
{: #range-list-all-apps}

Use the following request to list all Range applications:

```sh
curl --request GET \
  --url https://api-int.cis.dev.cloud.ibm.com/v1/crn:v1:staging:public:internet-svcs-ci:global:a/ce12845bf2914ca18db35bedcd9aefa2:e04e7ccd-9197-4b6d-bf98-933de5074fe6::/zones/2566bebb17f5c0b559a9873a692ccab5/range/apps \
  --header'content-type: application/json'
  --header 'X-AUTH-USER-TOKEN: Bearer XXXX' \
{: pre}

Example response:

```sh
{
    "result": [
        {
            "id": "de4d336aea6f4f56b998ffdec9a0f00c",
            "protocol": "tcp/22",
            "dns": {
                "type": "CNAME",
                "name": "origin.entdemo5.batflare.com"
            },
            "origin_direct": [
                "tcp://8.8.8.8:22"
            ],
            "ip_firewall": true,
            "proxy_protocol": "off",
            "tls": "off",
            "traffic_type": "direct",
            "edge_ips": {
                "type": "dynamic",
                "connectivity": "all"
            },
            "created_on": "2025-08-13T07:39:54.175727Z",
            "modified_on": "2025-08-13T07:39:54.175727Z"
        }
    ],
    "success": true,
    "errors": [],
    "messages": []
}
```
{: codeblock}

For more information, see [Listing Range applications](/apidocs/cis#list-range-apps).

### Listing specific Range applications
{: #range-list-a-specific-range-app}

Use the following request to list specific Range applications:

```sh
curl -X GET \
https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps/4f70c3d4f20546b79135b898295e8093
```
{: pre}

Example responses:

* Applications by Origin IP:

    ```sh
    {
        "result": {
            "id": "4f70c3d4f20546b79135b898295e8093",
            "protocol": "tcp/22",
            "dns": {
                "type": "CNAME",
                "name": "ssh.example.com"
            },
            "origin_direct": [
                "tcp://172.0.2.1:22"
            ],
            "ip_firewall": true,
            "proxy_protocol": true,
            "created_on": "2019-01-09T17:33:09.190606Z",
            "modified_on": "2019-01-09T17:33:09.190606Z"
        },
        "success": true,
        "errors": [],
        "messages": []
    }
    ```
    {: codeblock}

* Applications by load balancer:

    ```sh
    {
        "result": {
            "id": "555359036e7f4acc82d69b916f62caba",
            "protocol": "tcp/22",
            "dns": {
                "type": "CNAME",
                "name": "ssh.example.com"
            },
            "origin_dns": {
                "name": "test_update"
            },
            "origin_port": 76,
            "ip_firewall": true,
            "proxy_protocol": true,
            "created_on": "2019-01-10T22:26:47.167008Z",
            "modified_on": "2019-01-10T22:26:47.167008Z"
        },
        "success": true,
        "errors": [],
        "messages": []
    }
    ```
    {: codeblock}
