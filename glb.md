---

copyright:
  years: 2018
lastupdated: "2018-03-05"

---

# Global Load Balancer (GLB) Concepts

This document contains some concepts and definitions related to the Global Load Balancer (GLB) and how it affects your IBM CIS deployment.

## Global Load Balancer

The Global Load Balancer (GLB) manages traffic across server resources located in multiple regions. The GLB utilizes a pool which allows for the traffic to be distributed to multiple origins. This provides many benefits including:

  * Minimize response time
  * Higher availability through redundancy
  * Maximize traffic throughput

## Pool

A pool is a group of origin servers that traffic is intelligently routed to when attached to a GLB. The minimum number of available origin servers for the pool to be marked healthy is configurable by the user along with which specific health check to use. The origin pool can be associated with a specific region or it can be made available to all regions.

## Health Check

A health check helps gain insight into the availability of pools so that traffic can be routed to the healthy ones. These checks periodically send HTTP/HTTPS requests and monitor the responses. They can be configured with customized intervals, timeouts, status codes, and more. As soon as a pool is marked unhealthy, traffic will be intelligently rerouted to another available pool, if available.
