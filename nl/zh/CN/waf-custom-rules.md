---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: WAF Custom Rules, Custom WAF Rules

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# WAF 定制规则
{:#waf-custom-rules}

通过**安全性 > Web 应用程序防火墙 > 定制规则**导航至“定制 WAF 规则”。“WAF 规则”适用于企业套餐，并根据客户的独特需求和/或其 Web 站点的流量模式进行创建。这意味着您可以要求我们阻止请求的几乎任何特征组合。 

“定制 WAF 规则”适合 IBM WAF 尚未提供规则以及攻击者使用特定模式或用户代理（专门针对您的 Web 站点的结构）的情况。在这些情况下，您可以针对 Web 属性创建定制规则。

## 请求定制规则
{:#request-a-custom-rule}

要请求规则，请发送电子邮件至 wafsup@us.ibm.com，并在电子邮件中包含规则需求或流量模式。 

请提供尽可能多的信息，包括：
* 显示约 100 个嫌疑恶意请求的样本的访问日志。
* 样本 POST 请求，包括 POST 数据（如果请求具有 POST 主体），以确定请求是否包含我们可阻止或触发的任何内容。
* 您是希望直接阻止请求，还是对请求进行质询，以防潜在误报。
* 要应用这些规则的特定域。
* 您希望缺省情况下是开启还是关闭这些规则。

创建定制 WAF 规则后，必须启用所有定制规则以使它们生效。
{:note}
