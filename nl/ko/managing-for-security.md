---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-26"

keywords: IBM CIS, optimal security, Security Level

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# 최적의 보안을 위한 IBM CIS 관리
{:#manage-your-ibm-cis-for-optimal-security}
IBM Cloud Internet Services(CIS) 보안 설정에는 트래픽의 부정적 영향과 거짓 긍정(false positive)을 피하기 위해 설계된 안전한 기본값이 포함되어 있습니다. 그러나 이러한 안전한 기본 설정은 모든 고객에 대한 최상의 보안 관점을 제공하지 않습니다. CIS 계정이 안전한 보안 방식으로 구성되도록 하려면 다음 단계를 수행하십시오.

**권장사항 및 우수 사례:**

* 프록싱 및 난독화 증가로 오리진 IP 주소 보호
* 선별적으로 보안 레벨 구성
* 안전하게 WAF(Web Application Firewall) 활성화

## 우수 사례: 오리진 IP 주소 보호
{:#best-practice-secure-origin-ip-address}

IBM CIS에 특정한 IP 주소로 당사가 적극적으로 응답하므로 하위 도메인이 IBM CIS를 사용하여 포록싱된 경우에는 모든 트래픽이 보호됩니다(예: 모든 클라이언트가 우선 CIS 프록시에 연결되고 오리진 IP 주소가 난독화됨).

### 오리진의 HTTP(S) 트래픽에 대한 모든 DNS 레코드의 IBM CIS 프록시 사용
{:#use-cis-proxies-for-dns-records}

오리진 IP 주소의 보안을 개선하려면 모든 HTTP(S) 트래픽이 프록싱되어야 합니다.

**직접 차이점 확인 - 비-프록싱 및 프록싱 레코드 조회:**

```
$ dig nonproxied.theburritobot.com +short
1.2.3.4 (The origin IP address)

$ dig proxied.theburritobot.com +short
104.16.22.6 , 104.16.23.6 (CIS IP addresses)
```

### 비표준 이름으로 비-프록싱 오리진 레코드 난독화
{:#obsure-non-proxied-origin-records-with-non-standard-names}
IBM CIS를 통해 프록싱될 수 없으며 여전히 오리진 IP(예: FTP)를 사용하는 레코드는 추가적인 난독화를 통해 보호될 수 있습니다. 특히 IBM CIS에 의해 프록싱될 수 없는 오리진의 레코드가 필요한 경우에는 비표준 이름을 사용하십시오. 예를 들어, `ftp.example.com` 대신에 `[random word or-random characters].example.com`을 사용하십시오. 이 난독화를 통해 DNS 레코드의 사전 스캔이 오리진 IP 주소를 덜 노출시키게 됩니다.

### 가급적 HTTP 및 비-HTTP 트래픽에 대해 별도의 IP 범위 사용
{:#use-separate-ipranges-for-traffic}
일부 고객은 HTTP 및 비-HTTP 트래픽에 대해 별도의 IP 범위를 사용함으로써 HTTP IP 범위를 지시하는 모든 레코드를 프록싱하고 다른 IP 서브넷으로 모든 비-HTTP 트래픽을 난독화할 수 있습니다.

## 우수 사례 2: 선별적으로 보안 레벨 구성
{:#best-practice-configure-security-level-selectively}
**보안 레벨**이 **IP 평판 데이터베이스**의 민감도를 설정합니다. 부정적 상호작용이나 거짓 긍정(false positive)을 방지하려면, 필요에 따라 보안성 강화를 위해 도메인별로 **보안 레벨**을 구성하고 해당되는 경우 이를 줄이십시오.

### 민간함 영역의 보안 레벨을 '높음'으로 올리기
{:#increase-security-level-for-sensitive-areas}
무차별 대입공격 시도를 줄이기 위해 도메인의 고급 보안 페이지를 통해 또는 로그인 페이지나 관리 페이지의 **페이지 규칙**을 추가하여 이 설정을 늘릴 수 있습니다.

1. API의 URL 패턴으로 **페이지 규칙**을 작성하십시오(예: `www.example.com/wp-login`). 
2. **보안 레벨** 설정을 식별하십시오.
3. 설정을 **높음**으로 표시하십시오.
4. **리소스 프로비저닝**을 선택하십시오.

### 거짓 긍정(false positive)을 줄이기 위해 민감하지 않은 경로 또는 API에 대해 보안 레벨 낮추기
{:#decrease-security-level-non-sensitive-paths-reduce-false-positives}
일반 페이지와 API 트래픽의 경우에 이 설정을 낮출 수 있습니다. 

1. API의 URL 패턴으로 **페이지 규칙**을 작성하십시오(예: `www.example.com/api/*`).
2. **보안 레벨** 설정을 식별하십시오.
3. 보안 레벨을 **낮음** 또는 **기본적으로 끄기**로 전환하십시오.
4. **리소스 프로비저닝**을 선택하십시오.

### 보안 레벨 설정의 의미
{:#what-do-security-level-settings-mean}
보안 레벨 설정은 네트워크에서 악의적 행위로부터 특정 IP 주소가 확보하는 위협 점수와 일치합니다. 위협 점수가 10을 초과하면 높다고 간주됩니다.

* **높음**: 0보다 큰 위협 점수가 인증 확인됩니다.
* **중간**: 14보다 큰 위협 점수가 인증 확인됩니다.
* **낮음**: 24보다 큰 위협 점수가 인증 확인됩니다.
* **기본적으로 끄기**: 49보다 큰 위협 점수가 인증 확인됩니다.
* **끄기**: *엔터프라이즈만 해당* 
* **공격받는 중**: 웹 사이트가 DDoS 공격을 받고 있을 때만 사용해야 합니다. CIS가 트래픽과 동작을 분석하여 방문자가 웹 사이트에 액세스하려는 합법적인 방문자인지 확인하는 약 5초 동안 이 방문자는 삽입광고 페이지를 수신합니다. **공격받는 중**은 API 사용과 같이 도메인에 대한 특정 조치에 영향을 줄 수 있습니다. 이 섹션에 대한 페이지 규칙을 작성하여 API의 사용자 정의 보안 레벨 또는 도메인의 다른 파트를 설정할 수 있습니다.

보안 레벨 설정을 주기적으로 검토하도록 권장합니다. 해당 지시사항은 [CIS 설정의 우수 사례 문서](/docs/infrastructure/cis?topic=cis-best-practices-for-cis-setup)를 참조하십시오.

## 우수 사례 3: 안전하게 WAF(Web Application Firewall) 활성화
{:#best-practice-activate-waf-safely}
WAF는 **보안** 섹션에서 사용 가능합니다. 전체 도메인에 대해 켜기 전에 WAF가 가급적 안전하게 구성되어 있음을 보장하기 위해 이러한 설정을 역순으로 안내하겠습니다. 이러한 초기 설정은 추가 조정을 위해 **보안 이벤트**를 채워 거짓 긍정(false positive)을 줄일 수 있습니다. 식별 시에 새로운 취약점을 처리할 수 있도록 WAF은 자동으로 업데이트됩니다.

WAF는 다음 유형의 공격으로부터 사용자를 보호합니다.
* SQL 인젝션 공격
* XSS(Cross-site scripting)
* 사이트 간 위조

WAF에는 가장 일반적인 공격을 중지하기 위한 규칙이 포함된 기본 규칙 세트가 포함되어 있습니다. 이 때 사용자는 WAF를 사용 또는 사용 안함으로 설정하고 WAF 규칙 세트의 특정 규칙을 세부 조정할 수 있습니다. 기본 규칙 세트와 각 규칙의 작동에 대한 상세 정보는 [WAF 기본 규칙 세트](/docs/infrastructure/cis?topic=cis-waf-default-rule-set) 문서를 참조하십시오.

WAF에 대한 자세한 정보는 [WAF 개념 문서](/docs/infrastructure/cis?topic=cis-web-application-firewall-concepts-q-a)를 참조하십시오.

## 우수 사례 4: TLS 설정 구성
{:#best-practice-configure-tls-settings}
IBM CIS는 트래픽을 암호화하기 위한 일부 옵션을 제공합니다. 리버스 프록시로서, 당사는 데이터 센터에서 TLS 연결을 닫고 오리진 서버에 대한 새 TLS 연결을 엽니다.

TLS에서는 네 개의 오퍼레이션 모드를 제공합니다.
* **끄기**: TLS가 이 모드에서 사용되지 않습니다. 권장하지 않습니다.
* **클라이언트 대 에지**: TLS이 CIS에서 클라이언트로의 트래픽을 암호화하지만, CIS에서 오리진 서버로의 트래픽은 암호화하지 않습니다.
* **엔드-투-엔드 유연성**: TLS이 모든 트래픽을 암호화하지만, 사용자는 자체 서명된 인증서를 사용하여 CIS와 오리진 서버 간의 트래픽을 보호할 수 있습니다.
* **엔드-투-엔드 CA 서명**: TLS이 모든 트래픽을 암호화하며, 사용자는 CA 서명된 인증서를 사용해야 합니다.

TLS 옵션에 대한 자세한 정보는 [이 문서](/docs/infrastructure/cis?topic=cis-tls-options)를 참조하십시오.

IBM CIS에서는 사용자 정의 인증서의 사용을 허용합니다. 또는 사용자가 CIS에서 제공하는 와일드카드 인증서를 사용할 수 있습니다.

### 사용자 정의 인증서 업로드
{:#upload-custom-certs}
**인증서 추가** 단추를 클릭하고 인증서, 개인 키 및 번들 메소드를 입력하여 사용자 정의 인증서를 업로드할 수 있습니다. 자체 인증서를 업로드하면 암호화된 트래픽과의 즉각적인 호환성이 확보되며 인증서(예: EV(Extended Validation) 인증서)에 대한 제어가 유지됩니다. 사용자 정의 인증서를 업로드하는 경우에는 사용자 자신이 인증서 관리를 책임진다는 점을 유념하십시오. 예를 들어, IBM CIS는 인증서 만기 날짜를 추적하지 않습니다. 

![사용자 정의 인증서](images/upload-custom-certificate.png)

### 전용 인증서 주문
{:#order-dedicated-certs}
CIS는 전용 인증서를 제공하여 인증서 관리를 용이하게 합니다. 더 이상 개인 키를 생성하거나 인증서 서명 요청(CSR)을 작성하거나 인증서를 갱신하지 않아도 됩니다. **인증서 추가** 단추를 클릭하고 와일드카드 인증서를 주문하거나 전용 사용자 정의 인증서를 주문하기 위한 호스트 이름을 입력하여 전용 인증서를 주문할 수 있습니다. 인증서 유형은 다음과 같습니다.

 * P-256키를 사용한 SHA-2/ECDSA 서명 인증서 
 * RSA 2048비트 키를 사용한 SHA-2/RSA 서명 인증서 
 * RSA 2048비트 키를 사용한 SHA-1/RSA 서명 인증서. 
 
CIS는 `.cu`, `.iq`, `.ir`, `.kp`, `.sd`, `.ss` 및 `.ye`를 제외한 모든 TLD에 대해 실행될 수 있습니다. CIS는 만기 날짜를 관리합니다. 전용 사용자 정의 인증서에서 호스트 이름을 편집하려면 다시 주문한 다음 삭제해야 합니다. 예를 들어, 호스트 이름이 `alpha.yourdomain.com`인 전용 사용자 정의 인증서를 주문합니다. 호스트 이름 `beta.yourdomain.com`을 전용 사용자 정의 인증서에 추가하려면 호스트 이름이 `alpha.yourdomain.com` 및 `beta.yourdomain.com`인 다른 전용 사용자 정의 인증서를 주문하십시오. 나중에 원래 전용 사용자 정의 인증서를 삭제_해야 합니다_.

전용 인증서를 처음 주문하면 DCV(Domain Control Validation) 프로세스가 발생하며 이를 통해 해당 TXT 레코드가 생성됩니다. TXT 레코드를 삭제하면, 다른 전용 인증서를 주문할 때 DCV 프로세스가 다시 발생합니다. 전용 인증서를 삭제해도 DCV 프로세스에 해당하는 TXT 레코드는 삭제되지 않습니다.
{:note}

다음은 전용 인증서를 주문할 때 표시되는 일반적인 오류입니다.
* `인증 서비스에 연결하는 중에 오류 발생.`
* `인증 서비스에서 요청하는 중에 오류 발생`
{:note}

인증서를 주문할 때 오류가 발생하면 페이지를 새로 고치고 다시 시도하십시오.

![전용 인증서](images/order-dedicated-certificate.png)

### 제공된 인증서 활용
{:#utilize-provisioned-certificate}
IBM은 여러 인증 기관(CA)과 협력하여 고객에 대해 도메인 와일드카드 인증서를 제공합니다. 이러한 인증서를 설정하기 위해 수동 확인이 필요할 수 있습니다. 지원 팀에서 이러한 추가 단계를 수행하는 데 도움을 줄 수 있습니다.

### 에지의 인증서 우선순위
{:#certificate-prioirity-at-our-edge}
인증서가 에지에 표시되는 우선순위 기준은 다음과 같습니다.
1. 업로드된 사용자 정의
2. 전용 사용자 정의
3. 전용 와일드카드
4. 유니버셜

### 최소 TLS 버전
{:#security-minimum-tls-version}
[최소 TLS 버전](/docs/infrastructure/cis?topic=cis-tls-options#minimum-tls-version)을 참조하십시오. TLS 레벨이 높으면 보안 수준이 높아지지만 고객이 사이트에 접속하는 것을 방해할 수 있습니다.
