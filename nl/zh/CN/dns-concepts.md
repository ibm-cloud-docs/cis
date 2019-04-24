---

copyright:
  years: 2018
lastupdated: "2018-03-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}


# DNS 概念

本文档包含与因特网的域名系统 (DNS) 相关的一些概念和定义，以及它如何影响 IBM Cloud Internet Services (CIS) 部署。 

域名系统 (DNS) 为常用的 Web 提供支持。此系统在后台透明地运行，将人类可读的 Web 站点名称转换为计算机可读的数字 IP 地址，该 IP 地址遵循 [RFC 1918 因特网准则（针对 IPv4）和 RFC 4193（针对 IPv6）](https://en.wikipedia.org/wiki/Private_network)。简而言之，DNS 服务器将域名（如“ibm.com”）与其关联 IP 地址（大多数人不需要知道）相匹配。

DNS 系统在通过因特网链接的 DNS 服务器的网络上查找此 IP 地址和主机名信息，这与用户使用电话簿或地图查找某个位置的方式类似。

## 名称服务器
**名称服务器**实施的服务能够对目录服务的查询提供响应。此服务器将基于文本的有含义的 Web 或主机标识符转换为 IP 地址。

**名称服务器授权**发生的情况是：某个域的名称服务器收到对子域记录的请求，然后以对代理服务器的引用作为响应。此功能使您能够将大型域（例如，`ibm.com`）的管理分散。

**定制域名服务器**允许您将 DNS 提供者的服务器与您自己域的定制引用名称配合使用。例如，可以将您的名称服务器定义为 `ns1.cloud.ibm.com`，而不是 `ns1.acme.com`。

## 安全 DNS

**DNSSec** 是一种用于对 DNS 数据进行数字签名以确保其有效的技术。要消除来自因特网的漏洞，必须在查找的每个步骤中部署 DNS，此查找范围从根区域到最终域名（例如 www.icann.org）。
