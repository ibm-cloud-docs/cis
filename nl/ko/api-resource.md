---

copyright:
  years: 2018
lastupdated: "2018-03-22"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# API 스펙

CIS API 스펙을 보는 방법은 다음과 같습니다.  

1. CIS API를 보려면 [CIS API 스펙](https://console.bluemix.net/apidocs/2640-cloud-internet-services) 페이지로 이동하십시오.  

2. 왼쪽 탐색 메뉴의 사용 가능한 API 목록에서 API를 선택하십시오. 


## 참고

1. API 엔드포인트: https://api.cis.cloud.ibm.com.

2. **X-Auth-User-Token** 헤더는 각각의 API 호출에 반드시 필요합니다. 이는 IAM에서 검색될 수 있는 사용자에 대한 베어러 토큰입니다(예: "bx iam oauth-tokens" 명령 사용). 

3. **crn** 필드도 각 API 호출의 경로에서 반드시 필요합니다. 이는 구성 중인 CIS 리소스 인스턴스의 전체 CRN(Cloud Resource Name)입니다(예: 리소스 인스턴스의 CRN은 "bx resource service-instance <instance-name>" 명령을 사용하여 해당 이름에서 검색이 가능함). CRN은 API 호출에서 URL 인코딩되어 있어야 합니다. 

4. API 호출 속도에는 제한이 있습니다. 1분에 총 100개의 API 호출이 작성될 수 있습니다. 이 속도를 벗어나면 일정 시간 동안 후속 호출이 차단됩니다. 
