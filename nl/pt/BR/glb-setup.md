---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: health checks, origin pools, load balancers, IBM CIS

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# Configure seus balanceadores de carga
{:#set-up-and-configure-your-load-balancers}
 
 O IBM CIS fornece balanceamento de carga global como um serviço. Confira a aparência do Painel do GLB:

![IMAGEM](images/glb-screen.png)

## Painel GLB
{:#glb-dashboard}

Em seu painel, você verá três listas que mostram os balanceadores de carga, os conjuntos de origem e as verificações de funcionamento. As listas exibem o balanceador de carga global novo ou atualizado ou um de seus componentes após você tê-lo provisionado ou atualizado. Inicialmente, as listas estão vazias e, antes de criar um balanceador de carga, deve-se realizar algumas ações.

Consulte o [Guia de iniciação rápida](/docs/infrastructure/cis?topic=cis-global-load-balancer-quick-setup) se já souber o que precisa fazer!

### Criar
{:#create-health-check}

<sup>`*`</sup> indica que essa etapa é opcional.
{:note}

1) <sup>`*`</sup>Para criar uma verificação de funcionamento, clique em **Criar verificação de funcionamento**.
  ![IMAGE](images/glb-health-check-list.png)
    <ul>
      <li><b>Caminho</b>: o caminho do terminal com relação ao qual verificar o funcionamento.</li> 
      <li><b>Tipo</b>: o protocolo a ser usado para a verificação de funcionamento.</li>
      <li><b>Descrição</b>: descrição fornecida pelo usuário.</li>
    </ul>

2) Para criar um conjunto, clique em **Criar conjunto**.
  ![IMAGE](images/glb-pool-list.png)
    <ul>
      <li><b>Funcionamento</b>: status do conjunto.</li>
      <li><b>Nome</b>: nome fornecido pelo usuário.</li>
      <li><b>Origens</b>: contagem de origens operantes no conjunto.</li>
      <li><b>Verificação de funcionamento</b>: caminho da verificação de funcionamento anexada, se houver.</li>
    </ul>

3) Para criar um balanceador de carga, clique em **Criar balanceador de carga**.
  ![IMAGE](images/glb-load-balancer-list.png)
    <ul>
      <li><b>Funcionamento</b>: status do balanceador de carga.</li>
      <li><b>Nome do host</b>: nome anexado ao nome de domínio.</li>
      <li><b>Conjuntos disponíveis</b>: contagem de conjuntos operantes.</li>
      <li><b>TTL</b>: tempo de vida.</li>
      <li><b>Proxy</b>: ativar ou desativar o fluxo de tráfego do proxy.</li>
      <li><b>Status</b>: ativar ou desativar o balanceador de carga.</li>
    </ul>

