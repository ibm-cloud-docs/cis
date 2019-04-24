---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Web Application Firewall Concepts, web application firewall

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Web 应用程序防火墙概念常见问题及解答
{:#waf-q-and-a}

Web 应用程序防火墙可抵御 ISO 第 7 层攻击，这可能是最棘手的问题。本文档提供一些详细信息。

## 什么是 Web 应用程序防火墙 (WAF)？
{:#what-is-a-waf}

WAF 或 Web 应用程序防火墙通过过滤和监视 Web 应用程序与因特网之间的 HTTP 流量来帮助保护 Web 应用程序。WAF 是 ISO 协议第 7 层防御（在 [OSI 模型中 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://en.wikipedia.org/wiki/OSI_model)），而并非设计为抵御所有类型的攻击。 

在 Web 应用程序前部署 WAF 类似于在 Web 应用程序和因特网之间放置一个盾牌。代理服务器使用中介保护客户机的身份（对于出局流量），但是 WAF 为逆向代理类型，通过使客户机流量在到达服务器前流经 WAF 来保护服务器避免暴露（对于入局流量）。

## WAF 可阻止哪些类型的攻击？
{:#what-types-of-attacks-can-waf-prevent}

WAF 通常会保护 Web 应用程序免受以下攻击，诸如跨站点伪造、跨站点脚本 (XSS)、文件包含和 SQL 注入等。WAF 通常是工具套件的一部分，它们一起针对一系列攻击向量创建整体防护。

## WAF 如何工作？
{:#how-does-waf-work}

WAF 通过一组通常称为策略的规则运行。这些策略旨在通过过滤掉恶意流量来保护应用程序中的漏洞。 

WAF 的价值在于可快速且轻松地实施策略修改，因此允许更快地响应不断变化的攻击向量。例如，在 [DDoS 攻击 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://en.wikipedia.org/wiki/Denial-of-service_attack) 期间，可通过修改 WAF 策略来实施速率限制。

## IBM Cloud CIS Web 应用程序防火墙有哪些关键优点？
{:#key-benefits-of-cis-waf}

通过 IBM Cloud CIS WAF，可轻松设置、管理和定制安全规则，以保护 Web 应用程序免受常见 Web 威胁。请参阅以下列表以了解关键功能：

 * **轻松设置**：CIS WAF 是我们的整体服务的一部分，只需几分钟即可进行设置。将您的 DNS 重定向到我们后，就可以开启 WAF 并设置所需的规则。

 * **详细报告** 在报告中查看更多详细信息，例如，规则/规则组所阻止的威胁。 
