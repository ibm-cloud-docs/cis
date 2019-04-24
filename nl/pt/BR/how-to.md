---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Overview page, page rules, Service Mode

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Gerencie sua implementação do IBM Cloud Internet Services (CIS)
{:#manage-your-cis-deployment}

Você começará usando a tela Visão geral como sua base de operações de serviço. Ela mostra todos os parâmetros atuais para sua implementação.

Após configurar o DNS, você estará pronto para começar!

## Usando a tela Visão geral
{:#using-the-overview-screen}

Usando a tela Visão geral, é possível ver o status de todas as suas seleções. Cada configuração é vinculada à seção da interface com o usuário na qual está definida. Para modificar qualquer seleção, é possível navegar clicando no link para a configuração. Por exemplo, para alterar a configuração do balanceador de carga ou incluir um novo balanceador de carga, clique no campo `Load Balancer`.

Na tela Visão geral, é possível ver que sua configuração de nome de domínio está no status **Pendente** ou no status **Ativo**, conforme mostrado na figura a seguir.


![imagem de tela de visão geral](images/overview-screen-configuration-summary.jpg)

O status **Pendente** indica que seu domínio ainda não está totalmente configurado. É necessário atualizar seu registrador ou provedor DNS com os servidores de nomes fornecidos como parte do processo de configuração.

**Apenas corporativo**: a seção **Detalhes do serviço** da Visão geral também permite incluir domínios adicionais em sua instância do CIS e alternar entre diversos domínios.

## Mudando o modo de serviço
{#changing-the-service-mode}

Na página Visão geral, na seção Modo de serviço, há uma lista suspensa para selecionar um dos dois modos:

* **Modo de defesa** auxilia na proteção contra ataques de DNS existentes ou previstos. Esse modo impede todo o tráfego de chegar a seus servidores de origem por meio de seu domínio.
* **Pausar serviço** desativa todos os benefícios de segurança e desempenho para seu domínio. As funções de DNS ainda são resolvidas para seu website, mas o tráfego é enviado diretamente para as origens configuradas. 

### Etapas para configurar o modo de serviço
{:#steps-to-set-service-mode}

1. Selecione o modo desejado no menu suspenso.
1. Clique no botão `Ativar`.
1. Confirme ou cancele a seleção no pop-up de confirmação.

Aparece uma notificação em todas as páginas para mostrar que Pausar serviço ou Modo de defesa está ativo.
Para retornar à operação normal, clique em `Desativar modo` dentro do banner de notificação. ![imagem do botão do modo de desativação](images/deactivate-mode.png)


## Configurando e gerenciando o DNS
{:#configure-and-manage-your-dns}

Acesse sua página DNS e inclua um registro (mais provavelmente um registro A). Digite as informações sobre seu registro de DNS e, em seguida, clique em `Incluir registro` para implementar suas mudanças.

![add-DNS](images/dns/create-a-type-record.png)

Depois de criar seus registros, considere ativar a configuração `Proxy`. A maioria dos recursos do CIS requer que o tráfego da Internet para seu site flua através da infraestrutura do CIS. Em outras palavras, aplica-se somente a registros com proxy e balanceadores de carga. Para realmente aproveitar o benefício do CIS, certifique-se de que seus balanceadores de carga e registros de DNS tenham a configuração de proxy ativada.

## Configure e gerencie seu armazenamento em cache
{:#set-up-and-manage-your-caching}

Em seguida, é possível configurar o armazenamento em cache. 

![IMAGEM](images/caching-screen.png)

Você tem a opção de 3 tipos de armazenamento em cache, disponíveis no menu suspenso da tela de armazenamento em cache: 

 * Nenhuma sequência de consultas: fornece recursos do cache apenas quando não há nenhuma sequência de consultas.
 * Independente da sequência de consultas: fornece o mesmo recurso para todos, independentemente da sequência de consultas. (Nota: a configuração **Ignorar sequência de consultas** se aplica apenas a extensões de arquivo estático. Essa configuração remove a sequência de consulta ao gerar a chave de cache, para que uma solicitação para `style.css?something` seja normalizada para `style.css` ao servir por meio do cache).
 * Dependente da sequência de consultas: entrega um recurso diferente cada vez que a sequência de consultas muda.
  
## Limpar cache
{:#purge-cache-overview}
 
É possível limpar seu cache para se preparar para atualizações a qualquer momento, apenas inserindo a URL no campo de limpeza de cache. É possível limpar um único arquivo ou vários arquivos (até 30 por vez).
 
 ## Expiração do navegador
 {:#browser-expiration}
 
É possível usar o menu suspenso para selecionar o tempo de expiração do navegador necessário, por exemplo, 8 horas ou 1 dia.

Apenas corporativo: também é possível instruir o CIS a não substituir o controle de cache do navegador, configurando-o para **Respeitar os cabeçalhos existentes**.
 
 ## Usando o modo de desenvolvimento
 {:#using-development-mode}
 
O **modo de desenvolvimento** é destinado ao uso quando atualizações principais ou novos uploads de arquivos são necessários ou sempre que você não desejar que os usuários finais trabalhem no cache, mas recuperem arquivos diretamente dos servidores de origem. Para iniciar o uso do **Modo de desenvolvimento**, alterne o comutador para a posição `Ativado`. Para parar de usar o **Modo de desenvolvimento**, alterne o comutador para a posição `Desativado`. O **Modo de desenvolvimento** expira automaticamente após 3 horas. 

## Gerenciando suas Regras de Página
{:#managing-your-page-rules}
 
É possível usar as regras de página para especificar configurações específicas que se aplicam apenas a determinadas URLs, por exemplo, para ter configurações de controle de cache diferentes para determinados caminhos de URL. Use os menus suspensos para configurar a Regra de Página. As configurações de regra são divididas em três categorias: **Segurança**, **Desempenho** e **Confiabilidade**.

Observe que, quando determinadas regras são ativadas, outras opções se tornam esmaecidas se estão em conflito com as outras regras que você acabou de selecionar. Depois de ter selecionado as Regras de Página desejadas, clique em **Provisionar** para ativá-las. As novas regras entram em vigor imediatamente e podem ser visualizadas imediatamente na tela Regras de página.
 
 ![MENUS DE REGRAS DE PÁGINA](images/page-rule-dropdown-settings.png)
 
Também é possível ativar ou desativar suas Regras de Página na tabela exibida na tela Regras de página. Consulte [Usando regras de página](/docs/infrastructure/cis?topic=cis-use-page-rules) para obter informações adicionais.
 
 ## Configurações de segurança
 {:#security-settings-overview}
 
Por padrão, a proteção DDoS é ativada para quaisquer registros DNS ou balanceadores de carga com proxy on. 
As configurações de segurança são: 

* Ative o WAF usando a alternância na página **Firewall do aplicativo da web**. Ao ativar ou desativar as regras, as mudanças são aplicadas imediatamente.

* **Apenas corporativo**: a página **Limitação de taxa** permite configurar regras de limitação de taxa para evitar problemas do efeito noisy-neighbor e de DDoS.

* Na página **Firewall de IP**, é possível configurar regras de acesso com base no IP, no código do país ou no ASN. Também é possível configurar regras para bloquear agentes de usuário. A seção de bloqueio de domínio dessa página permite limitar a determinados endereços IP o acesso ao seu domínio.

* É possível revisar eventos relacionados ao firewall na página **Eventos**.

## Certificados
{:#certificates-overview}

Quando você configura um domínio, o IBM CIS implementa automaticamente um certificado universal para ele. Dessa forma, não é necessário fazer nada para ter uma proteção baseada em certificado nesse domínio. Se desejar, será possível fazer upload de seu próprio certificado. Será necessário um certificado separado para cada domínio e você verá uma mensagem de erro se o certificado que você está transferindo por upload não corresponder ao seu domínio. Também é possível solicitar certificados customizados nessa página. 

![IMAGEM](images/certificates-table.png)
 
 
