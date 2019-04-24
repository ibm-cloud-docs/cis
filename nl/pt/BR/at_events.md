---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM Cloud Internet Services, CIS Activity Tracker events

subcollection: cis

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Eventos {{site.data.keyword.cloudaccesstrailshort}} do CIS
{: #at_events}

Use o serviço {{site.data.keyword.cloudaccesstrailfull}} para controlar como os usuários e os aplicativos interagem com o IBM Cloud Internet Services (CIS) no {{site.data.keyword.cloud}}.
{:shortdesc}

O serviço {{site.data.keyword.cloudaccesstrailfull_notm}} registra as atividades iniciadas pelo usuário que mudam
o estado de um serviço no {{site.data.keyword.cloud_notm}}. Para obter mais informações, consulte [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla).




## Lista de eventos: domínios DNS
{: #events_dns_domain}

A tabela a seguir lista as ações relacionadas a domínios DNS e que geram um evento:

|Ação|Descrição|
|---|---|  
|internet-svcs.zones.create|Criar um domínio DNS.|
|internet-svcs.zones.update|Atualize um domínio DNS.|
|internet-svcs.zones.delete|Excluir um domínio DNS.|
|internet-svcs.zones.activation_check.update|Executar a verificação de ativação para um domínio DNS.|
|internet-svcs.zones.dnssec.update|Ativar ou desativar o DNSSEC para um domínio DNS.|

## Lista de eventos: Registros DNS
{: #events_dns_record}

A tabela a seguir lista as ações relacionadas a registros de DNS e que geram um evento:

|Ação|Descrição|
|---|---|  
|internet-svcs.zones.dns_records.create|Criar um registro de DNS.|
|internet-svcs.zones.dns_records.update|Atualizar um registro de DNS.|
|internet-svcs.zones.dns_records.delete|Excluir um registro de DNS.|
|internet-svcs.zones.dns_records_bulk.create|Importar registros de DNS do arquivo de zona.|


## Lista de eventos: balanceadores de carga
{: #events_load_balancers}

A tabela a seguir lista as ações relacionadas aos balanceadores de carga e que geram um evento:

|Ação|Descrição|
|---|---|  
|internet-svcs.zones.load_balancers.create|Criar um balanceador de carga global.|
|internet-svcs.zones.load_balancers.update|Atualizar um balanceador de carga global.|
|internet-svcs.zones.load_balancers.delete|Excluir um balanceador de carga global.|
|internet-svcs.load_balancers.monitors.create|Criar um monitor de funcionamento.|
|internet-svcs.load_balancers.monitors.update|Atualizar um monitor de funcionamento.|
|internet-svcs.load_balancers.monitors.delete|Excluir um monitor de funcionamento.|
|internet-svcs.load_balancers.pools.create|Criar um conjunto do balanceador de carga global.|
|internet-svcs.load_balancers.pools.update|Atualizar um conjunto do balanceador de carga global.|
|internet-svcs.load_balancers.pools.delete|Excluir um conjunto do balanceador de carga global.|


## Lista de eventos: limpando o cache
{: #events_cache}

A tabela a seguir lista as ações relacionadas à limpeza do cache e que geram um evento:

|Ação|Descrição|
|---|---|  
|internet-svcs.zones.purge_cache.purge_all.update|Limpar todos os ativos em cache de um domínio do servidor edge.|
|internet-svcs.zones.purge_cache.purge_by_urls.update|Limpar do servidor de borda os ativos em cache por URLs.|
|internet-svcs.zones.purge_cache.purge_by_cache_tags.update|Limpar do servidor de borda os ativos em cache por tags de cache.|
|internet-svcs.zones.purge_cache.purge_by_hosts.update|Limpar do servidor de borda os ativos em cache por nomes de host.|


## Lista de eventos: regras de página
{: #events_page_rules}

A tabela a seguir lista as ações relacionadas às regras de página e que geram um evento:

|Ação|Descrição|
|---|---|  
|internet-svcs.zones.pagerules.create|Criar uma regra de página.|
|internet-svcs.zones.pagerules.update|Atualizar uma regra de página.|
|internet-svcs.zones.pagerules.delete|Excluir uma regra de página.|


## Lista de eventos: firewalls
{: #events_firewalls}

A tabela a seguir lista as ações relacionadas a firewalls e que geram um evento:

|Ação|Descrição|
|---|---|  
|internet-svcs.zones.firewall.waf.packages.groups.update|Ativar ou desativar um grupo de conjuntos de regras do WAF.|
|internet-svcs.zones.firewall.waf.packages.rules.update|Ativar ou desativar uma regra do WAF.|
|internet-svcs.zones.firewall.access_rules.rules.create|Criar uma regra de firewall de IP de nível de domínio.|
|internet-svcs.zones.firewall.access_rules.rules.update|Atualizar a regra de firewall de IP de nível de domínio.|
|internet-svcs.zones.firewall.access_rules.rules.delete|Excluir regra de firewall IP de nível de domínio.|
|internet-svcs.firewall.access_rules.rules.create|Criar uma regra de firewall de IP de nível de instância.|
|internet-svcs.firewall.access_rules.rules.update|Atualizar a regra de firewall de IP de nível de instância.|
|internet-svcs.firewall.access_rules.rules.delete|Excluir a regra de firewall de IP de nível de instância.|
|internet-svcs.zones.rate_limits.create|Criar uma regra de limitação de taxa.|
|internet-svcs.zones.rate_limits.update|Atualizar a regra de limitação de taxa.|
|internet-svcs.zones.rate_limits.delete|Excluir a regra de limitação de taxa.|
|internet-svcs.zones.ua_rules.create|Criar uma regra de bloqueio do agente do usuário.|
|internet-svcs.zones.ua_rules.update|Atualizar a regra de bloqueio do agente do usuário.|
|internet-svcs.zones.ua_rules.delete|Excluir a regra de bloqueio do agente do usuário.|
|internet-svcs.zones.firewall.lockdowns.create|Criar uma regra de bloqueio de domínio.|
|internet-svcs.zones.firewall.lockdowns.update|Atualizar a regra de bloqueio de domínio.|
|internet-svcs.zones.firewall.lockdowns.delete|Excluir a regra de bloqueio de domínio.|

## Lista de eventos: roteamento
{: #events_routing}

A tabela a seguir lista as ações relacionadas ao roteamento e que geram um evento:

|Ação|Descrição|
|---|---|  
|internet-svcs.zones.routing.smart_routing.update	|Ativar ou desativar o roteamento inteligente.|
|internet-svcs.zones.routing.tiered_caching.update	|Ativar ou desativar o armazenamento em cache em camadas.|

## Lista de eventos: Pacotes de certificados
{: #events_certificate_packs}

A tabela a seguir lista as ações relacionadas a pacotes de certificado e que geram um evento:

|Ação|Descrição|
|---|---|  
|internet-svcs.zones.ssl.certificate_packs.create|Solicitar um certificado dedicado.|
|internet-svcs.zones.ssl.certificate_packs.delete|Excluir um certificado dedicado.|


## Lista de eventos: certificados customizados
{: #events_custom_certificate}

A tabela a seguir lista as ações relacionadas a certificados customizados e que geram um evento:

|Ação|Descrição|
|---|---|  
|internet-svcs.zones.custom_certificates.create|Fazer upload de um certificado customizado.|
|internet-svcs.zones.custom_certificates.update|Atualizar um certificado customizado.|
|internet-svcs.zones.custom_certificates.delete|Exclua um certificado customizado.|


## Lista de eventos: configurações
{: #events_settings}

A tabela a seguir lista as ações que estão relacionadas à configuração de configurações e gerar um evento:

|Ação|Descrição|
|---|---|  
|internet-svcs.zones.settings.cache_level.update|Mudar o nível do armazenamento em cache.|
|internet-svcs.zones.settings.browser_cache_ttl.update|Mudar o TTL do cache do navegador.|
|internet-svcs.zones.settings.development_mode.update|Ativar ou desativar o modo de desenvolvimento.|
|internet-svcs.zones.settings.security_level.update|Mudar o nível de segurança.|
|internet-svcs.zones.settings.ssl.update|Altere a configuração de SSL.|
|internet-svcs.zones.settings.tls_1_2_only.update|Ativar ou desativar o suporte do TLS 1.2.|
|internet-svcs.zones.settings.waf.update|Ativar ou desativar o firewall do aplicativo da web.|
|internet-svcs.zones.settings.cname_flattening.update|Mudar a configuração de compressão do CNAME.|
|internet-svcs.zones.settings.always_online.update|Ativar ou desativar o fornecimento do conteúdo antigo para o domínio.|
|internet-svcs.zones.settings.sort_query_string_for_cache.update|Ativar ou desativar a classificação de argumentos de consulta ao consultar o conteúdo em cache.|
|internet-svcs.zones.settings.tls_1_3.update|Mudar a configuração do TLS 1.3.|
|internet-svcs.zones.settings.automatic_https_rewrites.update|Ativar ou desativar regravações automáticas de HTTPS.
|internet-svcs.zones.settings.opportunistic_encryption.update|Ativar ou desativar a criptografia oportunista.|


## Onde procurar os eventos
{: #ui}

Os eventos do {{site.data.keyword.cloudaccesstrailshort}} estão disponíveis no **domínio de conta** do {{site.data.keyword.cloudaccesstrailshort}}, que está disponível na região do {{site.data.keyword.cloud_notm}} na qual os eventos são gerados.



## Informações adicionais
{: #info}

Quando estiver monitorando os eventos do {{site.data.keyword.cloudaccesstrailshort}} gerados pelo IBM Cloud Internet Services (CIS) e identificar uma solicitação de API para a qual precisa de informações adicionais, verifique o campo requestData no evento. Abra um chamado de suporte e inclua o valor do campo **X-CORRELATION-ID**, que está disponível em requestData.
