---

copyright:
  years: 2018
lastupdated: "2018-03-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Configure seu Sistema de Nomes de Domínio (DNS) para o IBM CIS

Este documento contém algumas instruções específicas sobre como configurar seus registros de DNS do IBM CIS, incluindo como configurar DNS Seguro.

## DNS seguro

**DNSSec** é uma tecnologia para 'assinar' digitalmente dados DNS para garantir sua validade. Para eliminar a vulnerabilidade da Internet, DNSSec deve ser implementado em cada etapa na consulta, da zona raiz para o nome do domínio final (por exemplo, www.icann.org).

## Configurando e gerenciando seu DNS seguro 

O DNSSec inclui uma camada de autenticação para a infraestrutura de DNS da Internet, o qual de outra forma não é seguro. O DNS seguro garantirá que os visitantes sejam direcionados para o **seu** servidor da web quando eles digitarem seu nome de domínio em um navegador da web. Tudo o que você precisa fazer é ativar o DNSSec em sua página DNS de sua conta do IBM CIS e incluir o registro DS para seu registro.

![DNS Seguro](images/dns/secure-dns.png)

É possível selecionar o botão **Visualizar registros DS** para abrir uma caixa de diálogo que explica como incluir o registro DS para seu registro. Deve-se copiar partes do registro DS e colá-las no painel de seu registro. Cada registro é diferente e seu registro pode requerer que você insira informações apenas para alguns dos campos disponíveis.

## Incluindo registros de DNS

É possível usar o menu suspenso **Tipo** para selecionar o tipo de registro que você deseja criar. Cada tipo de registro de DNS tem um Nome e um Tempo de Vida (TTL) associado a ele. 

O que quer que seja inserido no campo Nome terá o nome de domínio anexado a ele, a menos que o nome de domínio já tenha sido anexado manualmente no campo (por exemplo, se `www` ou `www.example.com` for digitado no campo, a API tratará ambos como `www.example.com`). Se o nome de domínio exato for digitado no campo de nome, ele não será anexado em si mesmo (por exemplo, `example.com` será tratado como `example.com`). No entanto, a lista de registros de DNS mostrará apenas os nomes sem o nome de domínio que está sendo acrescentado, portanto, `www.example.com` será mostrado como `www` e `example.com` será mostrado como `example.com`. O TTL terá um valor padrão de `Automatic`, mas poderá ser mudado pelo usuário. Um registro de DNS com proxy sempre terá um TTL igual a `Automatic`, portanto, um registro de proxy recém-incluído mudará para essa configuração durante essa mudança.

### Registro de tipo A

Para incluir esse tipo de registro, valores válidos deverão existir nos campos **Nome** e **Endereço IPv4**. Um **TTL** também poderá ser especificado no menu suspenso, com um valor padrão de 'Automatic'.

![Criar registro Tipo A](images/dns/create-a-type-record.png)

    Campos obrigatórios: Nome, Endereço IPv4
    Campo opcional: TTL (valor padrão é Automatic)

### Registro de tipo AAAA

Para incluir esse tipo de registro, valores válidos deverão existir nos campos **Nome** e **Endereço IPv6**. Um **TTL** também pode ser especificado por meio do menu suspenso, com o valor padrão de 'Automatic'.

![Criar registro Tipo AAAA](images/dns/create-aaaa-type-record.png)

    Campos obrigatórios: Nome, Endereço IPv6
    Campo opcional: TTL (valor padrão é Automatic)

### Registro de tipo CNAME

Para incluir esse tipo de registro, um valor válido deverá existir no campo **Nome** e um nome completo do domínio deverá estar no campo**Nome de Domínio** (FQDN). Um **TTL** também pode ser especificado por meio do menu suspenso, com o valor padrão de 'Automatic'.


![Criar registro do Tipo CNAME](images/dns/create-cname-type-record.png)

    Campos obrigatórios: Nome, Nome de domínio (para CNAME)
    Campo opcional: TTL (valor padrão é Automatic)


### Registro de tipo MX

Para incluir esse tipo de registro, um valor válido deverá existir no campo **Nome** e um endereço válido deverá existir no campo **Servidor de correio**. Um **TTL** também pode ser especificado por meio do menu suspenso, com o valor padrão de 'Automatic'.

![Criar registro de Tipo MX](images/dns/create-mx-type-record.png)

    Campos obrigatórios: Nome, Servidor de correio
    Campos opcionais: TTL (valor padrão é Automatic), Prioridade (valor padrão é 1)

