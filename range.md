---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: range application, tls encryption, ddos protection, global tcp proxy

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Range
{:#cis-range}

The Range feature brings DDoS protection, load balancing, and content acceleration to any TCP-based protocol. 
Range is a global TCP Proxy running on CIS/Cloudflare’s edge nodes. 

Range can be used to: 
* Protect your TCP ports and protocols from **layer 3 and 4 DDoS** attacks. 
* Reduce the ability of attackers to snoop and steal sensitive data by enabling **TLS encryption**.
* Integrate with CIS IP Firewall, which allows you to block or challenge IP addresses, or entire IP ranges, from reaching your TCP services. 
* Configure load balancers with TCP health checks, failover, and steering policies to dictate where traffic should flow.

## Getting started with Range
{:#getting-started-with-range}

Range is only available to Enterprise customers for an additional cost, and is priced per bandwidth usage.
{:note}

### Add an application
{:#range-add-an-application}
Follow these steps to add an application.

1. Navigate to **Security > Range**
1. Click on the **Add application** button 
1. Enter the application name in the first input field. Your application becomes associated with a DNS name on your CIS domain.
1. Enter the edge port in the next input field. We'll listen for incoming connections to these addresses on this port. Connections to these addresses are proxied to your origin. (Proxying is supported on all ports except port 21.)
1. In the Origin section, enter the origin IP and Port of your TCP application. You may also select an existing Load Balancer
1. Enable IP Firewall. When enabled, firewall rules with a "block" or "whitelist" action are enforced for this application. Country or ASN-based rules are not yet supported.
1. Enable Proxy Protocol if you have a proxy in-line that supports PROXY Protocol v1. This feature is useful if you are running a service that requires knowledge of the true client IP. In most cases, this setting should remain disabled. 
1. Click **Provision**

Proxy Protocol prepends every connection with a header reporting the client IP address and port. A Proxy Protocol header has the format: 
  * PROXY_STRING + single space + INET_PROTOCOL + single space + CLIENT_IP + single space + PROXY_IP + single space + CLIENT_PORT + single space + PROXY_PORT + "\r\n"
  * Here's an example Proxy Protocol line for an IPv4 address:
    `PROXY TCP4 192.0.2.0 192.0.2.255 42300 443\r\n`
  * Here's an example Proxy Protocol line for an IPv6 address:
    `PROXY TCP6 2001:db8:: 2001:db8:ffff:ffff:ffff:ffff:ffff:ffff 42300 443\r\n`
   
Provisioning a Range application will incur additional costs, based on the amount of bandwidth used per app.
{:note}

Your application is now visible in a tile with the following properties:
  * Application name
  * Edge port
  * Origin & port
  * Connections from the past hour (polled every minute)
  * Throughput from the past hour (polled every minute)
  * Overflow menu (Top right corner) allows the following 
    * Edit the application
    * View metrics for the specified application
    * Delete the application 
    
When a Range application is created, it is assigned a unique IPv4 and IPv6 address. These IP addresses are not static and may be subject to change. You can determine the assigned IP address by using DNS. The DNS name will always return the IP addressed assigned to the application.     
    
### View Metrics
{:#range-view-metrics}
Your application is now ready to proxy TCP traffic through Cloudflare/CIS.

Navigate to **Metrics > Range** to view your number of Connections to applications and Throughput traffic.
The graphs show metrics for up to 10 applications. 
{:note}

Application metrics may be toggled via the Chart key or by clicking the **Select applications** button. The Metrics data time frame can be changed using the dropdown menu.

## Range AppTiles
{:#range-apptiles}
After creating a few apps, the **Security > Range** page will be populated with applications tiles. The application tiles contain the following information:
* Application name
* Edge port
* Origin & port
* Connections from the past hour (polled every minute)
* Throughput from the past hour (polled every minute)


The application tile also contains an overflow menu in the top corner (3 dots). The overflow menu provides users the option to:
* edit the application
* view metrics for the specified application
  * this takes the user to **Metrics > Range** page, which displays the metrics for only that application
* delete the application


## API usage examples
{:#range-api-usage-examples}
These are examples to create and list applications using Range.

### Create Range app
{:#create-range-app}
There are two ways you can designate an origin in a Range app
1. Origin IP - using parameter `origin_direct`
2. Load Balancer - using parameters `origin_dns` and `origin_port`

**Request:**
```
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps \
  -H 'X-Auth-User-Token: <token>' \
  -d '{"protocol":"tcp/22","dns":{"type":"CNAME","name":"ssh.example.com"},"origin_direct":["tcp://172.0.2.1:22"],"proxy_protocol":true,"ip_firewall":true}'

```
**Response:**
```
{
    "result": {
        "id": "4f70c3d4f20576b79135b898295e8093",
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

**Request:**
```
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps \
  -H 'X-Auth-User-Token: <token>' \
  -d '{"protocol":"tcp/22","dns":{"type":"CNAME","name":"ssh.example.com"},"origin_dns": {"name": "test"},"proxy_protocol":true,"ip_firewall":true, "origin_port": 43}'

```
**Response:**
```
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

**DNS Name:** Your application is associated with a DNS name on your Domain.

**Protocol/Edge port:** This is the port on which your application is running. Connections to these addresses are proxied to your origin.

**Origin direct:** This is the IP on which your application is running, and the port you want traffic to flow through from the edge to your origin.

**IP Firewall:** If enabled, firewall rules with a Block action are enforced for this Range application.

**PROXY Protocol:** Enable if you have a proxy in-line that supports PROXY Protocol v1. In most cases, this setting remains disabled.

**Origin DNS:** This is the name of the load balancer you want to set as your origin.

**Origin Port:** This is the port of your service. 

### List all apps
{:#range-list-all-apps}

**Request:**
```
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps
```

**Response:**
```
{
    "result": [
        {
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
        }
    ],
    "success": true,
    "errors": [],
    "messages": []
}
```

### List a specfic Range app
{:#range-list-a-specific-range-app}
**Request:**
```
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps/4f70c3d4f20546b79135b898295e8093
```

**Response:**
App using Origin IP
```
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

App using Load Balancer
```
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
