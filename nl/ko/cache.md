---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM CIS deployment, query strings, HTML files

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# 캐싱 개념
{:#caching-concepts}

이 문서에는 캐싱과 관련된 일부 개념 및 정의와 IBM CIS 배치에 어떻게 영향을 주는지가 포함되어 있습니다.

## 캐싱의 개념
{:#what-is-caching}

캐싱은 에지 서버에 파일을 저장하는 프로세스로서, 고객에게 해당 파일을 제공할 때 응답 시간을 개선할 목적으로 수행됩니다. 고객과 가까운 위치에 파일을 저장함으로써 네트워크 상에서 데이터 스트리밍에 걸리는 시간(통상 **대기 시간**이라고 함)을 줄일 수 있습니다.

캐시된 파일에는 만기 시간인 **TTL(Time-to-live)**이 지정되어 있습니다. 이 시간이 지나면 해당 파일이 캐시에서 영구 제거됩니다. 수동으로 캐시에서 파일을 영구 제거할 수도 있습니다. 파일이 캐시에서 제거된 후에 CIS는 오리진 서버로 돌아가서 파일을 다시 로드하고 캐시를 최신 버전으로 업데이트합니다.

캐시 설정과 캐싱 옵션에 대한 자세한 설명은 [캐싱 및 페이지 규칙 튜토리얼](/docs/infrastructure/cis?topic=cis-use-page-rules-with-caching)에 있습니다.

### 캐시되는 컨텐츠는 무엇입니까?
{:#what-content-is-cached}

기본적으로는 많은 유형의 이미지와 텍스트 파일(비-HTML 파일)이 포함된 **정적 파일**이 캐시됩니다. 여기에는 웹 사이트의 파일만 포함되고 소셜 네트워킹 사이트의 서드파티 리소스 등은 포함되지 않습니다. 또한 현재 MIME 유형으로 캐시되지 않습니다.

### HTML을 어떻게 캐시합니까? 
{:#how-do-i-cache-html}

기본적으로 정적 파일로 간주되지 않는 HTML 파일은 캐시되지 않습니다. 하지만 정적 HTML을 동적 HTML과 분명하게 구분할 수 있는 경우 [페이지 규칙 기능을 사용](/docs/infrastructure/cis?topic=cis-use-page-rules)하여 HTML 파일을 캐시할 수 있습니다.


## 조회 문자열 정렬
{:#query-string-sorting}

**엔터프라이즈만 해당** CIS는 조회 문자열의 순서가 캐시의 개별 파일의 순서와 다른 URL을 처리합니다. 즉, 하나의 사용자가 다음을 요청하고

`/video/123456?title=0&byline=0&portrait=0&color=987654`

다른 사용자가 다음을 요청하는 경우

`/video/123456?byline=0&color=987654&portrait=0&title=0`

캐시에 파일이 있음에도 CIS가 오리진으로 되돌아갑니다.

조회 문자열 정렬은 조회 문자열이 캐시에 적중하기 _전에_ 이 조회 문자열을 정렬하며, 이로 인해 캐시 적중률이 높아집니다. **캐싱** 페이지에서 토글을 사용하여 조회 문자열 정렬을 사용하십시오.

## 시간이 경과된(stale) 컨텐츠 제공
{:#serve-stale-content-caching}

서버가 작동 중지되면 사이트의 제한된 버전을 온라인 상태로 유지합니다. 컨텐츠가 만료된 경우에도, 오리진 서버가 오프라인이면 CIS는 캐시된 컨텐츠를 사용자에게 계속 제공합니다.
