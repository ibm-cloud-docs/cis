---
copyright:
  years: 2018
lastupdated: "2018-03-17"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Gerencie sua implementação do IBM Cloud Internet Services (CIS)

Você começará usando a tela Visão geral como sua base de operações de serviço. Ela mostra todos os parâmetros atuais para sua implementação.

Após configurar o DNS, você estará pronto para começar!

## Usando a tela Visão geral

Usando a tela Visão geral, é possível ver o status de todas as suas seleções. É possível mudar as configurações diretamente na tela Visão geral, basta clicar no nome sublinhado da configuração que você gostaria de mudar, por exemplo, seria possível clicar no campo `Balanceadores de carga` para incluir um Balanceador de Carga.

Na tela Visão geral, é possível ver que sua configuração de nome de domínio está no status **Pendente** ou no status **Ativo**, conforme mostrado na figura a seguir.

![imagem de tela de visão geral](images/overview-screen-configuration-summary.png)


## Configurando e gerenciando o DNS

Acesse sua página DNS e inclua um registro (mais provavelmente um registro A). Digite as informações sobre seu registro de DNS e, em seguida, clique em `Incluir registro` para implementar suas mudanças.

![add-DNS](images/dns/create-a-type-record.png)

## Configure e gerencie seu armazenamento em cache

Em seguida, é possível configurar o armazenamento em cache. 

![IMAGEM](images/caching-screen.png)

Você tem a opção de 3 tipos de armazenamento em cache, disponíveis no menu suspenso da tela de armazenamento em cache: 

 * Nenhuma sequência de consultas: fornece recursos do cache apenas quando não há nenhuma sequência de consultas.
 * Independente da sequência de consultas: fornece o mesmo recurso para todos, independentemente da sequência de consultas. (Nota: a configuração **Ignorar sequência de consultas** se aplica apenas a extensões de arquivo estático. Essa configuração remove a sequência de consulta ao gerar a chave de cache, para que uma solicitação para `style.css?something` seja normalizada para `style.css` ao servir por meio do cache).
 * Dependente da sequência de consultas: entrega um recurso diferente cada vez que a sequência de consultas muda.
  
## Limpar cache
 
É possível limpar seu cache para se preparar para atualizações a qualquer momento, apenas inserindo a URL no campo de limpeza de cache. É possível limpar um único arquivo ou vários arquivos (até 30 por vez).
 
 ## Expiração do navegador
 
É possível usar o menu suspenso para selecionar o tempo de expiração do navegador necessário, por exemplo, 8 horas ou 1 dia.
 
 ## Usando o modo de desenvolvimento
 
O **modo de desenvolvimento** é destinado ao uso quando atualizações principais ou novos uploads de arquivos são necessários ou sempre que você não desejar que os usuários finais trabalhem no cache, mas recuperem arquivos diretamente dos servidores de origem. Para iniciar o uso do **Modo de desenvolvimento**, alterne o comutador para a posição `Ativado`. Para parar de usar o **Modo de desenvolvimento**, alterne o comutador para a posição `Desativado`. O **Modo de desenvolvimento** expira automaticamente após 3 horas. 

## Gerenciando suas Regras de Página
 
É possível ativar até 50 Regras de Página. Use os menus suspensos para configurar a Regra de Página. As configurações de regra são divididas em três categorias: **Segurança**, **Desempenho** e **Confiabilidade**.

Observe que, quando determinadas regras são ativadas, outras opções se tornam esmaecidas se estão em conflito com as outras regras que você acabou de selecionar. Depois de ter selecionado as Regras de Página desejadas, clique em **Provisionar** para ativá-las. As novas regras entram em vigor imediatamente e podem ser visualizadas imediatamente na tela Regras de página.
 
 ![MENUS DE REGRAS DE PÁGINA](images/page-rule-dropdown-settings.png)
 
Também é possível ativar ou desativar suas Regras de Página na tabela exibida na tela Regras de página. Consulte [Usando regras de página](using-page-rules.html) para obter informações adicionais.
 
 ## Configurações de segurança
 
Por padrão, a proteção de DDoS está ativada para quaisquer registros de DNS com proxy ativado, o que pode ser feito na tabela **Registros** na página DNS. Ative o WAF usando o comutador. Ao ativar ou desativar as regras, as mudanças são aplicadas imediatamente.

![IMAGEM](images/ddos-waf-ssl-screen.png)

## Certificados

Ao implementar em um Zona, o IBM CIS implementa automaticamente um certificado universal para essa zona. Assim, não é necessário fazer nada para ter proteção baseada em certificado nessa zona. Se desejar, será possível fazer upload de seu próprio certificado. Será necessário um certificado separado para cada zona e você verá uma mensagem de erro se o certificado do qual você está fazendo upload não corresponder à sua zona.

![IMAGEM](images/certificates-table.png)
 
 ## Configure seus balanceadores de carga
 
 O IBM CIS fornece balanceamento de carga global como um serviço.

![IMAGEM](images/glb-screen.png)

### Painel GLB
Em seu painel, você verá três listas que mostram os balanceadores de carga, os conjuntos de origem e as verificações de funcionamento. As listas exibem o balanceador de carga global novo ou atualizado ou um de seus componentes após você tê-lo provisionado ou atualizado. Inicialmente, as listas estão vazias e, antes de criar um balanceador de carga, deve-se realizar algumas ações.

