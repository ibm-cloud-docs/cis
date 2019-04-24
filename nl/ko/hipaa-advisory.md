---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Advisory, Use of Caching, content caching, Cache-Control header

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# HIPAA 보안 권고문
{:#hipaa-advisory}

규제되는 데이터(예: PHI, ITAR)에 대한 캐싱 사용(CDN)이 **금지됩니다**. CIS를 사용하는 규제되는 모든 데이터를 **캐시 안함**으로 설정해야 합니다.
{:important}

CIS CDN을 통해 컨텐츠 캐싱을 사용 안함으로 설정하는 방법은 여러 가지가 있습니다. 
- 오리진 서버는 규제되는 컨텐츠에 대해 **Cache-Control** 헤더에서 **no-cache**를 설정할 수 있습니다.
- 오리진이 **no-cache** **Cache-Control** 헤더를 보내지 않는 경우에도 CIS 페이지 규칙을 사용하여 지정된 경로의 모든 컨텐츠에 대해 캐싱을 사용 안함으로 설정합니다. 
