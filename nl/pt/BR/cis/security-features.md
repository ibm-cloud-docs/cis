---
copyright:
  years: 2018
lastupdated: "2018-03-16"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Como o IBM Cloud Internet Services (CIS) mantém seu trabalho seguro

O IBM CIS é um serviço de nuvem distribuído globalmente que bloqueia ameaças e limita robôs e crawlers abusivos, os quais podem desperdiçar seus recursos de largura da banda e servidor. O IBM CIS funciona como um proxy reverso HTTP(S) global e um provedor de serviços DNS gerenciado. Seu tráfego da web é roteado por meio de nossa rede global inteligente para otimizar seu desempenho e sua segurança.

![security-graphic.png](images/security-graphic.png)

Aqui está uma visão geral rápida de recurso:

## Recursos de segurança

 * Web Application Firewall (WAF)
 * Mitigação de DDoS ilimitada

## Padrões de segurança e plataforma

 * TLS (SHA2 e SHA1)
 * IPv6
 * HTTP/2 e SPDY

## DNS

 * Rede anycast Global
 * DNSSEC

## Ataques de rede e mitigação

Geralmente, vemos ataques que se enquadram em duas categorias

| Ataques de Camada 3 ou Camada 4 | Ataques de Camada 7 |
|------------------------------|-----------------|
|Esses ataques consistem em um fluxo de tráfego em ISO Camada 3 (a camada de rede), tais como sobrecargas de ICMP, ou em Camada 4 (a camada de transporte), tais como sobrecargas de TCP SYN ou sobrecargas de UDP refletidas |Esses são ataques que enviam solicitações ISO Camada 7 maliciosas (a camada de aplicativo), tais como sobrecargas GET. |
| Automaticamente bloqueado em nossa borda | Nós manipulamos isso com “Modo de Defesa”, WAF e Configurações de nível de segurança |

## Resumo

 * O Modo de Defesa testa recursos do navegador que muitos clientes maliciosos não têm
 * O WAF bloqueia ou desafia padrões de solicitação conhecidos que provavelmente são maliciosos
