---

copyright:
  
  years: 2022

lastupdated: "2023-01-06"

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Enabling Proxy protocol
{: #enable-proxy-protocol}

{{site.data.keyword.cis_full_notm}} intercepts packets before forwarding them to your server, so that if you look up a client IP, you see {{site.data.keyword.cis_short_notm}}'s IP rather than the true client IP. However, some services you run might require you to know the true client IP. In those cases, you can use a proxy protocol for {{site.data.keyword.cis_short_notm}} to pass the client IP to your service. 
{: shortdesc}

Sending proxy information along is dependent on whether TCP or UDP is used. For TCP, Range supports adding Proxy Protocol v1, which is the human readable-version supported by Amazon ELB and NGINX. For UDP applications, {{site.data.keyword.cis_short_notm}} has developed a custom proxy protocol called Simple Proxy Protocol.

This feature requires an Enterprise plan. If you would like to upgrade, contact your account team.
{: note}

## Enable proxy protocol v1 for TCP
{: #tcp-proxy-protocol}

1. Log in to the {{site.data.keyword.cis_short_notm}} dashboard
1. Click **Range**.
1. Locate the application that will use the PROXY protocol and click **Configure**.
1. From the menu, select **PROXY Protocol v1**.

When TCP applications are configured to use proxy protocol v1, {{site.data.keyword.cis_short_notm}} prepends each inbound TCP connection with the proxy protocol plain-text header.

### The proxy protocol v1 header
{: #v1-proxy-protocol-header}

The proxy protocol prepends every connection with a header reporting the client IP address and port. A proxy protocol plain-text header has the following format:

```
PROXY_STRING + single space + INET_PROTOCOL + single space + CLIENT_IP + single space + PROXY_IP + single space + CLIENT_PORT + single space + PROXY_PORT + "\r\n"
```
{: codeblock}

The following is an example proxy protocol line for an IPv4 address:

`PROXY TCP4 192.0.2.0 192.0.2.255 42300 443\r\n`

The following is an example proxy protocol line for an IPv6 address:

`PROXY TCP6 2001:db8:: 2001:db8:ffff:ffff:ffff:ffff:ffff:ffff 42300 443\r\n`


## Enabling Proxy Protocol v2 for TCP/UDP
{: #v2-proxy-protocol}

1. Log in to the {{site.data.keyword.cis_short_notm}} dashboard.
1. Click **Range**.
1. Locate the application that will use the proxy protocol and click **Configure**.
1. From the menu, select **PROXY Protocol v2**.

When TCP applications are configured to use proxy protocol v2, {{site.data.keyword.cis_short_notm}} prepends each inbound TCP connection with the proxy protocol binary header.

When UDP applications are configured to use PROXY Protocol v2, {{site.data.keyword.cis_short_notm}} prepends the first UDP datagram on a stream with a proxy protocol binary header.

### The proxy protocol v2 header
{: #v2-proxy-protocol-header}

The proxy protocol prepends every connection with a header reporting the client IP address and port.

A proxy protocol binary header for a IPv4 incoming address has the following format:

```text
0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                                                               |
+                                                               +
|                  Proxy Protocol v2 Signature                  |
+                                                               +
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|Version|Command|   AF  | Proto.|         Address Length        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                      IPv4 Source Address                      |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    IPv4 Destination Address                   |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|          Source Port          |        Destination Port       |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```
{: screen}

A proxy protocol binary header for a IPv6 incoming address has the following format:

```text
0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                                                               |
+                                                               +
|                  Proxy Protocol v2 Signature                  |
+                                                               +
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|Version|Command|   AF  | Proto.|         Address Length        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                                                               |
+                                                               +
|                                                               |
+                      IPv6 Source Address                      +
|                                                               |
+                                                               +
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                                                               |
+                                                               +
|                                                               |
+                    IPv6 Destination Address                   +
|                                                               |
+                                                               +
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|          Source Port          |        Destination Port       |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```
{: screen}

## Enable Simple Proxy Protocol for UDP
{: #udp-proxy-protocol}

When using UDP, the client source IP and port information can be obtained by using Simple Proxy Protocol, a lightweight protocol developed specifically for UDP.

To enable it, click **Configure** on a Range application and toggle the setting for **Simple Proxy Protocol** to `On`.

Simple Proxy Protocol dictates that your origin must also prepend packets meant for the client with the same header, including original client source information. This is done to validate that packets coming in are in fact intended for the client.
