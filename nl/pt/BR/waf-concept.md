---
copyright:
  years: 2018
lastupdated: "2018-03-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# P e R de conceitos de firewall do aplicativo da web

O firewall do aplicativo da web protege contra ataques ISO Camada 7, que podem ser um dos mais complicados. Este documento fornece alguns detalhes.

## O que é um Web Application Firewall (WAF)?
Um WAF ou Web Application Firewall ajuda a proteger aplicativos da web filtrando e monitorando o tráfego HTTP entre um aplicativo da web e a Internet. Um WAF é uma defesa da camada 7 do protocolo ISO (no [modelo do OSI ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://en.wikipedia.org/wiki/OSI_model)), ele não foi projetado para defender contra todos os tipos de ataques. 

Implementar um WAF na frente de um aplicativo da web é como colocar um escudo entre o aplicativo da web e a Internet. Um servidor proxy protege a identidade da máquina do cliente usando um intermediário (para o tráfego de saída), mas um WAF é um tipo de proxy reverso que protege o servidor contra exposição, uma vez que o tráfego do cliente precisa passar pelo WAF antes de atingir o servidor (para o tráfego de entrada).

## Quais tipos de ataques um WAF pode evitar?
Um WAF geralmente protege aplicativos da web contra ataques como falsificação de site cruzado, cross-site scripting (XSS), inclusão de arquivo e injeção de SQL, entre outros. Um WAF geralmente é parte de um conjunto de ferramentas, que juntas podem criar uma defesa holística contra uma variedade de vetores de ataque.

## Como um WAF funciona?

Um WAF opera por meio de um conjunto de regras frequentemente chamadas de políticas. Essas políticas visam a proteger contra vulnerabilidades no aplicativo filtrando o tráfego malicioso. 

O valor de um WAF provém da velocidade e facilidade com que suas modificações de política podem ser implementadas, permitindo, assim, uma resposta mais rápida para diversos vetores de ataque. Por exemplo, durante um [ataque DDoS ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://en.wikipedia.org/wiki/Denial-of-service_attack), a limitação de taxa pode ser implementada modificando políticas do WAF.
