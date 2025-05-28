---

copyright:
  years: 2024, 2025
lastupdated: "2025-05-28"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# TCP connections and routing
{: #tcp-concepts}

Transmission Control Protocol (TCP) connections are established between clients and servers when accessing CIS-protected resources. When users request a website using CIS, their requests pass through the CIS infrastructure, enabling DDoS protection and enhanced security.
{: shortdesc}

## How CIS connects users to the origin server
{: #connect-users-to-origin-server}

CIS acts as an intermediary between the user and the origin by routing user requests through CIS/Cloudflare to the application's origin server. User traffic is routed to the nearest point of presence (PoP); where the request is then processed.
In case a request is not served from one of Cloudflare's data centers, a connection will be opened to the origin server to forward the request.

## Connection limits
{: #connection-limits}

When HTTP/HTTPS traffic is proxied through CIS, there are often two established TCP connections: the first is between the requesting client to CIS, and the second is between CIS and the origin server. Each connection has their own set of TCP and HTTP limits.

### Connection limits between the requesting client and CIS
{: #client-cis}

Table 1 lists connection limits between the requesting client and CIS.
{: shortdesc}

| Type | Limit (seconds)  | HTTP status code at limit | Configurable |
|----------------|---------|-----------|------|
| Connection Keep-Alive HTTP/1.1	| 400	| TCP connection closed	| No |
| Connection Idle HTTP/2 | 400 | TCP connection closed| No |
{: caption="Connection limits between the requesting client and CIS" caption-side="bottom"}

### Connection limits between CIS and the origin server
{: #cis-origin}

Table 2 lists connection limits between CIS and the origin server.
{: shortdesc}

| Type | Limit (seconds) | HTTP status code at limit | Configurable |
|----------------|---------|-----------|------|
| Complete TCP Connection [^1] |	15	| [522](/docs/cis?topic=cis-html-5xx-errors#522-error)	| No |
| TCP ACK Timeout [^2]	| 90	| [522](/docs/cis?topic=cis-html-5xx-errors#522-error)	| No |
| TCP Keep-Alive Interval [^3]	| 30 | [520](/docs/cis?topic=cis-html-5xx-errors#520-error)	| No |
| Proxy Idle Timeout [^4]	| 900	| [520](/docs/cis?topic=cis-html-5xx-errors#520-error)	| No |
| Proxy Read Timeout [^5]	| 100	| [524](/docs/cis?topic=cis-html-5xx-errors#524-error)	| [Yes](/apidocs/cis#get-proxy-read-timeout) |
| Proxy Write Timeout [^6]	| 30	| [524](/docs/cis?topic=cis-html-5xx-errors#524-error)	| No |
| HTTP/2 Pings to Origin	| Off	| N/A	| Yes |
| HTTP/2 Connection Idle [^7]	| 900	| No	| No |
{: caption="Connection limits between CIS and the origin server. Some TCP connections can be customized for Enterprise customers." caption-side="bottom"}

[^1]: TCP uses a three-way handshake to establish a reliable connection (SYN, SYN-ACK, ACK) over an IP based connection. SYN is short for synchronize, and ACK is short for acknowledgement.

[^2]: The final step in the TCP three-way handshake, confirming the establishment of a connection.

[^3]: A TCP keep-alive is used to maintain a connection between two endpoints by sending packets to check if the connection is still active. This helps prevent idle connections from being prematurely closed. If a response is not received after a defined period, the connection is terminated.

[^4]: When a TCP connection is in an idle state, it means that the connection has been established, but neither endpoint is sending any data. In the context of HTTP, an idle connection is when an established connection between a client and a server is not currently transmitting any HTTP requests or responses.

[^5]: A proxy read timeout is the maximum amount of time a proxy server waits for a response from the origin server before terminating the connection.

[^6]: A proxy write timeout is the maximum amount of time a proxy server allows for sending data to the client before terminating the connection.

[^7]: When a TCP connection is in an idle state, it means that the connection has been established, but neither endpoint is sending any data. In the context of HTTP, an idle connection is when an established connection between a client and a server is not currently transmitting any HTTP requests or responses.

## TCP connections and keep-alives
{: #tcp-connections-keep-alives}

CIS uses keep-alive connections to improve performance and reduce costs by minimizing the need for repeated TCP connections when proxying customer traffic to origin servers. To optimize this process, ensure that HTTP keep-alive is enabled on your origin server, allowing reuse of open TCP connections up to the Proxy Idle Timeout after the last request. This helps prevent connection resets and enhances efficiency.

Typically, HTTP opens a new TCP connection for each request-response cycle, which can add overhead. Keep-alives allow a single TCP connection to remain open for multiple requests, reducing latency and network traffic, ultimately enhancing user experience.

While TCP connections can remain active, idle connections are usually terminated after a certain time. CIS has a default idle timeout of 400 seconds for user connections and sends keep-alive probes every 75 seconds. If nine consecutive probes go unanswered, CIS ends the connection with a TCP Reset (RST) packet.

It's important to note that keep-alives do not guarantee connection stability due to factors like capacity balancing or maintenance, so applications should be designed to handle disconnections gracefully. Enterprise customers can customize TCP connection settings between users and CIS, as well as between CIS and the origin server.
