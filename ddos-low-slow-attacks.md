---

copyright:
  years: 2026
lastupdated: "2026-02-13"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Protecting against low and slow DDoS attacks
{: #ddos-low-slow-attacks}

A [low and slow DDoS attack](https://www.cloudflare.com/learning/ddos/ddos-low-and-slow-attack/){: external} is typically a non-volumetric attack in which an attacker sends a small number of HTTP requests at a very slow rate. These attacks are designed to avoid detection while gradually exhausting server resources.
{: shortdesc}

[Slowloris](https://www.cloudflare.com/learning/ddos/ddos-attack-tools/slowloris/){: external} is a common type of low and slow attack. In a Slowloris attack, the attacker establishes multiple [TCP connections](/docs/cis?topic=cis-tcp-concepts) to the target server by using HTTP or HTTPS. Instead of completing the HTTP request, the attacker sends incomplete HTTP header lines. The server waits for the request to complete and keeps the connection open.

To maintain the connection, the attacker periodically sends additional partial headers or header fields. This behavior can include sending partial HTTP headers or using the content-length header to declare a request body size that is larger than the data actually sent.

The recommended best practice to defend against low and slow attacks is to use an HTTP reverse proxy, such as CIS [CDN](/docs/cis?topic=cis-dns-concepts) or [WAF](/docs/cis?topic=cis-waf-q-and-a&interface=ui) service. The reverse proxy acts as a protective layer in front of the origin server. It waits for a complete HTTP request before forwarding traffic to the origin, serving content from cache, or applying other configured actions. By enabling request body buffering, CIS absorbs slow and incomplete requests at the edge. Incomplete requests are not forwarded to the origin server.

If possible, CIS serves requests from [Cache](/docs/cis?topic=cis-caching-concepts) or Edge functions. Otherwise, CIS forwards the request to the origin only after the request is fully received and passes all WAF checks. As a result, the attack traffic never reaches the origin server, similar to CIS protection against TCP-based Slowloris attacks.

CIS also enforces timeouts on incomplete HTTP requests after a series of [keepalive probes](/docs/cis?topic=cis-tcp-concepts#tcp-connections-keep-alives). There is no minimum traffic threshold required to activate this protection. In addition, custom firewall rules validate payload size and perform basic sanity checks to ensure that request content matches expected behavior.

The [RUDY (R-U-Dead-Yet?)](https://www.cloudflare.com/learning/ddos/ddos-attack-tools/r-u-dead-yet-rudy/){: external} attack is a low-rate denial-of-service (DoS) technique that targets web servers by holding connections open for long periods.

Unlike traditional DDoS attacks that overwhelm servers with a large volume of requests in a short time, RUDY creates a small number of long-running HTTP requests. It submits form data extremely slowly, which keeps server resources occupied and prevents the server from responding to legitimate users. Because the traffic volume is low and the requests appear valid, RUDY attacks are difficult to detect and often bypass volume-based DDoS protections.

RUDY targets the application layer (Layer 7) by exploiting how web forms process HTTP POST requests. The attacker sends form data one byte at a time and intentionally delays completion of the request. As a result, application threads remain open while waiting for the request to finish, eventually exhausting server resources and disrupting normal application operation.
