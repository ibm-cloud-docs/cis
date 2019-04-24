---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: edge functions beta, edge functions

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Edge Functions（測試版）
{: #edge-functions}

CIS Edge Functions 可讓您利用無伺服器執行環境，建立新的應用程式或修改現有的應用程式，而不需要配置或維護基礎架構。Edge Functions 可定義並上傳至雲端邊緣，在要求到達原點之前先處理要求。CIS Edge Functions 可用來修改 HTTP 要求及回應、提出平行要求或從雲端邊緣產生回應。

## Edge Functions 如何運作
{: #how-edge-functions-work}

Edge Functions 會根據已定義的網域，使**動作**與 URI 產生關聯。此關聯稱之為**觸發程式**。送入您網站的要求將在雲端邊緣進行截取，並與您帳戶或網域中的觸發程式進行比對。如果該要求 URL 符合觸發程式的 URI，則會執行與該觸發程式相關聯的動作。

Edge Functions 是以現代 Web 瀏覽器可用的[服務工作者節點](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)為模型，而且會儘可能使用相同的 API。

「服務工作者節點 API」可讓您截取對網站所提出的任何要求。當 JavaScript 在處理要求時，您可以決定要對您的網站或其他網站提出不限數量的任何子要求，最後再傳回任何您想要的回應給您的訪客。

與標準「服務工作者節點」不同，Edge Functions 是在 CIS 邊緣伺服器上執行，而不是在使用者的瀏覽器中執行。這表示您可以相信程式碼將在惡意用戶端無法避開的信任環境中執行。它也表示使用者不需要使用支援「服務工作者節點」的現代瀏覽器 - 您甚至可以截取根本不是瀏覽器之 API 用戶端所傳入的要求。

Edge Functions 在內部使用的 V8 JavaScript 引擎就是在 Google Chrome 瀏覽器中使用的相同引擎，可用來在基礎架構上執行工作者節點。V8 可動態地將 JavaScript 程式碼編譯成超快機器碼，使其具有非常高的效能。這可讓您的程式碼以微秒為單位來執行，並讓我們的邊緣伺服器每秒執行數千個 Script。

Edge Functions 確實會使用 V8，它不使用 Node.js。在工作者節點內可供您使用的 JavaScript API 由我們直接實作。直接使用 V8 可讓程式碼的執行更有效率，並透過所需要的安全控制來保護客戶及基礎架構的安全。


## 動作
{: #edge-functions-actions}

動作是以 JavaScript 撰寫，需要有事件接聽器才能回應觸發程式事件。除非是由觸發程式使用，否則動作不會影響資料流量。

### 企業方案與標準方案
{: #edge-functions-enterprise-v-standard-plans}

標準方案最多只有一個動作。該動作獲指派的名稱與您的網域相同。您可以上傳另一個檔案或使用程式碼編輯器來更新動作，以取代您的動作。上傳另一個檔案將移除現有的動作。

企業方案可上傳不限數量的 Script。您可以為這些 Script 給定唯一名稱。

### 建立動作
{: #edge-functions-create-actions}

選取**建立**以使用程式碼編輯器來新增動作。在「企業」方案上，輸入動作的名稱。在「標準」方案上，該名稱不可編輯，且會設為您網域的名稱。新增 Javascript 程式碼之後，選取**儲存**來建立動作。

### 上傳動作
{: #edge-functions-upload-actions}

使用**上傳**按鈕來上傳 Javascript 檔案。在「企業」方案上，動作的名稱就是該檔案的名稱。在「標準」方案上，動作名稱會設為您網域的名稱。

使用與現有動作相同的名稱上傳或建立動作，將會導致改寫現有動作。在上傳之前請將動作檔重新命名，或在建立時於文字輸入中輸入唯一名稱，以避免發生此行為。
{:note}

### 編輯動作
{: #edge-functions-edit-actions}

選取動作即會在編輯器中開啟該動作以供修改。每當您儲存變更時，動作就會上傳至雲端邊緣。更新之後，請選取**儲存**。如果該動作正在使用中，變更會立即生效。 

### 刪除動作
{: #edge-functions-delete-actions}

請按一下**動作**表格中的**刪除**圖示，以刪除動作。無法刪除使用中的動作。若要刪除該動作，請先從觸發程式中予以移除。**使用**直欄顯示與此動作相關聯的觸發程式數目。刪除無法復原。


### 相關聯的觸發程式
{: #edge-functions-associated-triggers}

新增觸發程式，並使它與動作產生關聯。

### Edge Functions 已知限制
{: #edge-functions-known-limitations}

上傳與現有動作同名的動作。將改寫現有動作。在上傳之前請將動作檔重新命名，以避免發生此行為。


## 觸發程式
{: #triggers}

### 關於觸發程式
{: #about-triggers}

觸發程式（路徑）決定「動作」的網域資料流量遞送。觸發程式會根據帳戶的網域，使特定 URL 型樣與預先定義的動作產生關聯。URL 必須包含該網域，但它可以包含萬用字元作為網域的字首或放在路徑的尾端。如果未提供型樣的路徑，則會隱含地新增 `/`。URL 型樣不能包含中置萬用字元或查詢參數。

您必須新增網域才能新增觸發程式。您可以在沒有動作的情況下新增觸發程式。

### 新增觸發程式
{: #add-triggers}

移至**觸發程式**標籤，並按一下**新增觸發程式**。輸入 URL 型樣，並從現有動作清單中選取動作。 

對於動作，您也可以選取**避免 Edge Functions**。這可讓觸發程式的路徑保持作用中，但避免使用任何「邊緣功能」動作。例如，有一個稱為 `my-function` 的動作，以及一個含有路徑 `beta.cistest-load.com/*` 的觸發程式。如果路徑 `beta.cistest-load.com/data` 不應該使用 `my-function` 動作，請建立另一個含有路徑 `beta.cistest-load.com/data` 的觸發程式，並選取**避免 Edge Functions** 選項。這可讓路徑 `beta.cistest-load.com/data` 保持作用中，而無需使用 `my-function` 動作。

### 編輯觸發程式
{: #edit-triggers}

針對所選取的觸發程式，使用表格列中的功能表選項來更新觸發程式。更新之後，請選取**儲存**。

### 刪除觸發程式
{: #delete-triggers}

針對所選取的觸發程式，使用表格列中的功能表選項來刪除觸發程式。這個動作無法復原。


## 使用案例
{: #edge-functions-use-cases-examples}

這些範例僅供示範之用，不適用於正式作業。
{:important}
* [A/B 測試](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#ab-testing)
* [新增回應標頭](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#add-response-header)
* [聚集多個要求](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#aggregate-multiple-requests)
* [條件式遞送](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#conditional-routing)
* [快速鏈結保護](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#hot-link-protection)
* [無原點回應](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#originless-responses)
* [POST 要求](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#post-requests)
* [設定 Cookie](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#setting-cookies)
* [已簽署的要求](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#signed-requests)
* [串流回應](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#streaming-responses)
