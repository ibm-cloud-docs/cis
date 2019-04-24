---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Web Application Firewall Concepts, web application firewall

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Web 應用程式防火牆概念問答集
{:#waf-q-and-a}

Web 應用程式防火牆可保護免受 ISO 第 7 層攻擊，這可能是最困難的部分。此文件提供部分詳細資料。

## 何謂「Web 應用程式防火牆 (WAF)」？
{:#what-is-a-waf}

WAF 或「Web 應用程式防火牆」透過過濾及監視 Web 應用程式與網際網路之間的 HTTP 資料流量，來協助保護 Web 應用程式。WAF 是 ISO 通訊協定第 7 層防禦（在 [OSI 模型 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://en.wikipedia.org/wiki/OSI_model) 中），其設計並不旨在防禦所有類型的攻擊。 

在 Web 應用程式前面部署 WAF，就像在 Web 應用程式與網際網路之間放了一塊盾牌。Proxy 伺服器會使用媒介來保護用戶端機器的身分（針對送出的資料流量），但 WAF 是一種反向 Proxy，可透過在到達伺服器之前讓用戶端的資料流量通過 WAF 來保護伺服器免於暴露（針對送入的資料流量）。

## WAF 可以防止哪些類型的攻擊？
{:#what-types-of-attacks-can-waf-prevent}

WAF 一般會保護 Web 應用程式免受跨網站偽造、跨網站 Script (XSS)、檔案併入及 SQL 注入等等這類攻擊。WAF 通常是工具套組的一部分，一起使用可以建立針對某範圍之攻擊向量的整體性防禦。

## WAF 如何運作？
{:#how-does-waf-work}

WAF 是透過一組通常稱為原則的規則進行操作。這些原則旨在過濾出惡意資料流量，以防範應用程式中的漏洞。 

WAF 的價值是源自可實作其原則修改的速度及簡易性，進而可更快速地回應各種攻擊向量。例如，在 [DDoS 攻擊 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://en.wikipedia.org/wiki/Denial-of-service_attack) 期間，修改 WAF 原則即可實作速率限制。

## IBM Cloud CIS Web 應用程式防火牆的主要優點為何？
{:#key-benefits-of-cis-waf}

IBM Cloud CIS WAF 是設定、管理及自訂安全規則以保護 Web 應用程式免於常見 Web 威脅的簡單方法。請參閱下列清單中的主要特性：

 * **簡易設定**：CIS WAF 是我們整體服務的一部分，只需要幾分鐘即可完成設定。將 DNS 重新導向我們之後，您就可以開啟 WAF 並設定您需要的規則。

 * **詳細報告**：請參閱報告中的更多詳細資料，例如，規則/規則群組所封鎖的威脅。 
