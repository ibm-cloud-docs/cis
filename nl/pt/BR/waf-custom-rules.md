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


# Regras customizadas do WAF
{:#waf-custom-rules}

Navegue até as Regras customizadas do WAF por meio de **Segurança > Firewall do aplicativo da web > Regras customizadas**. As Regras do WAF estão disponíveis em planos Enterprise e são criadas com base nos requisitos exclusivos do cliente e/ou nos padrões de tráfego de seu website. Isso significa que é possível solicitar o bloqueio de praticamente qualquer combinação de características de uma solicitação. 

As Regras customizadas do WAF destinam-se a situações nas quais o WAF da IBM ainda não tem uma regra que esteja em vigor e o invasor usa um padrão específico ou um agente do usuário destinado especificamente para a estrutura de seu website. Nessas situações, é possível criar uma regra customizada para sua propriedade da web.

## Solicitar uma regra customizada
{:#request-a-custom-rule}

Para solicitar uma regra, envie um e-mail para wafsup@us.ibm.com com requisitos de regras ou padrões de tráfego. 

Forneça o máximo de informações possível, incluindo:
* Logs de acesso mostrando uma amostra de cerca de 100 solicitações supostamente maliciosas.
* Uma solicitação POST de amostra incluindo os dados POST (se as solicitações tiverem um corpo POST) para determinar se a solicitação contém qualquer coisa que podemos bloquear ou acionar.
* Se deseja que as solicitações sejam totalmente bloqueadas ou desafiadas, no caso de possíveis falsos positivos.
* Os domínios específicos para os quais você deseja que essas regras sejam aplicadas.
* Se deseja que as regras sejam ativadas ou desativadas por padrão.

Após a criação das regras customizadas do WAF, deve-se ativar todas as regras customizadas para que entrem em vigor.
{:note}
