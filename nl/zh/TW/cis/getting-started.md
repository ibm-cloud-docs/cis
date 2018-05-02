---
copyright:
  years: 2018
lastupdated: "2018-03-19"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 開始使用 IBM Cloud Internet Services (CIS)

IBM Cloud Internet Services (CIS) 提供三個主要功能來加強工作流程：[安全](/docs/infrastructure/cis/managing-for-security.html)、[可靠性](/docs/infrastructure/cis/managing-for-reliability.html)及[效能](/docs/infrastructure/cis/managing-for-performance.html)。在您開啟 IBM CIS 應用程式之後，每一個功能區域都會呈現在畫面的左側導覽列中。

針對每一個功能，IBM CIS 可協助您調整其特性，以符合您的特定需求，包括：

 * 授權性 DNS 伺服器
 * 廣域及本端負載平衡
 * Web 應用程式防火牆 (WAF)
 * DDoS 保護
 * 快取及頁面規則



## 開始之前
開始使用 IBM CIS 之前，您需要先有 [IBM ID](https://www.ibm.com/account/us-en/signup/register.html)。您接著可以根據喜好設定，透過「IBM Cloud 帳戶」或新的 [IBM Cloud Internet Services 入口網站](https://console.bluemix.net/catalog/services/internet-services)來訂購服務。

如果您需要取得帳戶來使用 IBM Cloud Internet Services 的協助，請[與 IBM 業務代表聯絡](https://www.ibm.com/cloud-computing/bluemix/contact-us)，以取得開始使用的其他指引。

如果您具有現有 Softlayer 帳戶，則可以使用 IBM ID [鏈結帳戶](https://console.bluemix.net/docs/account/softlayerlink.html#unifyingaccounts)。 

## 處理程序概觀

您只要使用幾個步驟，就可以開始針對網際網路資料流量使用 IBM CIS。

 * 從 IBM Cloud 儀表板開啟 IBM CIS 應用程式。
 * 新增您要管理的網域。
 * 使用我們所提供的名稱伺服器來配置 DNS 資訊。
 * 遵循指導教學或設定其他特性，以繼續開始使用 IBM CIS。

### 步驟 1：開啟 IBM CIS 應用程式

開啟 [IBM Cloud 儀表板](https://console.bluemix.net/catalog/)。然後，導覽至 IBM CIS 應用程式圖示，方法是在儀表板的左側導覽列中選取**平台 -> 網路**種類。按一下您在接近畫面中間看到的圖示，以開啟 IBM Cloud Internet Services 應用程式。 

![型錄](images/catalog-cis-tile.png)

**概觀畫面**

在 IBM CIS 應用程式啟動之後，您會看到 IBM CIS **概觀**畫面，而且會在使用者介面顯示的左側區域上找到**安全**、**可靠性**及**效能**的標籤。

**我選擇的方案為何？**

針對_早期存取_ 版本，您只能選擇一個方案，而且是免費的。按一下**概觀**畫面左下方的**建立**按鈕，以開始佈建您的帳戶。

**開始佈建**

您將會看到 IBM CIS 應用程式的第一個畫面，而您將在其中選取**新增網域**按鈕來開始。

|**請注意，「早期存取方案」只能一個帳戶一個實例。** |
|-------------------------------------------------------------------|
| 建立資源實例並在其中新增網域之後，不允許您為 IBM CIS 新增資源實例。即使您刪除試用網域，然後再次嘗試將網域新增至相同的資源實例，也會強制執行此限制。如果您嘗試這麼做，則會發生錯誤。|

### 步驟 2. 新增及配置網域。

輸入網域或子網域，以開始保護及改善 Web 服務的效能。

**附註：**請指定 DNS 區域。您可以在網域的登記員或 DNS 提供者上配置這些網域或子網域的名稱伺服器。請不要使用 CNAME。

![開始使用](images/overview-add-domain.png)
「概觀」畫面會以`擱置`狀態顯示您的網域。除非您完成「步驟 3」，否則您的網域會保持`擱置`。

**附註：**新增網域之後，就無法刪除 IBM CIS 實例。若要刪除實例，請先從實例中刪除網域。

### 步驟 3. 使用登記員或現有 DNS 提供者配置名稱伺服器。

若要開始接收 IBM CIS 的好處，請配置您的登記員或網域名稱提供者以使用所列出的名稱伺服器。如果您要委派網域（例如 `example.com`），則請在網域設定中配置列出的名稱伺服器，而這些伺服器是由您的登記員進行管理（例如，在登記員的 Web 入口網站上）。如果您不確定誰是您網域的登記員，則可以在 https://whois.icann.org/ 查閱它。如果您從另一個 DNS 提供者委派子網域（例如，`subdomain.example.com`），則必須為每一個列出的名稱伺服器新增「名稱伺服器 (NS)」記錄。

在您配置登記員或 DNS 提供者之後，最多可能需要 24 小時，變更才會生效。驗證已針對網域或子網域正確地配置所指定的名稱伺服器之後，網域的狀態會從`擱置`變更為`作用中`。配置名稱伺服器之後，您可以按一下`概觀`頁面中的「重新檢查名稱伺服器」鏈結，可能會加速啟動網域（您一個小時只能提交這項檢查一次）。

### 步驟 4. 確定 IBM Cloud Internet Services 正在解析應用程式、主機名稱或網站的網域資訊。

若要繼續，請從左側覽導列中選取**可靠性**標籤，然後選取 **DNS** 選項。請務必新增適當的 _DNS 記錄_。新增已移入的 **A 記錄**及任何 **AAAA** 或 **MX** 項目。如果您忘記在登記員委派完成之前新增這些記錄，則 IBM Cloud Internet Services 無法解析您網際網路面向應用程式的網域資訊。  

![開始使用](images/dns-records.png)

### 步驟 5. 在此同時，您可以開始管理其他 IBM CIS 功能及特性。

如需管理其他功能及特性的詳細資料，請參閱[逐步指示](/docs/infrastructure/cis/how-to.html)。
