---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: edge functions beta, edge functions

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Edge Functions(베타)
{: #edge-functions}

CIS Edge Functions를 사용하면 인프라를 구성하거나 유지보수하지 않고도 서버리스(serverless) 실행 환경을 활용하여 새 애플리케이션을 작성하거나 기존 애플리케이션을 수정할 수 있습니다. Edge Functions를 정의하고 클라우드 에지로 업로드하여 오리진에 도달하기 전에 요청을 처리할 수 있습니다. CIS Edge Functions를 사용하여 HTTP 요청 및 응답을 수정하거나 병렬 요청을 작성하거나 클라우드 에지에서 응답을 생성할 수 있습니다.

## Edge Functions의 작동 방식
{: #how-edge-functions-work}

Edge Functions는 **조치**를 정의된 도메인을 기반으로 하는 URI와 연관시킵니다. 이 연관은 **트리거**라고 합니다. 사이트에 대한 수신 요청은 클라우드의 에지에서 인터셉트되고 계정이나 도메인의 트리거에 대해 일치됩니다. 요청 URL이 트리거의 URI와 일치하는 경우 트리거와 연관된 조치가 실행됩니다.

Edge Functions는 최신 웹 브라우저에서 사용 가능한 [서비스 작업자](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)에서 모델링되며 가능하면 동일한 API를 사용합니다.

서비스 작업자 API를 사용하면 사이트에 작성된 요청을 인터셉트할 수 있습니다. JavaScript가 요청을 처리하고 나면 사용자 사이트나 다른 사이트에 대한 임의의 수의 하위 요청을 작성하고 마지막으로 방문자에게 원하는 응답을 리턴하도록 선택할 수 있습니다.

표준 서비스 작업자와 달리 Edge Functions는 사용자의 브라우저가 아닌 CIS 에지 서버에서 실행됩니다. 즉, 악성 클라이언트가 우회할 수 없는 신뢰 환경에서 코드가 실행된다는 점을 믿을 수 있습니다. 또한 사용자는 서비스 작업자를 지원하는 최신 브라우저를 사용하지 않아도 됩니다. 브라우저가 아닌 API 클라이언트에서 요청을 인터셉트할 수도 있습니다.

내부적으로 Edge Functions는 Google Chrome 브라우저에 사용되는 동일한 V8 JavaScript 엔진을 사용하여 인프라에서 작업자를 실행합니다. V8은 동적으로 JavaScript 코드를 매우 빠른 기계 코드로 컴파일하며, 이를 통해 성능이 향상됩니다. 이렇게 하면 코드가 마이크로초 단위로 실행되고 에지가 초당 수천 개의 스크립트를 실행할 수 있습니다.

Edge Functions는 V8을 사용하지만 Node.js는 사용하지 않습니다. 작업자 내에서 사용 가능한 JavaScript API는 당사에 의해 직접 구현됩니다. 직접 V8로 작업을 수행하면 고객과 인프라를 안전하게 유지하는 데 필요한 보안 제어를 사용하여 효율적으로 코드를 실행할 수 있습니다.


## 조치
{: #edge-functions-actions}

조치는 Javascript로 작성되며 이 조치에서 이벤트 리스너는 트리거 이벤트에 응답해야 합니다. 조치는 트리거에서 사용되는 경우를 제외하고 트래픽에 영향을 주지 않습니다. 

### 엔터프라이즈 플랜 대 표준 플랜
{: #edge-functions-enterprise-v-standard-plans}

표준 플랜에는 최대 하나의 조치가 있습니다. 조치에 도메인과 동일한 이름이 지정됩니다. 다른 파일을 업로드하여 조치를 바꾸거나 코드 편집기를 사용하여 조치를 업데이트할 수 있습니다. 다른 파일을 업로드하면 기존 조치가 제거됩니다.

엔터프라이즈 플랜은 스크립트를 무제한 업로드할 수 있습니다. 이름은 고유하게 지정될 수 있습니다.

### 조치 작성
{: #edge-functions-create-actions}

코드 편집기를 사용하여 조치를 추가하려면 **작성**을 선택하십시오. 엔터프라이즈 플랜에서는 조치의 이름을 입력하십시오. 표준 플랜에서는 이름을 편집할 수 없으며 도메인 이름으로 설정됩니다. Javascript 코드를 추가한 후, **저장**을 선택하여 조치를 작성하십시오.

### 조치 업로드
{: #edge-functions-upload-actions}

Javascript 파일을 업로드하려면 **업로드** 단추를 사용하십시오. 엔터프라이즈 플랜에서 조치 이름은 파일 이름입니다. 표준 플랜에서는 조치 이름이 도메인 이름으로 설정됩니다.

기존 조치와 동일한 이름으로 조치를 업로드하거나 작성하면 기존 조치를 겹쳐쓰게 됩니다. 이 동작을 방지하기 위해 조치 파일을 작성할 때, 텍스트 입력에 고유한 이름을 업로드하거나 입력하기 전에 조치 파일의 이름을 바꾸십시오.
{:note}

### 조치 편집
{: #edge-functions-edit-actions}

조치를 선택하면 편집기에서 수정할 조치가 열립니다. 변경사항을 저장할 때마다 조치가 클라우드의 에지로 업로드됩니다. 업데이트 후 **저장**을 선택하십시오. 조치가 사용 중인 경우 변경사항이 즉시 적용됩니다. 

### 조치 삭제
{: #edge-functions-delete-actions}

**조치** 테이블에서 **삭제** 아이콘을 클릭하여 조치를 삭제하십시오. 사용 중에는 조치를 삭제할 수 없습니다. 조치를 삭제하려면 먼저 트리거에서 제거하십시오. **사용** 열에는 이 조치와 연관된 트리거의 수가 표시됩니다. 삭제는 실행 취소할 수 없습니다.


### 연관된 트리거
{: #edge-functions-associated-triggers}

트리거를 추가하고 조치와 연관시키십시오.

### Edge Functions의 알려진 제한사항
{: #edge-functions-known-limitations}

기존 조치와 동일한 이름의 조치를 업로드하면 기존 조치를 겹쳐쓰게 됩니다. 이 동작을 방지하려면 업로드하기 전에 조치 파일의 이름을 바꾸십시오.


## 트리거
{: #triggers}

### 트리거 정보
{: #about-triggers}

트리거(라우트)는 조치에 대한 도메인 트래픽 라우팅을 판별합니다. 트리거는 특정 URL 패턴을 계정의 도메인에 기반하여 사전 정의된 조치와 연관시킵니다. URL에 도메인이 있어야 하지만 와일드카드가 도메인에 대한 접두부로서 또는 경로의 끝에 포함될 수 있습니다. 패턴에 경로가 제공되지 않으면 `/`가 내재적으로 추가됩니다. URL 패턴에 삽입사 와일드카드 또는 조회 매개변수는 포함될 수 없습니다.

트리거를 추가하려면 도메인을 추가해야 합니다. 조치 없이 트리거를 추가할 수 있습니다.

### 트리거 추가
{: #add-triggers}

**트리거** 탭으로 이동하여 **트리거 추가**를 클릭하십시오. URL 패턴을 입력하고 기존 조치 목록에서 조치를 선택하십시오. 

조치에 대해 **Edge Functions 무시**를 선택할 수도 있습니다. 이렇게 하면 트리거의 경로가 활성 상태를 유지하지만 Edge Function 조치 사용을 막을 수 있습니다. 예를 들어, `my-function`이라고 하는 조치와 경로가 `beta.cistest-load.com/*`인 트리거가 있습니다. 경로 `beta.cistest-load.com/data`가 조치 `my-function`을 사용하면 안 되는 경우 경로가 `beta.cistest-load.com/data`이고 옵션이 **Edge Functions 무시**인 다른 트리거를 작성하십시오. 이렇게 하면 경로 `beta.cistest-load.com/data`가 조치 `my-function`을 사용하지 않고도 활성 상태를 유지할 수 있습니다.

### 트리거 편집
{: #edit-triggers}

선택한 트리거에 대해 테이블 행의 메뉴 옵션을 사용하여 트리거를 업데이트하십시오. 업데이트 후 **저장**을 선택하십시오.

### 트리거 삭제
{: #delete-triggers}

선택한 트리거에 대해 테이블 행의 메뉴 옵션을 사용하여 트리거를 삭제하십시오. 이 조치는 실행 취소할 수 없습니다.


## 유스 케이스
{: #edge-functions-use-cases-examples}

다음 예제는 오로지 데모용이며 프로덕션에는 사용되지 않습니다.
{:important}
* [A/B 테스트](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#ab-testing)
* [응답 헤더 추가](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#add-response-header)
* [다중 요청 집계](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#aggregate-multiple-requests)
* [조건부 라우팅](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#conditional-routing)
* [핫링크 보호](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#hot-link-protection)
* [오리진 없는 응답](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#originless-responses)
* [게시 요청](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#post-requests)
* [쿠키 설정](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#setting-cookies)
* [서명된 요청](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#signed-requests)
* [응답 스트리밍](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#streaming-responses)
