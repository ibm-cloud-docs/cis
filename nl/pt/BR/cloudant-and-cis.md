---

copyright:
  years: 2019
lastupdated: "2019-03-28"

keywords: Cloudant database, CORS, cross-origin resource sharing, host header

subcollection: cis

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"} 
{:note: .note}


# Acesse seu banco de dados Cloudant por meio do IBM Cloud Internet Services
{: #access-cloudant-through-cis}

Siga estas etapas para acessar o Cloudant Database por meio do IBM Cloud Internet Services (CIS).

## Antes de começar
{: #access-cloudant-through-cis-begin}

Essas instruções presumem que você já tenha incluído um domínio no CIS, conforme descrito na página [Introdução](/docs/infrastructure/cis?topic=cis-getting-started-with-ibm-cloud-internet-services-cis-).

### Etapa 1: inclua seu domínio do CIS no Compartilhamento de Recurso de Origem Cruzada (CORS)
{: #access-cloudant-through-cis-step1}

* Navegue até o banco de dados Cloudant e abra a página `Conta` -> `CORS`.
* Inclua seu domínio do CIS no campo de entrada de domínios de origem. Por exemplo, `https://cloudant.test.foo.com`.

### Etapa 2. Configure o CIS para apontar para o seu banco de dados Cloudant
{: #access-cloudant-through-cis-step2}

* Navegue até o painel do CIS e crie um balanceador de carga ou um registro de DNS que aponte para o nome de host do seu banco de dados Cloudant. Por exemplo, `https://cloudant.test.foo.com` -> `111-222-333-444-555-test.cloudant.com`.
* Ative o `proxy` para o registro de DNS ou balanceador de carga.


### Etapa 3. Crie uma regra de página para configurar a Substituição do cabeçalho do host
{: #access-cloudant-through-cis-step3}

* No painel do CIS, navegue até `Desempenho` -> `Regras de página`.
* Crie uma regra de página para a URL desejada, por exemplo, `https://cloudant.test.foo.com/*`.
* Selecione a configuração Comportamento de Regra `Substituição do cabeçalho do host`.
* Configure como o nome do host do banco de dados Cloudant, por exemplo, `111-222-333-444-555-test.cloudant.com`.

Para obter mais informações sobre o Cloudant, consulte a [Documentação do Cloudant](/docs/services/Cloudant?topic=cloudant-getting-started-with-cloudant).
