---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: API Specs, CIS APIs

subcollection: cis

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Especificações da API
{:#api-specs}

A seguir há instruções sobre como visualizar as especificações de API do CIS: 

1. Para visualizar as APIs do CIS, navegue até a página [Documentos de APIs](/apidocs/). 

2. No menu de navegação à esquerda, marque a caixa Rede para filtrar as APIs.

3. Escolha dentre a lista de APIs disponíveis do Cloud Internet Services.


## Notas
{:#api-notes}

1. Terminal de API: `https://api.cis.cloud.ibm.com`.

2. O cabeçalho **X-Auth-User-Token** é necessário para cada chamada de API. Esse cabeçalho é o token de acesso para o usuário, que pode ser recuperado por meio do IAM (por exemplo, usando o comando `ibmcloud iam oauth-tokens`).

3. O campo **crn** também é necessário no caminho para cada chamada API. Esse campo contém o Cloud Resource Name (CRN) completo para uma instância de recurso do CIS que está sendo configurada (por exemplo, o CRN para uma instância de recurso pode ser recuperado por meio de seu nome, com o uso do comando `ibmcloud resource service-instance<instance-name>`). O CRN deve ser a URL codificada na chamada API.

4. As chamadas API são limitadas por taxa. No total, 100 chamadas API podem ser feitas em 1 minuto. Se essa taxa for excedida, chamadas subsequentes serão bloqueadas por um período de tempo.
