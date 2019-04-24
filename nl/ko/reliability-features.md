---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM Cloud Internet Services, reliable IBM Cloud Internet Services, Global Load Balancing

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# IBM Cloud Internet Services(CIS)가 작업의 안정화를 유지하는 방법
{:#how-cis-keeps-your-work-reliable}

애플리케이션 및 인프라 가동 중단으로 인한 작동 중지 시간을 피하는 데 도움이 되므로 IBM Cloud Internet Services(CIS)는 웹 서비스와 애플리케이션의 안정성을 개선하는 데 도움이 됩니다. 예를 들어, 글로벌 로드 밸런싱을 사용하면 여러 지역에 웹 서비스와 애플리케이션을 배치할 수 있습니다. 글로벌 로드 밸런싱이 사용되는 경우, IBM CIS는 고객 요청을 사용 가능한 최인접 지역으로 라우팅합니다. 임의의 지역에서 장애가 발생하면 요청이 다음의 최인접 위치로 라우팅되므로 고객은 작동 중지에 따른 영향을 받지 않습니다. 웹 사이트 또는 API에서 장애가 발생하는 경우, IBM CIS는 자동으로 알림을 발송하며 복원 시점을 알려줍니다.


![reliability-graphic.png](images/reliability-graphic.png)

다음은 빠른 기능 개요입니다.

## 안정성 기능
{:#cis-reliability-features}

 * 글로벌 로드 밸런싱 
 * 로드 밸런싱을 위한 프록시 및 비-프록시 옵션
 * 오리진 풀 및 상태 모니터
 * DNS 관리
 
### 요약
{:#cis-reliability-features-summary}
 
  * 상태 모니터는 오리진 풀의 상태가 정상인지 여부를 확인합니다.
  * 상태 모니터에서 장애가 발생하면 요청이 정상 상태의 오리진으로 다시 라우팅됩니다.
  * 사용자는 웹 서비스나 API에서 장애가 발생하는 시점과 복원된 시점에 대해 지속적으로 알림을 받습니다.
