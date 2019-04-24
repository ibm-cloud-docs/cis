---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Bypass, header responses, brute-force login attempts

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# 速率限制
{:#cis-rate-limiting}

速率限制（仅限企业套餐）可防止拒绝服务攻击、暴力登录尝试以及针对应用程序层的其他类型的滥用行为。

选择速率限制规则的类型：**定制规则**或**保护登录**

## 创建定制速率限制规则
{:#create-a-custom-rate-limiting-rule}

输入规则名称以帮助您记住规则的功能。这是可选字段。

**流量匹配条件**使用 AND 运算。输入要进行速率限制的 URL，然后在来自**相同 IP 的请求数超过**指定的**每秒请求数**时，将触发指定的规则。

**高级条件**选项允许指定使用哪些 HTTP 方法、头响应和源响应代码以进一步限制匹配条件。 

从**方法**下拉列表中选择值（ANY 为缺省值）。  

更新 **HTTP 响应头**。您还可以**添加响应头**以包含源 Web 服务器返回的头。 

如果在 **HTTP 响应头**下有多个头，那么将应用 _AND_ 布尔值逻辑。要排除某个头而不予匹配，请使用_不等于_选项。另外，每个头必须是完全匹配。但是，区分大小写不适用。
{:note}

在**源响应代码**下，输入要匹配的每个 HTTP 响应代码的有效数字值。要包含两个或更多响应代码，请使用逗号分隔每个值。例如，如果只想考虑 401 和 403 这两个错误代码，那么可以输入 `401, 403`。 

### 配置响应
{:#rate-limiting-configure-response}

从列出的操作中进行选择，并指定超时时间段。在这种情况下，超时是指操作发生的禁止时间段。60 秒超时意味着该操作将应用 60 秒。

|操作 |描述|
|------|------------|
|阻止|在超过阈值时发出 429 错误|
|质询|在继续前，用户必须通过 Google reCaptcha 质询。如果成功，我们将接受请求。否则，请求将被阻止。| 	
|JS 质询|	在继续前，用户必须通过 Javascript 质询。如果成功，我们将接受请求。否则，请求将被阻止。|模拟|在活动环境中应用任何其他选项之前，可以使用此选项来测试规则。

**高级响应**

指定超过规则阈值时的响应类型。 

### 绕过
{:#rate-limiting-bypass}

通过绕过，可创建白名单等效项或者一组 URL 的例外。即使匹配“速率限制”规则，也不会针对这些 URL 触发任何操作。

## 保护登录
{:#rate-limiting-protect-login}

保护登录创建标准规则，用于保护登录页面免受暴力攻击。5 分钟内尝试登录 5 次以上的客户将被阻止 15 分钟。 

输入规则名称和登录 URL。
