---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM Cloud Internet Services, CIS Activity Tracker events

subcollection: cis

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# CIS {{site.data.keyword.cloudaccesstrailshort}} 事件
{: #at_events}

使用 {{site.data.keyword.cloudaccesstrailfull}} 服务可跟踪用户和应用程序如何与 {{site.data.keyword.cloud}} 中的 IBM Cloud Internet Services (CIS) 交互。
{:shortdesc}

{{site.data.keyword.cloudaccesstrailfull_notm}} 服务会记录哪些用户发起的活动会更改 {{site.data.keyword.cloud_notm}} 中服务的状态。有关更多信息，请参阅[{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla)。




## 事件列表：DNS 域
{: #events_dns_domain}

下表列出了与 DNS 域相关并生成事件的操作：

|操作 |描述|
|---|---|  
|internet-svcs.zones.create|创建 DNS 域。|
|internet-svcs.zones.update|更新 DNS 域。|
|internet-svcs.zones.delete|删除 DNS 域。|
|internet-svcs.zones.activation_check.update|对 DNS 域执行激活检查。|
|internet-svcs.zones.dnssec.update|启用或禁用 DNS 域的 DNSSEC。|

## 事件列表：DNS 记录
{: #events_dns_record}

下表列出了与 DNS 记录相关并生成事件的操作：

|操作 |描述|
|---|---|  
|internet-svcs.zones.dns_records.create|创建 DNS 记录。|
|internet-svcs.zones.dns_records.update|更新 DNS 记录。|
|internet-svcs.zones.dns_records.delete|删除 DNS 记录。|
|internet-svcs.zones.dns_records_bulk.create|从区域文件导入 DNS 记录。|


## 事件列表：负载均衡器
{: #events_load_balancers}

下表列出了与负载均衡器相关并生成事件的操作：

|操作 |描述|
|---|---|  
|internet-svcs.zones.load_balancers.create|创建全局负载均衡器。|
|internet-svcs.zones.load_balancers.update|更新全局负载均衡器。|
|internet-svcs.zones.load_balancers.delete|删除全局负载均衡器。|
|internet-svcs.load_balancers.monitors.create|创建运行状况监视器。|
|internet-svcs.load_balancers.monitors.update|更新运行状况监视器。|
|internet-svcs.load_balancers.monitors.delete|删除运行状况监视器。|
|internet-svcs.load_balancers.pools.create|创建全局负载均衡器池。|
|internet-svcs.load_balancers.pools.update|更新全局负载均衡器池。|
|internet-svcs.load_balancers.pools.delete|删除全局负载均衡器池。|


## 事件列表：清除高速缓存
{: #events_cache}

下表列出了与清除高速缓存相关并生成事件的操作：

|操作 |描述|
|---|---|  
|internet-svcs.zones.purge_cache.purge_all.update|清除边缘服务器中域的所有高速缓存资产。|
|internet-svcs.zones.purge_cache.purge_by_urls.update|按 URL 清除边缘服务器中高速缓存的资产。|
|internet-svcs.zones.purge_cache.purge_by_cache_tags.update|按高速缓存标记清除边缘服务器中高速缓存的资产。|
|internet-svcs.zones.purge_cache.purge_by_hosts.update|按主机名清除边缘服务器中高速缓存的资产。|


## 事件列表：页面规则
{: #events_page_rules}

下表列出了与页面规则相关并生成事件的操作：

|操作 |描述|
|---|---|  
|internet-svcs.zones.pagerules.create|创建页面规则。|
|internet-svcs.zones.pagerules.update|更新页面规则。|
|internet-svcs.zones.pagerules.delete|删除页面规则。|


## 事件列表：防火墙
{: #events_firewalls}

下表列出了与防火墙相关并生成事件的操作：

|操作 |描述|
|---|---|  
|internet-svcs.zones.firewall.waf.packages.groups.update|启用或禁用一组 WAF 规则集。|
|internet-svcs.zones.firewall.waf.packages.rules.update|启用或禁用 WAF 规则。|
|internet-svcs.zones.firewall.access_rules.rules.create|创建域级别 IP 防火墙规则。|
|internet-svcs.zones.firewall.access_rules.rules.update|更新域级别 IP 防火墙规则。|
|internet-svcs.zones.firewall.access_rules.rules.delete|删除域级别 IP 防火墙规则。|
|internet-svcs.firewall.access_rules.rules.create|创建实例级别 IP 防火墙规则。|
|internet-svcs.firewall.access_rules.rules.update|更新实例级别 IP 防火墙规则。|
|internet-svcs.firewall.access_rules.rules.delete|删除实例级别 IP 防火墙规则。|
|internet-svcs.zones.rate_limits.create|创建速率限制规则。|
|internet-svcs.zones.rate_limits.update|更新速率限制规则。|
|internet-svcs.zones.rate_limits.delete|删除速率限制规则。|
|internet-svcs.zones.ua_rules.create|创建用户代理程序阻止规则。|
|internet-svcs.zones.ua_rules.update|更新用户代理程序阻止规则。|
|internet-svcs.zones.ua_rules.delete|删除用户代理程序阻止规则。|
|internet-svcs.zones.firewall.lockdowns.create|创建域锁定规则。|
|internet-svcs.zones.firewall.lockdowns.update|更新域锁定规则。|
|internet-svcs.zones.firewall.lockdowns.delete|删除域锁定规则。|

## 事件列表：路由
{: #events_routing}

下表列出了与路由相关并生成事件的操作：

|操作 |描述|
|---|---|  
|internet-svcs.zones.routing.smart_routing.update	|启用或禁用智能路由。|
|internet-svcs.zones.routing.tiered_caching.update	|启用或禁用分层高速缓存。|

## 事件列表：证书包
{: #events_certificate_packs}

下表列出了与证书包相关并生成事件的操作：

|操作 |描述|
|---|---|  
|internet-svcs.zones.ssl.certificate_packs.create|订购专用证书。|
|internet-svcs.zones.ssl.certificate_packs.delete|删除专用证书。|


## 事件列表：定制证书
{: #events_custom_certificate}

下表列出了与定制证书相关并生成事件的操作：

|操作 |描述|
|---|---|  
|internet-svcs.zones.custom_certificates.create|上传定制证书。|
|internet-svcs.zones.custom_certificates.update|更新定制证书。|
|internet-svcs.zones.custom_certificates.delete|删除定制证书。|


## 事件列表：设置
{: #events_settings}

下表列出了与配置设置相关并生成事件的操作：

|操作 |描述|
|---|---|  
|internet-svcs.zones.settings.cache_level.update|更改高速缓存级别。|
|internet-svcs.zones.settings.browser_cache_ttl.update|更改浏览器高速缓存 TTL。|
|internet-svcs.zones.settings.development_mode.update|启用或禁用开发方式。|
|internet-svcs.zones.settings.security_level.update|更改安全级别。|
|internet-svcs.zones.settings.ssl.update|更改 SSL 设置。|
|internet-svcs.zones.settings.tls_1_2_only.update|启用或禁用 TLS 1.2 支持。|
|internet-svcs.zones.settings.waf.update|启用或禁用 Web 应用程序防火墙。|
|internet-svcs.zones.settings.cname_flattening.update|更改 CNAME 序列化设置。|
|internet-svcs.zones.settings.always_online.update|启用或禁用为域提供旧内容。|
|internet-svcs.zones.settings.sort_query_string_for_cache.update|启用或禁用在查询高速缓存中的内容时对查询自变量排序。|
|internet-svcs.zones.settings.tls_1_3.update|更改 TLS 1.3 设置。|
|internet-svcs.zones.settings.automatic_https_rewrites.update|启用或禁用自动 HTTPS 重写。
|internet-svcs.zones.settings.opportunistic_encryption.update|启用或禁用操作加密。|


## 在何处查找事件
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} 事件在 {{site.data.keyword.cloudaccesstrailshort}} **帐户域**中提供，该域在生成这些事件的 {{site.data.keyword.cloud_notm}} 区域中提供。



## 其他信息
{: #info}

在监视 IBM Cloud Internet Services (CIS) 生成的 {{site.data.keyword.cloudaccesstrailshort}} 事件并确定需要其他信息的 API 请求时，请检查事件中的 requestData 字段。开具支持凭单并包含 requestData 中提供的字段 **X-CORRELATION-ID** 的值。
