---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: OWASP Rule Set, Rule Set

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# WAF 的 OWASP 规则集
{:#owasp-rule-set-for-waf}

“OWASP 规则集”包含通用攻击检测规则。OWASP 规则可防止许多常见攻击类别，包括“SQL 注入”、“跨站点脚本编制”和“语言环境文件包含”等。IBM CIS 提供但不组织这些规则。OWASP 是一种业界标准，可提供优秀安全性基线。请参阅以下链接以获取更多信息：
  * [Github 上的 OWASP](https://github.com/SpiderLabs/owasp-modsecurity-crs)
  * [OWASP.org](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project)

## 管理 OWASP
{:#managing-owasp}

与 [CIS 规则集](/docs/infrastructure/cis?topic=cis-cis-rule-set-for-waf)不同，OWASP 允许设置敏感度。
请求可能触发一组 OWASP 规则，这些规则具有与之相关联的从高到低严重性分数。根据触发的所有规则计算最终分数。计算最终分数后，CIS 会将其与开始时选择的敏感度阈值进行比较，然后阻止或允许请求。

|敏感度分数|触发器阈值|
|------|---------------|
|低|60 和更高|
|中|40 和更高|
|高|25 和更高|

建议您将 OWASP 敏感度设置为`低`。如果将其设置为`高`，请检查 CIS 上的日志，并微调 OWASP 规则集以使其适合您的应用程序。

请记住，OWASP 规则只能_开启_或_关闭_，这不同于 CIS 规则集内的规则，后者可设置为_禁用_、_模拟_、_质询_或_阻止_。

## 如何处理误报？
{:#owasp-false-positives}

当变量或值求值为 _true_ 或_肯定_，但实际为否定时，可能发生误报。在 WAF 的上下文中，误报意味着请求由于被误评估为恶意而被阻止。

为处理误报并确保未来避免这些误报，您必须了解如何加以识别和更正。查看已阻止的请求的日志，然后评估在 Web 站点的预期流量和正常流量的上下文内，这些请求是否被合理阻止。
