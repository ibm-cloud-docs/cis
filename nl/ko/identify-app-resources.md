---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: origin pools, application resources, Origin Pools section

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# 애플리케이션 리소스 식별
{:#identify-your-application-resources}

애플리케이션의 리소스(예: 오리진 풀 및 상태 검사 메커니즘)를 식별하십시오.
 
1. **오리진 풀** 섹션으로 이동하고 **풀 작성**을 클릭하여 새 오리진 풀을 정의하십시오. 

   오리진 풀은 클라이언트에 애플리케이션을 제공하는 서버 리소스입니다. 
   
2. 오리진 풀에 이름을 지정하고 앞에서 정의한 상태 검사 메커니즘을 선택하십시오. 애플리케이션 서버를 오리진으로 추가하십시오. **오리진 추가**를 클릭하여 하나 이상의 오리진을 추가할 수 있습니다. 

   애플리케이션 서버가 IBM Cloud Load Balancer와 같은 로컬 로드 밸런서 뒤에 있는 경우, 개별 서버를 추가하는 대신 오리진으로서 로드 밸런서의 FQDN 또는 가상 IP를 추가하십시오.
   {:note}
   
3. **리소스 프로비저닝**을 클릭하여 오리진 풀 작성을 완료하십시오.  

   <img src="images/reliability8.png" alt="그림" style="width: 300px;"/>
   
   오리진 풀은 처음에 **비정상**으로 표시됩니다. 시스템이 상태 검사에 성공하면 상태가 **정상**으로 변경됩니다. 브라우저를 새로 고쳐 상태 변경사항을 봐야 합니다. 
   
   <img src="images/reliability9.png" alt="그림" style="width: 300px;"/>
   
   오리진 풀 내에 여러 오리진이 있는 경우 정상 오리진 임계값을 사용하여 풀이 정상임을 선언하기 전에 정상인 최소 오리진 수를 지정하십시오.
   {:note}
   
4. 가지고 있는 애플리케이션 팜의 수만큼 오리진 풀을 정의하십시오. 이러한 팜은 동일하거나 다른 지리적 지역 내에
있을 수 있습니다. 이 예제에서 미국 서부와 동부 해안의 애플리케이션 팜을 나타내는 두 개의 오리진 풀을 작성합니다. 

   <img src="images/reliability10.png" alt="그림" style="width: 300px;"/>
