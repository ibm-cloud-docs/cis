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

此文件包含網際網路之網域名稱系統 (DNS) 的一些相關概念及定義，以及它對 IBM Cloud Internet Services (CIS) 部署的影響。 

「網域名稱系統 (DNS)」支援我們每天使用的 Web。它可以在背景透明地運作，並將人類可讀網站名稱轉換為遵循[網際網路的 RFC 1918 準則（適用於 IPv4）及 RFC 4193 準則（適用於 IPv6）](https://en.wikipedia.org/wiki/Private_network)的電腦可讀取數值 IP 位址。簡言之，DNS 伺服器會比對網域名稱（例如 `ibm.com`）與其相關聯的 IP 位址（大多數人並不需要知道）。

DNS 系統會在網際網路的已鏈結 DNS 伺服器網路上查閱此 IP 位址及主機名稱資訊，這與人員如何使用電話簿或地圖來尋找某個位置類似。

## 名稱伺服器
{:#dns-concepts-nameservers}

**名稱伺服器**可實作提供目錄服務查詢之回應的服務。它會將有意義的文字型 Web 或主機 ID 轉換為 IP 位址。

網域的名稱伺服器收到子網域記錄的要求並回應名稱伺服器的委派伺服器參照時，會進行**名稱伺服器委派**。此功能可讓您分散大型網域（例如 `ibm.com`）的管理。

**自訂網域名稱伺服器**可讓您使用專屬網域的自訂參照名稱來利用 DNS 提供者的伺服器。例如，您可以將名稱伺服器定義為 `ns1.cloud.ibm.com`，而非 `ns1.acme.com`。

## 安全 DNS
{:#dns-concepts-secure-dns}

**DNSSec** 是一種技術，可數位「簽署」DNS 資料，讓您可以確定它是有效的。若要消除網際網路的漏洞，必須在查閱（從根區域到最終網域名稱（例如 www.icann.org））的每一個步驟上部署 DNSSec。

## Root 記錄的 CNAME 壓縮
{:#dns-concepts-root-record-cname-flattening}

IBM CIS 支援一種稱為「CNAME 壓縮」的特性。使用此方法，Root 記錄可以克服 IETF RFC 限制，亦即，如果 Root 記錄是 CNAME，則它不能具有該網域的任何其他記錄。CIS 主伺服器克服此限制的方式是傳回對應於 CNAME 目標的 A 記錄，而不是傳回 CNAME 本身，因而有效地隱藏 CNAME。此技術容許將其他記錄（例如 MX 記錄）新增至該網域，即使 Root 記錄是 CNAME 也一樣。

## 對 DNS 記錄進行 Proxy 處理
{:#dns-concepts-proxying-dns-records}

IBM CIS 支援切換是否對記錄進行 Proxy 處理的能力。對記錄進行 Proxy 處理時，表示其資料流量將直接透過 IBM CIS 執行。目前，**A**、**AAAA** 或 **CNAME** 類型的記錄可以進行 Proxy 處理。
