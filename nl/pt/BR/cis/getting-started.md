---
copyright:
  years: 2018
lastupdated: "2018-03-19"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Introdução ao IBM Cloud Internet Services (CIS)

O IBM Cloud Internet Services (CIS) oferece três recursos principais para aprimorar seu fluxo de trabalho: [segurança](/docs/infrastructure/cis/managing-for-security.html), [confiabilidade](/docs/infrastructure/cis/managing-for-reliability.html) e [desempenho](/docs/infrastructure/cis/managing-for-performance.html). Cada área de recurso é representada na barra de navegação esquerda de sua tela, ao abrir o aplicativo IBM CIS.

Para cada recurso, o IBM CIS ajuda você a ajustar seus recursos para atender às suas necessidades específicas, incluindo:

 * Servidores DNS autorizados
 * Balanceamento de carga global e local
 * Web Application Firewall (WAF)
 * Proteção de DDoS
 * Armazenamento em cache e regras de página



## Antes de começar
Antes de iniciar o uso do IBM CIS, primeiro será necessário um [IBMid](https://www.ibm.com/account/us-en/signup/register.html). Então será possível solicitar seus serviços por meio da Conta do IBM Cloud ou por meio do novo [IBM Cloud Internet Services Portal](https://console.bluemix.net/catalog/services/internet-services), dependendo de sua preferência.

Se precisar de assistência para obter uma conta para usar o IBM Cloud Internet Services, [entre em contato com seu representante de vendas IBM](https://www.ibm.com/cloud-computing/bluemix/contact-us) para obter orientações adicionais sobre como começar.

Se você tiver uma conta do Softlayer existente, será possível [vincular sua conta](https://console.bluemix.net/docs/account/softlayerlink.html#unifyingaccounts) ao seu IBMid. 

## Visão geral do processo

É possível começar a utilizar o IBM CIS para seu tráfego de Internet com apenas algumas etapas.

 * Abra o aplicativo IBM CIS por meio de seu painel do IBM Cloud.
 * Inclua o domínio que deseja gerenciar.
 * Configure as informações do DNS com os servidores de nomes já fornecidos.
 * Continue a introdução ao IBM CIS, seguindo um tutorial ou configurando outros recursos.

### Etapa 1: abra o aplicativo IBM CIS

Abra seu [painel do IBM Cloud](https://console.bluemix.net/catalog/). Em seguida, navegue até o ícone do aplicativo IBM CIS selecionando a categoria **Plataforma -> Rede** na barra de navegação esquerda do painel. Abra o aplicativo IBM Cloud Internet Services clicando no ícone que você verá perto do meio de sua tela. 

![Catálogo](images/catalog-cis-tile.png)

**A tela de visão geral**

Quando o aplicativo IBM CIS for inicializado, você verá a tela **Visão geral** do IBM CIS e localizará as guias para **Segurança**, **Confiabilidade** e **Desempenho** na área esquerda da tela de IU.

**Qual plano escolher?**

Para a liberação _Early Access_, há apenas um plano que você pode escolher e ele é gratuito. Clique no botão **Criar** na parte inferior esquerda da tela **Visão geral** para iniciar o fornecimento de sua conta.

**Iniciar fornecimento**

Você verá a primeira tela do aplicativo IBM CIS, na qual você selecionará o botão **Incluir domínio** para iniciar.

|**Observe que o programa Early Access está limitado a uma instância por conta.** |
|-------------------------------------------------------------------|
| Depois de ter criado uma instância de recurso e incluído um domínio nela, você não terá permissão para incluir novas instâncias de recursos para o IBM CIS. Essa restrição será impingida mesmo se você excluir um domínio de teste e, em seguida, tentar incluir um domínio novamente na mesma instância de recurso. Você vai encontrar um erro se tentar fazer isso.|

### Etapa 2. Inclua e configure seu domínio.

Comece protegendo e melhorando o desempenho de seu serviço da web inserindo seu domínio ou um subdomínio.

**Nota:** especifique zonas DNS. É possível configurar os servidores de nomes para esses domínios ou subdomínios no registro do domínio ou provedor DNS. Não use CNAMEs.

![Introdução](images/overview-add-domain.png)
A tela de Visão geral mostrará seu domínio no status `Pendente`. Seu domínio permanecerá `Pendente` até você concluir a Etapa 3.

**Nota:** a instância do IBM CIS não pode ser excluída após um domínio ter sido incluído. Para excluir a instância, exclua o domínio da instância primeiro.

### Etapa 3. Configure seus servidores de nomes com o registro ou provedor DNS existente.

Para começar a receber os benefícios do IBM CIS, configure seu registro ou provedor de nome de domínio para usar os servidores de nomes listados. Se você está delegando um domínio (algo como `example.com`), configure os servidores de nomes listados nas configurações de seu domínio, onde eles são gerenciados por seu registro (por exemplo, no portal da web do registro). Se você não tiver certeza sobre quem é o registro para seu domínio, será possível procurar em https://whois.icann.org/. Se você delegar um subdomínio (por exemplo, `subdomain.example.com`) de outro provedor DNS, deverá incluir um registro de Servidor de Nomes (NS) para cada um dos servidores de nomes listados.

Depois de ter configurado seu registro ou provedor DNS, poderá demorar até 24 horas para que as mudanças entrem em vigor. Assim que verificar se os servidores de nomes especificados foram configurados corretamente para seu domínio ou subdomínio, o status do domínio mudará de `Pendente` para `Ativo`. Depois de configurar os servidores de nomes, será possível clicar no link "Verificar novamente servidores de nomes" na página `Visão geral` para acelerar potencialmente a ativação de seu domínio (é possível enviar essa verificação apenas uma vez por hora).

### Etapa 4. Assegure-se de que o IBM Cloud Internet Services esteja resolvendo as informações de domínio para seu aplicativo, nome do host ou website.

Para continuar, selecione a guia **Confiabilidade** de sua barra de navegação esquerda, em seguida, selecione a opção**DNS**. Certifique-se de incluir os _Registros de DNS_ apropriados. Inclua o **Registro A** e quaisquer entradas **AAAA** ou **MX** que estejam preenchidas. Se você esquecer de incluir esses registros antes da delegação do registro ser concluída, o IBM Cloud Internet Services não poderá resolver as informações de domínio para seus aplicativos voltados à Internet.  

![Introdução](images/dns-records.png)

### Etapa 5. Enquanto isso, você pode começar a gerenciar outras funções e recursos do IBM CIS.

Para obter mais detalhes sobre como gerenciar outras funções e recursos, consulte as [instruções passo a passo](/docs/infrastructure/cis/how-to.html).
