---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM Cloud Internet Services, CIS Activity Tracker events

subcollection: cis

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# CIS {{site.data.keyword.cloudaccesstrailshort}} 이벤트
{: #at_events}

{{site.data.keyword.cloud}}에서 사용자 및 애플리케이션이 IBM Cloud Internet Services(CIS)와 상호작용하는 방법을 추적하려면 {{site.data.keyword.cloudaccesstrailfull}} 서비스를 사용하십시오.
{:shortdesc}

{{site.data.keyword.cloudaccesstrailfull_notm}} 서비스는 {{site.data.keyword.cloud_notm}}에서 서비스 상태를 변경하는 사용자 시작 활동을 기록합니다. 자세한 정보는 [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla)의 내용을 참조하십시오.




## 이벤트 목록: DNS 도메인
{: #events_dns_domain}

다음 표에서는 DNS 도메인과 관련된 조치를 나열하고 이벤트를 생성합니다.

|조치|설명|
|---|---|  
|internet-svcs.zones.create|DNS 도메인을 작성합니다.|
|internet-svcs.zones.update|DNS 도메인을 업데이트합니다.|
|internet-svcs.zones.delete|DNS 도메인을 삭제합니다.|
|internet-svcs.zones.activation_check.update|DNS 도메인에 대한 활성화 검사를 수행합니다.|
|internet-svcs.zones.dnssec.update|DNS 도메인에 대한 DNSSEC를 사용 또는 사용 안함으로 설정합니다.|

## 이벤트 목록: DNS 레코드
{: #events_dns_record}

다음 표에서는 DNS 레코드와 관련된 조치를 나열하고 이벤트를 생성합니다.

|조치|설명|
|---|---|  
|internet-svcs.zones.dns_records.create|DNS 레코드를 작성합니다.|
|internet-svcs.zones.dns_records.update|DNS 레코드를 업데이트합니다.|
|internet-svcs.zones.dns_records.delete|DNS 레코드를 삭제합니다.|
|internet-svcs.zones.dns_records_bulk.create|구역 파일에서 DNS 레코드를 가져옵니다.|


## 이벤트 목록: 로드 밸런서
{: #events_load_balancers}

다음 표에서는 로드 밸런서와 관련된 조치를 나열하고 이벤트를 생성합니다.

|조치|설명|
|---|---|  
|internet-svcs.zones.load_balancers.create|글로벌 로드 밸런서를 작성합니다.|
|internet-svcs.zones.load_balancers.update|글로벌 로드 밸런서를 업데이트합니다.|
|internet-svcs.zones.load_balancers.delete|글로벌 로드 밸런서를 삭제합니다.|
|internet-svcs.load_balancers.monitors.create|상태 모니터를 작성합니다.|
|internet-svcs.load_balancers.monitors.update|상태 모니터를 업데이트합니다.|
|internet-svcs.load_balancers.monitors.delete|상태 모니터를 삭제합니다.|
|internet-svcs.load_balancers.pools.create|글로벌 로드 밸런서를 작성합니다.|
|internet-svcs.load_balancers.pools.update|글로벌 로드 밸런서를 업데이트합니다.|
|internet-svcs.load_balancers.pools.delete|글로벌 로드 밸런서를 삭제합니다.|


## 이벤트 목록: 캐시 제거
{: #events_cache}

다음 표에서는 캐시 제거와 관련된 조치를 나열하고 이벤트를 생성합니다.

|조치|설명|
|---|---|  
|internet-svcs.zones.purge_cache.purge_all.update|에지 서버에서 도메인의 캐시된 모든 자산을 제거합니다.|
|internet-svcs.zones.purge_cache.purge_by_urls.update|에지 서버에서 URL을 기준으로 캐시된 자산을 제거합니다.|
|internet-svcs.zones.purge_cache.purge_by_cache_tags.update|에지 서버에서 캐시 태그를 기준으로 캐시된 자산을 제거합니다.|
|internet-svcs.zones.purge_cache.purge_by_hosts.update|에지 서버에서 호스트 이름을 기준으로 캐시된 자산을 제거합니다.|


## 이벤트 목록: 페이지 규칙
{: #events_page_rules}

다음 표에서는 페이지 규칙과 관련된 조치를 나열하고 이벤트를 생성합니다.

|조치|설명|
|---|---|  
|internet-svcs.zones.pagerules.create|페이지 규칙을 작성합니다.|
|internet-svcs.zones.pagerules.update|페이지 규칙을 업데이트합니다.|
|internet-svcs.zones.pagerules.delete|페이지 규칙을 삭제합니다.|


## 이벤트 목록: 방화벽
{: #events_firewalls}

다음 표에서는 방화벽과 관련된 조치를 나열하고 이벤트를 생성합니다.

|조치|설명|
|---|---|  
|internet-svcs.zones.firewall.waf.packages.groups.update|WAF 규칙 세트 그룹을 사용 또는 사용 안함으로 설정합니다.|
|internet-svcs.zones.firewall.waf.packages.rules.update|WAF 규칙을 사용 또는 사용 안함으로 설정합니다.|
|internet-svcs.zones.firewall.access_rules.rules.create|도메인 레벨 IP 방화벽 규칙을 작성합니다.|
|internet-svcs.zones.firewall.access_rules.rules.update|도메인 레벨 IP 방화벽 규칙을 업데이트합니다.|
|internet-svcs.zones.firewall.access_rules.rules.delete|도메인 레벨 IP 방화벽 규칙을 삭제합니다.|
|internet-svcs.firewall.access_rules.rules.create|인스턴스 레벨 IP 방화벽 규칙을 작성합니다.|
|internet-svcs.firewall.access_rules.rules.update|인스턴스 레벨 IP 방화벽 규칙을 업데이트합니다.|
|internet-svcs.firewall.access_rules.rules.delete|인스턴스 레벨 IP 방화벽 규칙을 삭제합니다.|
|internet-svcs.zones.rate_limits.create|속도 제한 규칙을 작성합니다.|
|internet-svcs.zones.rate_limits.update|속도 제한 규칙을 업데이트합니다.|
|internet-svcs.zones.rate_limits.delete|속도 제한 규칙을 삭제합니다.|
|internet-svcs.zones.ua_rules.create|사용자 에이전트 차단 규칙을 작성합니다.|
|internet-svcs.zones.ua_rules.update|사용자 에이전트 차단 규칙을 업데이트합니다.|
|internet-svcs.zones.ua_rules.delete|사용자 에이전트 차단 규칙을 삭제합니다.|
|internet-svcs.zones.firewall.lockdowns.create|도메인 잠금 규칙을 작성합니다.|
|internet-svcs.zones.firewall.lockdowns.update|도메인 잠금 규칙을 업데이트합니다.|
|internet-svcs.zones.firewall.lockdowns.delete|도메인 잠금 규칙을 삭제합니다.|

## 이벤트 목록: 라우팅
{: #events_routing}

다음 표에서는 라우팅과 관련된 조치를 나열하고 이벤트를 생성합니다.

|조치|설명|
|---|---|  
|internet-svcs.zones.routing.smart_routing.update	|스마트 라우팅을 사용 또는 사용 안함으로 설정합니다.|
|internet-svcs.zones.routing.tiered_caching.update	|티어링된 캐싱을 사용 또는 사용 안함으로 설정합니다.|

## 이벤트 목록: 인증서 팩
{: #events_certificate_packs}

다음 표에서는 인증서 팩과 관련된 조치를 나열하고 이벤트를 생성합니다.

|조치|설명|
|---|---|  
|internet-svcs.zones.ssl.certificate_packs.create|전용 인증서를 주문합니다.|
|internet-svcs.zones.ssl.certificate_packs.delete|전용 인증서를 삭제합니다.|


## 이벤트 목록: 사용자 정의 인증서
{: #events_custom_certificate}

다음 표에서는 사용자 정의 인증서와 관련된 조치를 나열하고 이벤트를 생성합니다.

|조치|설명|
|---|---|  
|internet-svcs.zones.custom_certificates.create|사용자 정의 인증서를 업로드합니다.|
|internet-svcs.zones.custom_certificates.update|사용자 정의 인증서를 업데이트합니다.|
|internet-svcs.zones.custom_certificates.delete|사용자 정의 인증서를 삭제합니다.|


## 이벤트 목록: 설정
{: #events_settings}

다음 표에서는 구성 설정과 관련된 조치를 나열하고 이벤트를 생성합니다.

|조치|설명|
|---|---|  
|internet-svcs.zones.settings.cache_level.update|캐싱 레벨을 변경합니다.|
|internet-svcs.zones.settings.browser_cache_ttl.update|브라우저 캐시 TTL을 변경합니다.|
|internet-svcs.zones.settings.development_mode.update|개발 모드를 사용 또는 사용 안함으로 설정합니다.|
|internet-svcs.zones.settings.security_level.update|보안 레벨을 변경합니다.|
|internet-svcs.zones.settings.ssl.update|SSL 설정을 변경합니다.|
|internet-svcs.zones.settings.tls_1_2_only.update|TLS 1.2 지원을 사용 또는 사용 안함으로 설정합니다.|
|internet-svcs.zones.settings.waf.update|WAF(Web Application Firewall)를 사용 또는 사용 안함으로 설정합니다.|
|internet-svcs.zones.settings.cname_flattening.update|CNAME 플래트닝 설정을 변경합니다.|
|internet-svcs.zones.settings.always_online.update|도메인의 시간이 경과된(stale) 컨텐츠 제공을 사용 또는 사용 안함으로 설정합니다.|
|internet-svcs.zones.settings.sort_query_string_for_cache.update|캐시에서 컨텐츠를 조회할 때 조회 인수 정렬을 사용 또는 사용 안함으로 설정합니다.|
|internet-svcs.zones.settings.tls_1_3.update|TLS 1.3 설정을 변경합니다.|
|internet-svcs.zones.settings.automatic_https_rewrites.update|자동 HTTPS 재작성을 사용 또는 사용 안함으로 설정합니다.
|internet-svcs.zones.settings.opportunistic_encryption.update|기회적 암호화를 사용 또는 사용 안함으로 설정합니다.|


## 이벤트를 찾을 위치
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} 이벤트는 이벤트가 생성되는 {{site.data.keyword.cloud_notm}} 지역에 있는 {{site.data.keyword.cloudaccesstrailshort}} **계정 도메인**에서 사용 가능합니다.



## 추가 정보
{: #info}

IBM Cloud Internet Services(CIS)에서 생성되는 {{site.data.keyword.cloudaccesstrailshort}} 이벤트를 모니터하고 추가 정보가 필요한 API 요청을 식별하는 경우 이벤트에서 requestData 필드를 확인하십시오. 지원 티켓을 열고 requestData에서 사용 가능한 **X-CORRELATION-ID** 필드의 값을 포함하십시오.
