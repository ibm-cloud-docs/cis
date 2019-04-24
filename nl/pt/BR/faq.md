---
copyright:
  years: 2018
lastupdated: "2018-28-03"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Perguntas mais frequentes

## O que eu ganho com um Plano Early Access?
O programa Early Access, por design, permite apenas uma zona por conta. É recomendado que apenas uma instância seja criada por conta e que o nome da zona seja verificado. É crítico que o nome da zona seja verificado antes de ser incluído. Se uma zona for excluída, ela ou outra zona não poderá ser incluída durante o programa Early Access.

## Por que meu domínio está no estado Pendente? Como ativá-lo?
Ao incluir um domínio no CIS, nós fornecemos alguns servidores de nomes para configurar em seu registro (ou em seu provedor DNS, se você estiver incluindo um subdomínio). O domínio ou subdomínio permanece no estado pendente até que você configure os servidores de nomes corretamente. Certifique-se de incluir ambos os servidores de nomes em seu registro ou provedor DNS. Periodicamente, nós varremos o sistema DNS público para verificar se os servidores de nomes foram configurados conforme o instruído. Assim que somos capazes de verificar a mudança do servidor de nomes (isso pode levar até 24 horas), nós ativamos seu domínio. É possível enviar uma solicitação para verificar novamente os servidores de nomes clicando em **Verificar novamente servidores de nomes** na página de visão geral.

## Qual é o registrar para meu domínio?
Consulte https://whois.icann.org/ para obter essas informações. **Nota**: deve-se ter o privilégio administrativo para editar a configuração de seu domínio no registro para atualizar ou incluir os servidores de nomes fornecidos para seu domínio ao incluí-lo no CIS. Se você não sabe quem é o registro para o domínio que você está tentando incluir no CIS, é improvável que você tenha permissão para atualizar a configuração de seu domínio no registro. Trabalhe com o proprietário do domínio em sua organização para fazer as mudanças necessárias.

## Eu desejo manter meu provedor DNS atual para meu domínio (example.com). Posso delegar um subdomínio (subdomain.example.com) de meu provedor DNS atual para o CIS?
Sim. O processo é semelhante à inclusão de um domínio, mas em vez do registro, você trabalha com o provedor DNS para o domínio de nível superior. Ao incluir um subdomínio no CIS, você recebe dois servidores de nomes para configurar, como de costume. Você configura um registro do Servidor de Nomes (NS) para cada um dos dois servidores de nomes como registros de DNS em seu domínio que está sendo gerenciado pelo outro provedor DNS. Quando somos capazes de verificar se os registros NS necessários foram incluídos, nós ativamos seu subdomínio. Se você não gerencia o domínio de nível superior dentro de sua organização, deve-se trabalhar com o proprietário do domínio de nível superior para que os registros NS sejam incluídos.

## O que é TLS?
TLS é um protocolo de segurança padrão para estabelecer links criptografados entre um servidor da web e um navegador em uma comunicação on-line. Um certificado TLS é necessário para criar uma conexão TLS com um website e é composto pelo nome de domínio, nome da empresa e dados adicionais como endereço da empresa, cidade, estado e país. O certificado também mostra a data de expiração e detalhes da Autoridade de Certificação (CA) emissora.

## Como o TLS funciona?
Quando um navegador inicia uma conexão com um website protegido por TLS, ele primeiro recupera o Certificado TLS do site para verificar se o certificado ainda é válido. Ele verifica se a CA é uma que o navegador confia e se o certificado está sendo usado pelo website para o qual ele foi emitido. Se qualquer uma dessas verificações falhar, você receberá um aviso indicando que o website não está protegido por um certificado válido.

Quando um certificado TLS é instalado em um servidor da web, ele permite uma conexão segura entre o servidor da web e o navegador que se conecta a ele. A URL do website é prefixada com "https" em vez de "http" e um cadeado é exibido na barra de endereço. Se o website usa um certificado de validação estendida (EV), o navegador também pode mostrar uma barra de endereço verde.

