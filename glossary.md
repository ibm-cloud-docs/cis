---
copyright:
  years: 2018
lastupdated: "2018-05-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Glossary
This glossary contains defiitions for common terms you may encounter when working with Global Load Balancer (GLB).

#### Load balancer
A load balancer is a device that acts as a reverse proxy and distributes network or application traffic across a number of servers. Load balancers are used to increase system capacity (the number of concurrent users) and improve the reliability of applications.

#### Pool
A pool is a group of origin servers that traffic is intelligently routed to when attached to a GLB. The minimum number of available origin servers for the pool to be marked healthy is configurable by the user along with which specific health check to use. The origin pool can be associated with a specific region or it can be made available to all regions.

#### Health check
A health check helps gain insight into the availability of pools so that traffic can be routed to the healthy ones. These checks periodically send HTTP/HTTPS requests and monitor the responses. They can be configured with customized intervals, timeouts, status codes, and more. As soon as a pool is marked unhealthy, traffic will be intelligently rerouted to another available pool, if available.

#### Origin Servers
An origin server processes and responds to incoming requests from clients, and are typically used with caching servers. Origin servers run one or more programs that are designed to listen for and process incoming Internet requests. The physical distance between the origin server and the client making a request adds latency to the connection, increasing load time. Using caching servers reduces this latency.


