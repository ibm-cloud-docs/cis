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

# IBM CIS의 DNS(Domain Name System) 설정

이 문서에는 보안 DNS 구성 방법을 포함하여 IBM CIS DNS 레코드 구성 방법에 대한 일부 특정 지시사항이 포함되어 있습니다. 

## 보안 DNS

**DNSSec**은 유효함을 보장할 수 있도록 DNS 데이터를 디지털 '서명'하는 기술입니다. 인터넷의 취약성을 제거하려면 루트 구역에서 최종 도메인 이름(예: www.icann.org)까지 검색의 각 단계에 DNSSec을 배치해야 합니다. 

## 보안 DNS 구성 및 관리 

DNSSec은 인증 계층을 인터넷의 DNS 인프라에 추가하며, 그렇지 않으면 이는 안전하지 않습니다. 보안 DNS는 도메인 이름을 웹 브라우저에 입력할 때 방문자가 **사용자의** 웹 서버로 경로 지정되도록 보장합니다. 사용자는 단지 IBM CIS 계정에서 DNS 페이지의 DNSSec을 사용하고 DS 레코드를 등록자에 추가하기만 하면 됩니다. 

![보안 DNS](images/dns/secure-dns.png)

**DS 레코드 보기** 단추를 선택하여 DS 레코드를 등록자에 추가하는 방법을 설명하는 대화 상자를 열 수 있습니다. 사용자는 DS 레코드의 일부를 복사하고 이를 등록자의 대시보드에 붙여넣어야 합니다. 모든 등록자는 서로 다르며 사용자의 등록자는 단지 사용 가능한 일부 필드에 대한 정보를 입력하도록 사용자에게 요구할 수 있습니다. 

## DNS 레코드 추가

**유형** 드롭 다운을 사용하여 작성할 레코드의 유형을 선택할 수 있습니다. 각각의 DNS 레코드 유형에는 이와 연관된 이름과 TTL(Time-To-Live)이 있습니다.  

도메인 이름이 이미 필드에 수동으로 추가되어 있지 않는 한 이름 필드에 입력되는 모든 항목에는 도메인 이름이 이에 추가됩니다(예: `www` 또는 `www.example.com`이 필드에 입력되면 API에서 둘 모두를 `www.example.com`으로 처리함). 정확한 도메인 이름이 이름 필드에 입력된 경우, 이는 더 이상 추가되지 않습니다(예: `example.com`이 `example.com`로서 처리됨). 그러나 DNS 레코드의 목록에서는 도메인 이름이 덧붙여지지 않은 이름만 표시합니다. 따라서 `www.example.com`은 `www`로 표시되며 `example.com`은 `example.com`으로 표시됩니다. TTL의 기본값은 `Automatic`이지만 사용자는 이를 변경할 수 있습니다. 프록싱 DNS 레코드의 TTL이 항상 `Automatic`이므로, 새로 프록싱된 레코드는 이러한 변경을 수행하는 중에 이 구성으로 변경됩니다. 

### A 유형 레코드

이 레코드 유형을 추가하려면 올바른 값이 **이름** 및 **IPv4 주소** 필드에 존재해야 합니다. 'Automatic'의 기본값으로 드롭 다운 메뉴에서 **TTL**을 지정할 수도 있습니다. 

![A 유형 레코드 작성](images/dns/create-a-type-record.png)

    필수 필드: 이름, IPv4 주소
    선택적 필드: TTL(기본값: Automatic)

### AAAA 유형 레코드

이 레코드 유형을 추가하려면 올바른 값이 **이름** 및 **IPv6 주소** 필드에 존재해야 합니다. 'Automatic'의 기본값으로 드롭 다운 메뉴에서 **TTL**을 지정할 수도 있습니다. 

![AAAA 유형 레코드 작성](images/dns/create-aaaa-type-record.png)

    필수 필드: 이름, IPv6 주소
    선택적 필드: TTL(기본값: Automatic)

### CNAME 유형 레코드

이 레코드 유형을 추가하려면 올바른 값이 **이름** 필드에 존재해야 하며 완전한 도메인 이름이 **도메인 이름**(FQDN) 필드에 있어야 합니다. 'Automatic'의 기본값으로 드롭 다운 메뉴에서 **TTL**을 지정할 수도 있습니다. 


![CNAME 유형 레코드 작성](images/dns/create-cname-type-record.png)

    필수 필드: 도메인 이름(CNAME의 경우)
    선택적 필드: TTL(기본값: Automatic)


### MX 유형 레코드

이 레코드 유형을 추가하려면 올바른 값이 **이름** 필드에 존재해야 하며 유효한 주소가 **메일 서버** 필드에 존재해야 합니다. 'Automatic'의 기본값으로 드롭 다운 메뉴에서 **TTL**을 지정할 수도 있습니다. 

