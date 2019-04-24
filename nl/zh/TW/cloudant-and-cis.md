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


# 透過 IBM Cloud Internet Services 存取 Cloudant 資料庫
{: #access-cloudant-through-cis}

請遵循下列步驟，透過 IBM Cloud Internet Services (CIS) 存取「Cloudant 資料庫」。

## 開始之前
{: #access-cloudant-through-cis-begin}

這些指示假設您已將網域新增至 CIS，如[開始使用](/docs/infrastructure/cis?topic=cis-getting-started-with-ibm-cloud-internet-services-cis-)頁面所概述。

### 步驟 1：將 CIS 網域新增至「跨原點資源共用 (CORS)」
{: #access-cloudant-through-cis-step1}

* 導覽至 Cloudant 資料庫，並開啟`帳戶` -> `CORS` 頁面。
* 將 CIS 網域新增至原點網域輸入欄位。例如，`https://cloudant.test.foo.com`。

### 步驟 2. 配置 CIS 以指向 Cloudant 資料庫
{: #access-cloudant-through-cis-step2}

* 導覽至 CIS 儀表板，並建立一個指向 Cloudant 資料庫主機名稱的負載平衡器或 DNS 記錄。例如，`https://cloudant.test.foo.com` -> `111-222-333-444-555-test.cloudant.com`。
* 針對 DNS 記錄或負載平衡器啟用 `proxy`。


### 步驟 3. 建立頁面規則以設定「主機標頭置換」
{: #access-cloudant-through-cis-step3}

* 在 CIS 儀表板中，導覽至`效能` -> `頁面規則`。
* 針對所需的 URL 建立頁面規則，例如，`https://cloudant.test.foo.com/*`。
* 選取「規則行為」設定`主機標頭置換`。
* 設定為 Cloudant 資料庫主機名稱，例如，`111-222-333-444-555-test.cloudant.com`。

如需 Cloudant 的相關資訊，請參閱 [Cloudant 文件](/docs/services/Cloudant?topic=cloudant-getting-started-with-cloudant)。
