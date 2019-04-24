---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: API Specs, CIS APIs

subcollection: cis

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# API 스펙
{:#api-specs}

CIS API 스펙을 보는 방법은 다음과 같습니다. 

1. CIS API를 보려면 [API 문서](/apidocs/) 페이지로 이동합니다. 

2. 왼쪽 탐색 메뉴에서 네트워킹 상자를 선택하여 API를 필터링합니다.

3. 사용 가능한 Cloud Internet Services API 목록에서 선택합니다.


## 참고
{:#api-notes}

1. API 엔드포인트: `https://api.cis.cloud.ibm.com`.

2. **X-Auth-User-Token** 헤더가 각 API 호출에 필요합니다. 이 헤더는 IAM에서 검색할 수 있는 사용자에 대한 베어러 토큰입니다(예: `ibmcloud iam oauth-tokens` 명령 사용).

3. **crn** 필드도 각 API 호출의 경로에서 반드시 필요합니다. 이 필드에는 구성 중인 CIS 리소스 인스턴스에 대한 전체 CRN(Cloud Resource Name)이 있습니다. (예를 들어, 리소스 인스턴스의 CRN은 `ibmcloud resource service-instance <instance-name>` 명령을 사용하여 해당 이름으로 검색할 수 있습니다.) CRN은 API 호출에서 URL 인코딩되어 있어야 합니다.

4. API 호출 속도에는 제한이 있습니다. 1분에 총 100개의 API 호출이 작성될 수 있습니다. 이 속도를 초과하면 후속 호출이 일정 시간 동안 차단됩니다.
