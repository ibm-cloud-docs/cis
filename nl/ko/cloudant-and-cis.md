---

copyright:
  years: 2019
lastupdated: "2019-03-28"

keywords: Cloudant database, CORS, cross-origin resource sharing, host header

subcollection: cis

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"} 
{:note: .note}


# IBM Cloud Internet Services를 통해 Cloudant 데이터베이스 액세스
{: #access-cloudant-through-cis}

IBM Cloud Internet Services(CIS)를 통해 Cloudant 데이터베이스에 액세스하려면 다음 단계를 수행하십시오.

## 시작하기 전에
{: #access-cloudant-through-cis-begin}

다음 지시사항에서는 [시작하기](/docs/infrastructure/cis?topic=cis-getting-started-with-ibm-cloud-internet-services-cis-) 페이지에 요약된 대로 CIS에 도메인을 이미 추가했다고 가정합니다.

### 1단계. CORS(Cross-Origin Resource Sharing)에 CIS 도메인 추가
{: #access-cloudant-through-cis-step1}

* Cloudant 데이터베이스로 이동하여 `계정` -> `CORS` 페이지를 엽니다.
* 오리진 도메인 입력 필드에 CIS 도메인을 추가합니다. 예를 들어, `https://cloudant.test.foo.com`입니다.

### 2단계. Cloudant 데이터베이스를 가리키도록 CIS 구성
{: #access-cloudant-through-cis-step2}

* CIS 대시보드로 이동하고 Cloudant 데이터베이스 호스트 이름을 가리키는 로드 밸런서 또는 DNS 레코드를 작성합니다. 예를 들어, `https://cloudant.test.foo.com` -> `111-222-333-444-555-test.cloudant.com`입니다.
* DNS 레코드 또는 로드 밸런서에 `프록시`를 사용합니다.


### 3단계. 호스트 헤더 대체를 설정하기 위한 페이지 규칙 작성
{: #access-cloudant-through-cis-step3}

* CIS 대시보드에서 `성능` -> `페이지 규칙`으로 이동합니다.
* 원하는 URL(예: `https://cloudant.test.foo.com/*`)의 페이지 규칙을 작성합니다.
* 규칙 동작 설정 `호스트 헤더 대체`를 선택합니다.
* Cloudant 데이터베이스 호스트 이름(예: `111-222-333-444-555-test.cloudant.com`)으로 설정합니다.

Cloudant에 대한 자세한 정보는 [Coudant 문서](/docs/services/Cloudant?topic=cloudant-getting-started-with-cloudant)를 참조하십시오.
