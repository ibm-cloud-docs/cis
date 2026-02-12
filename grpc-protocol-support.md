---

copyright:
  years: 2018, 2026
lastupdated: "2026-02-09"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# gRPC protocol support
{: #grpc-protocol-support}

gRPC (gRPC Remote Procedure Call) is an open source framework that allows applications to communicate efficiently and reliably. It enables the creation of compact, high-performance APIs that reduce bandwidth usage, lower latency, and support scalable service-to-service communication.
{: shortdesc}

## gRPC features
{: #grpc-features}

* Client-Server Model:
   gRPC uses a client-server architecture in which the client sends a request to the server, and the server processes the request and returns a response. This model supports efficient communication between services and simplifies integration across distributed systems.

* Protocol Buffers (Protobuf):
   gRPC uses Protocol Buffers (protobuf) as its Interface Definition Language (IDL). Protobuf provides a language-neutral and platform-neutral mechanism for serializing structured data, enabling strongly typed contracts between client and server and improving data transmission efficiency.

* HTTP/2:
   gRPC runs over HTTP/2, which provides multiplexing (multiple requests over a single connection), binary data transfer, header compression, and built-in support for streaming. Streaming enables clients and servers to send or receive data continuously without opening multiple connections, supporting both large datasets and real-time communication.

* Cross-platform and multi-language:
   gRPC supports multiple programming languages, such as Java, C++, Python, Go, Ruby, Node.js, and many more. This versatility makes it great for building systems where services are written in different languages.

{{site.data.keyword.cis_short_notm}} supports gRPC protocol for any proxied gRPC endpoints. To enable or disable gRPC support, navigate to the **Reliability** section, select the **Advanced** tab, and toggle the gRPC switch.

Before enabling gRPC support, ensure that your endpoint meets the following requirements:

* The gRPC endpoint must listen on port `443` and support TLS and HTTP/2.
* HTTP/2 must be advertised over Application-Layer Protocol Negotiation (ALPN).
* gRPC requests must use the `application/grpc` or `application/grpc+<message type>` content-type header.
