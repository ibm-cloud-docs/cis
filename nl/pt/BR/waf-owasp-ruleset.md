---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: OWASP Rule Set, Rule Set

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# Conjunto de regras do OWASP para o WAF
{:#owasp-rule-set-for-waf}

O Conjunto de regras do OWASP contém regras de detecção de ataques genéricos. As regras do OWASP protegem contra muitas categorias de ataques comuns, incluindo Injeção de SQL, Cross-Site Scripting e Locale File Inclusion, entre outros. O IBM CIS fornece, mas não controla essas regras. O OWASP é um padrão de mercado que fornece uma boa linha de base de segurança. Veja os links a seguir para obter mais informações:
  * [OWASP no Github](https://github.com/SpiderLabs/owasp-modsecurity-crs)
  * [OWASP.org](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project)

## Gerenciando o OWASP
{:#managing-owasp}

Diferentemente do [conjunto de regras do CIS](/docs/infrastructure/cis?topic=cis-cis-rule-set-for-waf), o OWASP permite configurar a Sensibilidade.  Uma solicitação pode acionar um conjunto de regras do OWASP que tenha uma pontuação de gravidade de alta para baixa associada a ele. A pontuação final é calculada com base em todas as regras acionadas. Depois de calcular a pontuação final, o CIS a compara com o limite de sensibilidade selecionado no início e, em seguida, bloqueia ou permite a solicitação.

|Pontuação de sensibilidade| Limite do acionador|
|------|---------------|
|Baixo   |  60 e superior|
|Médio|  40 e superior|
|Alto  |  25 e mais alto|

Sugerimos que você configure a sensibilidade do OWASP para `baixo`. Se você a configurar para `alto`, verifique os logs no CIS e ajuste o conjunto de regras do OWASP para trabalhar para seu aplicativo.

Lembre-se de que as regras do OWASP podem ser apenas _ligadas_ ou _desligadas_, ao contrário das regras nos conjuntos de regras do CIS, que podem ser configuradas para _Desativar_, _Simular_, _Desafio_ ou _Bloquear_.

## Como lidar com falsos positivos?
{:#owasp-false-positives}

Os falsos positivos podem ocorrer quando a variável ou o valor é avaliado como _true_ ou _positivo_, mas é, na verdade, um negativo. No contexto do nosso WAF, um falso positivo significa que uma solicitação está bloqueada porque foi avaliada erroneamente como maliciosa.

Para lidar com falsos positivos e ter certeza de evitá-los no futuro, você deve saber como localizá-los e corrigi-los. Revise os logs das solicitações bloqueadas e, em seguida, avalie se elas foram bloqueadas adequadamente dentro do contexto do tráfego esperado e normal de seu website.
