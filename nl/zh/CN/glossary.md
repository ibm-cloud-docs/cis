---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Glossary, load balancer, pool, health check

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# 词汇表
{:#glossary}

本词汇表包含使用全局负载均衡器 (GLB) 时可能会遇到的通用术语的定义。

## 池 (Pool)
{:#glossary-pool}

池是一组源服务器，在池连接到 GLB 时，会将流量智能路由到池中。用户可以配置池中最少有多少源服务器时可将池标记为正常运行，也可以配置要使用哪种特定的运行状况检查。源池可以与特定区域相关联，也可以使其对所有区域都可用。

## 负载均衡器 (Load balancer)
{:#glossary-load-balancer}

负载均衡器是充当逆向代理的设备，可跨多个服务器分发网络或应用程序流量。负载均衡器用于提高系统容量（并发用户数）和提高应用程序的可靠性。

## 源服务器 (Origin Servers)
{:#glossary-origin-servers}

源服务器处理和响应来自客户机的入局请求，并且通常与高速缓存服务器一起使用。源服务器运行一个或多个程序，这些程序旨在侦听和处理入局因特网请求。源服务器与发出请求的客户机之间的物理距离会增加连接的等待时间，从而增加装入时间。使用高速缓存服务器可缩短此等待时间。

## 运行状况检查 (Health check)
{:#glossary-health-check}

运行状况检查有助于深入了解池的可用性，以便可以将流量路由到运行正常的池。这些检查定期发送 HTTP/HTTPS 请求并监视响应。可以使用定制的时间间隔、超时和状态码等来进行配置。一旦将池标记为运行不正常，流量将智能地重新路由到其他可用池（如果可用）。




