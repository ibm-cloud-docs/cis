---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: domain Input information, IBM Cloud Internet Services, Global Load balancing

subcollection: cis

---


{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# IBM Cloud Internet Services에서 글로벌 로드 밸런싱으로 애플리케이션 안정성 및 확장성 향상
{:#improving-application-reliability-and-scalability-with-global-load-balancing-from-ibm-cloud-internet-services}

전자 상거래 웹 사이트가 있거나 일반 사용자가 항상 액세스할 수 있어야 하는 애플리케이션을 호스팅하는 경우, 애플리케이션의 24시간 가용성 및 성능을 고려할 수 있습니다. 

IBM Cloud Internet Services(CIS)에서 사용 가능한 글로벌 로드 밸런싱 기능을 사용하면 최고의 일반 사용자 경험을 제공하면서 애플리케이션의 안정성과 확장성을 향상시킬 수 있습니다. 이 안내서에서는 글로벌 로드 밸런싱 구성에 대한 둘러보기를 제공합니다.  

## 수행할 작업
{:#what-you-accomplish}

단계별로 다음에 설명된 방법과 유사하게 설정을 구성하는 방법을 알아봅니다.

<img src="images/reliability1.png" alt="그림" style="width: 300px;"/>

이 예제에서 애플리케이션 리소스는 두 데이터 센터 위치(미국 서부의 한 곳과 미국 동부 해안의 한 곳)에 배치됩니다. 일반 사용자는 전 세계에서 이 애플리케이션에 액세스할 수 있습니다. 

태스크 |설명
------------- | -------------
[CIS 인스턴스 작성](/docs/infrastructure/cis?topic=cis-create-your-ibm-cloud-internet-services-cis-instance) | IBM 고객 포털을 사용하여 IBM Cloud Internet Services(CIS) 인스턴스 작성을 시작합니다. |
[도메인에 대한 정보 입력](/docs/infrastructure/cis?topic=cis-input-information-about-your-domain) | 글로벌 로드 밸런싱을 보호하고 제공할 도메인에 대한 정보를 입력합니다.
[글로벌 로드 밸런서 구성 시작](/docs/infrastructure/cis?topic=cis-begin-global-load-balancer-configuration) | 글로벌 로드 밸런서 구성을 시작합니다.
[애플리케이션 리소스 식별](/docs/infrastructure/cis?topic=cis-identify-your-application-resources) | 애플리케이션의 리소스(예: 오리진 풀 및 상태 검사 메커니즘)를 식별합니다.
[글로벌 로드 밸런서 정의](/docs/infrastructure/cis?topic=cis-define-the-global-load-balancer) | 호스트 이름을 지정하고 오리진 풀을 추가하고 조정하며 추가 규칙을 정의하여 클라이언트에 트래픽을 제공하는 방법을 제어함으로써 글로벌 로드 밸런서 구성을 정의합니다.
