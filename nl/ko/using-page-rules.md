---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Use Page Rules, Page Rule

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# 페이지 규칙 사용
{:#use-page-rules}

페이지 규칙은 도메인을 참조하는 특정 URL 패턴에 적용될 수 있는 일부 설정 및 값을 지정합니다. 페이지 규칙은 사이트에서 각각의 개별 URL을 기반으로 보안, 성능 및 안정성을 관리하는 데 도움이 됩니다. 다음 표에는 모든 고객이 사용할 수 있는 페이지 규칙, 생성되는 작동 및 사용 전에 유념해야 할 특수 고려사항이 설명되어 있습니다.

## 보안
{:#page-rules-security}

|**설정** |**동작** |**고려사항** |
|-----------|----------|----------------|
|**브라우저 무결성 확인**|스팸 발송자가 오용한 공통 HTTP 헤더를 찾고 페이지에 대한 액세스를 거부합니다. 또한 사용자 에이전트가 없거나 비표준 사용자 에이전트를 추가(역시 오용 봇, 크롤러 또는 API에서 흔히 사용하는 전술임)하는 방문자를 차단합니다. | |
|**보안 사용 안함**|다음 기능을 사용하지 않습니다. <ul><li>이메일 난독화</li> <li>서버 측 제외</li> <li>WAF</li></ul>|하나의 규칙이 보안 사용 안함으로 설정되고 다른 규칙이 WAF 사용으로 설정된 경우에는 이들이 나타나는 순서와는 무관하게 WAF 규칙이 우선합니다.|
|**이메일 난독화**|이메일 난독화 켜기 또는 끄기를 토글합니다. | |
|**IP 지리 위치 헤더**|웹 사이트에 대한 모든 요청과 함께 방문자 위치의 국가 코드가 포함됩니다. 해당 정보는 `CF-IPCountry` HTTP 헤더에서 찾을 수 있습니다. | |  
|**보안 레벨**|클라이언트가 인증 확인 페이지를 접할 수 있도록 클라이언트 위협 점수가 얼마가 높아야 하는지를 제어합니다. 이 설정은 방문자가 사이트를 방문할 때 사이트가 항상 **방어 모드** 인증 확인을 방문자에게 제시할 수 있도록 하는 데 사용될 수 있습니다. | |
|**서버 측 제외**|서버 측 제외 켜기 또는 끄기를 토글합니다.  | |
|**TLS**|사용되는 TLS 모드를 제어합니다. | |
|**WAF**|WAF 켜기 또는 끄기를 토글합니다. | |  
|**자동 HTTPS 재작성**|자동 HTTPS 재작성 켜기 또는 끄기를 토글합니다.  | |
|**기회적 암호화**|기회적 암호화 켜기 또는 끄기를 토글합니다.  | |
|**캐시 기만 방어**|캐시 기만 방어 켜기 또는 끄기를 토글합니다.  | |
|**항상 HTTPS 사용**|`301` 경로 재지정을 작성하여 `http://` URL을 `https://` URL로 변환합니다.|IBM CIS가 요청에 대해 `HTTPS`로의 경로 재지정을 강제 실행하고 이는 새 요청이 된 후에 페이지 규칙에 대해 평가되므로 이 설정을 사용하면 규칙의 기타 모든 설정 구성이 사용되지 않습니다. |
|**트루 클라이언트 IP 헤더**|CIS는 `True-Client-IP` 헤더에서 일반 사용자의 IP 주소를 보냅니다. |엔터프라이즈만 해당|

## 성능
{:#page-rules-performance}

|**설정** |**동작** |**고려사항** |
|-----------|----------|----------------|
|**브라우저 캐시 TTL**|클라이언트 브라우저에서 캐시한 리소스가 유효한 상태를 유지하는 기간을 제어합니다. | |
|**쿠키의 캐시 무시**|특정 이름의 쿠키가 보이지 않는 한 캐시된 오브젝트를 서비스합니다. 예를 들어, 고객이 로그인되어 있으므로 개인화된 컨텐츠가 제시되어야 함을 표시하는 `SessionID` 쿠키가 보이지 않는 한 홈 페이지의 캐시된 버전을 서비스합니다. | |
|**캐시 레벨**|**무시** - 해당 페이지 규칙과 일치하는 리소스가 캐시되지 않습니다.<br>**조회 문자열 없음** - 조회 문자열이 없으면 단지 캐시의 리소스를 전달합니다.<br>**조회 문자열 무시** - 조회 문자열과 무관하게 모든 사용자에게 동일한 리소스를 전달합니다.<br>**표준** - 조회 문자열이 변경될 때마다 다른 리소스를 전달합니다.<br> **모두 캐시** - 페이지 규칙과 일치하는 리소스가 캐시됩니다.|기본적으로, HTML 컨텐츠는 캐시되지 않습니다. 정적 HTML 컨텐츠를 캐시하는 페이지 규칙이 작성되어야 합니다. |
|**에지 캐시 TTL**|IBM CIS가 캐시에서 파일을 보유하는 기간을 제어합니다. |이 설정은 캐시 레벨을 지정할 때 선택사항입니다. |
|**분석 대체**|페이지 규칙과 일치하는 요청이 분석되는 URL 또는 IP를 변경합니다.||
|**쿠키의 캐시**|쿠키 이름에 대한 정규식 일치를 기반으로 `모두 캐시` 옵션(`캐시 레벨` 설정)을 적용합니다. 이 설정과 `쿠키의 캐시 무시`를 둘 다 동일한 페이지 규칙에 추가하는 경우 `쿠키의 캐시`가 `쿠키의 캐시 무시`보다 우선합니다.|엔터프라이즈만 해당|
|**성능 사용 안함**|끄기:<ul><li>`웹 컨텐츠 축소`</li><li>`이미지 로드 최적화`</li><li>`이미지 크기 최적화`</li><li>`스크립트 로드 최적화`</li></ul> |엔터프라이즈만 해당|
|**웹 컨텐츠 축소**|해당 파일에서 불필요한 문자를 모두 제거하여 HTML, CSS 및/또는 JavaScript 파일을 축소합니다. |엔터프라이즈만 해당|
|**이미지 로드 최적화**|다음을 통해 네트워크 연결 및 디바이스 유형을 기반으로 이미지가 포함된 페이지의 로드 시간을 줄입니다.<ul><li>**이미지 가상화** - 이미지를 원본과 동일한 차원의 저해상도 플레이스홀더 이미지(서드파티 이미지 포함)로 바꿉니다. 페이지가 완전히 렌더링되면 전해상도 이미지가 지연 로드됩니다(브라우저 뷰포트에서 이미지 우선순위 지정). 이 프로세스를 사용하면 페이지가 빠르게 렌더링되고 브라우저 재플로우를 최소화할 수 있습니다.</li><li>**요청 간소화** - 이미지에 대한 다중 개별 네트워크 요청을 단일 요청으로 결합합니다.</li></ul> |엔터프라이즈만 해당|
|**이미지 크기 최적화**|메타데이터(날짜 및 시간, 카메라 제조업체 및 모델 등)를 제거하고 가능하면 이미지를 압축하여 이미지 파일 크기를 줄입니다. 파일 크기가 작으면 이미지 및 웹 페이지의 로드 시간이 빠릅니다. |엔터프라이즈만 해당 |
|**조회 문자열 정렬**|조회 문자열의 순서에 관계없이 조회 문자열이 동일한 파일을 캐시의 동일한 파일로 처리합니다. |엔터프라이즈만 해당 |
|**응답 버퍼링**|오리진 서버에서 응답 버퍼링을 사용 또는 사용 안함으로 설정합니다. 기본적으로 CIS는 패킷이 수신되면 클라이언트에 이 패킷을 전송합니다. 응답 버퍼링 사용은 CIS가 전체 파일이 일반 사용자에게 전달되기 전에 전체 파일을 갖게 될 때까지 대기함을 의미합니다. |엔터프라이즈만 해당 |
|**스크립트 로드 최적화**|페이지 컨텐츠의 렌더링을 차단하지 않도록 서드파티 스크립트를 포함한 Javascript를 비동기식으로 로드하여 페인트 시간을 줄입니다. |엔터프라이즈만 해당 |

## 안정성
{:#page-rules-reliability}

|**설정** |**동작** |**고려사항** |
|-----------|----------|----------------|
|**시간이 경과된(stale) 컨텐츠 제공**|서버가 작동 중지되면 사이트의 제한된 버전을 온라인 상태로 유지합니다. |자세한 정보는 [최적의 안정성을 위한 IBM CIS 배치 관리](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-deployment-for-optimal-reliability)를 참조하십시오. |
|**오리진 캐시 제어**|오리진에서 캐시되는 컨텐츠와 해당 컨텐츠의 업데이트 빈도를 판별합니다. |자세한 정보는 [최적의 안정성을 위한 IBM CIS 배치 관리](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-deployment-for-optimal-reliability)를 참조하십시오. |
|**URL 전달** |사이트가 사용 불가능할 때 사용되는 URL입니다. |사용자가 요청을 다른 위치로 전달하므로 이를 사용하면 기타 모든 설정 구성이 사용되지 않습니다. 자세한 정보는 [최적의 안정성을 위한 IBM CIS 배치 관리](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-deployment-for-optimal-reliability)를 참조하십시오.|
|**호스트 헤더 대체**|페이지 규칙과 일치하는 URI의 호스트 헤더를 지정된 값으로 바꿉니다. 이는 일반적으로 S3 버킷에서 호스팅되는 컨텐츠에 사용됩니다. |
|**앱 사용 안함**|CIS 앱을 모두 끕니다. |엔터프라이즈만 해당 |
|**오리진 오류 페이지 패스 스루**|오리진 서버에서 보낸 문제에 대해 트리거하는 CIS 오류 페이지를 사용 안함으로 설정하고, 대신 오리진에 설정된 오류 페이지를 표시합니다. |엔터프라이즈만 해당 ||

## 페이지 규칙 URL 패턴
{:#page-rule-url-patterns}

페이지 규칙은 다음 형식과 일치하는 주어진 URL 패턴에 영향을 줍니다.

`<scheme>://<hostname><:port>/<path>`

각 컴포넌트를 사용하는 예제는 다음과 같습니다.

`https://www.example.com:80/image.png`

*스킴* 및 *포트* 컴포넌트는 선택사항입니다. 스킴을 생략하는 경우, 이는 `http://` 및 `https://` 프로토콜을 둘 다 커버합니다. 포트가 지정되지 않으면 규칙이 모든 포트와 일치합니다. 단지 하나가 아닌 일련의 유사한 패턴과 일치할 수 있도록 허용하는 ‘*’ 기호를 규칙 패턴에서 사용하여 기본 와일드카드 일치를 수행할 수 있습니다.

페이지 규칙에서 유념해야 할 세 가지 중요한 사항은 다음과 같습니다.

 * 오직 하나의 페이지 규칙만 주어진 요청에서 적용됩니다.
 * 페이지 규칙에는 맨 위에서 맨 아래 순으로 우선순위가 지정됩니다.
 * 일단 URL이 규칙과 일치되면 해당 규칙만 적용됩니다. 즉, 페이지 규칙이 요청에서 이미 트리거된 경우에는 역시 URL 패턴과 일치하는 후속 규칙이 적용되지 않습니다. 일반 규칙으로서, _가장 특정한_ 규칙에서 _가장 특정하지 않은_ 규칙으로 순서를 지정하도록 권장합니다.

페이지 규칙을 사용하지 않을 수 있으며 이 경우에는 조치가 실행되지 않습니다. 이는 여전히 목록에 표시될 수 있으며 편집이 가능합니다. **사용됨** 토글을 **끄기**로 설정하면 초기에 사용되지 않은 페이지 규칙이 작성됩니다.

자세한 정보는 [캐싱 및 페이지 규칙 방법 문서](/docs/infrastructure/cis?topic=cis-use-page-rules-with-caching)를 참조하십시오.