---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: configuration domain, Free Trial plan, CIS instance

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:faq: data-hd-content-type='faq'}



# Perguntas mais frequentes
{:#faq}

## O que aconteceu com o Plano Early Access que estava no catálogo?
{:#cis-faq-early-access-plan}
{: faq}

O Plano Early Access foi removido do Catálogo em 31 de maio de 2018. Ele foi substituído pelo plano pago Standard e por um novo plano de Avaliação grátis de 30 dias. Se tiver uma instância do Plano Early Access, faça upgrade para o plano Standard imediatamente para evitar a perda de dados, pois não será permitido criar uma instância de Avaliação grátis se você participou do beta Early Access.

## Quais são os benefícios de um plano de Avaliação grátis?
{:#cis-faq-free-trial-plan}
{: faq}

O plano de Avaliação grátis foi projetado para permitir apenas uma zona por conta. É recomendado que apenas uma instância seja criada por conta e que o nome da zona seja verificado. É crítico que o nome da zona seja verificado antes de ser incluído. Se uma zona for excluída, ela ou outra zona não poderá ser incluída durante o plano de Avaliação grátis.

## Quantas instâncias de Avaliação grátis posso ter?
{:#cis-faq-free-trial-instances}
{: faq}

É possível ter, no máximo, uma instância de Avaliação grátis por conta durante o tempo de vida da conta. Se você já tiver ou excluir uma instância de Avaliação grátis ou se ela expirar, você não terá permissão para criar outra. No entanto, é possível criar instâncias de outros tipos de planos pagos (por exemplo, Standard), independentemente de quaisquer avaliações grátis que possam ter sido criadas.

## Eu tenho uma instância de serviço assinada para o Plano Early Access. Posso mudá-la para uma Avaliação grátis?
{:#cis-faq-early-access-to-free-trial-plan}
{: faq}

Não. O upgrade do Plano Early Access pode ser feito somente para um plano pago, ou seja, neste momento, o plano Standard.

## Eu tive uma instância de Acesso Antecipado que I (pode ou não ter) excluído. Posso criar uma instância de Avaliação grátis agora?
{:#cis-faq-early-access-and-free-trial-plan}
{: faq}

Não. Cada conta tem direito a apenas uma instância grátis. Tanto o Plano Early Access quanto o plano de Avaliação grátis que o substituiu contam como planos grátis. Isso também significa que é possível ter no máximo uma instância de Avaliação grátis.

## Posso fazer downgrade do Standard para a Avaliação grátis?
{:#cis-faq-downgrade-standard-to-free-plan}
{: faq}

Não. Isso não é permitido.

## Minha Avaliação grátis expirou. Quais são as minhas opções?
{:#cis-faq-free-trial-plan-expired}
{: faq}

Para evitar qualquer perda de dados, deve-se fazer upgrade da Avaliação grátis para a Standard antes da data de expiração. Depois disso, suportamos somente o upgrade do plano ou a exclusão da instância do CIS. Se a instância não for excluída ou atualizada após 45 dias (a partir da inicialização da instância), o domínio de configuração, o GLB, os conjuntos e as verificações de funcionamento serão excluídos automaticamente.

## Como excluo minha instância do CIS?
{:#{:#cis-faq-delete-instance}
{: faq}

Para excluir uma instância do CIS, deve-se primeiro excluir todos os GLBs, conjuntos e verificações de funcionamento. Em seguida, exclua o domínio associado (zona). Acesse a página **Visão geral** e clique no ícone da lixeira próximo ao nome do domínio localizado na seção **Detalhes do serviço** para iniciar o processo de exclusão.

## Incluí um usuário em minha conta e dei a ele permissão para gerenciar instâncias do Internet Services. Por que esse usuário está enfrentando problemas de autenticação?
{:#cis-faq-user-authentication-issue}
{: faq}

É possível que você não tenha designado "funções de acesso de serviço" para o usuário. Observe que há dois conjuntos separados de funções: "acesso de plataforma" e "acesso de serviço". As funções de acesso de plataforma são necessárias para criar e gerenciar instâncias de serviço, mas as funções de acesso de serviço são necessárias para executar operações específicas de serviço em instâncias de serviço. No console, essas configurações podem ser atualizadas selecionando **Gerenciar > Segurança > Identidade e Acesso**.

## Por que meu domínio está no estado Pendente? Como ativá-lo?
{:#cis-faq-pending-domain}
{: faq}

Ao incluir um domínio no CIS, nós fornecemos alguns servidores de nomes para configurar em seu registro (ou em seu provedor DNS, se você estiver incluindo um subdomínio). O domínio ou subdomínio permanece no estado pendente até que você configure os servidores de nomes corretamente. Certifique-se de incluir ambos os servidores de nomes em seu registro ou provedor DNS. Periodicamente, nós varremos o sistema DNS público para verificar se os servidores de nomes foram configurados conforme o instruído. Assim que somos capazes de verificar a mudança do servidor de nomes (isso pode levar até 24 horas), nós ativamos seu domínio. É possível enviar uma solicitação para verificar novamente os servidores de nomes clicando em **Verificar novamente servidores de nomes** na página de visão geral.

## Qual é o registrar para meu domínio?
{:#cis-faq-who-is-registrar}
{: faq}

Consulte https://whois.icann.org/ para obter essas informações. **Nota**: deve-se ter o privilégio administrativo para editar a configuração de seu domínio no registro para atualizar ou incluir os servidores de nomes fornecidos para seu domínio ao incluí-lo no CIS. Se você não sabe quem é o registro para o domínio que você está tentando incluir no CIS, é improvável que você tenha permissão para atualizar a configuração de seu domínio no registro. Trabalhe com o proprietário do domínio em sua organização para fazer as mudanças necessárias.

## Eu desejo manter meu provedor DNS atual para meu domínio (example.com). Posso delegar um subdomínio (subdomain.example.com) de meu provedor DNS atual para o CIS?
{:#cis-faq-keep-current-dns-provider}
{: faq}

Sim. O processo é semelhante à inclusão de um domínio, mas em vez do registro, você trabalha com o provedor DNS para o domínio de nível superior. Ao incluir um subdomínio no CIS, você recebe dois servidores de nomes para configurar, como de costume. Você configura um registro do Servidor de Nomes (NS) para cada um dos dois servidores de nomes como registros de DNS em seu domínio que está sendo gerenciado pelo outro provedor DNS. Quando somos capazes de verificar se os registros NS necessários foram incluídos, nós ativamos seu subdomínio. Se você não gerencia o domínio de nível superior dentro de sua organização, deve-se trabalhar com o proprietário do domínio de nível superior para que os registros NS sejam incluídos.

## O que é TLS?
{:#cis-faq-what-is-tls}
{: faq}

TLS é um protocolo de segurança padrão para estabelecer links criptografados entre um servidor da web e um navegador em uma comunicação on-line. Um certificado TLS é necessário para criar uma conexão TLS com um website e é composto pelo nome de domínio, nome da empresa e dados adicionais como endereço da empresa, cidade, estado e país. O certificado também mostra a data de expiração e detalhes da Autoridade de Certificação (CA) emissora.

## Como o TLS funciona?
{:#cis-faq-how-does-tls-work}
{: faq}

Quando um navegador inicia uma conexão com um website protegido por TLS, ele primeiro recupera o Certificado TLS do site para verificar se o certificado ainda é válido. Ele verifica se a CA é uma que o navegador confia e se o certificado está sendo usado pelo website para o qual ele foi emitido. Se qualquer uma dessas verificações falhar, você receberá um aviso indicando que o website não está protegido por um certificado válido.

Quando um certificado TLS é instalado em um servidor da web, ele permite uma conexão segura entre o servidor da web e o navegador que se conecta a ele. A URL do website é prefixada com "https" em vez de "http" e um cadeado é exibido na barra de endereço. Se o website usa um certificado de validação estendida (EV), o navegador também pode mostrar uma barra de endereço verde.

## Por que eu vejo um aviso de privacidade?
{:#cis-faq-privacy-warning}
{: faq}

Os certificados TLS emitidos pelo IBM Cloud CIS cobrem o domínio-raiz (`example.com`) e um nível de subdomínio (`*.example.com`). Se você está tentando atingir um subdomínio de segundo nível (`*.*.example.com`), verá um aviso de privacidade
em seu navegador, porque esses nomes de host não são incluídos na SAN.

Além disso, permita até 15 minutos para que uma de nossas Autoridades de certificação (CAs) parceiras emita um novo certificado. Você verá um aviso de privacidade em seu navegador se o novo certificado ainda não tiver sido emitido.

## Por que vejo um erro de certificado SSL inválido?
{:#cis-faq-invalid-ssl-cert-error}
{: faq}

Se você vê "Erro 526, certificado SSL inválido" ao visitar seu site, isso pode significar que seu certificado de origem é inválido. Quando o proxy do CIS estiver ativado, um certificado válido assinado pela CA será necessário na origem no modo SSL padrão, que é o "Assinado completamente pela CA". Observe que a configuração padrão para o modo SSL era anteriormente "Completamente Flexível", o que ignora a validade do certificado apresentado pela origem. O novo padrão é aplicado apenas aos domínios incluídos novamente. Se seu domínio foi incluído quando o modo SSL padrão era Completamente Flexível, essa configuração não será sobrescrita. É possível mudar para um modo menos rígido, mas isso não é recomendado para ambientes de produção.

## O que é DDoS?
{:#cis-faq-what-is-ddos}
{: faq}

Um ataque distribuído por negação de serviço (DDoS) é uma tentativa de tornar um serviço on-line indisponível sobrecarregando-o com o tráfego de várias origens. Em um ataque DDoS, vários sistemas de computador comprometidos atacam um destino como um servidor, website ou outro recurso de rede, o que afeta os usuários do recurso de destino.

O fluxo de mensagens recebidas, solicitações de conexão ou pacotes malformados no sistema de destino o força a desacelerar ou até mesmo travar e encerrar, negando, assim, o serviço para legitimar usuários ou sistemas. Ataques DDoS têm sido realizados por diferentes agentes de ameaça, que vão desde hackers criminosos individuais até organizações criminosas e agências do governo.

## O que eu faço se estiver sob um ataque DDoS?
{:#cis-faq-what-to-do-in-ddos}
{: faq}

**Etapa 1:** ative o “Modo de defesa" na tela **Visão geral**. 

![Modo de defesa](images/defense-mode.png)

**Etapa 2:** configure seus registros DNS para o máximo de segurança.

**Etapa 3:** não defina um limite de taxa nem regule solicitações do IBM CIS. Precisamos da largura da banda para ajudá-lo com sua situação.

**Etapa 4:** bloqueie países específicos e visitantes se necessário.

## Eu recebi um erro 522, o que faço agora?
{:#cis-faq-522-error}
{: faq}

Um erro 522 indica que não conseguimos estabelecer uma conexão com o seu servidor de origem (ou seja, seu host). Após cerca de 15 segundos de falha de conexão, fechamos a conexão e exibimos uma página de erro 522.

Esse problema geralmente é causado pelo software do firewall ou de segurança que acidentalmente bloqueia nossos endereços IP. Como o CIS age como um proxy reverso, as conexões com seu site parecerão vir de um intervalo de IPs do CIS. Esse comportamento pode fazer com que alguns firewalls bloqueiem essas conexões, o que nos impede de entregar conteúdo para os visitantes de seu site adequadamente.

Para corrigir esse problema, peça ao host para incluir na lista de desbloqueio todos os intervalos de IP do CIS, que são listados [aqui](/docs/infrastructure/cis?topic=cis-ibm-cloud-cis-whitelisted-ip-addresses).

Todos esses IPs devem ser incluídos na lista de desbloqueio para evitar erros 522. Também convém verificar se quaisquer IPs nesses intervalos estão bloqueados.

Erros 522 também podem ser causados por problemas de conectividade de rede, portanto, confirme se seu servidor e sua rede geralmente estão operantes e não sobrecarregados.

Se, após tomar as etapas acima, você ainda receber erros, entre em contato com o suporte do IBM CIS e confirme o seguinte:

* Você incluiu nossos intervalos de IP na lista de desbloqueio
* Seu servidor/rede está on-line e geralmente operante

Se você contatar nossa equipe de suporte, forneça um ID do raio de um erro 522 recente. Podemos usar isso para determinar qual Data Center do CIS você estava acessando e executar testes adicionais.

## O que é um registro com proxy e por que eu preciso deles?
{:#cis-faq-proxied-record}
{: faq}

Os registros com proxy são registros que efetuam proxy de seu tráfego por meio do IBM CIS. Somente registros com proxy recebem benefícios do CIS, tal como o mascaramento de IP, em que um IP do CIS é substituído pelo IP de origem para protegê-lo:

```
$ whois 104.28.22.57 | grep OrgName
OrgName:        IBM
```

Caso prefira efetuar bypass do CIS em um domínio (nós ainda resolveremos o DNS), não incluir proxy no registro é uma solução possível.

## Eu recebi um erro de validação DNS: 1004; o que posso fazer agora?
{:#cis-faq-dns-validation-error}
{: faq}

Para que as regras de página funcionem, o DNS precisa resolver para sua zona. Como resultado, deve-se ter um registro de DNS com proxy para sua zona. 

## Posso incluir um CNAME para um registro raiz?
{:#cis-faq-add-cname-root-record}
{: faq}

Sim. O IBM CIS suporta um recurso chamado "Compactação de CNAME", que permite que nossos usuários incluam um CNAME como um registro raiz. Nossos servidores DNS autorizados enumeram os registros do destino CNAME e respondem com esses registros em vez do CNAME, ocultando efetivamente o fato de que o usuário configurou um CNAME na raiz do domínio.

## Qual é o tempo limite padrão da verificação de funcionamento?
{:#cis-faq-default-health-check-timeout}
{: faq}

O tempo limite padrão da verificação de funcionamento para os planos de Avaliação grátis e Standard é de 60 segundos.

## As verificações de funcionamento podem ser configuradas para um tráfego que não é HTTP/HTTPS?
{:#cis-faq-health-check-non-http-traffic}
{: faq}

Não, eles podem ser configurados apenas com HTTP/HTTPS.

## O GLB pode ser configurado para um tráfego que não é HTTP/HTTPS?
{:#cis-faq-glb-non-http-traffic}
{: faq}

Não, eles podem ser configurados apenas com HTTP/HTTPS.

## A desativação de todas as minhas origens em um conjunto de origem desativará o conjunto de origem inteiro?
{:#cis-faq-disabling-origins-disable-origin-pool}
{: faq}

Sim, se o conjunto de origem estiver sendo usado em um balanceador de carga, o tráfego será roteado para o próximo conjunto de prioridade mais alta ou para o conjunto de fallback.

## Há um erro em meu Ingresso do Kubernetes, o que faço?
{:#cis-faq-kubernetes-ingress-error}
{: faq}

O nome do host em um ingresso do Kubernetes deve consistir em caracteres alfanuméricos minúsculos, '-' ou '.' e deve começar e terminar com um caractere alfanumérico. O uso de `_` no nome do balanceador de carga, embora permitido, pode causar um erro de ingresso em clusters do Kubernetes. Recomendamos que você não use `-` no nome do balanceador de carga para evitar problemas com clusters do Kubernetes.

## Recebi um erro 502 ao tentar salvar uma ação do Edge Functions, o que faço?
{:#cis-faq-502-error}
{: faq}

Entre em contato com o [suporte IBM](/docs/infrastructure/cis?topic=cis-getting-help-and-support) e forneça o script que você estava tentando salvar.
