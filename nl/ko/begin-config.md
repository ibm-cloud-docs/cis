---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: global load balancer configuration, glb configuration

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}

# 글로벌 로드 밸런서 구성 시작
{:#begin-global-load-balancer-configuration}

 글로벌 로드 밸런서 구성을 시작하십시오.

1. **안정성** 섹션에서 **글로벌 로드 밸런서**를 선택합니다. 
    
    <img src="images/reliability6.png" alt="그림" style="width: 300px;"/>

2. 상태 검사 섹션으로 스크롤합니다. 

   이 구성은 선택사항입니다. 사용자 정의 상태 검사를 정의하지 않으면 시스템이 “/”를 기본 상태 검사 경로로 사용합니다.
   {:note}

3. **상태 검사 작성** 단추를 클릭하여 사용자 정의 상태 검사를 정의합니다.   

   상태 검사를 수행할 경로를 제공하십시오. 상태 검사에 HTTP 또는 HTTPS 프로토콜을 사용할 수 있습니다. 
   
4. **고급 옵션**에서 상태 검사 간격, 재시도 수, 요청 메소드와 응답 본문과 같은 기타 매개변수를 사용자 정의할 수 있습니다. 
   
   <img src="images/reliability7.png" alt="그림" style="width: 300px;"/>
   
5. **리소스 프로비저닝**을 클릭하여 상태 검사 구성을 완료합니다. 
