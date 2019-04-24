---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Helpful tools, whois, IPv4

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# CIS 배치의 관리에 유용한 도구
{:#helpful-tools-for-managing-your-cis-deployment}

IBM CIS 배치를 관리하는 데 도움이 될 수 있는 일부 퍼블릭 도메인 unix 시스템 관리 도구가 있습니다.

## Sysadmin 도구
{:#cis-sysadmin-tools}

 * whois (도메인 식별 도구)
 * dig (DNS 도구)
 * curl (HTTP 및 HTTPS 도구)
 * netcat (IP 및 포트 도구)
 * traceroute (네트워크 도구)

## 외부 및 원격 테스트용 상용 도구
{:#commercial-tools-for-external-and-remote-testing}

 * GTMetrix (http)
 * 웹 페이지 테스트 (http)
 * WhatsMyDNS (DNS 도구)
 * G Suite Toolbox (DNS 및 HTTP)

## 로그 및 히스토리를 보는 도구
{:#tools-for-looking-at-logs-and-history}

 * HTTP 아카이브 파일 (HAR 파일)


### `whois` 사용
{:#using-whois}

`whois`는 제공된 도메인 이름이나 IP 주소에 대한 등록자 정보(예: 도메인의 제공된 권한 서버 또는 특정 IP 주소의 소유자)를 검색하는 데 사용할 수 있는 unix 시스템 명령행 도구입니다.

예제:

`whois example.com`

`whois 8.8.8.8`

### `dig` 사용
{:#using-dig}

`dig`은 DNS 조회를 수행하고 특정 도메인의 DNS 레코드를 검사할 수 있는 unix 명령행 도구입니다. 이는 `nslookup`과 유사합니다.

이 명령의 스키마: dig <recordtype. <domainname> <options>

**예제: **

`dig example.com`

`dig my.example.com`

`dig example.com +trace`

`dig NS example.com`

`dig example.com @ns.example.com`

### `cURL` 사용
{:#using-curl}

`cURL`은 URL 구문을 사용하여 데이터를 전송할 수 있도록 하는 unix 명령행 도구입니다. 이는 일반적으로 HTTP 요청을 작성하고 서버 응답을 비교하는 데 사용됩니다.

이 명령의 스키마는 `curl -option1 -option2 http://example.com/url`입니다.

**예제: **

`curl -svo /dev/null http://www.example.com`

`curl -svo /dev/null -A “USER_AGENT_STRING” http://www.example.com`

`curl -svo /dev/null -H “host: www.example.com” http://ORIGIN_IP`

`curl -svo /dev/null -H https://www.example.com --resolve www.example.com:443:ORIGIN_IP`

### `mtr` 및 `traceroute` 사용
{:#using-mtr-and-traceroute}

MTR 및 `traceroute`는 지정된 호스트나 대상 서버에 대한 특정 네트워크 경로에 따라 성능이나 대기 시간을 측정할 수 있도록 하는 unix 명령행 도구입니다.

**예제: **

`mtr -rwc 20 example.com -T -4`
`mtr -rwc 20 8.8.8.8 -T -6`

`traceroute example.com -T -4`

`traceroute 8.8.8.8 -T -6`

|옵션 |정의 |
|---------|-----------|
|-c |전송된 Ping 수 설정 |
|-T |TCP traceroute 강제 실행(일반적으로 ICMP) |
|-4 |IPv4 사용 강제 실행 |
|-6 |IPv6 사용 강제 실행 |

### HAR 파일 생성
{:#generating-a-har-file}

HAR 파일은 웹 브라우저의 HTTP 요청에 대한 레코딩입니다. Chrome 등의 브라우저에는 HAR 파일 작성을 위한 설정에 도움이 될 수 있는 개발자 도구 섹션이 있습니다.
