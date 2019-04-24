---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: CIDR blocks, Whitelist Block Challenge, IBM Cloud Internet Services, security features

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Como o IBM Cloud Internet Services (CIS) mantém seu trabalho seguro
{:#how-cis-keeps-your-work-secure}

O IBM CIS é um serviço de nuvem distribuído globalmente que bloqueia ameaças e limita robôs e crawlers abusivos, os quais podem desperdiçar seus recursos de largura da banda e servidor. O IBM CIS funciona como um proxy reverso HTTP(S) global e um provedor de serviços DNS gerenciado. Seu tráfego da web é roteado por meio de nossa rede global inteligente para otimizar seu desempenho e sua segurança.

![security-graphic.png](images/security-graphic.png)

Aqui está uma visão geral rápida de recurso:

## Recursos de segurança
{:#cis-security-features}

 * Proxy [Registros DNS](/docs/infrastructure/cis?topic=cis-dns-concepts#proxying-dns-records) ou [GLB](/docs/infrastructure/cis?topic=cis-global-load-balancer-glb-concepts) para usar os recursos de segurança. Isso permite que o tráfego flua por meio de nossos servidores e, assim, os dados podem ser monitorados.
### Web Application Firewall (WAF)
{:#cis-web-application-firewall}

 * O WAF é implementado por meio de dois conjuntos de regras: [OWASP](/docs/infrastructure/cis?topic=cis-owasp-rule-set-for-waf) e [CIS](/docs/infrastructure/cis?topic=cis-waf-settings#cis-rule-set-for-waf).
### Mitigação de DDoS ilimitada
{:#cis-unlimited-ddos-mitigation}

 * A mitigação de DDoS é tipicamente um serviço caro, que pode encarecer ainda mais quando sob ataque. Incluímos a mitigação ilimitada de DDoS com o CIS sem nenhum custo adicional.

## Padrões de segurança e plataforma
{:#security-standards-and-platform}

 * TLS (SHA2 e SHA1)
 * IPv6
 * HTTP/2 e SPDY

## DNS
{:#cis-dns}

 * Rede anycast Global
 * DNSSEC

## Ataques de rede e mitigação
{:#network-attacks-and-mitigation}

Geralmente, vemos ataques que se enquadram em duas categorias

| Ataques de Camada 3 ou Camada 4 | Ataques de Camada 7 |
|------------------------------|-----------------|
|Esses ataques consistem em um fluxo de tráfego em ISO Camada 3 (a camada de rede), tais como sobrecargas de ICMP, ou em Camada 4 (a camada de transporte), tais como sobrecargas de TCP SYN ou sobrecargas de UDP refletidas |Esses são ataques que enviam solicitações ISO Camada 7 maliciosas (a camada de aplicativo), tais como sobrecargas GET.  |
| Automaticamente bloqueado em nossa borda | Nós manipulamos isso com “Modo de Defesa”, WAF e Configurações de nível de segurança |

## Firewall de IP
{:#cis-ip-firewall}

O IBM Cloud Internet Services oferece várias ferramentas para controlar seu tráfego para que você proteja seus domínios, URLs e diretórios com relação a volumes de tráfego, determinados grupos de solicitantes e solicitações de IPs específicos. Essa seção detalha as ferramentas disponíveis.

### Regras de IP
{:#cis-ip-rules}

As Regras de IP permitem que você controle o acesso para endereços IP específicos, intervalos de IP, países específicos, ASNs específicos e determinados blocos CIDR. As ações disponíveis em solicitações recebidas são:
  * Lista de desbloqueio 
  * Bloquear 
  * Desafio (Captcha) 
  * Desafio do JavaScript (desafio do IUAM)

Por exemplo, se você observar que um IP específico está causando solicitações maliciosas, será possível bloquear esse usuário por endereço IP.

### Regras de bloqueio de agente do usuário
{:#user-agent-blocking-rules}

As regras de Bloqueio de agente do usuário permitem que você tome ação em qualquer sequência de Agente do usuário selecionada. Esse recurso funciona como o Bloqueio de domínio, conforme descrito anteriormente, exceto pelo fato de que o bloco examina a sequência de Agente do usuário recebida em vez do IP. É possível escolher como manipular uma solicitação correspondente com a mesma lista de ações estabelecida nas Regras de IP (Bloqueio, Desafio e Desafio JS). Observe que o bloqueio de Agente do usuário se aplica a toda a sua zona. Não é possível especificar subdomínios da mesma maneira que Bloqueios de domínio.

Esta ferramenta é útil para bloquear qualquer sequência de Usuário-Agente que você considera suspeito. 

### Bloqueio de domínio
{:#cis-domain-lockdown}

O Bloqueio de domínio permite a você endereços IP e intervalos IP da lista de desbloqueio, de modo que todos os outros IPs são incluídos na lista de bloqueio. O Bloqueio de domínio suporta:

  * Subdomínios específicos. Por exemplo, é possível permitir o acesso de IP `1.2.3.4` ao domínio `foo.example.com` e o acesso de IP `5.6.7.8` ao domínio `bar.example.com`, sem necessariamente permitir o inverso.
  * URLs específicas. Por exemplo, é possível permitir o acesso de IP `1.2.3.4` ao diretório `example.com/foo/*` e o acesso de IP `5.6.7.8` ao diretório `example.com/bar/*`, sem necessariamente permitir o inverso.  Esse recurso é útil quando você precisa de mais granularidade em suas regras de acesso porque, com as Regras de IP, é possível aplicar o bloco a todos os subdomínios do domínio atual ou a todos os domínios em sua conta e não é possível especificar URIs.

### Passagem de desafio
{:#cis-challenge-passage}

Localizada nas configurações de segurança **Avançado**, essa configuração permite controlar por quanto tempo um visitante que passou por um desafio ou desafio JavaScript obterá acesso ao seu site até ser desafiado novamente. Isso é baseado no IP do visitante e, portanto, não se aplica aos desafios apresentados pelas regras do WAF, porque eles são baseados em uma ação que o usuário executa em seu site.

### Verificação de integridade do navegador
{:#cis-browser-integrity-check}

Essa configuração está localizada nas configurações de segurança **Avançado**. A verificação de integridade do navegador procura cabeçalhos HTTP que são comumente abusados por remetentes de spam. Ela impede que o tráfego com esses cabeçalhos acesse sua página. Também bloqueia ou desafia os visitantes que não têm um agente do usuário ou que incluem um agente do usuário que não seja padrão (essa tática é comumente usada por robôs de abuso, crawlers ou APIs).