![MX 유형 레코드 작성](images/dns/create-mx-type-record.png)

    필수 필드: 이름, 메일 서버
    선택적 필드: TTL(기본값: Automatic), 우선순위(기본값: 1) 

### LOC 유형 레코드

이 레코드 유형을 추가하려면 올바른 값이 **이름** 필드에 존재해야 합니다. 보다 특정한 정보가 필요하면 **LOC 옵션 구성** 단추를 선택하십시오. 'Automatic'의 기본값으로 드롭 다운 메뉴에서 **TTL**을 지정할 수도 있습니다. 

![LOC 유형 레코드 작성](images/dns/create-loc-type-record-1.png)

    필수 필드: 이름
    선택적 필드: LOC 옵션(구성하려면 단추 클릭)

![LOC 유형 레코드 작성](images/dns/create-loc-type-record-2.png)

### CAA 유형 레코드

이 레코드 유형을 추가하려면 올바른 값이 **이름** 및 **값** 필드에 존재해야 합니다. 값 필드는 기본값이 "URL에 위반 보고서 전송"인 **태그** 드롭 다운 필드의 값과 연관성이 있습니다. 'Automatic'의 기본값으로 드롭 다운 메뉴에서 **TTL**을 지정할 수도 있습니다. 

![CAA 유형 레코드 작성](images/dns/create-caa-type-record.png)

    필수 필드: 이름, 값(태그와 연관됨)
    선택적 필드: TTL(기본값: Automatic), 태그(기본값: URL에 위반 보고서 전송)

### SRV 유형 레코드

이 레코드 유형을 추가하려면 올바른 값이 **이름**, **서비스 이름** 및 **대상** 필드에 존재해야 합니다. 드롭 다운 메뉴를 사용하여 **프로토콜**을 선택하십시오(기본값: UDP 프로토콜). 추가로 **우선순위**, **가중치** 및 **포트**를 지정할 수 있습니다. 이러한 세 개의 필드는 기본값이 1입니다. 'Automatic'의 기본값으로 드롭 다운 메뉴에서 **TTL**을 지정할 수도 있습니다. 

![SRV 유형 레코드 작성](images/dns/create-srv-type-record.png)

    필수 필드: 이름, 서비스 이름, 대상
    선택적 필드: TTL(기본값: Automatic), 프로토콜(기본값: UDP), 우선순위(기본값: 1), 가중치(기본값: 1), 포트(기본값: 1)

### SPF 유형 레코드

이 레코드 유형을 추가하려면 올바른 값이 **이름** 및 **컨텐츠** 필드에 존재해야 합니다. 'Automatic'의 기본값으로 드롭 다운 메뉴에서 **TTL**을 지정할 수도 있습니다. 

![SPF 유형 레코드 작성](images/dns/create-spf-type-record.png)

    필수 필드: 이름, 컨텐츠
    선택적 필드: TTL(기본값: Automatic)

### TXT 유형 레코드

이 레코드 유형을 추가하려면 올바른 값이 **이름** 및 **컨텐츠** 필드에 존재해야 합니다. 'Automatic'의 기본값으로 드롭 다운 메뉴에서 **TTL**을 지정할 수도 있습니다. 

![TXT 유형 레코드 작성](images/dns/create-txt-type-record.png)

    필수 필드: 이름, 컨텐츠
    선택적 필드: TTL(기본값: Automatic)

### NS 유형 레코드

이 레코드 유형을 추가하려면 올바른 값이 **이름** 및 **이름 서버** 필드에 존재해야 합니다. 'Automatic'의 기본값으로 드롭 다운 메뉴에서 **TTL**을 지정할 수도 있습니다. 

![NS 유형 레코드 작성](images/dns/create-ns-type-record.png)

    필수 필드: 이름, 이름 서버
    선택적 필드: TTL(기본값: Automatic)

## DNS 레코드 업데이트

각각의 레코드 행에서 메뉴의 **레코드 편집** 옵션을 클릭할 수 있습니다. 그러면 대화 상자가 열리며 이를 사용하여 레코드를 업데이트할 수 있습니다. 

![DNS 레코드 편집](images/dns/edit-dns-record.png)

예를 들어, 이는 **A** 유형 레코드에 대한 업데이트 대화 상자입니다. 일단 변경이 완료되면 **레코드 업데이트**를 선택하여 이를 저장하십시오. 

![DNS 레코드 편집 대화 상자](images/dns/update-dns-dialog.png)

## 레코드 삭제

각각의 레코드 행에서 메뉴의 **레코드 삭제** 옵션을 선택할 수 있습니다. 그러면 삭제 프로세스를 확인하는 대화 상자가 열립니다. 

![DNS 레코드 삭제](images/dns/delete-record.png)

**삭제** 단추를 선택하여 삭제 조치를 확인할 수 있습니다. 삭제를 원하지 않으면 **취소**를 선택하십시오. 

![DNS 레코드 삭제 대화 상자](images/dns/delete-record-dialog.png)