As regiões geográficas da IBM são diferentes das regiões do Cloudflare. Para obter detalhes sobre as regiões geográficas que a Cloudflare usa, consulte [Balanceamento de carga: regiões geográficas ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://support.cloudflare.com/hc/en-us/articles/115000540888-Load-Balancing-Geographic-Regions){:new_window}.  
{:note}

### Editar/Excluir
{:#edit-delete-load-balancer}
Para editar ou excluir um balanceador de carga ou um de seus componentes, clique no botão do menu overflow localizado na extrema direita de cada linha.

Botão do menu overflow:

![IMAGEM](images/overflow.png)

As opções a seguir são fornecidas para cada lista.

* Verificação de funcionamento
    * **Visualizar verificação de funcionamento**: essa opção mostra um breve resumo da verificação de funcionamento, com um link que o direciona ao fluxo de edição.
    * **Editar verificação de funcionamento**: essa opção redireciona o usuário para o fluxo de edição. 
    * **Excluir verificação de funcionamento**: essa opção abre a caixa de diálogo de confirmação para o fluxo de exclusão.

* Conjunto
    * **Visualizar detalhes do conjunto**: essa opção abre uma caixa de diálogo modal com informações sobre o conjunto.
    * **Editar conjunto**: essa opção redireciona o usuário para o fluxo de edição.
    * **Excluir conjunto**: essa opção abre a caixa de diálogo de confirmação para o fluxo de exclusão.

* Balanceador de carga
    * **Desativar/Ativar**: ative ou desative um balanceador de carga.
    * **Editar balanceador de carga**: redireciona para o fluxo de edição. 
    * **Excluir balanceador de carga**: exibe a caixa de diálogo de confirmação para o fluxo de exclusão.

## Inclua uma verificação de funcionamento
{:#add-a-health-check}

As verificações de funcionamento são anexos opcionais para conjuntos de origem. Elas usam um intervalo de repetição customizado para análise de um corpo de resposta específico, ou para um código de status, para monitorar o funcionamento do conjunto. Uma vez criadas, as verificações de funcionamento poderão ser incluídas em um conjunto de origem novo ou existente.

Ao criar uma verificação de funcionamento, apenas um campo é necessário:
 * **Código de resposta**: o código de resposta HTTP ou o intervalo de códigos da verificação de funcionamento esperado. Esse valor deve ser entre 200 e 299 com curingas denotados por um 'x'.

Campos opcionais adicionais:
 * **Caminho**: o caminho do terminal com relação ao qual executar a verificação de funcionamento (padrão é /).
 * **Tipo**: o protocolo a ser usado para a verificação de funcionamento (padronizado como HTTP).
 * **Descrição**: descrição da verificação de funcionamento.
 * **Intervalo**: o intervalo (em segundos) entre cada verificação de funcionamento. Intervalos mais curtos podem melhorar o tempo de failover, mas aumentam a carga nas origens, pois as verificações vêm de vários locais (padronizado como 60).
 * **Método**: o método de HTTP a ser usado para a verificação de funcionamento (padronizado como GET).
 * **Tempo limite**: o tempo (em segundos) antes de marcar a verificação de funcionamento como com falha (padronizado como 5).
 * **Novas tentativas**: o número de novas tentativas no caso de um tempo limite antes de marcar a origem como inoperante. As novas tentativas são tentadas imediatamente (padronizado como 2).
 * **Corpo de resposta**: uma subsequência sem distinção entre maiúsculas e minúsculas para correspondência no corpo de resposta. Se essa cadeia não for localizada, a origem será marcada como inoperante.
 * **Cabeçalhos da solicitação**: os cabeçalhos da solicitação de HTTP a serem enviados na verificação de funcionamento. É recomendado que você configure um cabeçalho do Host por padrão. O cabeçalho `User-Agent` não pode ser substituído.

## Inclua um conjunto
{:#add-a-pool}

Pelo menos um conjunto é necessário para cada balanceador de carga provisionado. Os conjuntos agrupam suas origens para o balanceador de carga usar.

Ao criar um conjunto, dois campos são necessários:
 * **Nome**: um nome abreviado (tag) para o conjunto. Apenas caracteres alfanuméricos, hifens e sublinhados são permitidos.
 * **Origens**: a lista de origens dentro desse conjunto. O tráfego direcionado nesse conjunto é balanceado em todas as origens atualmente operantes, desde que o conjunto em si esteja operante.

Campos opcionais adicionais:
 * **Descrição**: uma descrição legível do conjunto.
 * **Ativado**: se é necessário ativar (o padrão) esse conjunto. Conjuntos desativados não recebem tráfego e são excluídos de verificações de funcionamento. A desativação de um conjunto faz com que quaisquer balanceadores de carga que o utilizem efetuem failover para o próximo conjunto, se houver (padronizado como true).
 * **Limite de origens operantes**: o número mínimo de origens que devem estar operantes para esse conjunto servir o tráfego. Se o número de origens operantes ficar abaixo desse número, o conjunto será marcado como inoperante e efetuará failover para o próximo conjunto disponível. (padronizado como 1)
 * **Regiões de verificação de funcionamento**: região da qual a verificação de funcionamento executará o monitoramento. **Nota**: as regiões geográficas da IBM são diferentes das regiões da Cloudflare. Para obter detalhes sobre as regiões geográficas que a Cloudflare usa, consulte [Balanceamento de carga: regiões geográficas ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://support.cloudflare.com/hc/en-us/articles/115000540888-Load-Balancing-Geographic-Regions){:new_window}. 
 * **Verificação de funcionamento**: a verificação de funcionamento a ser usada para verificar as origens dentro desse conjunto. (padronizado como sem verificação de funcionamento)
 * **E-mail de notificação**: o endereço de e-mail que deve receber notificações de status de funcionamento. Esse endereço pode ser uma caixa de correio individual ou uma lista de distribuição.

## Inclua um balanceador de carga
{:#add-a-load-balancer}

Balanceadores de carga ajudam a distribuir seu tráfego em proxy entre vários conjuntos de origem usando uma distribuição round-robin.

Ao criar um balanceador de carga, os campos obrigatórios são:
 * **Nome**: o nome do host DNS para associar ao seu Load Balancer. Se esse nome do host já existir como um registro de DNS no DNS da IBM, o Load Balancer terá precedência e o registro de DNS não será usado.
 * **Conjuntos padrão**: uma lista de IDs do conjunto. A lista é ordenada pela prioridade do failover. Conjuntos definidos aqui são usados por padrão ou quando conjuntos de regiões não estão configurados para uma determinada região.

Opcionalmente, os campos a seguir podem ser configurados:
 * **Proxy**: rotear o tráfego por meio do serviço de desempenho e métricas da IBM.
 * **Afinidade de sessão**: sempre rotear por meio da mesma instância de desempenho e métricas. Essa opção está disponível somente se o proxy está ativado.
 * **TTL**: tempo de vida (TTL) da entrada DNS para o endereço IP retornado por esse balanceador de carga. Essa opção se aplica apenas aos balanceadores de carga sem proxy, caso contrário, ela é padronizada como `Automatic`.
 * **Conjuntos de regiões**: um mapeamento de códigos de região ou país para uma lista de conjuntos (ordenados por sua prioridade de failover) para a região especificada. Todas as regiões não definidas explicitamente efetuarão fallback para usar os conjuntos padrão. **Nota**: as regiões geográficas da IBM são diferentes das regiões da Cloudflare. Para obter detalhes sobre as regiões geográficas que a Cloudflare usa, consulte [Balanceamento de carga: regiões geográficas ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://support.cloudflare.com/hc/en-us/articles/115000540888-Load-Balancing-Geographic-Regions){:new_window}. 
 
Para obter definições de termos utilizados neste documento, que geralmente são termos comuns usados em todo o segmento de mercado, consulte o [Glossário](/docs/infrastructure/cis?topic=cis-glossary).
