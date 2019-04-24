---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: range application, tls encryption, ddos protection, global tcp proxy

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Range
{:#cis-range}

Range 特性為任何 TCP 型通訊協定帶來 DDoS 保護、負載平衡和及容加速。
Range 是在 CIS/Cloudflare 邊緣節點上執行的廣域 TCP Proxy。 

Range 可用來： 
* 保護 TCP 埠及通訊協定免於**第 3 層和第 4 層 DDoS** 攻擊。 
* 透過啟用 **TLS 加密**來削弱攻擊者探查及竊取機密資料的能力。
* 與「CIS IP 防火牆」整合，讓您能夠封鎖或盤查 IP 位址或整個 IP 範圍，以免呼叫到您的 TCP 服務。 
* 為負載平衡器配置 TCP 性能檢查、失效接手及引導原則，以指定資料流量傳輸處。

## 開始使用 Range
{:#getting-started-with-range}

Range 僅適用於企業客戶，需額外付費，並依頻寬使用量計價。
{:note}

### 新增應用程式
{:#range-add-an-application}
請遵循下列步驟來新增應用程式。

1. 導覽至**安全 > Range**
1. 按一下**新增應用程式**按鈕 
1. 在第一個輸入欄位中輸入應用程式名稱。您的應用程式會變成與 CIS 網域上的 DNS 名稱相關聯。
1. 在下一個輸入欄位中輸入邊緣埠。我們將在此埠接聽要通往這些位址的送入連線。通往這些位址的連線會進行 Proxy 處理到您的原點。（埠 21 以外的所有埠都支援 Proxy。）
1. 在「原點」區段中，輸入 TCP 應用程式的原點 IP 及埠。您也可以選取現有的「負載平衡器」
1. 啟用「IP 防火牆」。如已啟用，就會對此應用程式施行具有「封鎖」或「白名單」動作的防火牆規則。尚未支援國家/地區或 ASN 型規則。
1. 如果您有支援「PROXY 通訊協定第 1 版」的行內 Proxy，請啟用「Proxy 通訊協定」。如果您執行的是需要瞭解真正用戶端 IP 的服務，則此特性非常有用。在大部分情況下，這項設定應保留停用狀態。
1. 按一下**佈建**

Proxy 通訊協定會將報告用戶端 IP 位址及埠的標頭附加到每一個連線的前面。Proxy 通訊協定標頭的格式如下：
  * PROXY_STRING + single space + INET_PROTOCOL + single space + CLIENT_IP + single space + PROXY_IP + single space + CLIENT_PORT + single space + PROXY_PORT + "\r\n"
  * 以下是 IPv4 位址的 Proxy 通訊協定行範例：
    `PROXY TCP4 192.0.2.0 192.0.2.255 42300 443\r\n`
  * 以下是 IPv6 位址的 Proxy 通訊協定行範例：
    `PROXY TCP6 2001:db8:: 2001:db8:ffff:ffff:ffff:ffff:ffff:ffff 42300 443\r\n`
   
佈建 Range 應用程式將根據每個應用程式使用的頻寬數量而需要額外付費。
{:note}

現在，您的應用程式會出現在具有下列內容的磚中：
  * 應用程式名稱
  * 邊緣埠
  * 原點及埠
  * 過去一小時的連線（每分鐘輪詢）
  * 過去一小時的傳輸量（每分鐘輪詢）
  * 溢位功能表（右上角）可讓您執行下列動作 
    * 編輯應用程式
    * 檢視所指定應用程式的度量值
    * 刪除應用程式 
    
建立 Range 應用程式時，會為其指派唯一的 IPv4 及 IPv6 位址。這些 IP 位址不是靜態的，可能會變更。您可以使用 DNS 來判定所指派的 IP 位址。DNS 名稱將一律傳回指派給該應用程式的 IP 位址。     
    
### 檢視度量值
{:#range-view-metrics}
您的應用程式現在已準備好透過 Cloudflare/CIS 進行 Proxy TCP 傳輸。

導覽至**度量值 > Range**，以檢視應用程式的連線數及傳輸量資料流量。
這些圖形顯示最多 10 個應用程式的度量值。
{:note}

您可以透過「圖表」鍵或按一下**選取應用程式**按鈕，來切換應用程式度量值。使用下拉功能表可以變更「度量值」資料時間範圍。

## Range AppTiles
{:#range-apptiles}
建立一些應用程式之後，會將應用程式磚移入**安全 > Range** 頁面中。應用程式磚包含下列資訊：
* 應用程式名稱
* 邊緣埠
* 原點及埠
* 過去一小時的連線（每分鐘輪詢）
* 過去一小時的傳輸量（每分鐘輪詢）


應用程式磚也會在頂端包含溢位功能表（3 個點）。溢位功能表可讓使用者選擇：
* 編輯應用程式
* 檢視所指定應用程式的度量值
  * 這會將使用者帶到**度量值 > Range** 頁面，其中只顯示該應用程式的度量值
* 刪除應用程式


## API 用法範例
{:#range-api-usage-examples}
這些範例是使用 Range 來建立及列出應用程式。

### 建立 Range 應用程式
{:#create-range-app}
有兩種方式可讓您在 Range 應用程式中指定原點
1. 原點 IP - 使用參數 `origin_direct`
2. 負載平衡器 - 使用參數 `origin_dns` 及 `origin_port`

**要求：**
```
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps \
  -H 'X-Auth-User-Token: <token>' \
  -d '{"protocol":"tcp/22","dns":{"type":"CNAME","name":"ssh.example.com"},"origin_direct":["tcp://172.0.2.1:22"],"proxy_protocol":true,"ip_firewall":true}'

```
**回應：**
```
{
    "result": {
        "id": "4f70c3d4f20576b79135b898295e8093",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_direct": [
            "tcp://172.0.2.1:22"
        ],
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-09T17:33:09.190606Z",
        "modified_on": "2019-01-09T17:33:09.190606Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}
```

**要求：**
```
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps \
  -H 'X-Auth-User-Token: <token>' \
  -d '{"protocol":"tcp/22","dns":{"type":"CNAME","name":"ssh.example.com"},"origin_dns": {"name": "test"},"proxy_protocol":true,"ip_firewall":true, "origin_port": 43}'

```
**回應：**
```
{
    "result": {
        "id": "4f70c3d4f20576b79135b898295e8093",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_dns": {
          "name": "test"
        },
        "origin_port": 43,
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-09T17:39:09.190606Z",
        "modified_on": "2019-01-09T17:39:09.190606Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}
```

**DNS 名稱：**您的應用程式與您網域上的 DNS 名稱相關聯。

**通訊協定/邊緣埠：**這是您應用程式執行所在的埠。通往這些位址的連線會進行 Proxy 處理到您的原點。

**原點直接：**這是您應用程式執行所在的 IP，以及您想要資料流量從邊緣到原點所通過的埠。

**IP 防火牆：**如已啟用，就會對這個 Range 應用程式施行具有「封鎖」動作的防火牆規則。

**PROXY 通訊協定：**如果您有支援「PROXY 通訊協定第 1 版」的行內 Proxy，請予以啟用。在大部分情況下，這項設定會保留停用狀態。

**原點 DNS：**這是您想要設為原點的負載平衡器名稱。

**原點埠：**這是服務的埠。 

### 列出所有應用程式
{:#range-list-all-apps}

**要求：**
```
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps
```

**回應：**
```
{
    "result": [
        {
            "id": "4f70c3d4f20546b79135b898295e8093",
            "protocol": "tcp/22",
            "dns": {
                "type": "CNAME",
                "name": "ssh.example.com"
            },
            "origin_direct": [
                "tcp://172.0.2.1:22"
            ],
            "ip_firewall": true,
            "proxy_protocol": true,
            "created_on": "2019-01-09T17:33:09.190606Z",
            "modified_on": "2019-01-09T17:33:09.190606Z"
        }
    ],
    "success": true,
    "errors": [],
    "messages": []
}
```

### 列出特定 Range 應用程式
{:#range-list-a-specific-range-app}
**要求：**
```
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps/4f70c3d4f20546b79135b898295e8093
```

**回應：**
使用原點 IP 的應用程式
```
{
    "result": {
        "id": "4f70c3d4f20546b79135b898295e8093",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_direct": [
            "tcp://172.0.2.1:22"
        ],
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-09T17:33:09.190606Z",
        "modified_on": "2019-01-09T17:33:09.190606Z"
    },
    "success": true,
    "errors": [],
    "messages": []
} 
```

使用負載平衡器的應用程式
```
{
    "result": {
        "id": "555359036e7f4acc82d69b916f62caba",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_dns": {
            "name": "test_update"
        },
        "origin_port": 76,
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-10T22:26:47.167008Z",
        "modified_on": "2019-01-10T22:26:47.167008Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}

```
