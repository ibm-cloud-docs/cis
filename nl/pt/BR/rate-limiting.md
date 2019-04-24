---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Bypass, header responses, brute-force login attempts

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Limitação de taxa
{:#cis-rate-limiting}

A Limitação de taxa (somente no plano Enterprise) protege contra ataques de negação de serviço, tentativas de login de força bruta e outros tipos de comportamento abusivo direcionados à camada do aplicativo.

Selecione o tipo de regra de limitação de taxa, **Regra customizada** ou **Proteger login**

## Crie uma regra de limitação de taxa customizada
{:#create-a-custom-rate-limiting-rule}

Insira um nome de regra que ajude você a se lembrar o que a regra faz. Este campo é opcional.

**Critérios de correspondência de tráfego** usam a operação AND. Insira uma URL cuja taxa deseja limitar e, em seguida, quando as solicitações do **Mesmo IP excederem** o número especificado de **Solicitações por segundo**, a regra especificada será acionada.

A opção **Critérios Avançados** permite especificar quais métodos de HTTP, respostas de cabeçalho e códigos de resposta de origem para restringir ainda mais os critérios de correspondência. 

Selecione um formulário de valor no menu suspenso **Método** (ANY é o padrão).  

Atualize o **cabeçalho de resposta HTTP**.  Também é possível **Incluir cabeçalho de resposta** para incluir cabeçalhos retornados por seu servidor da web de origem. 

Se tiver mais de um cabeçalho em **Cabeçalho de resposta HTTP**, uma lógica booleana _AND_ será aplicada.  Para excluir um cabeçalho e evitar sua correspondência, use a opção _Não é igual_. Além disso, cada cabeçalho deve ser uma correspondência exata. No entanto, a distinção entre maiúsculas e minúsculas não se aplica.
{:note}

Em **Código de resposta da origem**, digite o valor numérico válido de cada código de resposta HTTP a ser correspondido.  Para incluir dois ou mais códigos de resposta, separe cada valor com uma vírgula. Por exemplo, é possível inserir `401, 403` se você deseja que apenas esses dois códigos de erro sejam considerados. 

### Configurar resposta
{:#rate-limiting-configure-response}

Selecione dentre as ações listadas e especifique o período de tempo limite. Nesse caso, o tempo limite refere-se ao período de banimento no qual a ação ocorre. Um tempo limite de 60 segundos significa que a ação é aplicada por 60 segundos.

|Ação| Descrição|
|------|------------|
|Bloquear | Emite um erro 429 quando o limite é excedido|
|Desafiar | O usuário deve passar em um Desafio reCaptcha do Google antes de continuar. Se for bem-sucedido, aceitaremos a solicitação. Caso contrário, ela será bloqueada.| 	
|Desafio JS |	O usuário deve transmitir um Desafio Javascript antes de continuar. Se for bem-sucedido, aceitaremos a solicitação. Caso contrário, ela será bloqueada.
|Simular| É possível usar essa opção para testar sua regra antes de aplicar qualquer uma das outras opções em seu ambiente de produção.

**Resposta avançada**

Especifique o tipo de resposta quando o limite de uma regra for excedido. 

### Bypass
{:#rate-limiting-bypass}

O bypass permite que você crie o equivalente a uma lista de desbloqueio ou exceção para um conjunto de URLs.  Nenhuma ação acionará essas URLs, mesmo se a regra de Limitação de taxa for correspondida.

## Proteger login
{:#rate-limiting-protect-login}

Proteger login cria uma regra padrão que protege as páginas de login com relação a ataques de força bruta. Os clientes que tentam efetuar login mais de 5 vezes em 5 minutos serão bloqueados por 15 minutos. 

Insira um nome para a regra e a URL de login.
