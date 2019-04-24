---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: domain Input information, IBM Cloud Internet Services, Global Load balancing

subcollection: cis

---


{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Melhorando a confiabilidade e a escalabilidade do aplicativo com o Balanceamento de Carga Global do IBM Cloud Internet Services
{:#improving-application-reliability-and-scalability-with-global-load-balancing-from-ibm-cloud-internet-services}

Se tem um website de e-commerce ou está hospedando um aplicativo que precisa ser acessível para seus usuários finais o tempo todo, provavelmente você está preocupado com a disponibilidade e o desempenho 24 x 7 de seu aplicativo. 

Os recursos de balanceamento de carga global disponíveis com o IBM Cloud Internet Services (CIS) podem ajudar você a melhorar a confiabilidade e a escalabilidade de seus aplicativos, ao mesmo tempo em que oferecem a melhor experiência de usuário final possível. Este guia fornece uma visão geral da configuração do balanceamento de carga global.  

## O que você realizará
{:#what-you-accomplish}

Neste passo a passo, você aprenderá como definir uma configuração semelhante à ilustrada abaixo.

<img src="images/reliability1.png" alt="desenho" style="width: 300px;"/>

Nesse exemplo, os recursos do aplicativo são implementados em dois locais de data center, um no Oeste dos EUA e o outro na Costa Leste dos EUA. Os usuários finais podem acessar esse aplicativo de todo o mundo. 

Tarefa  | Descrição
------------- | -------------
[Criar uma instância do CIS](/docs/infrastructure/cis?topic=cis-create-your-ibm-cloud-internet-services-cis-instance) | Comece criando sua instância do IBM Cloud Internet Services (CIS) usando o portal do cliente IBM.|
[Inserir informações sobre seu domínio](/docs/infrastructure/cis?topic=cis-input-information-about-your-domain) | Insira informações sobre o domínio que deseja proteger e para o qual deseja fornecer o balanceamento de carga global.
[Iniciar a configuração do balanceador de carga global](/docs/infrastructure/cis?topic=cis-begin-global-load-balancer-configuration) | Inicie a configuração de seu balanceador de carga global.
[Identificar os recursos de seu aplicativo](/docs/infrastructure/cis?topic=cis-identify-your-application-resources) | Identifique os recursos de seu aplicativo, como conjuntos de origem e mecanismos de verificação de funcionamento.
[Definir o balanceador de carga global](/docs/infrastructure/cis?topic=cis-define-the-global-load-balancer) | Defina a configuração de seu balanceador de carga global especificando um nome de host, incluindo e ajustando seus conjuntos de origem e definindo regras adicionais para controlar como o tráfego é entregue aos clientes.
