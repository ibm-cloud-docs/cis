---

copyright:
  years: 2018
lastupdated: "2018-03-22"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# API 规范

以下提供了如何查看 CIS API 规范的方法： 

1. 要查看 CIS API，请浏览至 [CIS API 规范](https://console.bluemix.net/apidocs/2640-cloud-internet-services)页面。 

2. 从左侧导航菜单中的可用 API 列表中进行选择。


## 注

1. API 端点：https://api.cis.cloud.ibm.com。

2. 每个 API 调用都需要 **X-Auth-User-Token** 头。这是可从 IAM 检索到的用户的不记名令牌，例如，使用“bx iam oauth-tokens”命进行检索）。

3. 每个 API 调用的路径中也需要 **crn** 字段。这是正在配置的 CIS 资源实例的完整云资源名称 (CRN)（例如，可以使用命令“bx resource service-instance <instances-name>”从其名称中检索资源实例的 CRN）。CRN 必须是在 API 调用中编码的 URL。

4. API 调用的速率有限。在 1 分钟内总共可以进行 100 个 API 调用。如果超过此速率，那么后续调用将在一段时间内被阻塞。