### Registro de tipo LOC

Para incluir esse tipo de registro, um valor válido deverá existir no campo **Nome**. Se forem necessárias informações mais específicas, selecione o botão **Configurar opções de LOC**. Um **TTL** também pode ser especificado por meio do menu suspenso, com o valor padrão de 'Automatic'.

![Criar registro de Tipo LOC](images/dns/create-loc-type-record-1.png)

    Campos obrigatórios: Nome
    Campos opcionais: opções do LOC (clique no botão para configurar)

![Criar registro de Tipo LOC](images/dns/create-loc-type-record-2.png)

### Registro de tipo CAA

Para incluir esse tipo de registro, valores válidos deverão existir nos campos **Nome** e **Valor**. O campo Valor será correlacionado ao valor do campo suspenso **Tag**, que é padronizado como "Enviar relatórios de violação à URL". Um **TTL** também pode ser especificado por meio da lista suspensa, com o valor padrão de 'Automatic'.

![Criar registro do Tipo CAA](images/dns/create-caa-type-record.png)

    Campos obrigatórios: Nome, Valor (associado à tag)
    Campos opcionais: TTL (valor padrão é Automatic), Tag (padrão é enviar relatórios de violação à URL)

### Registro de tipo SRV

Para incluir esse tipo de registro, valores válidos deverão existir nos campos **Nome**, **Nome do serviço** e **Destino**. Use o menu suspenso para selecionar um **protocolo**, o qual é padronizado com o protocolo UDP. Além disso, é possível especificar **Prioridade**, **Peso** e **Porta**. Esses três campos são padronizados com um valor igual a 1. Um **TTL** também pode ser especificado por meio do menu suspenso, com o valor padrão de 'Automatic'.

![Criar registro de Tipo SRV](images/dns/create-srv-type-record.png)

    Campos obrigatórios: Nome, Nome do serviço, Destino
    Campos opcionais: TTL (valor padrão é Automatic), Protocolo (padronizado como UDP), Prioridade (padronizado como 1), Peso (padronizado como 1), Porta (padronizado como 1)

### Registro de tipo SPF

Para incluir esse tipo de registro, valores válidos deverão existir nos campos **Nome** e **Conteúdo**. Um **TTL** também pode ser especificado por meio do menu suspenso, com o valor padrão de 'Automatic'.

![Criar registro de Tipo SPF](images/dns/create-spf-type-record.png)

    Campos necessários: nome, campo de conteúdo opcional: TTL (o valor padrão é Automatic)

### Registro de tipo TXT

Para incluir esse tipo de registro, valores válidos deverão existir nos campos **Nome** e **Conteúdo**. Um **TTL** também pode ser especificado por meio do menu suspenso, com o valor padrão de 'Automatic'.

![Criar registro de Tipo TXT](images/dns/create-txt-type-record.png)

    Campos necessários: nome, campo de conteúdo opcional: TTL (o valor padrão é Automatic)

### Registro de tipo NS

Para incluir esse tipo de registro, valores válidos deverão existir nos campos **Nome** e **Servidor de nomes**. Um **TTL** também pode ser especificado por meio do menu suspenso, com o valor padrão de 'Automatic'.

![Criar registro de Tipo NS](images/dns/create-ns-type-record.png)

    Campos obrigatórios: Nome, Servidor de nomes
    Campo opcional: TTL (valor padrão é Automatic)

## Atualizando registros de DNS

Em cada linha do registro, é possível clicar na opção **Editar registro** no menu, que abrirá uma caixa de diálogo, a qual poderá ser usada para atualizar o registro.

![Editar registro de DNS](images/dns/edit-dns-record.png)

Por exemplo, esse é o diálogo de atualização para o registro do tipo **A**. Quando você terminar de fazer suas mudanças, selecione **Atualizar registro** para salvá-las.

![Diálogo editar registro de DNS](images/dns/update-dns-dialog.png)

## Excluindo registros

Em cada linha do registro, é possível selecionar a opção **Excluir registro** no menu, que abrirá uma caixa de diálogo para confirmar o processo de exclusão.

![Excluir registro de DNS](images/dns/delete-record.png)

É possível selecionar o botão **Excluir** para confirmar sua ação de exclusão. Selecione **Cancelar** se você não deseja excluir.

![Diálogo excluir registro de DNS](images/dns/delete-record-dialog.png)
