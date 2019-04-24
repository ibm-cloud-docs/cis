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

# 范围
{:#cis-range}

“范围”功能为任何基于 TCP 的协议引入 DDoS 保护、负载均衡和内容加速。
“范围”是在 CIS/Cloudflare 的边缘节点上运行的全局 TCP 代理。 

“范围”可用于： 
* 保护 TCP 端口和协议免受**第 3 层和第 4 层 DDoS** 攻击。 
* 通过启用 **TLS 加密**，降低攻击者监听和窃取敏感数据的能力。
* 与 CIS IP 防火墙集成，该防火墙允许您阻止 IP 地址或整个 IP 范围访问 TCP 服务，或者对这些 IP 地址或范围进行质询。 
* 使用 TCP 运行状况检查、故障转移和转向装置策略来配置负载均衡器，以指明流量应该流向的位置。

## “范围”入门
{:#getting-started-with-range}

“范围”仅适用于企业客户，需额外成本，并且按带宽使用量计费。
{:note}

### 添加应用程序
{:#range-add-an-application}
要添加应用程序，请执行以下步骤。

1. 导航至**安全性 > 范围**
1. 单击**添加应用程序**按钮 
1. 在第一个输入字段中输入应用程序名称。应用程序将与 CIS 域上的 DNS 名称相关联。
1. 在下一个输入字段中输入边缘端口。我们将在此端口上侦听这些地址的入局连接。与这些地址的连接将采用针对源服务器的代理。（在除端口 21 之外的所有端口上支持代理。）
1. 在“源”部分中，输入 TCP 应用程序的源 IP 和端口。您还可以选择现有负载均衡器
1. 启用 IP 防火墙。在启用时，将针对此应用程序实施包含“阻止”或“白名单”操作的防火墙规则。尚不支持基于国家或地区或者 ASN 的规则。
1. 如果您有支持 PROXY Protocol v1 的内置代理，请启用代理协议。如果正在运行需要了解真实客户机 IP 的服务，那么此功能非常有用。在大多数情况下，此设置应该保持禁用。
1. 单击**供应**

“代理协议”将在每个连接前面添加用于报告客户机 IP 地址和端口的头。“代理协议”头具有以下格式：
  * PROXY_STRING + 单个空格 + INET_PROTOCOL + 单个空格 + CLIENT_IP + 单个空格 + PROXY_IP + 单个空格 + CLIENT_PORT + 单个空格 + PROXY_PORT + "\r\n"
  * 以下是针对 IPv4 地址的示例“代理协议”行：`PROXY TCP4 192.0.2.0 192.0.2.255 42300 443\r\n`
  * 以下是针对 IPv6 地址的示例“代理协议”行：`PROXY TCP6 2001:db8:: 2001:db8:ffff:ffff:ffff:ffff:ffff:ffff 42300 443\r\n`
   
供应“范围”应用程序将产生基于每个应用程序使用的带宽量的额外成本。
{:note}

现在，您的应用程序在磁贴中显示，具有以下属性：
  * 应用程序名称
  * 边缘端口
  * 源和端口
  * 过去 1 小时的连接数（每分钟轮询）
  * 过去 1 小时的吞吐量（每分钟轮询）
  * 溢出菜单（右上角）允许以下功能 
    * 编辑应用程序
    * 查看指定应用程序的度量值
    * 删除应用程序 
    
创建“范围”应用程序时，将为其分配唯一的 IPv4 和 IPv6 地址。这些 IP 地址非静态，并且可能会更改。您可以使用 DNS 来确定分配的 IP 地址。DNS 名称将始终返回分配给应用程序的 IP 地址。     
    
### 查看度量值
{:#range-view-metrics}
应用程序现在已准备好通过 Cloudflare/CIS 代理 TCP 流量。

导航至**度量值 > 范围**以查看应用程序的连接数和吞吐量流量。
图形最多显示 10 个应用程序的度量值。
{:note}

可通过图表键或通过单击**选择应用程序**按钮来切换应用程序度量值。可使用下拉菜单更改“度量值”数据时间范围。

## 范围应用程序磁贴
{:#range-apptiles}
创建一些应用程序后，将使用应用程序磁贴填充**安全性 > 范围**页面。应用程序磁贴包含以下信息：
* 应用程序名称
* 边缘端口
* 源和端口
* 过去 1 小时的连接数（每分钟轮询）
* 过去 1 小时的吞吐量（每分钟轮询）


应用程序磁贴还在上角（3 个点）包含溢出菜单。溢出菜单为用户提供以下选项：
* 编辑应用程序
* 查看指定应用程序的度量值
  * 这会将用户转至**度量值 > 范围**页面，此页面仅显示该应用程序的度量值
* 删除应用程序


## API 用法示例
{:#range-api-usage-examples}
以下是使用“范围”创建和列出应用程序的示例。

### 创建“范围”应用程序
{:#create-range-app}
可通过两种方法在“范围”应用程序中指定源
1. 源 IP - 使用参数 `origin_direct`
2. 负载均衡器 - 使用参数 `origin_dns` 和 `origin_port`

**请求：**
```
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps \
  -H 'X-Auth-User-Token: <token>' \
  -d '{"protocol":"tcp/22","dns":{"type":"CNAME","name":"ssh.example.com"},"origin_direct":["tcp://172.0.2.1:22"],"proxy_protocol":true,"ip_firewall":true}'

```
**响应：**
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

**请求：**
```
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps \
  -H 'X-Auth-User-Token: <token>' \
  -d '{"protocol":"tcp/22","dns":{"type":"CNAME","name":"ssh.example.com"},"origin_dns": {"name": "test"},"proxy_protocol":true,"ip_firewall":true, "origin_port": 43}'

```
**响应：**
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

**DNS 名称：**应用程序与域上的 DNS 名称相关联。

**协议/边缘端口：**这是应用程序运行所在的端口。与这些地址的连接将采用针对源服务器的代理。

**源直接：**这是应用程序运行所在的 IP 以及想要从边缘到源的流量流经的端口。

**IP 防火墙：**如果启用，将针对此“范围”应用程序实施包含“阻止”操作的防火墙规则。

**PROXY 协议：**如果您具有支持 PROXY 协议 v1 的内置代理，那么启用。在大多数情况下，此设置保持禁用。

**源 DNS：**这是要设置为源的负载均衡器的名称。

**源端口：**这是服务的端口。 

### 列出所有应用程序
{:#range-list-all-apps}

**请求：**
```
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps
```

**响应：**
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

### 列出特定“范围”应用程序
{:#range-list-a-specific-range-app}
**请求：**
```
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps/4f70c3d4f20546b79135b898295e8093
```

**响应：**
使用源 IP 的应用程序
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

使用负载均衡器的应用程序
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