## Por que eu vejo um aviso de privacidade?
Os certificados TLS emitidos pelo IBM Cloud CIS cobrem o domínio-raiz (`example.com`) e um nível de subdomínio (`*.example.com`). Se você está tentando atingir um subdomínio de segundo nível (`*.*.example.com`), verá um aviso de privacidade
em seu navegador, porque esses nomes de host não são incluídos na SAN.

Além disso, permita até 15 minutos para que uma de nossas Autoridades de certificação (CAs) parceiras emita um novo certificado. Você verá um aviso de privacidade em seu navegador se o novo certificado ainda não tiver sido emitido.

## O que é DDoS?
Um ataque distribuído por negação de serviço (DDoS) é uma tentativa de tornar um serviço on-line indisponível sobrecarregando-o com o tráfego de várias origens. Em um ataque DDoS, vários sistemas de computador comprometidos atacam um destino como um servidor, website ou outro recurso de rede, o que afeta os usuários do recurso de destino.

O fluxo de mensagens recebidas, solicitações de conexão ou pacotes malformados no sistema de destino o força a desacelerar ou até mesmo travar e encerrar, negando, assim, o serviço para legitimar usuários ou sistemas. Ataques DDoS têm sido realizados por diferentes agentes de ameaça, que vão desde hackers criminosos individuais até organizações criminosas e agências do governo.

## O que eu faço se estiver sob um ataque DDoS?

**Etapa 1:** ative o “Modo de defesa" na tela **Visão geral**. 

![Modo de defesa](images/defense-mode.png)

**Etapa 2:** configure seus registros DNS para o máximo de segurança.

**Etapa 3:** não defina um limite de taxa nem regule solicitações do IBM CIS. Precisamos da largura da banda para ajudá-lo com sua situação.

**Etapa 4:** bloqueie países específicos e visitantes se necessário.

## Eu recebi um erro 522, o que faço agora?

Um erro 522 indica que não conseguimos estabelecer uma conexão com o seu servidor de origem (ou seja, seu host). Após cerca de 15 segundos de falha de conexão, fechamos a conexão e exibimos uma página de erro 522.

Esse problema geralmente é causado pelo software do firewall ou de segurança que acidentalmente bloqueia nossos endereços IP. Como o CIS age como um proxy reverso, as conexões com seu site parecerão vir de um intervalo de IPs do CIS. Esse comportamento pode fazer com que alguns firewalls bloqueiem essas conexões, o que nos impede de entregar conteúdo para os visitantes de seu site adequadamente.

Para corrigir esse problema, peça ao host para incluir na lista de desbloqueio todos os intervalos de IP do CIS, que são listados [aqui](whitelisted-ips.html).

Todos esses IPs devem ser incluídos na lista de desbloqueio para evitar erros 522. Também convém verificar se quaisquer IPs nesses intervalos estão bloqueados.

Erros 522 também podem ser causados por problemas de conectividade de rede, portanto, confirme se seu servidor e sua rede geralmente estão operantes e não sobrecarregados.

Se depois de executar as etapas acima você ainda receber erros, entre em contato com o suporte do IBM CIS e confirme o seguinte:

* Você incluiu nossos intervalos de IP na lista de desbloqueio
* Seu servidor/rede está on-line e geralmente operante

Se você contatar nossa equipe de suporte, forneça um ID do raio de um erro 522 recente. Podemos usar isso para determinar qual Data Center do CIS você estava acessando e executar testes adicionais.

## O que é um registro com proxy e por que eu preciso deles?

Os registros com proxy são registros que efetuam proxy de seu tráfego por meio do IBM CIS. Somente registros com proxy recebem benefícios do CIS, tal como o mascaramento de IP, em que um IP do CIS é substituído pelo IP de origem para protegê-lo:

```
$ whois 104.28.22.57 | grep OrgName
OrgName:        IBM
```

Se você preferir efetuar bypass do CIS em um domínio (nós ainda resolveremos o DNS), o não proxy do registro será uma solução possível.

## Eu recebi um erro de validação DNS: 1004; o que posso fazer agora?

Para que as regras de página funcionem, o DNS precisa resolver para sua zona. Como resultado, deve-se ter um registro de DNS com proxy para sua zona. 
