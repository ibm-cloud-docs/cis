---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: edge functions beta, edge functions

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Edge Functions (Beta)
{: #edge-functions}

CIS Edge Functions 通过使用无服务器执行环境，允许您创建新应用程序或修改现有应用程序，而不必配置或维护基础架构。可定义 Edge Functions 并将其上传到 Cloud Edge 以在请求到达源之前进行处理。CIS Edge Functions 可用于修改 HTTP 请求和响应，发出并行请求或者从 Cloud Edge 生成响应。

## Edge Functions 工作方式
{: #how-edge-functions-work}

Edge Functions 根据定义的域将**操作**与 URI 相关联。此关联称为**触发器**。将在云边缘拦截站点的入局请求，并针对帐户或域中的触发器进行匹配。如果请求 URL 匹配触发器的 URI，那么将执行与触发器相关联的操作。

Edge Functions 在现代 Web 浏览器中可用的 [Service Worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) 上建模，并且尽可能使用相同的 API。

Service Worker API 允许拦截对站点发出的任何请求。在 JavaScript 处理请求后，可以选择向您的站点或其他站点发出任意数量的子请求，并最终将任何想要的响应返回给访问者。

与标准 Service Worker 不同，Edge Functions 在 CIS Edge 服务器上运行，而不是用户的浏览器中。这意味着您可以确信您的代码将在恶意客户机无法绕过该代码的可信环境中运行。还意味着用户不需要使用支持 Service Worker 的现代浏览器 - 您甚至可以拦截来自根本不是浏览器的 API 客户机的请求。

在内部，Edge Functions 使用 Google Chrome 浏览器中所使用的相同 V8 JavaScript 引擎，以在我们的基础架构上运行工作程序。V8 动态地将 JavaScript 代码编译为超快速机器代码，从而实现高性能。这允许在微秒级别执行代码，并且允许 Edge 每秒执行数以千计的脚本。

虽然 Edge Functions 使用 V8，但不使用 Node.js。工作程序内可供您使用的 JavaScript API 由我们直接实现。直接使用 V8 将允许代码通过保证客户和基础架构安全所需的安全性控制更高效地运行。


## 操作
{: #edge-functions-actions}

操作使用 JavaScript 编写，并且需要事件侦听器以响应触发器事件。除非由触发器使用，否则操作将不会影响流量。

### 企业套餐与标准套餐
{: #edge-functions-enterprise-v-standard-plans}

标准套餐最多有一个操作。操作分配有与域相同的名称。您可以通过上传另一个文件来替换操作，或使用代码编辑器更新操作。上传另一个文件将除去现有操作。

企业套餐可上传无限数量的脚本。可以为这些脚本指定唯一名称。

### 创建操作
{: #edge-functions-create-actions}

选择**创建**以使用代码编辑器添加操作。在企业套餐中，输入操作的名称。在标准套餐中，名称不可编辑，并且设置为域的名称。添加 Javascript 代码后，选择**保存**以创建操作。

### 上传操作
{: #edge-functions-upload-actions}

使用**上传**按钮以上传 Javascript 文件。在企业套餐中，操作的名称是文件的名称。在标准套餐中，操作名称设置为域的名称。

上传或创建与现有操作同名的操作将导致覆盖现有操作。在上传之前重命名操作文件，或者在创建时在文本输入中输入唯一名称以避免此行为。
{:note}

### 编辑操作
{: #edge-functions-edit-actions}

选择操作会在编辑器中打开操作以进行修改。每当保存更改时，都会将操作上传到 Cloud Edge。更新后，选择**保存**。如果操作正在使用中，那么更改将立即生效。 

### 删除操作
{: #edge-functions-delete-actions}

通过单击**操作**表中的**删除**图标，删除操作。无法删除正在使用的操作。要删除操作，请首先将其从触发器中除去。**使用**列显示与此操作相关联的触发器的数量。删除无法撤销。


### 关联的触发器
{: #edge-functions-associated-triggers}

添加触发器并将其与操作相关联。

### Edge Functions 已知限制
{: #edge-functions-known-limitations}

上传与现有操作同名的操作。这将覆盖现有操作。在上传前重命名操作文件以避免此行为。


## 触发器
{: #triggers}

### 关于触发器
{: #about-triggers}

触发器（路由）确定到操作的域流量路由。触发器基于帐户上的域将特定 URL 模式与预定义的操作相关联。URL 必须包含域，但是可以包含通配符作为域前缀或者在路径末尾包含通配符。如果未在模式上给定路径，那么会隐式添加 `/`。URL 模式不能包含中缀通配符或查询参数。

您必须添加域以添加触发器。您可以在没有操作的情况下添加触发器。

### 添加触发器

{: #add-triggers}

转至**触发器**选项卡，然后单击**添加触发器**。输入 URL 模式，然后从现有操作列表中选择操作。 

对于操作，您还可以选择**避免 Edge Functions**。这允许触发器的路径保持活动状态，但避免使用任何 Edge Functions 操作。例如，存在名为 `my-function` 的操作以及路径为 `beta.cistest-load.com/*` 的触发器。如果路径 `beta.cistest-load.com/data` 不应使用操作 `my-function`，请使用路径 `beta.cistest-load.com/data` 和选项**避免 Edge Functions** 创建另一个触发器。这允许路径 `beta.cistest-load.com/data` 保持活动状态而不使用操作 `my-function`。

### 编辑触发器
{: #edit-triggers}

使用选中触发器的表行中的菜单选项来更新触发器。更新后，选择**保存**。

### 删除触发器
{: #delete-triggers}

使用选中触发器的表行中的菜单选项来删除触发器。该操作无法撤销。


## 用例
{: #edge-functions-use-cases-examples}

这些示例仅用于演示目的，而不用于生产。
{:important}
* [A/B 测试](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#ab-testing)
* [添加响应头](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#add-response-header)
* [聚集多个请求](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#aggregate-multiple-requests)
* [条件路由](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#conditional-routing)
* [热链接保护](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#hot-link-protection)
* [无源响应](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#originless-responses)
* [Post 请求](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#post-requests)
* [设置 Cookie](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#setting-cookies)
* [已签名请求](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#signed-requests)
* [以流式方法传递响响应](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#streaming-responses)
