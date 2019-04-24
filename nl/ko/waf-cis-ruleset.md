---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: CIS Rule Set, WAF settings, WAF CIS Rules

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# WAF 설정
{:#waf-settings}

다음 표에는 WAF(Web Application Firewalls)가 수행할 수 있는 조치가 표시됩니다. 


|조치|정의|
|---|---|
|차단 | 공격을 차단하면 웹 사이트에 게시되기 전에 조치가 중지됩니다.|
|시뮬레이션 | 거짓 긍정(false positive)을 테스트하려면 WAF를 시뮬레이션 모드로 설정하여 인증 확인하거나 차단하지 않고도 가능한 공격에 대한 응답을 기록합니다. |
|인증 확인 | 인증 확인 페이지에서는 방문자가 웹 사이트에 계속 방문하기 위해 CAPTCHA를 제출해야 합니다.|
|임계값 또는 민감도 설정 | 민감도에 따라 트리거하도록 규칙을 설정합니다.|

## WAF에 대한 CIS 규칙 세트
{:#cis-ruleset-for-waf}

이 패키지의 규칙 세트를 표시하려면 **CIS 규칙 보기**를 선택하십시오. 규칙 세트는 다음을 따릅니다.
  * Drupal
  * Flash
  * Joomla
  * Magento
  * Miscellaneous
  * PHP
  * Plone
  * Specials
  * WHMCS
  * Wordpress

**Specials**에는 인터넷의 거의 모든 애플리케이션과 웹 사이트에 맞는 여러 규칙이 포함됩니다. 이 규칙 세트는 WAF가 제공하는 보안의 핵심이며, SQLi, XSS 및 LFI와 같은 일반적인 공격을 대상으로 하는 규칙을 포함합니다. 이 Specials는 항상 사용하도록 권장합니다.

기술 스택에 해당하는 규칙 세트만 사용으로 설정하십시오. 예를 들어, Wordpress를 사용하고 다른 기술은 사용하지 않는 경우 Specials 및 Wordpressm 규칙 세트만 사용으로 설정하십시오. 기술 스택과 관련 없는 규칙 세트는 사용하지 마십시오.

포함된 각 규칙에 대한 세부사항을 보려면 특정 규칙 세트 중 하나를 선택하십시오.

CIS 규칙 세트를 사용하면 각 규칙에 대해 네 가지 조치를 수행할 수 있습니다.
  1. **사용 안함**: 규칙을 끕니다.
  2. **시뮬레이션**: 이벤트를 로그하며 방문자를 차단하거나 인증 확인하지 않습니다. 로그를 검토한 후 차단하거나 인증 확인하도록 설정할 수 잇습니다.
  3. **차단**: 요청을 완전히 차단하며, 이 요청에 대해 이를 무시할 수 있는 옵션은 없습니다.
  4. **인증 확인**: 요청에서 액세스가 허용되기 전에 완료해야 하는 인증 확인(CAPTCHA) 페이지를 표시합니다.

규칙 이름은 규칙이 작동하는 방식을 정확하게 보여주지 않으며 대부분 해당 기능에 대한 일반적인 요약입니다. 이것은 의도적인 것입니다. 보안을 이유로 트래픽을 필터링하는 데 사용하는 코드(또는 기타 정확한 정보)를 표시하지 않습니다. 이렇게 하면 악의적 행위자들이 리버스 엔지니어링을 통해 방어벽을 우회하는 것을 막을 수 있습니다.
