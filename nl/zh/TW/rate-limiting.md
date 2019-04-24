---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Bypass, header responses, brute-force login attempts

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# 速率限制
{:#cis-rate-limiting}

「速率限制」（僅限企業方案）會防範拒絕服務攻擊、強制入侵登入嘗試，以及以應用程式層為目標的其他類型不當行為。

請選取速率限制規則的類型：**自訂規則**或**保護登入**

## 建立自訂速率限制規則
{:#create-a-custom-rate-limiting-rule}

請輸入可協助您記住規則用途的規則名稱。這是選用欄位。

**資料流量比對準則**會使用 AND 運算。請輸入您有速率限制的 URL，然後當來自**相同 IP 的要求超出**您指定的**每秒要求數**時，會觸發指定的規則。

**進階準則**選項可讓您指定哪些 HTTP 方法、標頭回應及原點回應碼來進一步限制比對準則。 

從**方法**下拉清單中選取一值（ANY 是預設值）。  

更新 **HTTP 回應標頭**。您也可以**新增回應標頭**，以包括原點 Web 伺服器傳回的標頭。 

如果 **HTTP 回應標頭**下有多個標頭，則會套用 _AND_ 布林邏輯。若要排除要比對的標頭，請使用_不等於_ 選項。此外，每一個標頭都必須完全相符。但是，不會套用區分大小寫。
{:note}

在**原點回應碼**下，鍵入要比對之每一個 HTTP 回應碼的有效數值。若要包含兩個以上的回應碼，請以逗點區隔每個值。比方說，如果您只想要計入 401 及 403 這兩個錯誤碼，請輸入 `401, 403`。 

### 配置回應
{:#rate-limiting-configure-response}

請從列出的動作中選取，然後指定逾時期間。在此情況下，逾時是指執行該動作的禁止期間。60 秒逾時表示套用該動作 60 秒。

|動作   | 說明|
|------|------------|
|封鎖|超出臨界值時發出 429 錯誤|
|盤查|使用者必須先通過 Google reCaptcha 盤查才能繼續。如果順利完成，我們就接受該要求。否則，會封鎖該要求。| 	
|JS 盤查|	使用者必須先通過 Javascript 盤查才能繼續。如果順利完成，我們就接受該要求。否則，會封鎖該要求。
|模擬| 您可以使用此選項，在您的即時環境中套用任何其他選項之前先測試規則。

**進階回應**

指定超出規則臨界值時的回應類型。 

### 略過
{:#rate-limiting-bypass}

略過可讓您為一組 URL 建立對等的白名單或異常狀況。即使符合「速率限制」規則，也不會對那些 URL 觸發任何動作。

## 保護登入
{:#rate-limiting-protect-login}

保護登入會建立標準規則，用來保護登入頁面免遭強制入侵攻擊。在 5 分鐘內嘗試登入超過 5 次的用戶端將被封鎖 15 分鐘。 

請輸入規則的名稱，以及登入 URL。
