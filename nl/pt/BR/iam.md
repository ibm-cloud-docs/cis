---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Access Group Writer role, CIS instance, IAM

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# IAM e CIS
{:#iam-and-cis}

O IBM Cloud Internet Services (CIS) utiliza o IAM para executar a autorização e a autenticação.

Caso não deseje incluir ninguém em sua instância do CIS, é possível desconsiderar essa página.
{:note}

Restringir acesso por três Escopos Funcionais do CIS, com base na árvore de navegação: 
* confiabilidade - como DNS, GLB
* segurança - como certificado, regras de firewall de IP e limitação de taxa
* desempenho - como regras de página, armazenamento em cache e roteamento

Essa seção explica como fornecer o controle de acesso de baixa granularidade de sua instância.

## Funções
{:#iam-and-cis-roles}

Use as três funções a seguir para utilizar o IAM
* Leitor - Capaz de obter informações sobre a instância e o domínio
* Gravador - Capaz de fazer mudanças na configuração existente
* Gerenciador - Capaz de criar ou excluir instâncias, domínios, configuração

## Grupos e usuários de acesso
{:#iam-and-cis-access-groups-users}

Uma política pode ser designada a um Usuário diretamente ou a um Grupo de Acesso.
Recomendamos designá-la a um grupo de acesso para minimizar o número de políticas criadas e reduzir o esforço de gerenciá-las.

## Cache
{:#iam-and-cis-cache}

Armazenamos em cache os resultados da autorização e utilizamos o cache para tomar uma decisão quando a mesma solicitação chega novamente. Depois que o cache atingir seu tempo de vida (10 min), ele expira.

## Melhores práticas
{:#iam-and-cis-best-practices}

1. Em vez de modificar, exclua a política existente e, em seguida, crie uma nova.

## Cenários
{:#iam-and-cis-scenarios}

Essa seção explica os diferentes exemplos de políticas de acesso criadas por meio do CIS. 

### Nível de domínio com o tipo `config`
{:#iam-and-cis-scenarios-domain-level}

#### Acesso ao domínio único com `configuração de segurança` em um grupo de acesso
##### Função de gravador

Bob tem uma instância do CIS, `cis-test-instance`, e dois domínios, `bob.com` e `bob-ibm.com`.
Ele deseja fornecer a todos os engenheiros de segurança (sec-group) da empresa o acesso à função de Gravador apenas para a **configuração de segurança** de **`bob.com`**.

Essas etapas mostram como criar uma política do IAM para tornar esse cenário possível.

Depois de Bob efetuar login em cis-test-instance, ele:
1. Clica na guia **Conta > Acesso** na barra de navegação
1. Seleciona o **grupo de acesso** - **sec-group** para o qual deseja fornecer acesso
1. Seleciona **`bob.com`**
1. Seleciona a função **Gravador**
1. Seleciona a opção **Configuração de Segurança**
1. Clica **Criar Política**

Na guia Gerenciar:
As políticas a seguir são criadas para **sec-group**:

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e

Instância de Serviço 
    nome: cis-test-instance  
    id: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9 
Domínio 
    nome: bob.com
    id: 4b23ec772965f672f96f05670e36827e 
Tipo de Configuração
    cfgType: segurança
```

Agora, sec-group tem acesso para ver apenas `bob.com` e pode modificar valores relativos à segurança. 

##### Atualização de função de Gravador para Gerenciador para um grupo de acesso

Se Bob deseja atualizar a função de sec-group de Gravador para Gerenciador, precisa excluir a política existente. 
1. Acesse **a guia Gerenciar o IAM > Grupos de acesso > sec-group > políticas de acesso**
1. Exclua a política a seguir 
  ```
  Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
  ```

Em seguida, Bob tem que criar a nova política. 
1. Clique na guia **Conta > Acesso** na barra de navegação
1. Selecione o **grupo de acesso** - **sec-group** para o qual deseja fornecer acesso
1. Selecione **`bob.com`**
1. Selecione a função **Gerenciador**
1. Selecione a opção **Configuração de segurança**
1. Clique em **criar política**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

Se a política existente (gravador) não for excluída, a tentativa de criar a política para Gerenciador falhará.

##### Atualize a configuração para incluir o Desempenho junto com a Segurança

Para Bob fornecer ao Gerenciador acesso de sec-group à configuração de desempenho em `bob.com` com segurança, ele:
1. Clica na guia **Conta > Acesso** na barra de navegação
1. Seleciona o **grupo de acesso** - **sec-group** para o qual deseja fornecer acesso
1. Seleciona **`bob.com`**
1. Seleciona a função **Gerenciador**
1. Seleciona a opção **Configuração de desempenho**
1. Clica **Criar Política**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: performance, domainId: 4b23ec772965f672f96f05670e36827e

```

#### Acesso a todos os domínios com a `configuração de segurança`

Se quer fornecer ações de segurança para `bob.com` e `bob-ibm.com` a partir do exemplo anterior, deve-se criar uma nova política repetindo as etapas para cada domínio. A única diferença é selecionar o respectivo domínio para cada política.

1. Clique na guia **Conta > Acesso** na barra de navegação
1. Selecione o **grupo de acesso** - **sec-group** para o qual deseja fornecer acesso
1. Selecione **`bob.com`**
1. Selecione a função **Gerenciador**
1. Selecione a opção **Configuração de segurança**
1. Clique em **criar política**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

1. Clique na guia **Conta > Acesso** na barra de navegação
1. Selecione o **grupo de acesso** - **sec-group** para o qual deseja fornecer acesso
1. Selecione **`bob-ibm.com`**
1. Selecione a função **Gerenciador**
1. Selecione a opção **Configuração de segurança**
1. Clique em **criar política**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 7ad7341865246f5df482ad9f76aafb5a
```



#### Acesso a um único domínio com `configuração de segurança` e `configuração de confiabilidade`

Bob tem uma instância cis-test-instance do CIS e 2 domínios, `bob.com` e `bob-ibm.com`.
Ele deseja fornecer a Tony acesso à função de Gravador somente para as **ações de segurança e confiabilidade** de **`bob-ibm.com`**.

Depois de Bob efetuar login em cis-test-instance, ele:
1. Clica na guia **Conta > Acesso** na barra de navegação
1. Seleciona **Tony**, que é a pessoa para quem ele deseja fornecer acesso
1. Seleciona **`bob-ibm.com`**
1. Seleciona a função **Gravador**
1. Marca a caixa de seleção para a opção **Segurança e confiabilidade** 
1. Clica **Criar Política**

Isso cria duas políticas no back-end para cada tipo de configuração.

### Nível de domínio com todos os tipos de configuração
{:#iam-and-cis-scenarios-domain-level-all-config-types}

Bob quer conceder leitura / write/mange a um nível de domínio para Tony.

#### Gravação
Depois de Bob efetuar login em cis-test-instance, ele:
1. Clica na guia **Conta > Acesso** na barra de navegação
1. Seleciona **Tony**, que é a pessoa para quem ele deseja fornecer acesso
1. Seleciona **`bob.com`**
1. Seleciona a função **Gravador**
1. Marca todas as caixas para o Escopo funcional do CIS
1. Clica **Criar Política**

```
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: security	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: performance	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: reliability	
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

#### Gerenciador
Depois de Bob efetuar login em cis-test-instance, ele:
1. Clica na guia **Conta > Acesso** na barra de navegação
1. Seleciona **Tony**, que é a pessoa para quem ele deseja fornecer acesso
1. Seleciona **`bob.com`**
1. Seleciona a função **Gerenciador**
1. Marca todas as caixas para o Escopo funcional do CIS
1. Clica **Criar Política**

```
Gerenciador	Recurso	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: security	
Gerenciador	Recurso	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: desempenho	
Gerenciador	Recurso	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: confiabilidade	
Leitor	Recurso	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Visualizador	Recurso	Apenas instância de serviço cis-test-instance of CIS 	
```

#### Leitor
Depois de Bob efetuar login em cis-test-instance, ele:
1. Clica na guia **Conta > Acesso** na barra de navegação
1. Seleciona **Tony**, que é a pessoa para quem ele deseja fornecer acesso
1. Seleciona **`bob.com`**
1. Seleciona a função **Leitor**
  1. Todas as caixas de seleção são pré-marcadas para mostrar que o usuário precisa de acesso de leitura *mín* para o domínio inteiro e que não é possível fornecer acesso parcial a um domínio
1. Clique em **criar política**


```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

### Nível de instância - todos os seus domínios
{:#iam-and-cis-scenarios-instance-level}

Essa política deve ser criada e gerenciada por meio da página de gerenciamento do IAM.

O acesso ao nível de instância significa que Bob pode fornecer permissão a Tony para a Instância 1 das 10 instâncias presentes.
Tony é capaz de visualizar todos os domínios nessa instância. 

Se Bob deseja fornecer ao Gravador ou Gerenciador acesso ao seguinte, precisa fornecer acesso de nível de instância:
* Balanceador de carga - conjuntos e verificações de funcionamento
* Regras de acesso ao firewall
* Trabalhadores 

Na página Gerenciar o IAM, crie uma política de gravador/gerenciador na instância de serviço cis-test-instance.

```
Instância de serviço cis-test-instance Somente Recurso do Gerenciador	do CIS
ou
Instância de serviço cis-test-instance Somente Recurso do Gravador do CIS
```

## Gerenciar políticas do IAM 
{:#manage-iam-policies}

O CIS permite que os usuários criem políticas do IAM, mas o gerenciamento deve ser feito por meio da [Página do IAM](
https://{DomainName}/iam#/overview).

## Nota
{:#iam-note}
Para cada política criada na página Acesso na instância do CIS, de duas a três políticas serão criadas por vez.

1. A função de visualizador de Plataforma da instância de serviço permite que o usuário incluído visualize a instância no painel.

**Exemplo**
```
Visualizador	Recurso	Apenas instância de serviço cis-instance-instance of CIS 	
```

2. O acesso de leitura de nível de domínio é o requisito mínimo para o acesso de baixa granularidade funcionar.

**Exemplo**
```
Leitor	Recurso	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f962f96f05670e36827e	
```
3. A política criada com o tipo de configuração presente.

**Exemplo**
```
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

**Perguntas mais frequentes**
1. Como obtenho o ID da minha instância de serviço?

   Copie o CRN na página de visão geral
   ```
   crn:v1:test:public:internet-svcs:global:a/2c38d9a9913332006a27665dab3d26e8:836f33a5-d3e1-4bc6-876a-982a8668b1bb::
   ```
   A última parte do CRN é a sua instância de serviço: `836f33a5-d3e1-4bc6-876a-982a8668b1bb`.
   
   ou
   
   Clique na linha que contém a instância do CIS na página principal da lista de recursos e copie o GUID para o ID da instância de serviço.

2. Eu deletei uma política, mas o usuário que eu dei a política ainda pode executar essa ação!

   O CIS armazena em cache os resultados da autorização e o TTL para o cache é de 10 minutos.  
   
   Após a autorização do IAM, ele usa as políticas de acesso do grupo de acesso e as próprias políticas do usuário antes de tomar uma decisão.

3. Quais permissões são necessárias para provisionar o Internet Services?

   Caso não seja possível criar um recurso e incluí-lo em um grupo de recursos, provavelmente há um problema de acesso. Deve-se ter pelo menos a função de Visualizador no próprio grupo de recursos e pelo menos a função de Editor no serviço na conta. É possível entrar em contato com o administrador da conta para verificar seu acesso designado na conta. Consulte [Gerenciando o acesso a recursos](/docs/iam?topic=iam-iammanidaccser) para obter mais informações.
   
 
