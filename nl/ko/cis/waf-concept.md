---
copyright:
  years: 2018
lastupdated: "2018-03-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# WAF(Web Application Firewall) 개념 Q & A

WAF(Web Application Firewall)는 일부 가장 까다로울 수 있는 ISO 계층 7 공격에 대해 보호합니다. 이 문서에서는 일부 상세 정보를 제공합니다. 

## WAF(Web Application Firewall)는 무엇입니까? 
WAF(Web Application Firewall)는 웹 애플리케이션과 인터넷 간의 HTTP 트래픽을 필터링하고 모니터링하여 웹 애플리케이션 보호에 도움을 줍니다. WAF는 ISO 프로토콜 계층-7 방어입니다([OSI 모델 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://en.wikipedia.org/wiki/OSI_model)에서). 이는 모든 유형의 공격에 대해 방어하도록 설계되지 않았습니다.  

웹 애플리케이션 앞에 WAF를 배치하면 웹 애플리케이션과 인터넷 간에 보호막을 배치하는 것과 같습니다. 프록시 서버는 (발신 트래픽에 대해) 중개자를 사용하여 클라이언트 시스템의 ID를 보호하지만, WAF는 (수신 트래픽에 대해) 서버에 도달하기 전에 클라이언트의 트래픽이 WAF를 통해 전달되도록 함으로써 서버의 노출을 방지하는 리버스 프록시의 유형입니다. 

## WAF에서 방지할 수 있는 공격의 유형은 무엇입니까? 
일반적으로 WAF는 무엇보다도 사이트 간 위조, XSS(Cross-site scripting), 파일 포함 및 SQL 인젝션 등의 공격으로부터 웹 애플리케이션을 보호합니다. WAF는 대개 도구 스위트의 일부이며, 이는 다양한 공격 벡터에 대한 전체적인 방어를 함께 구축할 수 있습니다. 

## WAF는 어떻게 작동됩니까? 

WAF는 정책이라고도 하는 규칙 세트를 통해 작동됩니다. 이러한 정책의 용도는 악성 트래픽을 필터링으로 걸러내서 애플리케이션의 취약점을 보호하는 것입니다.  

WAF의 가치는 해당 정책 수정이 구현될 수 있는 속도와 용이성 및 이에 따라 다양한 공격 벡터에 대한 보다 빠른 응답을 허용하는 데 있습니다. 예를 들어, [DDoS 공격 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://en.wikipedia.org/wiki/Denial-of-service_attack) 중에 속도 제한은 WAF 정책을 수정하여 구현될 수 있습니다. 
