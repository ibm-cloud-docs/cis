---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Glossary, load balancer, pool, health check

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Glossário
{:#glossary}

Esse glossário contém definições para termos comuns que podem ser encontrados ao trabalhar com o balanceador de carga global (GLB).

## Balanceador de carga
{:#glossary-load-balancer}

Um balanceador de carga é um dispositivo que age como um proxy reverso e distribui o tráfego de rede ou de aplicativo por diversos servidores. Os balanceadores de carga são usados para aumentar a capacidade do sistema (o número de usuários simultâneos) e melhorar a confiabilidade dos aplicativos.

## Conjunto
{:#glossary-pool}

Um conjunto é um grupo de servidores de origem para os quais o tráfego é roteado de forma inteligente quando conectado a um GLB. O número mínimo de servidores de origem disponíveis para que o conjunto seja marcado como operante é configurável pelo usuário junto com qual verificação de funcionamento específica usar. O conjunto de origem pode ser associado a uma região específica ou pode ser disponibilizado para todas as regiões.

## Verificação de funcionamento
{:#glossary-health-check}

Uma verificação de funcionamento ajuda a ganhar insight sobre a disponibilidade de conjuntos para que o tráfego possa ser roteado para os operantes. Essas verificações enviam periodicamente solicitações HTTP/HTTPS e monitoram as respostas. Elas podem ser configuradas com intervalos customizados, tempos limites, códigos de status, e mais. Assim que um conjunto for marcado como inoperante, o tráfego será roteado novamente de forma inteligente para outro conjunto disponível, se disponível.

## Servidores de origem
{:#glossary-origin-servers}

Um servidor de origem processa e responde a solicitações recebidas de clientes e é geralmente usado com servidores de armazenamento em cache. Os servidores de origem executam um ou mais programas projetados para atender e processar solicitações da Internet recebidas. A distância física entre o servidor de origem e o cliente fazendo uma solicitação inclui a latência para a conexão, aumentando o tempo de carregamento. O uso de servidores de armazenamento em cache reduz essa latência.


