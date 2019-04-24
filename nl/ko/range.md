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

Range 기능은 DDoS 보호, 로드 밸런싱 및 컨텐츠 가속화를 TCP 기반 프로토콜로 가져옵니다.
Range는 CIS/Cloudflare의 에지 노드에서 실행되는 글로벌 TCP 프록시입니다. 

Range를 사용하여 다음을 수행할 수 있습니다. 
* **계층 3 및 4 DDoS** 공격으로부터 TCP 포트 및 프로토콜을 보호합니다. 
* **TLS 암호화**를 사용하여 민감한 데이터를 염탐하고 훔치는 공격자의 능력을 감소시킵니다.
* TCP 서비스에 접근 시 IP 주소 또는 전체 IP 범위를 차단하거나 인증 확인할 수 있게 하는 CIS IP 방화벽으로 통합합니다. 
* 트래픽이 플로우되는 방향을 지시하도록 TCP 상태 검사, 장애 복구 및 조정 정책으로 로드 밸런서를 구성합니다.

## Range 시작하기
{:#getting-started-with-range}

Range는 추가 비용을 지불하는 엔터프라이즈 고객만 사용 가능하며 대역폭 사용량에 따라 가격이 책정됩니다.
{:note}

### 애플리케이션 추가
{:#range-add-an-application}
다음 단계를 수행하여 애플리케이션을 추가하십시오.

1. **보안 > Range**로 이동합니다.
1. **애플리케이션 추가** 단추를 클릭합니다. 
1. 첫 번째 입력 필드에 애플리케이션 이름을 입력합니다. 애플리케이션은 CIS 도메인의 DNS 이름과 연관됩니다.
1. 다음 입력 필드에 에지 포트를 입력합니다. 이 포트의 해당 주소에 대한 수신 연결을 청취합니다. 이러한 주소에 대한 연결은 오리진으로 프록싱됩니다. (프록싱은 포트 21을 제외한 모든 포트에서 지원됩니다.)
1. 오리진 섹션에 TCP 애플리케이션의 오리진 IP와 포트를 입력합니다. 기존 로드 밸런서를 선택할 수도 있습니다.
1. IP 방화벽을 사용으로 설정합니다. 사용하는 경우 "차단" 또는 "화이트리스트" 조치가 있는 방화벽 규칙이 이 애플리케이션에 적용됩니다. 국가 또는 ASN 기반 규칙은 아직 지원되지 않습니다.
1. PROXY 프로토콜 v1을 지원하는 프록시가 인라인인 경우 프록시 프로토콜을 사용으로 설정합니다. 이 기능은 트루 클라이언트 IP 지식이 필요한 서비스를 실행하는 경우에 유용합니다. 대부분의 경우 이 설정은 사용 불가능으로 유지되어야 합니다.
1. **프로비저닝**을 클릭합니다.

프록시 프로토콜은 모든 연결에 클라이언트 IP 주소 및 포트를 보고하는 헤더를 첨부합니다. 프록시 프로토콜 헤더의 형식은 다음과 같습니다.
  * PROXY_STRING + 하나의 공백 + INET_PROTOCOL + 하나의 공백 + CLIENT_IP + 하나의 공백 + PROXY_IP + 하나의 공백 + CLIENT_PORT + 하나의 공백 + PROXY_PORT + "\r\n"
  * 다음은 IPv4 주소에 대한 프록시 프로토콜 행의 예제입니다.
    `PROXY TCP4 192.0.2.0 192.0.2.255 42300 443\r\n`
  * 다음은 IPv6 주소에 대한 프록시 프로토콜 행의 예제입니다.
    `PROXY TCP6 2001:db8:: 2001:db8:ffff:ffff:ffff:ffff:ffff:ffff 42300 443\r\n`
   
Range 애플리케이션을 프로비저닝하면 앱마다 사용되는 대역폭 양에 따라 추가 비용이 발생합니다.
{:note}

애플리케이션은 이제 다음 특성이 있는 타일에서 볼 수 있습니다.
  * 애플리케이션 이름
  * 에지 포트
  * 오리진 및 포트
  * 지난 시간의 연결(매분 폴링됨)
  * 지난 시간의 처리량(매분 폴링됨)
  * 오버플로우 메뉴(맨 위 오른쪽 모서리)에서는 다음을 수행할 수 있습니다. 
    * 애플리케이션 편집
    * 지정된 애플리케이션의 메트릭 보기
    * 애플리케이션 삭제 
    
Range 애플리케이션이 작성되면 고유 IPv4 및 IPv6 주소가 지정됩니다. 이러한 IP 주소는 정적이 아니며 변경될 수 있습니다. DNS를 사용하여 지정된 IP 주소를 판별할 수 있습니다. DNS 이름은 항상 애플리케이션에 지정된 IP 주소를 리턴합니다.     
    
### 메트릭 보기
{:#range-view-metrics}
애플리케이션은 이제 Cloudflare/CIS를 통해 TCP 트래픽을 프록싱할 수 있습니다.

**메트릭 > Range**로 이동하여 애플리케이션에 대한 연결 수 및 처리량 트래픽을 보십시오.
그래프에는 최대 10개의 애플리케이션에 대한 메트릭이 표시됩니다.
{:note}

애플리케이션 메트릭은 차트 키를 통해 또는 **애플리케이션 선택** 단추를 클릭하여 토글할 수 있습니다. 메트릭 데이터 시간 범위는 드롭 다운 메뉴를 사용하여 변경할 수 있습니다.

## Range 앱 타일
{:#range-apptiles}
몇 가지 앱을 작성하면 **보안 > Range** 페이지가 애플리케이션 타일로 채워집니다. 애플리케이션 타일에는 다음 정보가 포함됩니다.
* 애플리케이션 이름
* 에지 포트
* 오리진 및 포트
* 지난 시간의 연결(매분 폴링됨)
* 지난 시간의 처리량(매분 폴링됨)


애플리케이션 타일의 맨 위 모서리에 오버플로우 메뉴가 포함됩니다(3개의 점). 오버플로우 메뉴는 사용자에게 다음을 수행할 옵션을 제공합니다.
* 애플리케이션 편집
* 지정된 애플리케이션의 메트릭 보기
  * 이를 통해 사용자는 **메트릭 > Range** 페이지로 이동하며, 이 페이지에는 이 애플리케이션에 대한 메트릭만 표시됩니다.
* 애플리케이션 삭제


## API 사용 예제
{:#range-api-usage-examples}
다음은 Range를 사용하여 애플리케이션을 작성하고 나열하는 예제입니다.

### Range 앱 작성
{:#create-range-app}
Range 앱에서 오리진을 지정할 수 있는 방법은 다음 두 가지입니다.
1. 오리진 IP - 매개변수 `origin_direct` 사용
2. 로드 밸런서 - 매개변수 `origin_dns` 및 `origin_port` 사용

**요청:**
```
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps \
  -H 'X-Auth-User-Token: <token>' \
  -d '{"protocol":"tcp/22","dns":{"type":"CNAME","name":"ssh.example.com"},"origin_direct":["tcp://172.0.2.1:22"],"proxy_protocol":true,"ip_firewall":true}'

```
**응답:**
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

**요청:**
```
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps \
  -H 'X-Auth-User-Token: <token>' \
  -d '{"protocol":"tcp/22","dns":{"type":"CNAME","name":"ssh.example.com"},"origin_dns": {"name": "test"},"proxy_protocol":true,"ip_firewall":true, "origin_port": 43}'

```
**응답:**
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

**DNS 이름:** 애플리케이션은 도메인의 DNS 이름과 연관됩니다.

**프로토콜/에지 포트:** 이는 애플리케이션이 실행되는 포트입니다. 이러한 주소에 대한 연결은 오리진에 프록싱됩니다.

**오리진 방향:** 이는 애플리케이션이 실행되는 IP 및 트래픽이 에지에서 오리진으로 플로우되도록 할 포트입니다.

**IP 방화벽:** 사용하는 경우, 차단 조치가 있는 방화벽 규칙이 이 Range 애플리케이션에 적용됩니다.

**프록시 프로토콜:** 프록시 프로토콜 v1을 지원하는 프록시가 인라인인 경우 사용하십시오. 대부분의 경우 이 설정은 사용 불가능으로 유지됩니다.

**오리진 DNS:** 이는 오리진으로 설정할 로드 밸런서의 이름입니다.

**오리진 포트:** 이는 서비스의 포트입니다. 

### 모든 앱 나열
{:#range-list-all-apps}

**요청:**
```
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps
```

**응답:**
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

### 특정 Range 앱의 목록
{:#range-list-a-specific-range-app}
**요청:**
```
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps/4f70c3d4f20546b79135b898295e8093
```

**응답:**
오리진 IP를 사용하는 앱
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

로드 밸런서를 사용하는 앱
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
