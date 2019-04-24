---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: domain name system, DNS servers, match domain names, DNS Concepts

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}


# DNS 概念
{:#dns-concepts}

本文档包含与因特网的域名系统 (DNS) 相关的一些概念和定义，以及它如何影响 IBM Cloud Internet Services (CIS) 部署。 

域名系统 (DNS) 为常用的 Web 提供支持。此系统在后台透明地运行，将人类可读的 Web 站点名称转换为计算机可读的数字 IP 地址，该 IP 地址遵循 [RFC 1918 因特网准则（针对 IPv4）和 RFC 4193（针对 IPv6）](https://en.wikipedia.org/wiki/Private_network)。简而言之，DNS 服务器将域名（如 `ibm.com`）与其关联 IP 地址（大多数人不需要知道）相匹配。

DNS 系统在通过因特网链接的 DNS 服务器的网络上查找此 IP 地址和主机名信息，这与用户使用电话簿或地图查找某个位置的方式类似。

## 名称服务器
{:#dns-concepts-nameservers}

**名称服务器**实现提供针对目录服务的查询响应的服务。此服务器将有意义的基于文本的 Web 或主机标识符转换为 IP 地址。

**名称服务器授权**是指域的名称服务器接收子域记录的请求并以名称服务器与代理服务器的引用进行响应。此功能使您能够将大型域（例如，`ibm.com`）的管理分散。

**定制域名服务器**允许您将 DNS 提供者的服务器与您自己域的定制引用名称配合使用。例如，可以将您的名称服务器定义为 `ns1.cloud.ibm.com`，而不是 `ns1.acme.com`。

## 安全 DNS
{:#dns-concepts-secure-dns}

**DNSSec** 是一种用于对 DNS 数据进行数字签名以确保其有效的技术。要消除来自因特网的漏洞，必须在查找的每个步骤中部署 DNSSec，从根区域到最终域名（例如 www.icann.org）都要部署。

## 根记录 CNAME 序列化
{:#dns-concepts-root-record-cname-flattening}

IBM CIS 支持名为“CNAME 序列化”的功能。使用此方法，根记录可克服 IETF RFC 限制，即如果根记录为 CNAME，那么该域不能有任何其他记录。CIS 授权服务器通过返回与 CNAME 目标相对应的 A 记录来克服此限制，而不是返回 CNAME 本身，从而有效地隐藏 CNAME。此方法允许将其他记录（例如，MX 记录）添加到域，尽管根记录为 CNAME。

## 代理 DNS 记录
{:#dns-concepts-proxying-dns-records}

IBM CIS 支持切换是否代理记录。当代理记录时，意味着其流量将直接通过 IBM CIS 运行。目前，可代理类型为 **A**、**AAAA** 或 **CNAME** 的记录。
