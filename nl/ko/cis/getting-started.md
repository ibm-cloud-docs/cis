---
copyright:
  years: 2018
lastupdated: "2018-03-19"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# IBM CIS(Cloud Internet Services) 시작하기

IBM CIS(Cloud Internet Services)는 워크플로우를 개선하기 위해 [보안](/docs/infrastructure/cis/managing-for-security.html), [안정성](/docs/infrastructure/cis/managing-for-reliability.html) 및 [성능](/docs/infrastructure/cis/managing-for-performance.html)의 세 가지 기본 기능을 제공합니다. 일단 IBM CIS 애플리케이션을 열면 기능의 각 영역이 화면의 왼쪽 탐색줄에 표시됩니다. 

각각의 기능마다 IBM CIS는 다음을 포함하여 특정 요구사항에 맞게 해당 기능을 튜닝하는 데 도움을 줍니다. 

 * 권한 DNS 서버
 * 글로벌 및 로컬 로드 밸런싱
 * WAF(Web Application Firewall)
 * DDoS 보호
 * 캐싱 및 페이지 규칙



## 시작하기 전에
IBM CIS 사용을 시작하려면 우선 [IBM ID](https://www.ibm.com/account/us-en/signup/register.html)가 필요합니다. 그리고 사용자는 환경 설정에 따라 IBM Cloud 계정을 통하거나 새 [IBM Cloud Internet Services 포털](https://console.bluemix.net/catalog/services/internet-services)을 통해 서비스를 주문할 수 있습니다. 

IBM Cloud Internet Services 사용 계정을 얻을 때 지원을 받으려면 시작하기와 관련된 추가 안내에 대해 [IBM 영업 담당자에게 문의](https://www.ibm.com/cloud-computing/bluemix/contact-us)하십시오. 

기존의 Softlayer 계정이 있는 경우에는 IBM ID로 [계정에 연결](https://console.bluemix.net/docs/account/softlayerlink.html#unifyingaccounts)할 수 있습니다.  

## 프로세스 개요

몇 가지 단계만 수행하면 인터넷 트래픽과 관련하여 IBM CIS 사용을 시작할 수 있습니다. 

 * IBM Cloud 대시보드에서 IBM CIS 애플리케이션을 여십시오. 
 * 관리할 도메인을 추가하십시오. 
 * 제공된 이름 서버로 DNS 정보를 구성하십시오. 
 * 튜토리얼을 따르거나 기타 기능을 설정하여 IBM CIS 시작하기를 계속 진행하십시오. 

### 1단계: IBM CIS 애플리케이션 열기

[IBM Cloud 대시보드](https://console.bluemix.net/catalog/)를 여십시오. 그리고 대시보드의 왼쪽 탐색줄에서 **플랫폼 -> 네트워크** 카테고리를 선택하여 IBM CIS 애플리케이션 아이콘으로 이동하십시오. 화면 중앙 근처에 표시되는 아이콘을 클릭하여 IBM Cloud Internet Services 애플리케이션을 여십시오.  

![카탈로그](images/catalog-cis-tile.png)

**개요 화면**

일단 IBM CIS 애플리케이션이 시작되면 IBM CIS **개요** 화면이 나타납니다. 그리고 UI 표시장치의 왼쪽 영역에서 **보안**, **안정성** 및 **성능**에 대한 탭이 나타납니다. 

**선택해야 할 플랜**

_조기 액세스_ 릴리스의 경우, 하나의 플랜만 선택할 수 있으며 이는 무료입니다. **개요** 화면의 왼쪽 하단의 **작성** 단추를 클릭하여 계정의 프로비저닝을 시작하십시오. 

**프로비저닝 시작**

IBM CIS 애플리케이션의 첫 번째 화면이 나타나며, 여기서 **도메인 추가** 단추를 선택하여 시작할 수 있습니다. 

|**참고로, 조기 액세스 프로그램은 계정당 하나의 인스턴스로 제한됩니다.** |
|-------------------------------------------------------------------|
| 리소스 인스턴스를 작성하고 이에 도메인을 추가한 후에는 IBM CIS의 새 리소스 인스턴스를 추가할 수 없습니다. 이 제한사항은 시범 도메인을 삭제한 후에 도메인을 다시 동일한 리소스 인스턴스에 추가하려는 경우에도 적용됩니다. 이를 수행하려고 시도하면 오류가 발생합니다. |

### 2단계: 도메인 추가 및 구성

도메인 또는 하위 도메인을 입력하여 웹 서비스의 성능 개선과 보호를 시작하십시오. 

**참고:** DNS 구역을 지정하십시오. 도메인의 등록자 또는 DNS 제공자에서 이러한 도메인이나 하위 도메인의 이름 서버를 구성할 수 있습니다. CNAME은 사용하지 마십시오. 

![시작하기](images/overview-add-domain.png)
개요 화면에서 `보류 중` 상태의 도메인을 표시합니다. 3단계를 완료할 때까지 도메인은 `보류 중` 상태를 유지합니다. 

**참고:** 도메인이 추가된 후에는 IBM CIS 인스턴스를 삭제할 수 없습니다. 인스턴스를 삭제하려면 우선 인스턴스에서 도메인을 삭제하십시오. 

### 3단계. 등록자 또는 기존 DNS 제공자로 이름 서버 구성

IBM CIS의 이점을 이용하기 시작하려면 나열된 이름 서버를 사용하도록 등록자 또는 도메인 이름 제공자를 구성하십시오. 도메인(종종 `example.com`와 유사함)을 위임 중인 경우에는 도메인 설정의 나열된 이름 서버를 구성하십시오. 여기서 이는 등록자에 의해 관리됩니다(예: 등록자의 웹 포털에서). 도메인의 등록자가 누구인지 잘 모르는 경우에는 다음에서 찾을 수 있습니다. https://whois.icann.org/ 다른 DNS 제공자에서 하위 도메인(예: `subdomain.example.com`)을 위임한 경우에는 각각의 나열된 이름 서버에 대해 이름 서버(NS) 레코드를 추가해야 합니다. 

등록자 또는 DNS 제공자를 구성한 후에 변경사항이 적용되려면 최대 24시간이 필요할 수 있습니다. 일단 지정된 이름 서버가 사용자의 도메인 또는 하위 도메인에 대해 올바르게 구성되어 있는지 확인되면, 도메인의 상태가 `보류 중`에서 `활성`으로 변경됩니다. 이름 서버를 구성한 후에 `개요` 페이지에서 "이름 서버 재확인" 링크를 클릭하여 잠재적으로 도메인의 활성화 속도를 높일 수 있습니다(한 시간에 한 번만 이 확인을 제출할 수 있음). 

### 4단계. IBM Cloud Internet Services가 애플리케이션, 호스트 이름 또는 웹 사이트의 도메인 정보를 해석 중인지 확인

계속하려면 왼쪽 탐색줄에서 **안정성** 탭을 선택하고 **DNS** 옵션을 선택하십시오. 반드시 적합한 _DNS 레코드_를 추가하십시오. **A 레코드** 및 채워진 **AAAA** 또는 **MX** 항목을 추가하십시오. 등록자의 위임이 완료되기 전에 해당 레코드를 추가하지 못한 경우, IBM Cloud Internet Services는 인터넷과 접하는 애플리케이션의 도메인 정보를 분석할 수 없습니다.   

![시작하기](images/dns-records.png)

### 5단계: 그 동안에 기타 IBM CIS 함수 및 기능 관리를 시작할 수 있습니다. 

기타 함수 및 기능 관리에 대한 상세 정보는 [단계별 지시사항](/docs/infrastructure/cis/how-to.html)을 참조하십시오. 
