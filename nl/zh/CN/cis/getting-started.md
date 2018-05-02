---
copyright:
  years: 2018
lastupdated: "2018-03-19"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# IBM Cloud Internet Services (CIS) 入门

IBM Cloud Internet Services (CIS) 提供三种主要功能来增强工作流程：[安全性](/docs/infrastructure/cis/managing-for-security.html)、[可靠性](/docs/infrastructure/cis/managing-for-reliability.html)和[性能](/docs/infrastructure/cis/managing-for-performance.html)。一旦您打开了 IBM CIS 应用程序，就会在屏幕的左侧导航栏中显示每个功能区域。

对于每个功能，IBM CIS 将帮助您调整其功能以满足您的特定需求，包括：

 * 授权 DNS 服务器
 * 全局负载均衡和局部负载均衡
 * Web 应用程序防火墙 (WAF)
 * DDoS 保护
 * 高速缓存和页面规则



## 开始之前
开始使用 IBM CIS 之前，首先会需要 [IBMid](https://www.ibm.com/account/us-en/signup/register.html)。然后，可以根据您的偏好通过 IBM Cloud Account 或者通过新 [IBM Cloud Internet Services Portal](https://console.bluemix.net/catalog/services/internet-services) 订购服务。

如果在获取帐户以使用 IBM Cloud Internet Services 时需要帮助，请[联系您的 IBM 销售代表](https://www.ibm.com/cloud-computing/bluemix/contact-us)以获取其他入门指南。

如果具有现有 Softlayer 帐户，那么可以将[您的帐户链接](https://console.bluemix.net/docs/account/softlayerlink.html#unifyingaccounts) IBMid。 

## 流程概述

只需几个步骤就可以开始将 IBM CIS 用于因特网流量。

 * 从 IBM Cloud 仪表板打开 IBM CIS 应用程序。
 * 添加要管理的域。
 * 使用我们提供的名称服务器来配置 DNS 信息。
 * 通过遵循教程或设置其他功能，继续开始使用 IBM CIS。

### 步骤 1：打开 IBM CIS 应用程序

打开 [IBM Cloud 仪表板](https://console.bluemix.net/catalog/)。然后，通过在仪表板的左侧导航栏中选择**平台 > 网络**类别来浏览至 IBM CIS 应用程序图标。通过单击屏幕中间附近的图标，打开 IBM Cloud Internet Services 应用程序。 

![目录](images/catalog-cis-tile.png)

**概述屏幕**

IBM CIS 应用程序启动后，会显示 IBM CIS **概述**屏幕，可在 UI 显示屏左侧区域上找到**安全性**、**可靠性**和**性能**选项卡。

**我选择什么套餐？**

针对 _Early Access_ 发行版，只有一个套餐可供选择，也是免费套餐。单击“**概述**”屏幕左下方的**创建**按钮以开始供应帐户。

**开始供应**

将看到 IBM CIS 应用程序的第一个屏幕，可在其中选择**添加域**按钮以开始。

|**请注意，Early Access 计划仅限每个帐户一个实例。**|
|-------------------------------------------------------------------|
| 创建资源实例并向其添加域后，不允许为 IBM CIS 添加新资源实例。即使您删除了一个试用域，然后再次尝试将域添加到同一资源实例，也会强制实施此限制。如果您尝试这样做，那么会遇到错误。|

### 步骤 2 添加并配置您的域。

通过输入域或子域，开始保护和提高 Web Service 的性能。

**注：**指定 DNS 区域。您可以在域的注册器或 DNS 提供者处配置这些域或子域的名称服务器。请勿使用 CNAME。

![入门](images/overview-add-domain.png)
“概述”屏幕将显示域处于`暂挂`状态。在完成步骤 3 之前，您的域将保持为`暂挂`状态。

**注：**添加域后，无法删除 IBM CIS 实例。要删除该实例，请先从实例中删除该域。

### 步骤 3 使用注册器或现有 DNS 提供者配置您的名称服务器。

要开始享受 IBM CIS 的优势，请配置注册器或域名提供者以使用所列示的名称服务器。如果您正在委托域（例如，`example.com`），请在域的设置中配置所列示的名称服务器，这些服务器由您的注册器（例如，在注册器的 Web 门户网站上）进行管理。如果您不确定自己的域的注册器，那么可以在 https://whois.icann.org⁄上查看。如果您从另一个 DNS 提供者委派子域（例如，`subdomain.example.com`），那么必须为每个列出的名称服务器添加名称服务器 (NS) 记录。

配置注册器或 DNS 提供者后，可能需要最多 24 小时才能使更改生效。确认为域或子域正确配置了指定的名称服务器后，该域的状态将从`暂挂`更改为`活动`。配置名称服务器后，单击`概述`页面中的“重新检查名称服务器”链接，可能会加速激活域（每小时只能提交此检查一次）。

### 步骤 4 确保 IBM Cloud Internet Services 解析应用程序、主机名或 Web 站点的域信息。

要继续，请从左侧导航栏中选择**可靠性**选项卡，然后选择 **DNS** 选项。确保添加适当的 _DNS 记录_。添加 **A 记录** 以及任何已填充的 **AAAA** 或 **MX** 条目。如果您忘记在注册器的授权完成之前添加这些记录，那么 IBM Cloud Internet Services 无法解析面向因特网的应用程序的域信息。  

![入门](images/dns-records.png)

### 步骤 5 在此期间，可以开始管理其他 IBM CIS 功能和功能部件。

有关管理其他功能和功能部件的更多详细信息，请参阅[逐步指示信息](/docs/infrastructure/cis/how-to.html)。
