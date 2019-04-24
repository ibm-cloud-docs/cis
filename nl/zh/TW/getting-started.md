---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-29"

keywords: IBM Cloud Internet Services, IBM CIS application, Authoritative DNS servers

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# 開始使用 IBM Cloud Internet Services (CIS)
{:#getting-started}

IBM Cloud Internet Services (CIS) 採用 Cloudflare 的技術，提供三個主要功能來加強工作流程：[安全](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-for-optimal-security)、[可靠性](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-deployment-for-optimal-reliability)及[效能](/docs/infrastructure/cis?topic=cis-manage-your-cis-deployment-for-best-performance)。在您開啟 IBM CIS 應用程式之後，每一個功能區域都會呈現在畫面的左側導覽列中。

針對每一個功能，IBM CIS 可協助您調整其特性，以符合您的特定需求，包括：

 * 授權性 DNS 伺服器
 * 廣域及本端負載平衡
 * Web 應用程式防火牆 (WAF)
 * DDoS 保護
 * 快取及頁面規則


## 開始之前
{:#before-you-begin}

開始使用 IBM CIS 之前，您需要先有 [IBM ID](https://www.ibm.com/account/reg/us-en/signup?formid=urx-19776)。您接著可以根據喜好設定，透過「IBM Cloud 帳戶」或新的 [IBM Cloud Internet Services 入口網站](https://{DomainName}/catalog/services/internet-services)來訂購服務。

如果您需要取得帳戶來使用 IBM Cloud Internet Services 的協助，請[與 IBM 業務代表聯絡](https://{DomainName}/cloud/support)，以取得開始使用的其他指引。

如果您具有現有 Softlayer 帳戶，則可以使用 IBM ID [鏈結帳戶](https://{DomainName}/docs/account?topic=account-unifyingaccounts)。 

## 處理程序概觀
{:#process-overview}

只需要幾個步驟，您就可以開始使用 IBM CIS 來處理網際網路資料流量。

 * 從 IBM Cloud 儀表板開啟 IBM CIS 應用程式。
 * 新增您要管理的網域。
 * 使用我們所提供的名稱伺服器來配置 DNS 資訊。
 * 遵循指導教學或設定其他特性，以繼續開始使用 IBM CIS。

### 步驟 1：開啟 IBM CIS 應用程式
{:#open-cis-application}

開啟 [IBM Cloud 儀表板](https://{DomainName}/catalog/)。然後，在儀表板的左側導覽列中選取**基礎架構 -> 網路**種類，以導覽至 IBM CIS 應用程式圖示。按一下您在接近畫面中間看到的圖示，以開啟 IBM Cloud Internet Services 應用程式。 

![型錄](images/catalog-cis-tile.png)

**概觀畫面**

在 IBM CIS 應用程式啟動之後，您會看到 IBM CIS **概觀**畫面，而且會在使用者介面顯示畫面左側區域上找到**安全**、**可靠性**及**效能**的標籤。

**我選擇的方案為何？**

以下這 4 個方案可供選擇： 
* **企業使用情形** 
* **企業套件** 
* **標準方案** 
* **免費試用**. 

**免費試用**會在 30 天之後到期，屆時您可以升級至**標準方案**或**企業方案**。單一**標準**實例可以管理一個網域。您可以在單一帳戶內建立任意數量的多個**標準**服務實例，每個實例管理單一網域。 

**企業方案**可讓您在單一服務實例中管理多個網域。請選取**概觀**畫面上的**建立**按鈕，以開始佈建您的帳戶。

**免費試用**限制為每個帳戶只能有一個實例。
{:note}

**開始佈建**

您將會看到 IBM CIS 應用程式的第一個畫面，而您將在其中選取**新增網域**按鈕來開始。


### 步驟 2. 新增及配置網域。
{:#add-configure-your-domain}

從歡迎使用頁面中選取**開始使用**，以開始設定 CIS。

![開始使用](images/overview-setup-step1.png)

接著，輸入網域或子網域，以開始保護及改善 Web 服務的效能。

請指定 DNS 區域。您可以在網域的登記員或 DNS 提供者上配置這些網域或子網域的名稱伺服器。請不要使用 CNAME。
{:note}

![開始使用](images/overview-setup-step2.png)

「概觀」畫面會以`擱置`狀態顯示您的網域。在您完成「步驟 4」之前，您的網域會一直保持`擱置`。

新增網域之後，就無法刪除 IBM CIS 實例。若要刪除實例，請先從實例中刪除網域。
{:note}

### 步驟 3. 設定 DNS 記錄（選用）。
{:#setup-your-dns-records}

在將網域的資料流量轉移至 CIS 之前，強烈建議您在 CIS 中匯入或重建 DNS 記錄。您可以選擇跳過此步驟，但如果沒有在 CIS 中正確配置您的 DNS 記錄，則可能會導致網站的某些部分無法存取。

請透過從現行 DNS 上傳匯出的記錄，或手動建立您的 DNS 記錄，來匯入記錄。若要匯入記錄，請選取**匯入記錄**。

![開始使用](images/overview-setup-step3.png)

完成時，或者如果您想要跳過此步驟，請選取**下一步**。

### 步驟 4. 使用登記員或現有的 DNS 提供者來配置您的名稱伺服器。
{:#configure-your-name-servers-with-the-registrar-or-existing-dns-provider}

若要開始接收 IBM CIS 的好處，請配置您的登記員或網域名稱提供者以使用所列出的名稱伺服器。如果您要委派網域（例如 `example.com`），則請在網域設定中配置列出的名稱伺服器，而這些伺服器是由您的登記員進行管理（例如，在登記員的 Web 入口網站上）。如果您不確定誰是您網域的登記員，則可以在 https://whois.icann.org/ 查閱它。如果您從另一個 DNS 提供者委派子網域（例如，`subdomain.example.com`），則必須為每一個列出的名稱伺服器新增「名稱伺服器 (NS)」記錄。如需提供者的詳細指示，請參閱由我們在 Cloudflare 的夥伴所撰寫的[管理 DNS 記錄 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://support.cloudflare.com/hc/en-us/articles/360019093151-Managing-DNS-records-in-Cloudflare){:new_window}。

在您配置登記員或 DNS 提供者之後，最多可能需要 24 小時，變更才會生效。驗證已針對網域或子網域正確配置所指定的名稱伺服器之後，網域的狀態會從`擱置`變更為`作用中`。配置名稱伺服器之後，您可以按一下`概觀`頁面中的「重新檢查名稱伺服器」鏈結，可能會加速啟動網域（您一個小時只能提交這項檢查一次）。

您的網域必須在 60 天內進入`作用中`狀態，否則將會移除您的網域或任何配置資料。
{:note}

![開始使用](images/overview-setup-step4.png)

### 步驟 5. 確定 IBM Cloud Internet Services 正在解析應用程式、主機名稱或網站的網域資訊。
{:#ensure-cis-is-resolving-domain-info}

若要繼續，請從左側覽導列中選取**可靠性**標籤，然後選取 **DNS** 選項。請務必新增適當的 _DNS 記錄_。新增已移入的 **A 記錄**及任何 **AAAA** 或 **MX** 項目。如果您忘記在登記員委派完成之前新增這些記錄，則 IBM Cloud Internet Services 無法解析您網際網路面向應用程式的網域資訊。

![開始使用](images/dns-records.png)

### 步驟 6. 在此同時，您可以開始管理其他 IBM CIS 功能及特性。
{:#manage-other-cis-functions}

如需管理其他功能及特性的詳細資料，請參閱[逐步指示](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cloud-internet-services-cis-deployment)。
