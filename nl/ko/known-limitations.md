---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: health checks, Free Trial plan, dedicated certificate, known issues

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"} 
{:note: .note} 
{:important: .important} 
{:deprecated: .deprecated} 
{:generic: data-hd-programlang="generic"}

# 알려진 제한사항
{:#known-limitations}

 * Chrome을 사용하는 것이 좋습니다.
 
 * 무료 평가판 플랜은 계정당 하나의 인스턴스로 제한됩니다. 리소스 인스턴스를 작성하고 이에 도메인을 추가한 후에는 CIS에 대한 새 리소스 인스턴스를 추가할 수 없습니다. 이 제한사항은 시범 도메인을 삭제한 후에 도메인을 다시 동일한 리소스 인스턴스에 추가하려는 경우에도 적용됩니다. 이를 수행하려고 시도하면 오류가 발생합니다.

 * 이 서비스의 경우에는 다른 제공자의 NS 레코드만 사용하는 하위 도메인 위임이 지원됩니다. CNAME 위임은 지원되지 않습니다.
  
 * A, AAAA 및 CNAME 와일드카드 레코드(*)를 프록싱할 수 없습니다.

 * 전용 인증서를 삭제하는 경우 삭제를 완료하기 전 잠깐 동안 목록에 다시 표시될 수 있습니다.
 
 * 주문 후 사용자 정의 전용 인증서의 호스트 이름을 수정하려면 인증서를 새로 주문한 다음 이전 인증서를 삭제해야 합니다. 
 
 * 두 문자의 국가 코드로 작성된 IP 규칙은 `인증 확인` 조치로만 이루어질 수 있습니다. 한 국가의 방문자를 차단하려면 엔터프라이즈 플랜으로 업그레이드하거나 서버에 규칙을 배치하여 완전히 차단하십시오.

## 글로벌 로드 밸런서(GLB)
{:#known-limitations-glb}

 * Cloud Internet Services를 사용하면 로드 밸런서 호스트 이름에 `_` 문자를 사용할 수 있지만 Kubernetes 클러스터는 `_`를 사용할 수 없습니다. 

 * 표준 플랜은 최대 5개의 로드 밸런서, 풀 및 상태 검사를 허용합니다. 각 풀에는 총 6개의 오리진이 있을 수 있지만 6개의 고유 오리진만 각 CIS 인스턴스에서 허용됩니다.

* 삭제된 풀과 오리진에 대한 상태 검사 이벤트는 필터링할 수 없지만 테이블에 여전히 표시됩니다.

* `풀 상태`를 기준으로 상태 검사 이벤트를 필터링하는 경우, `성능 저하된` 풀이 기술적으로는 정상이기 때문에 포함되지만 하나 이상의 위험한 오리진이 포함될 수 있습니다.

* 상태 검사에 대한 요청 헤더 이름을 추가하는 경우 `Host`를 사용하십시오. 상태 검사에 소문자 `host` 사용 시 실패합니다.

## DNS
{:#known-limitations-dns}

 * 내보내는 DNS 레코드에 숨겨야 하는 Cloudflare CNAME 레코드가 포함됩니다. 이러한 레코드는 `_`로 시작되며 대개 이름이 같은 두 번째 레코드를 포함하지만 `_`는 제거됩니다.
   ```
   Ex.
   _cf.generate.yourdomain.com 0	IN	CNAME address.alias.com
   cf.generate.yourdomain.com 0	IN	CNAME address2.alias.com
   ```
 
   이러한 레코드를 올바르게 가져오려면 구역 파일에서 제거해야 합니다.
 
 * CAA DNS 레코드 내보내기가 올바르게 작동하지 않습니다. `<tag>` 및 `<value>`가 16진으로 인코딩됩니다. 
 
    CAA `<flags>` `<tag>` `<value>`
  {:note}
   ```
   Ex.
   Original CAA record
   caa.yourdomain.com.	1	IN	CAA	0 issue "letsencrypt.org"
 
   Exported CAA record
   caa.yourdomain.com.	1	IN	CAA	0 6973737565 "6c657473656e63727970742e6f7267"
   ```
   이러한 레코드를 가져오기 전에 16진에서 문자열로 변환하거나 수동으로 제거하고 추가해야 합니다.

## 페이지 규칙
{:#known-limitations-pagerules}

   * 페이지 규칙 ID가 업데이트를 위한 JSON 문자열 또는 JSON 파일에 포함되지 않은 경우, IBM Cloud CLI의 CIS 플러그인을 사용하여 페이지 규칙 설정을 업데이트하면 오류가 발생할 수 있습니다. 이 문제점을 해결하려면 ID를 포함하여 페이지 규칙에 대한 완전한 JSON 구성 파일을 사용하여 업데이트를 제출하십시오.
   * UI가 업데이트 성공을 보고하더라도 CIS UI를 사용하여 페이지 규칙 설정을 제거할 때 설정이 제거되지 않을 수 있습니다. 이 문제점을 해결하려면 IBM Cloud CLI의 CIS 플러그인을 사용하여 설정을 제거하고 JSON 업데이트 문서에 페이지 규칙 ID를 포함하십시오.
      ```
      $> ibmcloud cis page-rule-update <domain-id> <rule-id> -j <file>
      ```
      JSON 파일에는 필수 업데이트와 함께 ID를 포함한 완전한 페이지 규칙 구성이 있어야 합니다.
