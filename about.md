---
copyright:
  years: 2018
lastupdated: "2018-12-03"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"} 

# About IBM Cloud Internet Services (CIS)
IBM Cloud Internet Services (CIS), powered by Cloudflare, provides a fast, highly performant, reliable, and secure internet service for customers running their business on IBM Cloud.   

IBM CIS gets you going quickly by establishing defaults for you, which you can change easily using the API or UI. Here are some commonly changed parameters:

 * **DNS settings**: you can use IBM CIS to host your DNS or you can create CNAME records.
 * **Crypto settings (TLS)**: the default is `flexible` mode, which encrypts the connection between your host and the IBM CIS edge server, but does not encrypt the communication between the IBM CIS edge server and origin server.

## Web Application Firewall (WAF)
IBM CIS provides Web Application Firewall (WAF) capability, which examines web traffic to look for suspicious activity. It can filter out illegitimate traffic automatically — based on rule sets — to look at GET and POST-based web requests. You can use various rule sets to determine which traffic to block, challenge, or let pass. Our WAF can block comment spam, cross-site scripting attacks, and SQL injections.

You can enable or disable the WAF at your discretion. We recommend that you always leave it on.

## Protection from DDoS attacks
IBM CIS supplies DDoS protection that stands between your website and attackers, regardless of the attack's size or duration.

## Load Balancing
IBM CIS Load Balancing operates at the Authoritative DNS level. It incorporates advanced health checks to monitor the health of the origins, and dynamically adjusts DNS responses. Additionally, you can configure Geo policies for Global Load Balancing (GLB).

### Health checks
Load Balancing Health Checks are performed on specific URLs through periodic HTTP or HTTPS requests, and they are configured with customizable intervals, timeouts, and status codes. When an origin server is marked as unhealthy, visitors are routed away from failures, using our fast failover routes.
 
### Geo Policies and Global Load Balancing (GLB)
Geo policies give you control of the origin servers to which a given client is directed, based on the geographic location of that client. For instance, you could configure your Geo policies so that visitors in Europe are sent to the nearest European origin for your website or application, U.S. visitors are sent to a North American origin, and so forth.

## Caching
Caching is a way to store your static web content closest to your site visitors, thus significantly enhancing the performance of the website. Our globally distributed delivery environment enables web content owners to provide a seamless experience, worldwide.  
 
## Encryption with TLS
Encrypt communication to and from your website using Transport Layer Security (TLS). It may take up to 24 hours after the site becomes active for your new certificates to be issued.

You can find more information about TLS in our [FAQ](faq.html).
