---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Smart Routing Route connections, routing decisions, Eliminate excess latency

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 路由
{:#cis-routing}

通过使用实时网络连接来分析和优化整个全球因特网中的路由决策，从而消除过多的等待时间。因特网等待时间平均降低 35%，连接错误减少 27%。 
## 智能路由
{:#cis-smart-routing}

通过避免丢包、拥堵和宕机，在整个因特网中高效路由连接。

智能路由可优化数据在整个因特网上采取的路径。通过分析从实时网络连接收集的等待时间和丢包数据，可确定最佳路径。智能路由使用此数据来检测在地球上任意两点之间表现最佳的传输提供商。

## 分层高速缓存
{:#cis-tiered-caching}

使用集中连接提高高速缓存命中率，以减少对客户源的请求。

分层高速缓存可减少对客户源的请求，并降低源服务器上的负载。分层高速缓存实现这一点的方法是，在发生高速缓存不命中时首先询问其他 PoP 是否具有所请求的数据。由于 PoP 之间的距离通常短于 PoP 与源之间的距离，因此客户将发现性能提高。通过利用高速缓存的数据，客户将因其源服务器上的负载降低而受益。

分层高速缓存还会将连接集中到源服务器，以便这些连接来自更少的 PoP。这样就可以减少到源的打开连接数。
