---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM CIS connection, CIS network connection, Origin web server, troubleshooting

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# CIS 네트워크 연결 문제점 해결
{:#troubleshooting-your-cis-network-connection}

## 내 데이터가 내 IBM CIS 연결을 통해 전달되는지를 어떻게 알 수 있습니까?
{:#how-do-i-know-if-my-data-is-passing-through-my-cis-connection}

IBM Cloud Internet Services(CIS)는 읽기, 추가 또는 수정이 가능한 HTTP 헤더를 사용합니다. 헤더를 이용하면 CF-Ray 번호를 사용하여 요청이 라우팅된 방법을 추적할 수 있습니다. CF-Ray 번호는 `curl` 명령이나 "Claire"라고 하는 Google Chrome 플러그인을 사용하여 찾을 수 있습니다.

데이터가 IBM CIS를 통해 전달되었는지 여부를 확인하려면 모든 패킷에 존재하는 `Ray ID`를 찾으십시오.

**Unix 명령행 도구:**

 * HTTP용 curl:
`$ curl -vso /dev/null http://example.com`

 * DNS용 dig:
`$ dig www.example.com`

 * 네트워크용 traceroute:
`$ traceroute example.com`

**예:**

터미널 명령:  `curl -svo /dev/null YOUR_URL_HERE. -L`

결과: `CF-RAY: 1ca349b6c1300da3-SJC`

## CF-Ray 헤더 추가

CF-RAY 헤더가 추가되어 네트워크를 통해 웹 사이트에 대한 요청을 추적할 수 있습니다. 연결과 관련된 문제를 해결하기 위해 지원 팀과 함께 작업할 때 사용하십시오. Apache 및 nginx에서 구성 파일을 편집하여 로그에 이 "Ray ID"를 표시할 수 있습니다.

### Apache
{:#troubleshooting-cis-apache}

```
LogFormat "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-agent}i\" %{CF-Ray}i" cf_custom

CustomLog log/access_log cf_custom
```

### nginx
{:#troubleshooting-cis-nginx}

```
log_format cf_custom '$remote_addr - $remote_user [$time_local]  '
                    '"$request" $status $body_bytes_sent '
                    '"$http_referer" "$http_user_agent" '
                    '$http_cf_ray';

access_log  /var/log/nginx/access.log cf_custom;
```

## 라우트를 어떻게 추적합니까?
{:#how-do-i-trace-a-route}

라우트가 IBM CIS 경로를 통해 이동되는지 여부를 확인하려면 Mac 또는 Linux의 터미널 창에서‘dig’을 실행하거나 Windows의 Windows 명령 프롬프트에서 `nslookup`을 사용할 수 있습니다.

패킷에 CF-Ray 값이 있으면 이는 CIS를 통해 이동된 것입니다.

`traceroute` 명령은 IP 요청이 취한 전체 경로를 표시합니다.

지원 팀은 이러한 명령을 사용하여 사용자를 지원합니다.

## 개인정보 보호 경고가 표시된 경우
{:#troubleshooting-cis-privacy-warning}

IBM CIS에서 발행한 인증서는 루트 도메인(`example.com`) 및 한 레벨의 하위 도메인(`*.example.com`)을 커버합니다. 2차 레벨 하위 도메인(`*.*.example.com`)에 도달하려고 시도하는 경우, 해당 호스트 이름이 SAN에 추가되지 않았으므로 브라우저에서 개인정보 보호 경고가 표시됩니다.

또한 파트너 인증 기관(CA) 중 하나가 새 인증서를 발행하는 동안 최대 15분 정도 대기하십시오. 새 인증서가 아직 발행되지 않았으면 브라우저에서 개인정보 보호 경고가 표시됩니다.

## DDoS 공격을 받으면 어떻게 해야 합니까?
{:#troubleshooting-cis-ddos-attack}

 * **1단계:** 대시보드에서 "방어 모드" 켜기
 * **2단계:** 보안을 최대화하도록 DNS 레코드 설정
 * **3단계:** IBM CIS에서 요청 제한 또는 속도 제한을 수행하지 않음
 
"방어 모드" 중에 각각의 새 방문자는 "Captcha" 보안 인증 확인에 접하게 되며, 해당 방문자는 인증 확인되지 않은 액세스에 대한 쿠키가 제공되기 전에 이를 통과해야 합니다. 해당 방식으로 봇네트 트래픽은 "방어 모드"가 꺼질 때까지 차단됩니다. 보안 인증 확인을 충족하지 않은 방문자는 (나쁜) IP 평판 데이터베이스에 추가됩니다.

## 발생할 수 있는 기타 문제점
{:#troubleshooting-cis-other-problems}

사용자나 지원 팀에서 볼 수 있는 일부 공통 오류 메시지는 다음과 같습니다.

|오류 코드    |이유 |
| ------------- | ------------- |
|1001  |DNS 분석 오류. 고객이 최근에 서명하고 해당 DNS 정보가 아직 전파되지 않았거나 DNS를 관리하는 사용자에게 장애가 발생했기 때문입니다. |
|521  |오리진 웹 서버가 CIS의 연결을 거부했습니다. 오리진 웹 서버가 실행 중이 아니거나 무언가가 IBM CIS IP 주소를 차단 중입니다. |
|522  |오리진 서버에 대한 연결 제한시간(기본값: 30초)이 초과되었습니다. CIS 속도가 제한되고 웹 서버가 모든 리소스(공유 서버)를 이용 중이거나 웹 서버와 IBM CIS 간에 네트워크 연결 문제가 있을 수 있습니다. |
|523  |오리진 서버에 연결할 수 없습니다. DNS 레코드의 오리진 IP 주소가 CIS DNS 설정 페이지에 나타나는 주소와 동일한지 확인하십시오. |
|524  |IBM CIS가 TCP 연결을 설정할 수 있었지만 웹 서버의 응답을 받지 못했습니다. 장기 실행 애플리케이션이나 데이터베이스 조회가 방해를 받고 있습니다. |

### 네트워크 트래픽을 볼 수 없음
{:#troubleshooting-cis-network-traffic}

트래픽이 보이지 않으며 CNAME을 사용 중인 경우에는 트래픽이 루트 도메인으로 라우팅되지 않도록 경로 재지정이 적절한지 확인하십시오. 일부 DNS 전파를 완료하려면 최대 48시간 정도 걸릴 수 있음을 유념하십시오.

### 웹 사이트 오프라인
{:#troubleshooting-cis-website-offline}

다음을 볼 수 있습니다.

`IBM CIS cannot connect to the origin server (error 521, 522, 523)`.

**웹 사이트 오프라인 - 캐시된 버전이 없음**

1. 서버가 온라인이지만 여기서 IBM CIS 요청을 차단합니다.
2. 오리진 서버가 오프라인이며 IBM CIS에 백업 웹 사이트 이미지가 없습니다. 

수행할 수 있는 작업:

* IBM CIS IP 주소가 화이트리스트에 추가되었는지 확인합니다.
* IBM CIS IP 속도가 제한되지 않음을 확인합니다.
* [화이트리스트에 추가할 IP](/docs/infrastructure/cis?topic=cis-ibm-cloud-cis-whitelisted-ip-addresses)의 목록 위치

### 502 오류 “드레드된 502”
{:#troubleshooting-cis-502-error}

이 오류는 볼 수 있는 가장 일반적인 오류 중 하나입니다. 이는 일반적으로 네트워크의 일부가 사용 불가능할 때 발생합니다(예: DDoS 공격의 초기에). 특정 데이터 센터가 일정 시간 사용 불가능할 수 있습니다. 트래픽이 경로 재지정됩니다. 추적 라우트를 실행하십시오. 

나타날 수 있는 오류: `Error 502 - bad gateway error`

발생한 내용:

* IBM CIS 네트워크 중 일부에 문제가 있습니다.
* 일반적으로 문제점은 1개 데이터 센터의 1개 서버로 국한됩니다.
* 이는 사이트 방문자 중 일부에만 영향을 줍니다.
* IBM CIS 기술 운영 팀에서 이를 처리합니다.

수행할 수 있는 작업:

* 티켓에서 `www.YOUR_DOMAIN.com/cdn-cgi/trace`의 결과를 [지원 팀](/docs/get-support?topic=get-support-getting-customer-support)에 보냅니다.
* 임시로 DNS 레코드를 끄기(프록시 없음)로 토글합니다.

