---
copyright:
  years: 2018
lastupdated: "2018-03-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# About IBM Cloud Internet Services (CIS)
IBM Cloud Internet Services (CIS) provides a fast, highly performant, reliable, and secure internet service for customers running their business on IBM Cloud.   

IBM CIS gets you going quickly by establishing defaults for you, which you can change easily using the API or UI. Here are some commonly changed parameters:

 * **DNS settings**: you can use IBM CIS to host your DNS or you can create CNAME records.
 * **Crypto settings (TLS)**: the default is `flexible` mode, which encrypts the connection between your host and the IBM CIS edge server, but does not encrypt the communication between the IBM CIS edge server and origin server.
 * **Cache**: the standard mode leads to the most bandwidth savings, but it can be adjusted. Clear individual files when you are uploading new content, rather than rebuilding your entire cache, which takes much longer. You can use **Development Mode** to bypass the cache and still take advantage of security features.
 * **Page Rules**: lets specific settings be applied according to each URL. Changes take effect immediately.

## Caching
Caching is a way to store your static web content closest to your site visitors, thus significantly enhancing the performance of the website. Our globally distributed delivery environment enables web content owners to provide a seamless experience, worldwide.  

### Origin and Edge Servers
An **origin** server is a host computer running programs that are designed to listen for and process incoming requests from the internet. It can take on the full responsibility of serving up the content for an internet property such as a website. The origin server is represented by an IP address or a DNS name at which the application is exposed on the internet, and it can be a virtual or physical server, or even a local load balancer that is proxying multiple backend servers on which the application runs.

Static content is stored on an **edge server** that is hosted by a caching service. Caching uses a variety of technologies to optimize the website experience: it automatically caches static content, it offers the facility for quick cache purging, and it allows you to set your edge cache expiration time (TTL). The edge servers also implement a Web Application Firewall (WAF), if enabled, and they offer DDoS mitigation functions when the proxy mode is in effect.

### Caching Options
Caching options include:
 - **Page Rules**: Define how traffic from visitors to the website is handled. Websites can be set up to exercise fine-grained control over how visitors interact with the site on a page-by-page basis.
 - **TLS**: Supports users who would like to use latest web encryption technologies (TLS 1.2).
 - **Purge Cache**: Allows you to purge the cache content to allow for instant static content update.
 - **Browser Expiration**:  Defines the length of time the user's browser stores cached assets.
 - **Caching Level**: Defines the URL conditions under which you want to deliver cached assets to users.
    - **No query string**: Delivers cached assets when there is no query string.
    - **Query string independent**: Ignores the query string and delivers the same asset.
    - **Query string dependent**: Delivers a different asset when the query string changes.
 
## Encryption with TLS
Encrypt communication to and from your website using Transport Layer Security (TLS). It may take up to 24 hours after the site becomes active for your new certificates to be issued.

You can find more information about TLS in our [FAQ](faq.html).

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
