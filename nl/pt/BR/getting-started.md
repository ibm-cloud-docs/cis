---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-29"

keywords: IBM Cloud Internet Services, IBM CIS application, Authoritative DNS servers

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Introdução ao IBM Cloud Internet Services (CIS)
{:#getting-started}

O IBM Cloud Internet Services (CIS), desenvolvido com o Cloudflare, oferece três recursos principais para aprimorar o fluxo de trabalho: [segurança](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-for-optimal-security), [confiabilidade](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-deployment-for-optimal-reliability)e [desempenho](/docs/infrastructure/cis?topic=cis-manage-your-cis-deployment-for-best-performance). Cada área de recurso é representada na barra de navegação esquerda de sua tela, ao abrir o aplicativo IBM CIS.

Para cada recurso, o IBM CIS ajuda você a ajustar seus recursos para atender às suas necessidades específicas, incluindo:

 * Servidores DNS autorizados
 * Balanceamento de carga global e local
 * Web Application Firewall (WAF)
 * Proteção de DDoS
 * Armazenamento em cache e regras de página


## Antes de começar
{:#before-you-begin}

Antes de iniciar o uso do IBM CIS, primeiro será necessário um [IBMid](https://www.ibm.com/account/reg/us-en/signup?formid=urx-19776). Então será possível solicitar seus serviços por meio da Conta do IBM Cloud ou por meio do novo [IBM Cloud Internet Services Portal](https://{DomainName}/catalog/services/internet-services), dependendo de sua preferência.

Se precisar de assistência para obter uma conta para usar o IBM Cloud Internet Services, [entre em contato com seu representante de vendas IBM](https://{DomainName}/cloud/support) para obter orientações adicionais sobre como começar.

Se você tiver uma conta do Softlayer existente, será possível [vincular sua conta](https://{DomainName}/docs/account?topic=account-unifyingaccounts) ao seu IBMid. 

## Visão geral do processo
{:#process-overview}

É possível começar a usar o IBM CIS para seu tráfego de Internet com apenas algumas etapas.

 * Abra o aplicativo IBM CIS por meio de seu painel do IBM Cloud.
 * Inclua o domínio que deseja gerenciar.
 * Configure as informações do DNS com os servidores de nomes já fornecidos.
 * Continue a introdução ao IBM CIS, seguindo um tutorial ou configurando outros recursos.

### Etapa 1: abra o aplicativo IBM CIS
{:#open-cis-application}

Abra seu [painel do IBM Cloud](https://{DomainName}/catalog/). Em seguida, navegue até o ícone do aplicativo IBM CIS selecionando a categoria **Infraestrutura -> Rede** na barra de navegação esquerda do painel. Abra o aplicativo IBM Cloud Internet Services clicando no ícone que você verá perto do meio de sua tela. 

![Catálogo](images/catalog-cis-tile.png)

**A tela de visão geral**

Assim que o aplicativo IBM CIS for inicializado, você verá a tela **Visão geral** do IBM CIS e encontrará as guias para **Segurança**, **Confiabilidade** e **Desempenho** na área esquerda da exibição da IU.

**Qual plano devo escolher?**

Há 4 planos para escolher, 
* **Uso Enterprise** 
* **Pacote Enterprise** 
* **Plano Standard** 
* **Avaliação grátis**. 

A **Avaliação grátis** expira após 30 dias, quando é possível fazer upgrade para o **Plano Standard** ou para um **Plano Enterprise**. Uma única instância **Standard** pode gerenciar um domínio. É possível criar quantas instâncias de serviço **Standard** você desejar dentro de uma única conta, cada uma gerenciando um único domínio. 

Os **Planos Enterprise** permitem gerenciar diversos domínios em uma única instância de serviço. Selecione o botão **Criar** na tela **Visão Geral** para começar a provisionar sua conta.

A **Avaliação grátis** é limitada a uma instância por conta.
{:note}

**Iniciar fornecimento**

Você verá a primeira tela do aplicativo IBM CIS, na qual você selecionará o botão **Incluir domínio** para iniciar.


### Etapa 2. Inclua e configure seu domínio.
{:#add-configure-your-domain}

Selecione **Vamos começar** na página de boas-vindas para começar a configurar o CIS.

![Introdução](images/overview-setup-step1.png)

Em seguida, comece a proteger e melhorar o desempenho de seu serviço da web inserindo seu domínio ou um subdomínio.

Especifique as zonas de DNS. É possível configurar os servidores de nomes para esses domínios ou subdomínios no registro do domínio ou provedor DNS. Não use CNAMEs.
{:note}

![Introdução](images/overview-setup-step2.png)

A tela Visão Geral mostrará seu domínio no status `Pendente`. Seu domínio permanecerá `Pendente` até que você conclua a Etapa 4.

A instância do IBM CIS não poderá ser excluída após a inclusão de um domínio. Para excluir a instância, exclua o domínio da instância primeiro.
{:note}

### Etapa 3. Configure seus registros de DNS (opcional).
{:#setup-your-dns-records}

Antes de executar a transição para o CIS do tráfego para o seu domínio, recomendamos que você importe ou recrie seus registros de DNS no CIS. É possível escolher ignorar essa etapa, mas se seus registros de DNS não estiverem configurados corretamente no CIS, ele poderá deixar partes de seu website inacessíveis.

Faça upload dos registros exportados do seu DNS atual para importá-los ou os crie manualmente. Para importar registros, selecione **Importar registros**.

![Introdução](images/overview-setup-step3.png)

Ao concluir ou se desejar ignorar essa etapa, selecione **Próxima etapa**.

### Etapa 4. Configure seus servidores de nomes com o registrador ou o provedor DNS existente.
{:#configure-your-name-servers-with-the-registrar-or-existing-dns-provider}

Para começar a receber os benefícios do IBM CIS, configure seu registro ou provedor de nome de domínio para usar os servidores de nomes listados. Se você está delegando um domínio (algo como `example.com`), configure os servidores de nomes listados nas configurações de seu domínio, onde eles são gerenciados por seu registro (por exemplo, no portal da web do registro). Se você não tiver certeza sobre quem é o registro para seu domínio, será possível procurar em https://whois.icann.org/. Se você delegar um subdomínio (por exemplo, `subdomain.example.com`) de outro provedor DNS, deverá incluir um registro de Servidor de Nomes (NS) para cada um dos servidores de nomes listados. Consulte [Gerenciando Registros DNS ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://support.cloudflare.com/hc/en-us/articles/360019093151-Managing-DNS-records-in-Cloudflare){:new_window}, gravados por nossos parceiros no Cloudflare, para obter instruções detalhadas por provedor.

Depois de ter configurado seu registro ou provedor DNS, poderá demorar até 24 horas para que as mudanças entrem em vigor. Assim que verificarmos se os servidores de nomes especificados foram configurados corretamente para seu domínio ou subdomínio, o status do domínio será mudado de `Pendente` para `Ativo`. Depois de configurar os servidores de nomes, será possível clicar no link "Verificar novamente servidores de nomes" na página `Visão geral` para acelerar potencialmente a ativação de seu domínio (é possível enviar essa verificação apenas uma vez por hora).

Seu domínio deve ser movido para o estado `Ativo` dentro de 60 dias ou ele e quaisquer dados de configuração serão removidos.
{:note}

![Introdução](images/overview-setup-step4.png)

### Etapa 5. Certifique-se de que o IBM Cloud Internet Services esteja resolvendo as informações de domínio para seu aplicativo, nome de host ou website.
{:#ensure-cis-is-resolving-domain-info}

Para continuar, selecione a guia **Confiabilidade** de sua barra de navegação esquerda, em seguida, selecione a opção**DNS**. Certifique-se de incluir os _Registros de DNS_ apropriados. Inclua o **Registro A** e quaisquer entradas **AAAA** ou **MX** que estejam preenchidas. Se você esquecer de incluir esses registros antes da delegação do registro ser concluída, o IBM Cloud Internet Services não poderá resolver as informações de domínio para seus aplicativos voltados à Internet.

![Introdução](images/dns-records.png)

### Etapa 6. Enquanto isso, é possível começar a gerenciar outras funções e recursos do IBM CIS.
{:#manage-other-cis-functions}

Para obter mais detalhes sobre como gerenciar outras funções e recursos, consulte as [instruções passo a passo](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cloud-internet-services-cis-deployment).
