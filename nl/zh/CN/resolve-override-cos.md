---

copyright:
  years: 2019
lastupdated: "2019-03-28"

keywords: resolve override, Cloud Object Storage, bucket resource

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# 使用 COS 解析覆盖
{: #resolve-override-cos}

## 用例
{: #cos-use-cases}

将匹配页面规则的请求解析为 Cloud Object Storage (COS) 存储区资源。


## 先决条件
{: #cos-prerequisites}

以下步骤假定您有具有公共访问权的现有 COS 实例和存储区。有关公共访问权的信息，请参阅[允许公共访问](/docs/services/cloud-object-storage/iam?topic=cloud-object-storage-allowing-public-access)。


## 创建页面规则步骤
{: #cos-create-page-rule}

* 导航至**性能 -> 页面规则**。
* 单击**创建规则**按钮。
* 输入 URL 匹配所需的值。例如，`*.foo.com/*`。
  * 请注意，URL 匹配必须与 COS 对象名相匹配。
  * 例如，如果在存储区 `my-bucket1` 下有一个名为 reports.txt 的对象，那么以下两个 URL 匹配都将有效：
    * `*.foo.com/*`
    * `*.foo.com/reports.txt`
* 使用下拉菜单以选择**性能**部分下的**使用 COS 解析覆盖**。section.
* 使用 **Cloud Object Storage 实例**下拉列表以选择期望的实例。
* 使用**存储区**下拉列表以选择期望的存储区。
* 要创建“页面规则”，请单击**供应 1 个资源**按钮。


## 概念的详细说明
{: #cos-detail-concepts}

在创建**使用 COS 解析覆盖**页面规则时，CIS 将自动针对 COS 集成创建其他必需资源。这些包括：

**CNAME**
* 作为 `<bucket-name>` 的 `<bucket-name>.<cos-endpoint>` 的 CNAME DNS 记录。
* 例如，如果 CIS 域为 `foo.com`，并且您有名为 `images` 的 COS 存储区，公共 COS 端点为 `s3.us-west.objectstorage.uat.test.net`，那么 CIS 将创建名为 `images.foo.com` 的 CNAME 以指向 `images.s3.us-west.objectstorage.uat.test.net`。
如果不再需要“使用 COS 解析覆盖”页面规则，那么应手动删除该 CNAME 以及页面规则。
{:note}

**主机头覆盖**
* “主机头覆盖”设置将匹配页面规则的 URI 的主机头替换为 `<bucket-name>.<cos-endpoint>`。
* 使用先前示例，“主机头覆盖”值将设置为 `images.s3.us-west.objectstorage.uat.test.net`。


## 删除页面规则
{: #cos-delete-page-rule}

如果不再需要“使用 COS 解析覆盖”页面规则，那么应_手动_删除该 CNAME 以及页面规则。



## 编辑页面规则
{: #cos-edit-page-rule}

编辑页面规则后，页面上将不再显示**使用 COS 解析覆盖**。但是，**解析覆盖** `<bucket>.<domain>` 和**主机头覆盖** `<bucket>.<cos-endpoint>` 将替换**使用 COS 解析覆盖**。

对**解析覆盖**进行更改_不会_自动创建新的 CNAME 记录（例如，`<updated-bucket>.<domain>`）。仅在使用**使用 COS 解析覆盖**初始创建页面规则时完成此操作。要自动针对存储区创建 CNAME 记录，请遵循[创建页面规则](#cos-create-page-rule)步骤。
