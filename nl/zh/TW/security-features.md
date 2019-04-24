---
copyright:
  years: 2018
lastupdated: "2018-03-16"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# IBM Cloud Internet Services (CIS) 如何保持工作安全

IBM CIS 是一種廣域分散式雲端服務，可封鎖威脅，以及限制浪費頻寬和伺服器資源的濫用機器人及搜索器。IBM CIS 作為廣域 HTTP(S) 反向 Proxy 及受管理 DNS 服務提供者。Web 資料流量會透過智慧型廣域網路進行遞送，以最佳化效能及安全性。

![security-graphic.png](images/security-graphic.png)

以下是快速特性概觀：

## 安全特性

 * Web 應用程式防火牆 (WAF)
 * 無限制 DDoS 降低

## 安全標準及平台

 * TLS（SHA2 及 SHA1）
 * IPv6
 * HTTP/2 及 SPDY

## DNS

 * 廣域 Anycast 網路
 * DNSSEC

## 網路攻擊及降低

一般而言，攻擊分成兩種種類：

| 第 3 層或第 4 層攻擊       | 第 7 層攻擊     |
|------------------------------|-----------------|
|這些攻擊包含 ISO 第 3 層（網路層）（例如 ICMP 洪水）或第 4 層（傳輸層）（例如 TCP SYN 洪水或反映的 UDP 洪水）的大量資料流量|這些攻擊會傳送惡意 ISO 第 7 層要求（應用程式層），例如 GET 洪水。|
| 在邊緣自動封鎖| 我們使用「防禦模式」、WAF 及「安全層次」設定來處理這些攻擊|

## 摘要

 * 「防禦模式」可測試許多惡意用戶端缺乏的瀏覽器特性
 * WAF 會封鎖或盤查可能為惡意的已知要求型樣
