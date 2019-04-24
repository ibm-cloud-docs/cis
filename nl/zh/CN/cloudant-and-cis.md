---

copyright:
  years: 2019
lastupdated: "2019-03-28"

keywords: Cloudant database, CORS, cross-origin resource sharing, host header

subcollection: cis

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"} 
{:note: .note}


# 通过 IBM Cloud Internet Services 访问 Cloudant 数据库
{: #access-cloudant-through-cis}

执行以下步骤通过 IBM Cloud Internet Services (CIS) 访问 Cloudant 数据库。

## 开始之前
{: #access-cloudant-through-cis-begin}

这些指示信息假定您已向 CIS 添加域，如[入门](/docs/infrastructure/cis?topic=cis-getting-started-with-ibm-cloud-internet-services-cis-)页面中所述。

### 步骤 1：向跨源资源共享 (CORS) 添加 CIS 域
{: #access-cloudant-through-cis-step1}

* 导航至 Cloudant 数据库并打开 `Acccount` -> `CORS` 页面。
* 将 CIS 域添加到源域输入字段。例如，`https://cloudant.test.foo.com`。

### 步骤 2. 配置 CIS 以指向 Cloudant 数据库
{: #access-cloudant-through-cis-step2}

* 导航至 CIS 仪表板，创建指向 Cloudant 数据库主机名的负载均衡器或 DNS 记录。例如，`https://cloudant.test.foo.com` -> `111-222-333-444-555-test.cloudant.com`。
* 针对 DNS 记录或负载均衡器启用 `proxy`。


### 步骤 3. 创建用于设置“主机头覆盖”的页面规则
{: #access-cloudant-through-cis-step3}

* 在 CIS 仪表板中，导航至 `Performance` -> `Page Rules`。
* 针对期望的 URL 创建页面规则，例如，`https://cloudant.test.foo.com/*`。
* 选择“规则行为”设置 `Host Header Override`。
* 设置为 Cloudant 数据库主机名，例如，`111-222-333-444-555-test.cloudant.com`。

有关 Cloudant 的更多信息，请参阅 [Coudant 文档](/docs/services/Cloudant?topic=cloudant-getting-started-with-cloudant)。
