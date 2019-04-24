---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Access Group Writer role, CIS instance, IAM

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# IAM 與 CIS
{:#iam-and-cis}

IBM Cloud Internet Services (CIS) 運用 IAM 來執行授權與鑑別。

如果您不想將任何人新增至 CIS 實例，則可以不處理此頁面。
{:note}

根據導覽樹狀結構，依三個 CIS 功能範圍限制存取： 
* 可靠性 - 例如 DNS、GLB
* 安全 - 例如憑證、IP 防火牆規則及速率限制
* 效能 - 例如頁面規則、快取及遞送

本節會指導如何提供實例的細部存取控制。

## 角色
{:#iam-and-cis-roles}

使用下列三個角色來運用 IAM
* 讀者 - 可以取得實例及網域的相關資訊
* 撰寫者 - 可對現有的配置進行變更
* 管理員 - 可以建立或刪除實例、網域、配置

## 存取群組及使用者
{:#iam-and-cis-access-groups-users}

原則可以直接指派給「使用者」或「存取群組」。
建議將它指派給存取群組，以便將建立的原則數目減至最少，以及減少管理這些原則的工作量。

## 快取
{:#iam-and-cis-cache}

當相同的要求再次送達時，我們會快取授權結果，並使用快取來做出決策。在快取達到其存活時間（10 分鐘）之後，即會到期。

## 最佳作法
{:#iam-and-cis-best-practices}

1. 刪除現有的原則，然後建立新原則，而不要修改原則。

## 情境
{:#iam-and-cis-scenarios}

本節將逐步演練透過 CIS 所建立的不同存取原則範例。 

### 具有`配置`類型的網域層次
{:#iam-and-cis-scenarios-domain-level}

#### 在存取權群組上存取具有`安全配置`的單一網域
##### 撰寫者角色

Bob 有一個 CIS 實例 `cis-test-instance` 和兩個網域 `bob.com` 及 `bob-ibm.com`。
Bob 只想要在 **`bob.com`** 的**安全配置**上為公司的所有安全工程師 (sec-group) 提供「撰寫者」角色的存取權。

這些步驟顯示如何建立 IAM 原則來實現此一情境。

當 Bob 登入 cis-test-instance 之後，他：
1. 按一下導覽列的**帳戶 > 存取權**標籤
1. 選取**存取群組** - 您要提供存取權的 **sec-group**
1. 選取 **`bob.com`**
1. 選取**撰寫者**角色
1. 選取**安全配置**選項
1. 按一下**建立原則**

在「管理」標籤上：
為 **sec-group** 建立了下列原則：

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e

Service Instance
    name: cis-test-instance
    id: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9
Domain
    name: bob.com
    id: 4b23ec772965f672f96f05670e36827e
Config Type
    cfgType: security
```

現在，sec-group 具有只能查看 `bob.com` 的存取權，可以修改與安全相關的值。 

##### 針對存取群組，從「撰寫者」更新為「管理員」角色

如果 Bob 想要將 sec-group 的角色從「撰寫者」更新為「管理員」，他需要刪除現有的原則。 
1. 移至**「管理 IAM 」標籤 > 存取群組 > sec-group > 存取原則**
1. 刪除下列原則 
  ```
  Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
  ```

然後，Bob 必須建立新的原則。 
1. 按一下導覽列的**帳戶 > 存取權**標籤
1. 選取**存取群組** - 您要提供存取權的 **sec-group**
1. 選取 **`bob.com`**
1. 選取**管理員**角色
1. 選取**安全配置**選項
1. 按一下**建立原則**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

如果未刪除現有原則（撰寫者），則嘗試建立「管理員」的原則會失敗。

##### 更新配置以包含「效能」及「安全」

如果 Bob 想要將 `bob.com` 上的效能配置連同安全設定的 sec-group 存取權提供給「管理員」，他：
1. 按一下導覽列的**帳戶 > 存取權**標籤
1. 選取**存取群組** - 您要提供存取權的 **sec-group**
1. 選取 **`bob.com`**
1. 選取**管理員**角色
1. 選取**效能配置**選項
1. 按一下**建立原則**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: performance, domainId: 4b23ec772965f672f96f05670e36827e

```

#### 具有`安全配置`之所有網域的存取權

如果您想要為前一個範例中的 `bob.com` 及 `bob-ibm.com` 提供安全動作，則必須針對每一個網域重複這些步驟來建立新原則。唯一的差異在於為每個原則選取各自的網域。

1. 按一下導覽列的**帳戶 > 存取權**標籤
1. 選取**存取群組** - 您要提供存取權的 **sec-group**
1. 選取 **`bob.com`**
1. 選取**管理員**角色
1. 選取**安全配置**選項
1. 按一下**建立原則**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

1. 按一下導覽列的**帳戶 > 存取權**標籤
1. 選取**存取群組** - 您要提供存取權的 **sec-group**
1. 選取 **`bob-ibm.com`**
1. 選取**管理員**角色
1. 選取**安全配置**選項
1. 按一下**建立原則**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 7ad7341865246f5df482ad9f76aafb5a
```



#### 具有`安全配置`及`可靠性配置`之單一網域的存取權

Bob 有一個 CIS 實例 cis-test-instance 和兩個網域 `bob.com` 及 `bob-ibm.com`。
Bob 想要只針對 **`bob-ibm.com`** 的**安全及可靠性動作**，為 Tony 提供「撰寫者」角色的存取權。

當 Bob 登入 cis-test-instance 之後，他：
1. 按一下導覽列的**帳戶 > 存取權**標籤
1. 選取他想要為其提供存取權的 **Tony**
1. 選取 **`bob-ibm.com`**
1. 選取**撰寫者**角色
1. 選取**安全及可靠性**選項的勾選框 
1. 按一下**建立原則**

這會在後端為每一個配置類型建立兩個原則。

### 具有所有配置類型的網域層次
{:#iam-and-cis-scenarios-domain-level-all-config-types}

Bob 想要在網域層次授與讀取/撰寫/管理權給 Tony。

#### 撰寫
當 Bob 登入 cis-test-instance 之後，他：
1. 按一下導覽列的**帳戶 > 存取權**標籤
1. 選取他想要為其提供存取權的 **Tony**
1. 選取 **`bob.com`**
1. 選取**撰寫者**角色
1. 勾選「CIS 功能範圍」的所有方框
1. 按一下**建立原則**

```
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: security	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: performance	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: reliability	
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

#### 管理員
當 Bob 登入 cis-test-instance 之後，他：
1. 按一下導覽列的**帳戶 > 存取權**標籤
1. 選取他想要為其提供存取權的 **Tony**
1. 選取 **`bob.com`**
1. 選取**管理員**角色
1. 勾選「CIS 功能範圍」的所有方框
1. 按一下**建立原則**

```
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: security	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: performance	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: reliability	
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

#### 讀者
當 Bob 登入 cis-test-instance 之後，他們：
1. 按一下導覽列的**帳戶 > 存取權**標籤
1. 選取他想要為其提供存取權的 **Tony**
1. 選取 **`bob.com`**
1. 選取**讀者**角色
  1. 所有勾選框都會預先勾選，以顯示使用者對整個網域需要*最低* 讀取權，而無法提供網域局部存取權
1. 按一下**建立原則**


```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

### 實例層次 - 所有網域
{:#iam-and-cis-scenarios-instance-level}

此原則必須透過 IAM 管理頁面來建立及管理。

實例層次存取權表示 Bob 可以將目前 10 個實例中的「實例 1」許可權提供給 Tony。
Tony 可以檢視此實例中的所有網域。 

如果 Bob 想要提供「撰寫者」或「管理員」角色來存取下列項目，他需要提供實例層次存取權：
* 負載平衡器 - 儲存區及性能檢查
* 防火牆存取規則
* 工作者節點 

在管理 IAM 頁面中，於服務實例 cis-test-instance 上建立撰寫者/管理員原則。

```
Manager	Resource	Only service instance cis-test-instance of CIS 	
or
Writer	Resource	Only service instance cis-test-instance of CIS 	
```

## 管理 IAM 原則 
{:#manage-iam-policies}

CIS 容許使用者建立 IAM 原則，但管理必須透過 [IAM 頁面](
https://{DomainName}/iam#/overview)來完成。

## 附註
{:#iam-note}
針對 CIS 實例之「存取權」頁面上所建立的每一個原則，將輪流建立 2-3 個原則。

1. 服務實例「平台」檢視者角色容許新增的使用者在儀表板上檢視實例。

**範例**
```
Viewer	Resource	Only service instance cis-instance-instance of CIS 	
```

2. 網域層次讀取權是進行細部存取的最低需求。

**範例**
```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
```
3. 您以目前的配置類型建立的原則。

**範例**
```
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

**常見問題**
1. 如何取得服務實例 ID？

   複製概觀頁面上的 CRN
   ```
   crn:v1:test:public:internet-svcs:global:a/2c38d9a9913332006a27665dab3d26e8:836f33a5-d3e1-4bc6-876a-982a8668b1bb::
   ```
   CRN 的最後部分是您的服務實例：`836f33a5-d3e1-4bc6-876a-982a8668b1bb`。
   
   或
   
   按一下資源清單主頁面上包含 CIS 實例的列，然後複製服務實例 ID 的 GUID。

2. 我已刪除原則，但我為其提供原則的使用者仍可執行該動作！

   CIS 會快取授權結果，且快取的 TTL 為 10 分鐘。  
   
   當 IAM 授權時，它會先使用存取群組的存取原則以及使用者本身的原則，然後再做出決策。

3. 佈建「網際網路服務」需要哪些許可權？

   如果您無法建立資源並將它新增至資源群組，很可能是遇到存取問題。您必須至少具有資源群組本身的「檢視者」角色，且至少必須在帳戶中具有該服務的「編輯者」角色。您可以與帳戶管理者聯絡，以驗證您在帳戶中的已指派存取權。如需相關資訊，請參閱[管理資源的存取權](/docs/iam?topic=iam-iammanidaccser)。
   
 
