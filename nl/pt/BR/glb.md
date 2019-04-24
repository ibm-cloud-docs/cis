---

copyright:
  years: 2018
lastupdated: "2018-03-05"

---

# Conceitos do Balanceador de carga global (GLB)

Este documento contém alguns conceitos e definições relacionados ao Balanceador de Carga Global (GLB) e como ele afeta sua implementação do IBM CIS.

## Balanceador de carga global

O Balanceador de carga global (GLB) gerencia o tráfego entre recursos do servidor localizados em múltiplas regiões. O GLB utiliza um conjunto que permite que o tráfego seja distribuído para várias origens. Isso fornece muitos benefícios, incluindo:

  * Minimiza o tempo de resposta
  * Aumenta a disponibilidade por meio de redundância
  * Maximiza o rendimento do tráfego

## Conjunto

Um conjunto é um grupo de servidores de origem para os quais o tráfego é roteado de forma inteligente quando conectado a um GLB. O número mínimo de servidores de origem disponíveis para que o conjunto seja marcado como operante é configurável pelo usuário junto com qual verificação de funcionamento específica usar. O conjunto de origem pode ser associado a uma região específica ou pode ser disponibilizado para todas as regiões.

## Verificação de funcionamento

Uma verificação de funcionamento ajuda a ganhar insight sobre a disponibilidade de conjuntos para que o tráfego possa ser roteado para os operantes. Essas verificações enviam periodicamente solicitações HTTP/HTTPS e monitoram as respostas. Elas podem ser configuradas com intervalos customizados, tempos limites, códigos de status, e mais. Assim que um conjunto for marcado como inoperante, o tráfego será roteado novamente de forma inteligente para outro conjunto disponível, se disponível.
