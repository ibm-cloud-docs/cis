---
copyright:
  years: 2018
lastupdated: "2018-03-16"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# IBM Cloud Internet Services (CIS) 如何确保工作安全

IBM CIS 是全球分布式云服务，可阻止威胁和限制滥用机器人和搜寻器，而这些可能浪费您的带宽和服务器资源。IBM CIS 充当全球 HTTP(S) 逆向代理和受管 DNS 服务提供者。您的 Web 流量将流经我们的智能全球网络以优化性能和安全性。

![security-graphic.png](images/security-graphic.png)

以下是快速功能概述：

## 安全性功能

 * Web 应用程序防火墙 (WAF)
 * 无限制 DDoS 缓解

## 安全标准和平台

 * TLS（SHA2 和 SHA1）
 * IPv6
 * HTTP/2 和 SPDY

## DNS

 * 全球 anycast 网络
 * DNSSEC

## 网络攻击和缓解

通常，我们看到属于两个类别的攻击

| 第 3 层或第 4 层攻击| 第 7 层攻击|
|------------------------------|-----------------|
|这些攻击包括 ISO 第 3 层（网络层）流量攻击，例如，ICMP flood，或者第 4 层（传输层），例如，TCP SYN flood 或所谓 UDP flood|这些攻击会发送恶意 ISO 第 7 层请求（应用程序层）例如，GET flood。|
| 在边缘自动阻止| 我们通过“防御模式”、WAF 和“安全级别”设置来处理这些攻击|

## 摘要

 * “防御模式”测试众多恶意客户机缺乏的浏览器功能
 * WAF 阻止或质疑可能存在恶意的请求模式
