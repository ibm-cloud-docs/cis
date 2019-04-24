---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: edge functions beta, edge functions

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Edge Functions (Beta)
{: #edge-functions}

O CIS Edge Functions permite que você crie novos aplicativos ou modifique os aplicativos existentes, sem precisar configurar ou manter a infraestrutura, utilizando um ambiente de execução sem servidor. O Edge Functions pode ser definido e transferido por upload para a borda do Cloud para processar solicitações antes que elas atinjam a origem. O CIS Edge Functions pode ser usado para modificar solicitações e respostas de HTTP, fazer solicitações paralelas ou gerar respostas da borda do Cloud.

## Como o Edge Functions funciona
{: #how-edge-functions-work}

O Edge Functions associa **ações** a URIs com base em um domínio definido. Essa associação é chamada de **acionador**. Pedidos de entrada para seu site serão interceptados na borda da nuvem e correspondidos com relação aos acionadores em sua conta ou domínio. Se a URL de solicitação corresponder ao URI do acionador, a ação associada ao acionador será executada. 

O Edge Functions é modelado nos [Trabalhadores de Serviço](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) disponíveis em navegadores da web modernos e usam a mesma API sempre que possível.

A API do Trabalhador de Serviço permite que você intercepte qualquer solicitação feita ao seu site. Quando seu JavaScript estiver manipulando a solicitação, será possível escolher fazer qualquer número de subsolicitações ao seu site ou a outros e, finalmente, retornar qualquer resposta desejada ao seu visitante.

Diferentemente de Trabalhadores de Serviço padrão, o Edge Functions é executado em servidores de borda do CIS e não no navegador do usuário. Isso significa que é possível ter a segurança de que seu código será executado em um ambiente confiável no qual ele não sofrerá bypass de clientes maliciosos. Também significa que o usuário não precisa estar usando um navegador moderno que suporte Trabalhadores de Serviço, pois é possível interceptar até mesmo solicitações de clientes de API que não são navegadores.

Internamente, o Edge Functions usa o mesmo mecanismo JavaScript V8 que é usado no navegador Google Chrome para executar trabalhadores em nossa infraestrutura. A V8 compila dinamicamente seu código JavaScript no código de máquina ultrarrápido, tornando-o muito eficaz. Isso possibilita que seu código seja executado em microssegundos e que nossa borda execute muitos milhares de scripts por segundo.

Embora o Edge Functions use a V8, ele não usa o Node.js. As APIs JavaScript disponíveis para você dentro dos trabalhadores são implementadas por nós diretamente. O trabalho com V8 permite que o código seja executado de forma mais eficiente e com os controles de segurança necessários para manter os clientes e a infra-estrutura segura.


## Ações
{: #edge-functions-actions}

As ações são gravadas em JavaScript e requerem que um listener de eventos responda a um evento acionador. As ações não afetarão seu tráfego, a menos que sejam usadas por um acionador. 

### Planos Enterprise vs. Standard
{: #edge-functions-enterprise-v-standard-plans}

Os planos Standard têm um máximo de uma ação. Um nome igual ao do seu domínio é designado à ação. É possível substituir sua ação fazendo upload de outro arquivo ou atualizá-la com o uso do editor de código. Fazer upload de outro arquivo removerá a ação existente.

Os planos Enterprise podem fazer upload de um número ilimitado de scripts. Eles podem receber nomes exclusivos.

### Criar ações
{: #edge-functions-create-actions}

Selecione **Criar** para incluir uma ação usando o editor de código. Nos planos Enterprise, insira um nome para sua ação. Em planos Standard, o nome não é editável e está configurado para o nome de seu domínio. Depois de incluir seu código Javascript, selecione **Salvar** para criar sua ação. 

### Upload de ações
{: #edge-functions-upload-actions}

Use o botão **Upload** para fazer upload de um arquivo Javascript. Em planos Enterprise, o nome da ação é o nome do arquivo. Nos planos Standard, o nome da ação é configurado para o nome de seu domínio.

Fazer upload ou criar uma ação com o mesmo nome de uma ação existente fará com que a ação existente seja sobrescrita. Renomeie o arquivo de ação antes de fazer upload ou insira um nome exclusivo na entrada de texto durante a criação para evitar esse comportamento.
{:note}

### Editar ações
{: #edge-functions-edit-actions}

A seleção de uma ação a abre no editor para a modificação. Sempre que salvar suas mudanças, a ação será transferida por upload para a borda da nuvem. Após a atualização, selecione **Salvar**. Se a ação estiver em uso, as mudanças entrarão em vigor imediatamente. 

### Excluir ações
{: #edge-functions-delete-actions}

Exclua uma ação clicando no ícone **excluir**, na tabela **Ações**. Não é possível excluir uma ação que está em uso. Para excluir a ação, primeiro remova-a dos acionadores. A coluna **Usos** mostra o número de acionadores associados a essa ação. Não é possível desfazer a exclusão.


### Acionadores associados
{: #edge-functions-associated-triggers}

Inclua um acionador e associe-o a uma ação.

### Limitações conhecidas do Edge Functions
{: #edge-functions-known-limitations}

Fazendo upload de uma ação com o mesmo nome de uma ação existente. A ação existente será sobrescrita. Renomeie o arquivo de ação antes de fazer upload para evitar esse comportamento.


## Acionadores
{: #triggers}

### Sobre acionadores
{: #about-triggers}

Acionadores (rotas) determinam o roteamento do tráfego de domínio para as Ações. Acionadores associam determinados padrões de URL, com base em um domínio na conta, com uma ação predefinida. A URL deve conter o domínio, mas pode conter curingas como um prefixo para o domínio ou no final do caminho. Se nenhum caminho for fornecido no padrão, `/` será incluído implicitamente. O padrão de URL não pode conter curingas ou parâmetros de consulta de infix. 

Deve-se incluir um domínio para incluir acionadores. É possível incluir acionadores sem ter ações.

### Incluir acionadores
{: #add-triggers}

Acesse a guia **Acionadores** e clique em **Incluir acionador**. Insira um padrão de URL e selecione uma ação a partir da lista de ações existentes. 

Para uma ação, também é possível selecionar **Evitar o Edge Functions**. Isso permite que o caminho do acionador permaneça ativo, mas evita o uso de quaisquer ações do Edge Function. Por exemplo, há uma ação chamada `my-function` e um acionador com o caminho `beta.cistest-load.com/*`. Se o caminho `beta.cistest-load.com/data` não deve usar a ação `my-function`, crie outro acionador com o caminho `beta.cistest-load.com/data` e a opção **Evitar o Edge Functions**. Isso permite que o caminho `beta.cistest-load.com/data` permaneça ativo sem usar a ação `my-function`.

### Editar acionadores
{: #edit-triggers}

Atualize um acionador usando a opção de menu na linha da tabela para um acionador selecionado. Após a atualização, selecione **Salvar**.

### Excluir acionadores
{: #delete-triggers}

Exclua um acionador usando a opção de menu na linha da tabela para um acionador selecionado. Não é possível desfazer essa ação.


## Casos de uso
{: #edge-functions-use-cases-examples}

Esses exemplos são apenas para fins demonstrativos e não devem ser usados na produção.
{:important}
* [Teste A/B](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#ab-testing)
* [Incluindo um cabeçalho de resposta](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#add-response-header)
* [Agregando diversas solicitações](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#aggregate-multiple-requests)
* [Roteamento condicional](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#conditional-routing)
* [Proteção de hot-link](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#hot-link-protection)
* [Respostas sem origem](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#originless-responses)
* [Solicitações de post](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#post-requests)
* [Configurando um cookie](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#setting-cookies)
* [Solicitações assinadas](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#signed-requests)
* [Aperfeiços de Fluxo](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#streaming-responses)
