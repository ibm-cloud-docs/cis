---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: OWASP Rule Set, Rule Set

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# WAF에 대한 OWASP 규칙 세트
{:#owasp-rule-set-for-waf}

OWASP 규칙 세트에는 일반 공격 발견 규칙이 포함됩니다. OWASP 규칙은 SQL 인젝션, XSS(Cross-site scripting) 및 로케일 파일 포함을 포함한 많은 일반 공격 카테고리로부터 보호합니다. IBM CIS는 이러한 규칙을 제공하지만 큐레이션하지는 않습니다. OWASP는 적절한 보안 기준선을 제공하는 산업 표준입니다. 자세한 정보는 다음 링크를 참조하십시오.
  * [Github의 OWASP](https://github.com/SpiderLabs/owasp-modsecurity-crs)
  * [OWASP.org](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project)

## OWASP 관리
{:#managing-owasp}

[CIS 규칙 세트](/docs/infrastructure/cis?topic=cis-cis-rule-set-for-waf)와 달리 OWASP를 사용하면 민감도를 설정할 수 있습니다.
요청은 높음부터 낮음까지의 심각도 점수가 연관되어 있는 OWASP 규칙 세트를 트리거할 수 있습니다. 최종 점수는 트리거된 모든 규칙에 따라 계산됩니다. CIS는 최종 점수를 계산한 후 처음에 선택된 민감도 임계값과 비교한 다음 요청을 차단하거나 허용합니다.

|민감도 점수| 트리거 임계값|
|------|---------------|
|낮음(low) |  60 이상      |
|중간(medium) |  40 이상      |
|높음(high) |  25 이상      |

OWASP 민감도를 `low`로 설정하는 것이 좋습니다. `high`로 설정한 경우 CIS에서 로그를 확인하고 애플리케이션에서 작동하도록 OWASP 규칙 세트를 세부 조정하십시오.

CIS 규칙 세트의 규칙과 달리 OWASP 규칙은 _설정_ 또는 _해제_로만 토글할 수 있으며, _사용 안함_, _시뮬레이션_, _인증 확인_ 또는 _차단_으로 설정될 수 있습니다.

## 거짓 긍정(false positive)은 어떻게 처리합니까?
{:#owasp-false-positives}

변수 또는 값이 _참(true)_ 또는 _긍정(positive)_으로 평가되지만 실제로는 부정적이면 거짓 긍정(false positive)이 발생할 수 있습니다. WAF 컨텍스트에서 거짓 긍정(false positive)은 요청이 실수로 악의적으로 평가되어 차단되었음을 의미합니다.

거짓 긍정(false positive)을 처리하고 향후 발생하지 않도록 하려면 이를 발견하여 정정하는 방법을 알아야 합니다. 차단된 요청의 로그를 검토한 다음 웹 사이트의 예상 및 정상 트래픽의 컨텍스트 내에서 이러한 요청을 합리적으로 차단했는지 여부를 평가하십시오.
