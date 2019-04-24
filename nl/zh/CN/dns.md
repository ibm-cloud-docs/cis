---

copyright:
  years: 2018
lastupdated: "2018-03-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# 为 IBM CIS 设置域名系统 (DNS)

本文档包含有关如何配置 IBM CIS DNS 记录（包括如何配置安全 DNS）的一些具体指示信息。

## 安全 DNS

**DNSSec** 是一种用于对 DNS 数据进行数字签名以确保其有效的技术。要消除来自因特网的漏洞，必须在查找的每个步骤中部署 DNS，此查找范围从根区域到最终域名（例如 www.icann.org）。

## 配置和管理安全 DNS 

DNSSec 向因特网的 DNS 基础结构添加一层认证以确保安全。安全 DNS 可保证访客在将域名输入到 Web 浏览器时会定向到**您的** Web 服务器。只需从 IBM CIS 帐户在 DNS 页面中启用 DNSSec ，然后将 DS 记录添加到注册器。

![安全 DNS](images/dns/secure-dns.png)

可以选择**查看 DS 记录**按钮以打开一个对话框，该对话框说明如何向注册器添加 DS 记录。必须复制 DS 记录部分，并将其粘贴到注册器的仪表板。每个注册器都不同，您的注册器可能只需要您在某些可用字段输入信息。

## 添加 DNS 记录

您可以使用**类型**下拉菜单，选择要创建的记录的类型。每种 DNS 记录类型都有关联的“名称”和“生存时间 (TTL)”。 

除非已在“名称”字段中手动追加域名（例如，如果在此字段中输入 `www` 或 `www.example.com`，API 将这两者一起处理为 `www.example.com`），否则会向在此字段中输入的任何内容追加域名。如果在“名称”字段中输入精确域名，那么不会向其追加域名（例如，`example.com` 会处理为 `example.com`）。但是，DNS 记录的列表在显示名称时不会跟踪域名，因此 `www.example.com` 将显示为 `www`，而 `example.com` 将显示为 `example.com`。TTL 将具有缺省值 `Automatic`，但用户可进行更改。代理的 DNS 记录的 TTL 值始终为 `Automatic`，因此在此更改期间，新代理的记录将更改为此配置。

### “类型”记录

要添加此记录类型，**名称**和 **IPv4 地址**字段中必须存在有效值。也可以从下拉菜单中指定 **TTL**，缺省值为“Automatic”。

![创建类型记录](images/dns/create-a-type-record.png)

    必填字段：名称、IPv4 地址
    可选字段：TTL（缺省值为“Automatic”）

### AAA 类型记录

要添加此记录类型，**名称**和 **IPv6 地址**字段中必须存在有效值。也可以从下拉菜单中指定 **TTL**，缺省值为“Automatic”。

![创建 AAAA 类型记录](images/dns/create-aaaa-type-record.png)

    必填字段：名称、IPv6 地址
    可选字段：TTL（缺省值为“Automatic”）

### CNAME 类型记录

要添加此记录类型，**名称**字段中必须存在有效值，**域名** (FQDN) 字段中必须存在标准域名。也可以从下拉菜单中指定 **TTL**，缺省值为“Automatic”。


![创建 CNAME 类型记录](images/dns/create-cname-type-record.png)

    必填字段：名称、域名（针对 CNAME）
    可选字段：TTL（缺省值为“Automatic”）


### MX 类型记录

要添加此记录类型，**名称**字段中必须存在有效值，**邮件服务器**字段中必须存在有效地址。也可以从下拉菜单中指定 **TTL**，缺省值为“Automatic”。

![创建 MX 类型记录](images/dns/create-mx-type-record.png)

    必填字段：名称、邮件服务器
    可选字段：TTL（缺省值为 Automatic）、属性（缺省值为 1）

### LOC 类型记录

要添加此记录类型，**名称**字段中必须存在有效值。如果需要更具体的信息，请选择**配置 LOC 选项**按钮。也可以从下拉菜单中指定 **TTL**，缺省值为“Automatic”。

![创建 LOC 类型记录](images/dns/create-loc-type-record-1.png)

    必填字段：名称
    可选字段：LOC 选项（单击此按钮以进行配置）

![创建 LOC 类型记录](images/dns/create-loc-type-record-2.png)

### CAA 类型记录

要添加此记录类型，**名称**和**值**字段中必须存在有效值。“值”字段将与**标记**下拉字段的值相关，缺省情况下，该字段为“将违例报告发送到 URL”。也可以从下拉菜单中指定 **TTL**，缺省值为“Automatic”。

![创建 CAA 类型记录](images/dns/create-caa-type-record.png)

    必填字段：名称、值（与标记关联）
    可选字段：TTL（缺省值为 Automatic），标记（缺省值为“将违例报告发送到 URL”）

### SRV 类型记录

要添加此记录类型，**名称**、**服务名称**和**目标**字段中必须存在有效值。使用下拉菜单来选择**协议**，缺省情况下，为 UDP 协议。此外，可以指定**优先级**、**权重**和**端口**。这三个字段缺省值为 1。还可以从下拉菜单中指定 **TTL**，缺省值为“Automatic”。

![创建 SRV 类型记录](images/dns/create-srv-type-record.png)

    必填字段：名称、服务名称、目标
    可选字段：TTL（缺省值为 Automatic）、协议（缺省值为 UDP）、优先级（缺省值为 1）、权重（缺省值为 1）、端口（缺省值为 1）

### SPF 类型记录

要添加此记录类型，**名称**和**内容**字段中必须存在有效值。也可以从下拉菜单中指定 **TTL**，缺省值为“Automatic”。

![创建 SPF 类型记录](images/dns/create-spf-type-record.png)

    必填字段：名称、内容
    可选字段：TTL（缺省值为 Automatic）

### TXT 类型记录

要添加此记录类型，**名称**和**内容**字段中必须存在有效值。也可以从下拉菜单中指定 **TTL**，缺省值为“Automatic”。

![创建 TXT 类型记录](images/dns/create-txt-type-record.png)

    必填字段：名称、内容
    可选字段：TTL（缺省值为 Automatic）

### NS 类型记录

要添加此记录类型，**名称**和**名称服务器**字段中必须存在有效值。也可以从下拉菜单中指定 **TTL**，缺省值为“Automatic”。

![创建 NS 类型记录](images/dns/create-ns-type-record.png)

    必填字段：名称、名称服务器
    可选字段：TTL（缺省值为 Automatic）

## 更新 DNS 记录

在每个记录行中，可以单击菜单中的**编辑记录**选项，这将打开一个对话框，可使用此对话框来更新记录。

![编辑 DNS 记录](images/dns/edit-dns-record.png)

例如，这是 **A** 类型记录的更新对话框。完成更改后，选择**更新记录**以保存更改。

![编辑 DNS 记录对话框](images/dns/update-dns-dialog.png)

## 删除记录

在每个记录行中，可以从菜单中选择**删除记录**选项，这将打开一个对话框，可使用此对话框来确认删除过程。

![删除 DNS 记录](images/dns/delete-record.png)

可以选择**删除**按钮来确认删除操作。如果不希望删除，请选择**取消**。

![删除 DNS 记录对话框](images/dns/delete-record-dialog.png)
