---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Best practices, CIS setup

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# CIS 설정의 우수 사례
{:#best-practices-for-cis-setup}

IBM CIS가 네트워크의 에지에 위치하므로 CIS 서비스와 원만하게 통합할 수 있으려면 몇 가지 단계를 수행해야 합니다. CIS를 오리진 서버와 통합하기 위한 일부 권장 우수 사례가 여기에 제시되어 있습니다. 

DNS를 변경하고 프록시 서비스를 활성화하기 전후에 이러한 단계를 수행할 수 있습니다. 이러한 권장사항에 따라 IBM CIS는 오리진 서버에 올바르게 연결할 수 있습니다. 권장사항은 API 또는 HTTPS 트래픽에서 발생하는 문제를 방지하고 보안 CIS IP 주소가 아닌 고객의 올바른 IP 주소를 로그에서 캡처할 수 있도록 도움을 줍니다.

다음을 설정해야 합니다.

 * 우수 사례 1: 고객의 오리진 IP 복원
 * 우수 사례 2: CIS IP 주소 포함
 * 우수 사례 3: 보안 설정이 API 트래픽을 방해하지 않는지 확인
 * 우수 사례 4: 가급적 엄격하게 보안 설정 구성
 
## 우수 사례 1: 고객의 오리진 IP 복원 방법 알아보기
{:#best-practice-know-how-to-restore-origininating-ip}

리버스 프록시로서, 당사는 다음의 헤더에서 오리진 IP를 제공합니다.

  * `CF-Connecting-IP`
  * `X-Forwarded-For`
  * `True-Client-IP`(선택사항)

Apache, Windows IIS 및 NGINX 등의 인프라에 대해 다양한 도구를 사용하여 사용자 IP 주소를 복원할 수 있습니다.

## 우수 사례 2: 원만한 통합을 위해 CIS IP 주소 포함
{:#best-practice-incorporate-cis-ip-addresses}

두 가지 단계를 취해야 합니다.

  * CIS IP 주소의 속도 제한 제거
  * CIS IP 주소 및 기타 신뢰 기관만 허용하도록 ACL 설정

IBM CIS의 업데이트된 IP 범위 목록은 [이 위치에서](/docs/infrastructure/cis?topic=cis-ibm-cloud-cis-whitelisted-ip-addresses) 찾을 수 있습니다.

## 우수 사례 3: 보안 설정을 검토하여 API 트래픽을 방해하지 않는지 확인
{:#best-practice-review-security-settings-interference}

IBM CIS는 일반적으로 연결 오버헤드를 제거하여 API 트래픽의 속도를 높입니다. 그러나 기본 보안 스탠스는 많은 API 호출에 방해가 될 수 있습니다. 일단 프록싱이 활성화되면 API 트래픽이 방해를 받지 않도록 일부 조치를 취하도록 권장합니다.

 * **페이지 규칙** 기능을 사용하여 보안 기능을 선별적으로 끄십시오.
   * API의 URL 패턴으로 페이지 규칙 작성(예: `api.example.com`).
   * 다음의 규칙 동작을 추가하십시오.
     * **보안 레벨**을 **기본적으로 끄기**로 선택
     * **TLS**를 **끄기**로 선택
     * **브라우저 무결성 확인**을 **끄기**로 선택
   * **리소스 프로비저닝** 선택

 * 또는 보안 페이지에서 전체적으로 **WAF(Web Application Firewall)**를 끌 수도 있습니다.

|*브라우저 무결성 확인에서 수행하는 작업* | 
|------------------------------------------------|
|*브라우저 무결성 확인은 흔히 스팸 발송자가 오용하는 HTTP 헤더를 찾습니다. 이는 페이지에 대한 해당 헤더 액세스의 트래픽을 거부합니다. 또한 사용자 에이전트가 없거나 비표준 사용자 에이전트를 추가(오용 봇, 크롤러 또는 API에서 흔히 사용하는 전술임)하는 방문자를 차단합니다. * |

## 우수 사례 4: 가급적 엄격하게 보안 설정 구성
{:#best-practice-configure-stict-security-settings}

CIS는 트래픽을 암호화하는 일부 옵션을 제공합니다. 리버스 프록시로서, 당사는 데이터 센터에서 TLS 연결을 닫고 오리진 서버에 대한 새 TLS 연결을 엽니다. CIS 종료의 경우, 계정의 사용자 정의 인증서를 업로드하거나 CIS에서 제공한 와일드카드 인증서를 업로드할 수 있습니다. 또는 두 작업을 모두 수행할 수도 있습니다.

### 사용자 정의 인증서 업로드
{:#strict-upload-custom-cert}
 
엔터프라이즈 도메인을 작성할 때 공개 키와 개인 키를 업로드할 수 있습니다. 자체 인증서를 업로드하면 암호화된 트래픽과의 즉각적인 호환성이 확보되며 인증서(예: EV(Extended Validation) 인증서)에 대한 제어가 유지됩니다. 사용자 정의 인증서를 업로드하는 경우에는 사용자 자신이 인증서 관리를 책임진다는 점을 유념하십시오. 예를 들어, IBM CIS는 인증서 만기 날짜를 추적하지 않습니다. 
 
### 또는 CIS에서 제공한 인증서 활용
{:#strict-utilize-cert-cis-provisioned}
 
기본적으로, IBM CIS는 여러 인증 기관(CA)과 협력하여 고객에 대해 도메인 와일드카드 인증서를 제공합니다. 이러한 인증서를 설정하기 위해 수동 확인이 필요할 수 있으며, 지원 팀에서 이러한 추가 단계를 수행하는 데 도움을 줄 수 있습니다.
 
### TLS 설정을 **엔드-투-엔드 CA 서명**으로 변경
{:#strict-change-tls-setting}
 
대부분의 엔터프라이즈 고객은 엔드-투-엔드 CA 서명 보안 설정을 활용합니다. **엔드-투-엔드 CA 서명** 설정에서는 웹 서버에 설치된 유효한 CA-서명 인증서가 필요합니다. 인증서의 만기 날짜는 미래의 날짜여야 하며, 일치하는 *호스트 이름* 또는 *SAN(Subject Alternative Name)*이 있어야 합니다.

