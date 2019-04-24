---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: origin server, pool implementation, origin servers

subcollection: cis

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"} 
{:note: .note}

# Conceitos do Balanceador de carga global (GLB)
{:#global-load-balancer-glb-concepts}

Este documento contém alguns conceitos e definições relacionados ao Global Load Balancer (GLB) e como ele afeta sua implementação do IBM CIS.

## Balanceador de carga global
{:#global-load-balancer-cis}

O Balanceador de carga global (GLB) gerencia o tráfego entre recursos do servidor localizados em múltiplas regiões. O servidor de origem pode fornecer todo o conteúdo para um website, desde que o tráfego da web não se estenda além dos recursos de processamento do servidor e a latência não seja uma preocupação primária. O GLB utiliza uma implementação de _conjunto_ que permite que o tráfego seja distribuído para diversas origens. Esse recurso de conjunto fornece muitos benefícios, incluindo:

  * Minimiza o tempo de resposta
  * Cria maior disponibilidade por meio da redundância
  * Maximiza o rendimento do tráfego

O GLB roteia o tráfego para o conjunto com a maior prioridade, distribuindo a carga entre seus servidores de origem. Consulte a seção _Conjunto_ a seguir para saber como o tráfego é distribuído em um conjunto. Se o conjunto primário se tornar indisponível, o tráfego será roteado automaticamente para o próximo conjunto na lista com base na prioridade.

Se os conjuntos estiverem configurados para regiões específicas, o tráfego dessas regiões será enviado primeiro para os conjuntos da região especificada. O tráfego será enviado de volta aos conjuntos padrão somente se todos os conjuntos para uma determinada região estiverem inativos. Nesse caso, o conjunto de fallback é o conjunto com a menor prioridade. 

### Como funciona
{:#how-glb-works}
Quando o GLB é criado, um registro de DNS é incluído automaticamente para ele com o nome do balanceador de carga. Em seguida, o GLB retorna um dos endereços IP de origem para um cliente que faz uma solicitação de DNS.

Por exemplo, um conjunto de origem é criado com duas origens que identificam os endereços IP `169.61.244.18` e `169.61.244.19`. Se um balanceador de carga global for criado com o nome `glbcust.ibmmo.com` usando o conjunto de origem, então um cliente na Internet poderá executar o comando:
```
$ ping glbcust.ibmom.com
PING glbcust.ibmom.com (169.61.244.18): 56 data bytes
```
Nesse exemplo, o CIS:

    * criou um registro de DNS chamado `glbcust.ibmmo.com`
    * usou o GLB para resolver o nome do DNS para um dos endereços IP identificados no conjunto de origem

Observe que o balanceador de carga global não finaliza a conexão TCP.
{:note}

A configuração de um elemento do DNS ou do GLB para "proxy" muda o comportamento.
Se, por exemplo, você ativar o proxy e **Segurança > TLS > Modo** para algo diferente de `Desativado`, o CIS encerrará a conexão TCP e estabelecerá uma segunda conexão entre o CIS e o originador.

Nesse exemplo, o CIS:

    * criou um registro DNS denominado: `glbcust.ibmmo.com`
    * usou o GLB para resolver o nome do DNS para um endereço IP fornecido pelo CIS
    
Agora, as conexões com `glbcust.ibmmo.com` serão finalizadas pelo CIS e os certificados HTTPS serão hospedados por ele (necessário para o encerramento do TCP).

Após a conexão do cliente com o aplicativo, a figura será semelhante a essa:

`[client]<--tls-->[cis]<-->[origin server]`

## Conjunto
{:#glb-pools}

Um conjunto é um grupo de servidores de origem para os quais o tráfego é roteado de forma inteligente quando conectado a um GLB. O número mínimo de servidores de origem disponíveis para que o conjunto seja marcado como operante é configurável pelo usuário junto com qual verificação de funcionamento específica usar. O conjunto de origem pode ser associado a uma região específica ou pode ser disponibilizado para todas as regiões.

### Distribuição de tráfego dentro de um conjunto
{:#distribution-of-traffic-within-a-pool}

Por padrão, todo o tráfego é distribuído uniformemente entre as origens no conjunto com o uso do protocolo round-robin. O mesmo ocorre para GLBs sem proxy.

As origens podem ser configuradas com pesos e, para GLBs com proxy, os pesos determinam a quantidade de tráfego que cada servidor de origem recebe com relação a outras origens no conjunto. Os pesos são configurados como números entre 0 e 1 e especificam qual parte do tráfego irá para a origem. 

Para cada origem: 

` Percentual de tráfego para a origem = peso da origem/soma de todos os pesos das origens`

Se todas as origens tiverem peso `1`, o tráfego será distribuído uniformemente. 

Origens com peso `0` não recebem nenhum tráfego para esse conjunto. No entanto, a afinidade de sessão ainda pode fazer essa substituição até que todas as sessões sejam encerradas. Se a origem for um membro em outro conjunto, ainda poderá receber o tráfego para esse conjunto.

**Exemplo:** 

Um conjunto de origem está configurado com 3 origens que possuem os pesos a seguir: origem-A: 0,4, origem-B: 0,3 e origem-C: 0,3. 

* Inicialmente, todas as origens estão funcionando. A quantidade de tráfego que cada origem recebe é: origin-A: 40%, origin-B: 30%, e origina-C: 30%.
* Em seguida, origina-se crítico; ele não recebe mais tráfego. As origens restantes têm o mesmo peso e, portanto, o tráfego é distribuído uniformemente, cada um recebendo 50%.
* O administrador muda o peso da origem-C para `0`. Agora, 100% do novo tráfego será encaminhado para a origem-B. Mas, com a afinidade de sessão ativada, o tráfego para as sessões existentes na origem-C continua sendo encaminhado para ela, até que essas sessões sejam encerradas (máximo de 24 horas).

### Conjunto de fallback
{:#fallback-pool}

O conjunto de origem com a menor prioridade (o maior número) é o "conjunto de fallback" designado. Quando todos os conjuntos para uma determinada região estiverem inativos, o tráfego será roteado para esse conjunto, independentemente de seu funcionamento.

Quando todos os conjuntos estiverem desativados, o conjunto de fallback não estará disponível.
{:note}

## Verificação de funcionamento
{:#cis-health-check}

Uma verificação de funcionamento ajuda a ganhar insight sobre a disponibilidade de conjuntos para que o tráfego possa ser roteado para os operantes. Essas verificações enviam periodicamente solicitações de HTTP, HTTPS ou TCP e monitoram as respostas. Elas podem ser configuradas com customização de porta, intervalo, tempo limite, código de status e muito mais. Assim que um conjunto é marcado como não funcional, o tráfego é roteado inteligentemente para outro conjunto disponível.  Esteja ciente de que seus logs têm referências à Cloudflare por causa da parceria da IBM com a Cloudflare para desenvolver o CIS.
{:note}

### Eventos de verificação de funcionamento
{:#health-check-events}

Os Eventos de verificação de funcionamento são mudanças de status de conjuntos com verificações de funcionamento conectadas e seus servidores de origem associados. Se um status de origem estiver comprometido, um novo item aparecerá em uma tabela com a descrição do evento. Navegue até **Confiabilidade > Balanceador de carga global > Eventos de verificação de funcionamento** para ver uma tabela de Eventos de verificação de funcionamento. É possível filtrar por data, funcionamento do conjunto ou da origem, nome do conjunto e nome da origem, selecionando os parâmetros de filtro nos menus suspensos. Colunas dentro da tabela são classificáveis clicando no nome da coluna.
![Health Check Events table](images/health-check-events-table.png)

Linhas individuais dentro da tabela se expandem com mais informações sobre a entrada. Se o conjunto estiver funcionando, somente o tile **Detalhes do conjunto** ficará visível. Quando a linha tiver uma origem crítica ou um conjunto comprometido, o tile **Detalhes da origem afetada** também aparecerá. 

![Detalhes de eventos de verificação de funcionamento](images/health-check-events-details.png)

#### Detalhes do conjunto:
* Nome do conjunto - Nome do conjunto
* Origens funcionais - Razão de origens funcionais/total de origens em um conjunto
* Limite funcional - Número de origens funcionais necessárias para considerar o conjunto funcional
* Origens Saudáveis-Nomes das Origens de Saúde
* Origens criticais - Nomes das origens não funcionais

#### Detalhes da origem afetada:
* Nome da origem - Nome da origem
* Endereço da origem - Endereço da origem
