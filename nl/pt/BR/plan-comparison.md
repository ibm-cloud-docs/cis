---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Plan Comparison, Cloud Internet Services, Free Trial, enterprise

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Comparação de plano
{:#cis-plan-comparison}

O Cloud Internet Services oferece três planos para a escolha: Avaliação grátis, Standard e Enterprise. A tabela a seguir compara cada oferta para ajudar você a escolher a que é certa para você. Para saber mais sobre a oferta individual, clique em seu nome na tabela.

Role para a direita para visualizar o restante da tabela!


|         | Avaliação grátis | Standard | Pacote ou Uso Enterprise  
| ------- | :--------- | :------------ | :--------- | 
|**Horário**|Somente 30 Dias|Faturamento Mensal|Faturamento Mensal|
|**Domínio**|1|1|Até 1000, mas recomenda-se não exceder 20|
|**DNS**|3500 registros por Domínio| 3500 registros por Domínio| Diversos domínios e subdomínios|
|**GLB**|<ul><li>6 servidores de origem</li><li>Verificações de funcionamento de 60 segundos</li><li>Roteamento de Geo</li><li>Verificações de funcionamento de uma única região</li><li>TTL mínimo de 60s para GLBs sem proxy</li></ul>|<ul><li>6 servidores de origem</li><li>Verificações de funcionamento de 60 segundos</li><li>Roteamento de Geo</li><li>Verificações de funcionamento de uma única região</li><li>TTL mínimo de 60s para GLBs sem proxy</li></ul>|<ul><li>100 servidores de origem</li><li>Verificações de funcionamento de 5 segundos</li><li>Roteamento inteligente</li><li>Verificações de funcionamento de diversas regiões</li><li>TTL mínimo de 10s para GLBs sem proxy</li></ul>|
|**WAF**|Regras pré-configuradas|Regras pré-configuradas|Regras pré-configuradas e customizadas|
|**DDoS**|Ligado (com Proxy) ou Desligado (sem Proxy)|Ligado (com Proxy) ou Desligado (sem Proxy)|Ligado (com Proxy) ou Desligado (sem Proxy)|
|**TLS**|<ul><li>1 curinga Universal</li><li>1 curinga Dedicado</li><li>1 customização Dedicada</li><li>1 Customizado Upload</li></ul>|<ul><li>1 curinga Universal</li> <li>1 curinga Dedicado</li><li>1 customização Dedicada</li><li>1 Customizado Upload</li></ul>|<ul><li>1 curinga Universal por domínio. Até 10 certificados grátis por instância do CIS</li> <li>2 curingas Dedicados, com capacidade para mais solicitações</li><li>10 customizações Dedicadas</li><li>1 Customizado Upload</li></ul>
|**Regras de página**|50 Regras de página|50 Regras de página|<ul><li>100 Regras de página</li><li>Configurações adicionais para o controle de baixa granularidade</li></ul> |
|**Limitação de taxa**|Não|Não|Sim|
|**Firewall de IP**|<ul><li>Desafio</li><li>Bloquear (Indisponível para o filtro `Country`)</li><li>Desafio JS</li><li>Lista de desbloqueio</li></ul>|<ul><li>Desafio</li><li>Bloquear (Indisponível para o filtro `Country`)</li><li>Desafio JS</li><li>Lista de desbloqueio</li></ul>|<ul><li>Desafio</li><li>Bloquear</li><li>Desafio JS</li><li>Lista de desbloqueio</li></ul>|
|**Armazenamento em cache**|TTL mínimo de 30 minutos do cache do navegador|TTL mínimo de 30 minutos do cache do navegador|TTL mínimo de 30 segundos do cache do navegador|
|**Range**|Não|Não|Sim<br/>(com custo adicional por GB)|
|**Edge Functions (Beta)**|1 ação<br/>(deve ser nomeada após o domínio)|1 ação<br/>(deve ser nomeada após o domínio)|Ações ilimitadas|



