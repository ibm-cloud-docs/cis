---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: CIS Rule Set, WAF settings, WAF CIS Rules

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# WAF 设置
{:#waf-settings}

下表显示 Web 应用程序防火墙 (WAF) 可执行的操作。 


|操作 |定义
|
|---|---|
|阻止|阻止攻击将停止任何操作，以防将其发布到 Web 站点。|
|模拟|要测试误报，请将 WAF 设置为模拟方式，这将记录可能攻击的响应，而不进行质询或阻止。|
|质询|质询页面要求访问者提交 CAPTCHA 才能继续访问 Web 站点。|
|阈值或敏感度设置|根据敏感度，设置规则以触发更多或更少。|

## WAF 的 CIS 规则集
{:#cis-ruleset-for-waf}

选择**查看 CIS 规则**以显示此包的规则集。规则集如下：
  * Drupal
  * Flash
  * Joomla
  * Magento
  * Miscellaneous
  * PHP
  * Plone
  * Specials
  * WHMCS
  * Wordpress

**Specials** 包含适用于因特网上的几乎所有应用程序和 Web 站点的若干规则。此规则集是 WAF 提供的安全性的核心，包含针对常见攻击（例如，SQLi、XSS 和 LFI）的规则。建议始终将 Specials 保持为“已启用”。

仅启用与您的技术堆栈相对应的规则集。例如，如果使用 Wordpress，但不使用任何其他技术，请仅启用 Specials 和 Wordpress 规则集。避免启用与技术堆栈无关的规则集。

选择任何特定规则集以查看有关所包含的每个规则的进一步详细信息。

CIS 规则集允许对每个规则执行四个操作：
  1. **禁用**：关闭规则。
  2. **模拟**：记录事件并且不阻止或质询访问者（在查看日志后，您仍可以决定设置为阻止或质询）。
  3. **阻止**：阻止会径直阻止整个请求，而没有任何选项可针对该请求绕过阻止。
  4. **质询**：显示质询 (CAPTCHA) 页面，必须完成该页面才能允许相关请求进行访问。

您可能会注意到，规则名称并未准确揭示其工作方式，而且名称主要是其功能的一般摘要。这是有意为之。出于安全目的，我们不会揭示用于过滤流量的代码（或其他确切信息)。这可防止恶意参与者进行逆向工程，从而绕过我们的防御。
