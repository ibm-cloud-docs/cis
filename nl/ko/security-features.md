---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: CIDR blocks, Whitelist Block Challenge, IBM Cloud Internet Services, security features

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# IBM Cloud Internet Services(CIS)가 작업의 보안을 유지하는 방법
{:#how-cis-keeps-your-work-secure}

IBM CIS는 대역폭과 서버 리소스를 낭비할 수 있는 오용 봇과 크롤러를 제한하고 위협을 차단하는 글로벌하게 분배된 클라우드 서비스입니다. IBM CIS는 글로벌 HTTP(S) 리버스 프록시 및 관리 대상 DNS 서비스 제공자로서 작동합니다. 웹 트래픽은 성능 및 보안을 모두 최적화하기 위해 지능형 글로벌 네트워크를 통해 라우트됩니다.

![security-graphic.png](images/security-graphic.png)

다음은 빠른 기능 개요입니다.

## 보안 기능
{:#cis-security-features}

 * [DNS 레코드](/docs/infrastructure/cis?topic=cis-dns-concepts#proxying-dns-records) 또는 [GLB](/docs/infrastructure/cis?topic=cis-global-load-balancer-glb-concepts)를 프록싱하여 보안 기능을 사용하십시오. 이렇게 하면 서버를 통해 트래픽이 플로우되며 데이터를 모니터할 수 있습니다.
### WAF(Web Application Firewall)
{:#cis-web-application-firewall}

 * WAF는 다음 두 개의 규칙 세트를 통해 구현됩니다. [OWASP](/docs/infrastructure/cis?topic=cis-owasp-rule-set-for-waf) 및 [CIS](/docs/infrastructure/cis?topic=cis-waf-settings#cis-rule-set-for-waf).
### 무제한 DDoS 경감
{:#cis-unlimited-ddos-mitigation}

 * DDoS 경감은 일반적으로 공격받을 때 비용이 증가할 수 있는 비싼 서비스입니다. 추가 비용 없이 CIS에 무제한 DDoS 경감이 포함됩니다.

## 보안 표준 및 플랫폼
{:#security-standards-and-platform}

 * TLS (SHA2 및 SHA1)
 * IPv6
 * HTTP/2 및 SPDY

## DNS
{:#cis-dns}

 * 글로벌 임의 캐스트 네트워크
 * DNSSEC

## 네트워크 공격 및 경감
{:#network-attacks-and-mitigation}

일반적으로 당사는 두 가지 카테고리에 속하는 공격을 지켜봅니다.

|계층 3 또는 계층 4 공격 |계층 7 공격 |
|------------------------------|-----------------|
|이러한 공격은 ISO 계층 3(네트워크 계층)의 트래픽 플러드(예: ICMP 플러드) 또는 계층 4(전송 계층)의 트래픽 플러드(예: TCP SYN 플러드 또는 반영된 UDP 플러드)로 구성되어 있습니다. |이는 악성 ISO 계층 7 요청(애플리케이션 계층)(예: GET 플러드)을 전송하는 공격입니다.  |
|에지에서 자동 차단됨 |“방어 모드”, WAF 및 보안 레벨 설정으로 이를 처리함 |

## IP 방화벽
{:#cis-ip-firewall}

IBM Cloud Internet Services가 트래픽을 제어하는 몇 가지 도구를 제공하므로, 트래픽 볼륨, 특정 요청자 그룹, 특정 요청 IP로부터 도메인, URL 및 디렉토리를 보호할 수 있습니다. 이 절에서는 사용 가능한 도구에 대해 자세히 설명합니다.

### IP 규칙
{:#cis-ip-rules}

IP 규칙을 사용하면 특정 IP 주소, IP 범위, 특정 국가, 특정한 ASN 및 특정 CIDR 블록에 대한 액세스를 제어할 수 있습니다. 수신 요청에 대해 사용 가능한 조치는 다음과 같습니다.
  * 화이트리스트 
  * 차단 
  * 인증 확인(Captcha) 
  * JavaScript 인증 확인(IUAM 인증 확인)

예를 들어, 특정 IP에서 악의적 요청이 발생하면 이 사용자를 IP 주소로 차단할 수 있습니다.

### 사용자 에이전트 차단 규칙
{:#user-agent-blocking-rules}

사용자 에이전트 차단 규칙을 사용하면 선택한 사용자 에이전트 문자열에 대한 조치를 수행할 수 있습니다. 차단이 IP가 아닌 수신 사용자 에이전트 문자열을 검사하는 경우를 제외하고 이 기능은 이전에 설명한 대로 도메인 잠금과 같이 작동합니다. IP 규칙(차단, 인증 확인 및 JS 인증 확인)에서 설정한 것과 동일한 조치 목록으로 일치 요청을 처리하는 방법을 선택할 수 있습니다. 사용자 에이전트 차단은 전체 구역에 적용됩니다. 도메인 잠금과 같은 방법으로 하위 도메인을 지정할 수는 없습니다.

이 도구는 의심스러운 사용자 에이전트 문자열을 차단하는 경우에 유용합니다. 

### 도메인 잠금
{:#cis-domain-lockdown}

도메인 잠금을 사용하면 다른 모든 IP가 블랙리스트에 추가되도록 특정 IP 주소와 IP 범위를 화이트리스트에 추가할 수 있습니다. 도메인 잠금이 다음을 지원합니다.

  * 특정 하위 도메인. 예를 들어, `foo.example.com` 도메인에 대한 IP `1.2.3.4` 액세스를 허용하고 `bar.example.com` 도메인에 대한 IP `5.6.7.8` 액세스를 허용할 수 있습니다(그 반대를 허용하지 않는 경우에도).
  * 특정 URL. 예를 들어, `example.com/foo/*` 디렉토리에 대한 IP `1.2.3.4` 액세스를 허용하고 `example.com/bar/*` 디렉토리에 대한 IP `5.6.7.8` 액세스를 허용할 수 있지만 그 반대를 반드시 허용하지는 않습니다.
IP 규칙을 사용하면 현재 도메인의 모든 하위 도메인 또는 계정의 모든 도메인에 차단을 적용할 수 있고 URI를 지정할 수 없으므로 액세스 규칙에 세분화가 필요한 경우에 이 기능이 유용합니다.

### 인증 확인 통과
{:#cis-challenge-passage}

**고급** 보안 설정에 있는 경우, 이 설정을 사용하면 인증 확인 또는 JavaScript 인증 확인을 통과한 방문자가 다시 인증 확인되기 전까지 사이트에 대한 액세스 권한을 얻는 기간을 제어할 수 있습니다. 이는 방문자의 IP를 기반으로 하므로 WAF 규칙에서 제공되는 인증 확인에 적용되지 않습니다. 이 인증 확인이 사용자가 사이트에서 수행하는 조치를 기반으로 하기 때문입니다.

### 브라우저 무결성 검사
{:#cis-browser-integrity-check}

이 설정은 **고급** 보안 설정에 있습니다. 브라우저 무결성 검사는 스팸 발송자가 흔히 오용하는 HTTP 헤더를 찾습니다. 이는 페이지에 대한 해당 헤더 액세스의 트래픽을 거부합니다. 또한 사용자 에이전트가 없거나 비표준 사용자 에이전트를 추가(오용 봇, 크롤러 또는 API에서 흔히 사용하는 전술임)하는 방문자를 차단하거나 인증 확인합니다.
