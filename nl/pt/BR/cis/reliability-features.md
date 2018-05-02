---
copyright:
  years: 2018
lastupdated: "2018-03-06"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Como o IBM Cloud Internet Services (CIS) mantém seu serviço confiável

O IBM Cloud Internet Services (CIS) ajuda você a melhorar a confiabilidade de seus serviços e aplicativos da web, porque ele ajuda a evitar o tempo de inatividade causado por interrupções de aplicativos e infraestrutura. Por exemplo, com o Balanceamento de Carga Global, é possível implementar seus serviços e aplicativos da web em múltiplas regiões. O IBM CIS roteia suas solicitações de clientes para as regiões mais próximas disponíveis quando o Balanceamento de Carga Global está ativado. Se alguma região falhar, as solicitações serão roteadas para o local mais próximo seguinte, para que seus clientes não sejam afetados pelo tempo de inatividade. Se seu website ou API falhar, o IBM CIS enviará notificações para você automaticamente e o notificará quando eles forem restaurados.


![reliability-graphic.png](images/reliability-graphic.png)

Aqui está uma visão geral rápida de recurso:

## Recursos de confiabilidade

 * Balanceamento de carga global 
 * Opções proxy e não proxy para balanceamento de carga
 * Conjuntos de origem e monitores de funcionamento
 * Gerenciamento de DNS
 
### Resumo
 
  * Os monitores de funcionamento verificam se seus conjuntos de origem estão operantes.
  * No caso de falha do monitor de funcionamento, as solicitações são roteadas novamente para origens operantes.
  * Você fica informado quando seu serviço da web ou API falha e quando eles são restaurados.
