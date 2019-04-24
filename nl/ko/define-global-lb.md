---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: global load balancer, global load balancer configuration

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# 글로벌 로드 밸런서 정의
{:#define-the-global-load-balancer}

호스트 이름을 지정하고 오리진 풀을 조정하며 추가 규칙을 정의하여 클라이언트에 트래픽을 제공하는 방법을 제어함으로써 글로벌 로드 밸런서 구성을 정의하십시오.

1. 오른쪽에 있는 로드 밸런서 작성 단추를 클릭하여 글로벌 로드 밸런서를 작성합니다.  

2. 도메인의 호스트 이름을 지정하고 원하는 경우 TTL 값(기본값은 60초임)을 조정한 후 **풀 추가**를 사용하여 오리진 풀을 추가합니다. 

   <img src="images/reliability11.png" alt="그림" style="width: 300px;"/>
   
   **참고:** 도메인 이름과 결합된 호스트 이름은 애플리케이션의 완전한 도메인 이름(FQDN)을 구성합니다. 일반 사용자는 이 FQDN을 사용하여 애플리케이션에 연결합니다. 
   
3. 풀의 왼쪽에 있는 위로 및 아래로 화살표를 클릭하여 오리진 풀의 상대적 우선순위를 조정합니다. 일반 사용자의 애플리케이션 요청은 이러한 오리진 풀에 의해 라운드 로빈 방식으로 제공됩니다. 
   
   <img src="images/reliability12.png" alt="그림" style="width: 300px;"/>   
   
4. 선택적으로 추가 규칙을 정의하여 여러 지리적 영역에서 클라이언트에 트래픽을 제공하는 방법을 제어할 수 있습니다. 다음 예제에서 남미 남부 지역에서 오는 클라이언트는 미국 서부 해안 오리진 풀로 라우팅됩니다. 이러한 규칙을 사용하여 가장 가까운 지역으로 클라이언트를 안내할 수 있습니다. 이러한 지역 중 하나에서 실패하면 일반 사용자가 작동 중지의 영향을 받지 않도록 요청이 다른 정상 위치로 라우팅됩니다. 

   <img src="images/reliability13.png" alt="그림" style="width: 300px;"/>   
   
5. **리소스 프로비저닝**을 클릭하여 글로벌 로드 밸런서의 구성을 완료합니다. 
6. 마지막으로 모바일 브라우저 창에 `FQDN URL`을 입력하여 애플리케이션에 대한 연결을 확인합니다. 연결할 수 있는 경우 환영 메시지가 표시됩니다.
