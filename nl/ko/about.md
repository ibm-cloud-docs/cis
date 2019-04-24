---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Caching, IBM Cloud Internet Services, Web Application Firewall

subcollection: cis

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"} 

# IBM Cloud Internet Services(CIS) 정보
{:#about-ibm-cloud-internet-services-cis}

Cloudflare에서 작동하는 IBM Cloud Internet Services(CIS)는 IBM Cloud에서 자체 비즈니스를 실행 중인 고객을 위해 고성능의 빠르고 안정적이며 안전한 인터넷 서비스를 제공합니다.   

IBM CIS를 이용하면 API 또는 UI를 사용하여 손쉽게 변경할 수 있는 기본값을 설정하여 빠르게 작업을 진행할 수 있습니다. 공통적으로 변경된 매개변수 중 일부는 다음과 같습니다.

 * **DNS 설정**: IBM CIS를 사용하여 DNS를 호스팅거나 CNAME 레코드를 작성할 수 있습니다.
 * **암호 설정(TLS)**: 기본값은 호스트와 IBM CIS 에지 서버 간의 연결은 암호화하지만 IBM CIS 에지 서버와 오리진 서버 간의 통신은 암호화하지 않는 `flexible` 모드입니다.

## WAF(Web Application Firewall)
{:#about-waf}

IBM CIS는 웹 트래픽을 검사하여 의심스러운 활동을 찾아내는 WAF(Web Application Firewall) 기능을 제공합니다. 이는 규칙 세트를 기반으로 불법적인 트래픽을 자동으로 필터로 걸러내어 GET 및 POST 기반 웹 요청을 볼 수 있습니다. 사용자는 다양한 규칙 세트를 사용하여 차단, 인증 확인하거나 통과시킬 트래픽을 판별할 수 있습니다. WAF는 주석 스팸, XSS(Cross-site scripting) 공격 및 SQL 인젝션을 차단할 수 있습니다.

원하면 언제든지 WAF를 사용하거나 사용하지 않을 수 있습니다. 하지만 이를 항상 사용하도록 권장합니다.

## DDoS 공격으로부터 보호
{:#ddos-protection}

IBM CIS는 공격의 규모나 지속 시간과는 무관하게 웹 사이트와 공격자 간에 자리를 잡고 DDoS 보호를 제공합니다.

## 로드 밸런싱
{:#about-load-balancing}

IBM CIS 로드 밸런싱은 권한 DNS 레벨에서 작동됩니다. 이는 오리진의 상태를 모니터링하는 고급 상태 검사를 포함하며 DNS 응답을 동적으로 조정합니다. 또한 글로벌 로드 밸런싱(GLB)을 위한 Geo 정책을 구성할 수 있습니다.

### 상태 검사
{:#about-health-checks}

로드 밸런싱 상태 검사는 주기적 HTTP 또는 HTTPS 요청을 통해 특정 URL에서 수행되며, 이는 사용자 정의할 수 있는 간격, 제한시간 및 상태 코드로 구성되어 있습니다. 오리진 서버가 비정상 상태로 표시된 경우, 방문자는 빠른 장애 복구 라우트를 사용하여 장애를 우회하여 라우팅됩니다.
 
### Geo 정책 및 글로벌 로드 밸런싱(GLB)
{geo-policies-and-glb}

Geo 정책은 해당 클라이언트의 지리적 위치에 기반하여 제공된 클라이언트가 방향 지정된 오리진 서버에 대한 제어를 제공합니다. 예를 들어, 유럽의 방문자는 사용자의 웹 사이트나 애플리케이션에 대해 최인접 유럽 오리진으로 전송되고 미국 방문자는 북미 오리진으로 전송되는 등의 방식으로 Geo 정책을 구성할 수 있습니다.

## 캐싱
{:#about-caching}

캐싱은 정적 웹 컨텐츠를 사이트 방문자와 가장 가까운 위치에 저장하여 웹 사이트의 성능을 현저히 높이는 방법입니다. 글로벌하게 분포된 전달 환경을 사용하여 웹 컨텐츠 소유자는 전 세계적으로 위치에 구애받지 않는 환경을 제공할 수 있습니다.  
 
## TLS를 사용한 암호화
{:#encryption-with-tls}

TLS(Transport Layer Security)를 사용하여 웹 사이트와 양방향으로 통신을 암호화합니다. 새 인증서가 발행되려면 해당 사이트가 활성화된 이후 최대 24시간까지 걸릴 수 있습니다.

[FAQ](/docs/infrastructure/cis?topic=cis-faq)에서 TLS에 대한 자세한 정보를 참조할 수 있습니다.
