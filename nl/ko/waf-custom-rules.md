---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: WAF Custom Rules, Custom WAF Rules

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# WAF 사용자 정의 규칙
{:#waf-custom-rules}

**보안 > WAF(Web Application Firewall) > 사용자 정의 규칙**을 통해 사용자 정의 WAF 규칙으로 이동하십시오. WAF 규칙은 엔터프라이즈 플랜에서 사용 가능하며 고객의 고유 요구사항 및/또는 해당 웹 사이트의 트래픽 패턴을 기반으로 작성됩니다. 이는 요청의 특성 조합을 가상으로 차단하도록 당사에 요청할 수 있음을 의미합니다. 

사용자 정의 WAF 규칙은 IBM WAF에 적용된 규칙이 없으며 공격자가 특히 사용자 웹 사이트의 구조에 맞게 대상으로 지정된 특정 패턴이나 사용자 에이전트를 사용하는 상황에 맞춰져 있습니다. 이러한 상황에서 웹 특성에 맞는 사용자 정의 규칙을 작성할 수 있습니다.

## 사용자 정의 규칙 요청
{:#request-a-custom-rule}

규칙을 요청하려면 규칙 요구사항 또는 트래픽 패턴에 대한 이메일을 wafsup@us.ibm.com으로 보내십시오. 

다음을 포함해 가능한 한 많은 정보를 제공하십시오.
* 약 100개의 악성 요청 샘플을 표시하는 액세스 로그.
* 요청에 차단하거나 트리거할 수 있는 항목이 포함되었는지 여부를 판별하기 위한, POST 데이터가 포함된 샘플 POST 요청(요청에 POST 본문이 있는 경우).
* 잠재적 거짓 긍정(false positive)의 경우 요청을 완전히 차단할지 아니면 인증 확인할지의 여부.
* 이러한 규칙을 적용할 특정 도메인.
* 기본적으로 규칙을 켤지 아니면 끌지의 여부.

사용자 정의 WAF 규칙을 작성한 후 적용하려면 모든 사용자 정의 규칙을 사용으로 설정해야 합니다.
{:note}
