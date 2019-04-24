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

# 使用 COS 解析置換
{: #resolve-override-cos}

## 使用案例
{: #cos-use-cases}

將符合頁面規則的要求解析為 Cloud Object Storage (COS) 儲存區資源。


## 必要條件
{: #cos-prerequisites}

下列步驟假設您現有的 COS 實例及儲存區具有公用存取權。如需公用存取權的相關資訊，請參閱[容許公用存取權](/docs/services/cloud-object-storage/iam?topic=cloud-object-storage-allowing-public-access)。


## 建立頁面規則步驟
{: #cos-create-page-rule}

* 導覽至**效能 -> 頁面規則**。
* 按一下**建立規則**按鈕。
* 輸入用於 URL 比對所需的值。例如，`*.foo.com/*`。
  * 請注意，URL 比對必須比對 COS 物件名稱。
  * 比方說，如果您在 `my-bucket1` 儲存區下有一個稱為 reports.txt 的物件，則這兩項 URL 比對都有效：
    * `*.foo.com/*`
    * `*.foo.com/reports.txt`
* 使用下拉清單來選取**效能**區段下的**使用 COS 解析置換**。
* 使用 **Cloud Object Storage 實例**下拉清單以選取所需的實例。
* 使用**儲存區**下拉功清單來選取所需的儲存區。
* 若要建立「頁面規則」，請按一下**佈建 1 個資源**按鈕。


## 概念的詳細說明
{: #cos-detail-concepts}

建立**使用 COS 解析置換**頁面規則時，CIS 會自動建立用於 COS 整合的其他必要資源。這些包括：

**CNAME**
* `<bucket-name>.<cos-endpoint>` 的 CNAME DNS 記錄，即 `<bucket-name>`。
* 比方說，如果 CIS 網域是 `foo.com`，您的 COS 儲存區稱為 `images`，且公用 COS 端點是 `s3.us-west.objectstorage.uat.test.net`，則 CIS 會將 CNAME 建立為 `images.foo.com`，其指向 `images.s3.us-west.objectstorage.uat.test.net`。
如果不再需要「使用 COS 解析置換」頁面規則，則應該手動刪除 CNAME 及頁面規則。
{:note}

**主機標頭置換**
* 「主機標頭置換」設定會將符合頁面規則的 URI 主機標頭取代為 `<bucket-name>.<cos-endpoint>`。
* 使用前一個範例，「主機標頭置換」值將設為 `images.s3.us-west.objectstorage.uat.test.net`。


## 刪除頁面規則
{: #cos-delete-page-rule}

如果不再需要「使用 COS 解析置換」頁面規則，則應該_手動_ 刪除 CNAME 及頁面規則。


## 編輯頁面規則
{: #cos-edit-page-rule}

編輯頁面規則之後，**使用 COS 解析置換**就不再顯示於頁面上。不過，**解析置換** `<bucket>.<domain>` 及**主機標頭置換** `<bucket>.<cos-endpoint>` 將取代**使用 COS 解析置換**。

對**解析置換**進行變更_不_ 會自動建立新的 CNAME 記錄（例如，`<updated-bucket>.<domain>`）。只有在利用**使用 COS 解析置換**起始建立頁面規則時，才會執行此動作。若要自動建立儲存區的 CNAME 記錄，請遵循[建立頁面規則](#cos-create-page-rule)步驟。
