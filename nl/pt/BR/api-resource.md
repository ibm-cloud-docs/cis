---

copyright:
  years: 2018
lastupdated: "2018-03-22"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Especificações da API

A seguir há instruções sobre como visualizar as especificações de API do CIS: 

1. Para visualizar APIs do CIS, navegue para a página [Especificação de API do CIS](https://console.bluemix.net/apidocs/2640-cloud-internet-services). 

2. No menu de navegação à esquerda, escolha na lista de APIs disponíveis.


## Notas

1. Terminal de API: https://api.cis.cloud.ibm.com.

2. O cabeçalho **X-Auth-User-Token** é necessário para cada chamada API. Esse é o token de acesso para o usuário que pode ser recuperado do IAM (por exemplo, usando o comando "bx iam oauth-tokens").

3. O campo **crn** também é necessário no caminho para cada chamada API. Esse é o Nome do Recurso em Nuvem (CRN) completo para uma instância de recurso do CIS que está sendo configurada (por exemplo, o CRN para uma instância de recurso pode ser recuperado por meio de seu nome usando o comando "bx resource service-instance <instance-name>"). O CRN deve ser a URL codificada na chamada API.

4. As chamadas API são limitadas por taxa. No total, 100 chamadas API podem ser feitas em 1 minuto. Se essa taxa for excedida, as chamadas subsequentes serão bloqueadas por um período.