#### Criar
**Nota**: <sup>`*`</sup> indica que essa etapa é opcional

1) <sup>`*`</sup>Crie uma verificação de funcionamento, clique em "Criar verificação de funcionamento". ![IMAGEM](images/glb-health-check-list.png)
    <ul>
      <li>* **Caminho**: o caminho do terminal com relação ao qual verificar o funcionamento.</li> 
      <li>* **Tipo**: o protocolo a ser usado para a verificação de funcionamento.</li>
      <li>* **Descrição**: descrição fornecida pelo usuário.</li>
    </ul>

2) Crie um conjunto, clique em "Criar conjunto".
  ![IMAGEM](images/glb-pool-list.png)
    <ul>
      <li>* **Funcionamento**: status do conjunto.</li>
      <li>* **Nome**: nome fornecido pelo usuário.</li>
      <li>* **Origens**: contagem de origens operantes no conjunto.</li>
      <li>* **Verificação de funcionamento**: caminho da verificação de funcionamento anexada, se houver.</li>
    </ul>

3) Crie um balanceador de carga, clique em "Criar balanceador de carga".
![IMAGEM](images/glb-load-balancer-list.png)
    <ul>
      <li>* **Funcionamento**: status do balanceador de carga.</li>
      <li>* **Nome do host**: nome anexado ao nome de domínio.</li>
      <li>* **Conjuntos disponíveis**: contagem de conjuntos operantes.</li>
      <li>* **TTL**: tempo de vida.</li>
      <li>* **Proxy**: ativar ou desativar o fluxo de tráfego do proxy.</li>
      <li>* **Status**: ativar ou desativar o balanceador de carga.</li>
    </ul>

#### Editar/Excluir
Para editar ou excluir um balanceador de carga ou um de seus componentes, clique no botão do menu overflow localizado na extrema direita de cada linha.

Botão do menu overflow:

![IMAGEM](images/overflow.png)

As opções a seguir são fornecidas para cada lista.

* Verificação de funcionamento
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

### Inclua uma verificação de funcionamento

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

### Inclua um conjunto

Pelo menos um conjunto é necessário para cada balanceador de carga provisionado. Os conjuntos agrupam suas origens para o balanceador de carga usar.

Ao criar um conjunto, dois campos são necessários:
 * **Nome**: um nome abreviado (tag) para o conjunto. Apenas caracteres alfanuméricos, hifens e sublinhados são permitidos.
 * **Origens**: a lista de origens dentro desse conjunto. O tráfego direcionado nesse conjunto é balanceado em todas as origens atualmente operantes, desde que o conjunto em si esteja operante.

Campos opcionais adicionais:
 * **Descrição**: uma descrição legível do conjunto.
 * **Ativado**: se é necessário ativar (o padrão) esse conjunto. Conjuntos desativados não recebem tráfego e são excluídos de verificações de funcionamento. A desativação de um conjunto faz com que quaisquer balanceadores de carga que o utilizem efetuem failover para o próximo conjunto, se houver (padronizado como true).
 * **Limite de origens operantes**: o número mínimo de origens que devem estar operantes para esse conjunto servir o tráfego. Se o número de origens operantes ficar abaixo desse número, o conjunto será marcado como inoperante e efetuará failover para o próximo conjunto disponível. (padronizado como 1)
 * **Regiões de verificação de funcionamento**: região da qual a verificação de funcionamento executará o monitoramento.
 * **Verificação de funcionamento**: a verificação de funcionamento a ser usada para verificar as origens dentro desse conjunto. (padronizado como sem verificação de funcionamento)
 * **E-mail de notificação**: o endereço de e-mail que deve receber notificações de status de funcionamento. Esse endereço pode ser uma caixa de correio individual ou uma lista de distribuição.

 ### Inclua um balanceador de carga

Balanceadores de carga ajudam a distribuir seu tráfego em proxy entre vários conjuntos de origem usando uma distribuição round-robin.

Ao criar um balanceador de carga, os campos obrigatórios são:
 * **Nome**: o nome do host DNS para associar ao seu Balanceador de Carga. Se esse nome do host já existir como um registro de DNS no DNS da IBM, o Balanceador de Carga terá precedência e o registro de DNS não será usado.
 * **Conjuntos padrão**: uma lista de IDs do conjunto. A lista é ordenada pela prioridade do failover. Conjuntos definidos aqui são usados por padrão ou quando conjuntos de regiões não estão configurados para uma determinada região.

Opcionalmente, os campos a seguir podem ser configurados:
 * **Proxy**: rotear o tráfego por meio do serviço de desempenho e métricas da IBM.
 * **Afinidade de sessão**: sempre rotear por meio da mesma instância de desempenho e métricas. Essa opção está disponível somente se o proxy está ativado.
 * **TTL**: tempo de vida (TTL) da entrada DNS para o endereço IP retornado por esse balanceador de carga. Essa opção se aplica apenas aos balanceadores de carga sem proxy, caso contrário, ela é padronizada como `Automatic`.
 * **Conjuntos de regiões**: um mapeamento de códigos de região ou país para uma lista de conjuntos (ordenados por sua prioridade de failover) para a região especificada. Todas as regiões não definidas explicitamente efetuarão fallback para usar os conjuntos padrão.
