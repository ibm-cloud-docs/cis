---

copyright:
  years: 2018
lastupdated: "2018-03-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}


# DNS 개념

이 문서에는 인터넷의 DNS(Domain Name System)와 관련된 일부 개념 및 정의와 IBM CIS(Cloud Internet Services) 배치에 어떻게 영향을 주는지가 포함되어 있습니다.  

DNS(Domain Name System)는 우리가 매일 사용하는 웹의 근간을 이룹니다. 이는 투명하게 백그라운드에서 작동하며, 사람이 읽을 수 있는 웹 사이트 이름을 [인터넷의 IPv6용 RFC 4193 및 IPv4용 RFC 1918 가이드라인](https://en.wikipedia.org/wiki/Private_network)을 준수하는 컴퓨터가 읽을 수 있는 숫자 IP 주소로 변환합니다. 간단히 말하면, DNS 서버는 도메인 이름(예: 'ibm.com')을 대부분의 사람들이 알 필요가 없는 연관된 IP 주소와 일치시킵니다. 

DNS 시스템은 인터넷 상의 링크된 DNS 서버의 네트워크에서 이 IP 주소와 호스트 이름 정보를 찾으며, 이는 마치 사람들이 전화번호부나 지도를 사용하여 특정 위치를 찾는 방법과 유사합니다. 

## 이름 서버
**이름 서버**는 디렉토리 서비스에 대한 조회의 응답을 제공하는 서비스를 구현합니다. 이는 의미 있는 텍스트 기반의 웹 또는 호스트 ID를 IP 주소로 변환합니다. 

**이름 서버 위임**은 도메인에 대한 이름 서버가 하위 도메인의 레코드에 대한 요청을 수신할 때 발생하고, 위임 서버에 대한 이름 서버의 참조로 응답합니다. 이 기능을 사용하면 대형 도메인(예: `ibm.com`)의 관리를 분권화할 수 있습니다. 

**사용자 정의 도메인 이름 서버**를 사용하면 자체 도메인의 사용자 정의된 참조 이름으로 DNS 제공자의 서버를 활용할 수 있습니다. 예를 들어, `ns1.acme.com` 대신에 `ns1.cloud.ibm.com`이 되도록 이름 서버를 정의할 수 있습니다. 

## 보안 DNS

**DNSSec**은 유효함을 보장할 수 있도록 DNS 데이터를 디지털 '서명'하는 기술입니다. 인터넷의 취약성을 제거하려면 루트 구역에서 최종 도메인 이름(예: www.icann.org)까지 검색의 각 단계에 DNSSec을 배치해야 합니다. 
