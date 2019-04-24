---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: CIS Rule Set, WAF settings, WAF CIS Rules

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# Configurações do WAF
{:#waf-settings}

A tabela a seguir mostra os recursos Firewalls de Aplicativo da Web (WAF) que podem ser tomadas. 


|Ação| Definição|
|---|---|
|Bloquear | Bloquear um ataque parará qualquer ação antes que ela seja postada em seu website.|
|Simular | Para testar em busca de falsos positivos, configure o WAF para o modo Simular, que registra a resposta para possíveis ataques sem desafiar ou bloquear.|
|Desafiar | Uma página de desafio solicita aos visitantes que enviem um CAPTCHA para continuar em seu website.|
|Configuração de limite ou sensibilidade | Configure regras para acionar mais ou menos, dependendo da sensibilidade.|

## Conjunto de Regras do CIS para o WAF
{:#cis-ruleset-for-waf}

Selecione **Visualizar regras do CIS** para revelar os conjuntos de regras desse pacote. A seguir, os conjuntos de regras:
  * Drupal
  * Flash
  * Joomla
  * Magento
  * Diversos
  * PHP
  * Plone
  * Especiais
  * WHMCS
  * Wordpress

**Especiais** contém uma série de regras apropriadas para praticamente todos os aplicativos e websites na Internet. Esse conjunto de regras é a base da segurança oferecida por nosso WAF, com regras que abordam ataques comuns, como SQLi, XSS e LFI. Recomendamos sempre deixar Especiais ativado.

Ative apenas os conjuntos de regras que correspondem à sua pilha de tecnologia. Por exemplo, se você usar o Wordpress, mas nenhuma das outras tecnologias, ative somente os conjuntos de regras Especiais e Wordpress. Evite ativar conjuntos de regras que não são relevantes para sua pilha de tecnologia.

Selecione qualquer um dos Conjuntos de regras específicos para ver detalhes adicionais sobre cada uma das regras incluídas.

O conjunto de regras do CIS permite executar quatro ações em cada regra:
  1. **Desativar**: Desativa a regra.
  2. **Simular**: registra o evento e não bloqueia nem desafia o visitante (ainda é possível decidir configurar para um bloqueio ou um desafio após a revisão de seus logs).
  3. **Bloquear**: O bloco simplesmente bloqueia o pedido completamente, sem opção de ignorá-lo para esse pedido.
  4. **Desafiar**: exibe uma página de desafio (CAPTCHA) que deve ser concluída antes que a solicitação em questão tenha o acesso permitido.

É possível observar que os nomes das regras não revelam exatamente como elas funcionam e que são, principalmente, um resumo geral de sua função. Isso é deliberado.  Para fins de segurança, não revelamos o código (ou outras informações exatas) que usamos para filtrar o tráfego. Isso evita que os agentes maliciosos realizem sua engenharia reversa para efetuar bypass em nossas defesas.
