---
copyright:
  years: 2018
lastupdated: "2018-03-06"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Conjunto de regras padrão WAF

| Regra | Ação |
|----------|---------------|
|Botnet de números|desafiar
|Botnet CtrlFunc|desafiar
|LFI genérico com relação a caminhos comuns em ARGS|bloquear
|Regra de Inclusão de Arquivo Local Genérico com aprimoramentos|simular
|LFI genérico com relação a caminhos comuns no URI|bloquear
|LFI genérico com relação a caminhos comuns no URI sem pós-processamento|bloquear
|RCE genérico com relação a comandos comuns|bloquear
|RCE genérico com relação a comandos shell|bloquear
|RCE genérico com relação a comandos de rede comuns|simular
|Evitar RCE com relação à família nc de comandos|bloquear
|Análise de SQLi|bloquear
|Bloquear evasão de função de sequência de caracteres SQLi|bloquear
|Bloquear evasões de concatenação de sequência de SQLi|bloquear
|Bloquear análise de suspensão de SQLi|bloquear
|Bloquear análise de suspensão de SQLi (aguardar)|bloquear
|Tentativa de SQLi (Condicional) |bloquear
|Tentativa de SQLi (Where)|bloquear
|Tentativa de SQLi (IS NULL)|bloquear
|Tentativa de SQLi (Equação) []|bloquear
|Tentativa de SQLi (Comparação Matemática) []|bloquear
|Tentativa de SQLi (Comparação Matemática) Beta []|simular
|Tentativa de SQLi (Comparação End) PATH []|bloquear
|Tentativa de SQLi (Comparação End) URI []|bloquear
|Tentativa de SQLi (Comparação End) ARGS []|bloquear
|Tentativa de SQLi (Evasão de Subconsulta) []|bloquear
|Tentativa de SQLi (Evasão de Curinga) []|bloquear
|Tentativa de SQLi (Função Antecipada) []|bloquear
|Tentativa de SQLi (Função Integrada) []|simular
|Tentativa de SQLi (Função Multinível) []|bloquear
|Tentativa de SQLi (Vetor de União) []|simular
|Análise de SQLi|bloquear
|Desaprovar comentários de SQLi  |bloquear
|Desaprovar que as sequências terminem em comentários de SQLi |simular
|Tentativa de SQLi (Escape de Curinga)|bloquear
|Bloquear cabeçalhos X-Forwarded-Host inválidos |desafiar
|Bloquear solicitações para sistemas de controle de versão|bloquear
|Bloquear Uau! Robô de Comentário de Sinal|bloquear
|CVE-2014-6271 - ShellShock|bloquear
|CVE-2014-6271 - ShellShock|bloquear
|Sobrecarga de DDoS comum|desafiar
|Análise de XSS comum|desafiar
|Análise de XSS com palavra-chave de alerta|desafiar
|Análise de XSS com tags de script|bloquear
|Análise de XSS com eventos Javascript|bloquear
|Análise de XSS com eventos Javascript (Estrito)|desafiar
|Análise de XSS com URI Javascript|desafiar
|XSS oculto em URIs de dados base64 |desafiar
|Evasão de detecção XSS atob()|bloquear
|Evasão de detecção eval() XSS|bloquear
|Evasão de detecção eval() XSS leniente|simular
|Bloquear crawler semalt|bloquear
|Descartar robô DDoS espaçado|bloquear
|Parar cabeçalhos de cookie nulo|bloquear
|Desaprovar identificações de código do PHP em cabeçalhos|bloquear
|Bloquear Agentes do Usuário Mozilla formatados incorretamente|bloquear
|Análise XSS Genérica|desafiar
|Tentativa de XSS SVG|desafiar
|Evitar IIS DoS - CVE-2015-1635 []|bloquear
|Evitar que googlebots falsos efetuem crawl|bloquear
|Evitar que bingbots falsos efetuem crawl|bloquear
|Evitar que BaiduBots falsos efetuem crawl|bloquear
|Evitar que yandexbot falso efetue crawl|bloquear
|Bloquear agentes do usuário baidu falsos usados em ataques DoS|bloquear
|Bloco tentativas de obter informações que podem revelar informações sobre o servidor de origem|bloquear
|Impedir o acesso a extensões que podem ser utilizadas por editores de texto durante salvamento/backup |bloquear
|Bloquear tentativas de acessar a página de status do Apache /server-status|simular
|Eliminar análises do scanner Acunetix|desafiar
|Eliminar análises Java do scanner Acunetix|desafiar
|Injeção de SQL CVE-2015-7857 Joomla|bloquear
|Registrar quando dois cabeçalhos do host são enviados com uma solicitação|simular
|Detecção de IE6 falso [Tipo B]|desafiar
|Detecção de IE6 falso [Tipo C]|desafiar
|Bloquear agentes do usuário do Google Chrome falsificados/corrompidos|bloquear
|Bloquear tentativas de injeção de cabeçalho de alias nginx|desafiar
|Bloquear bruteforces de login conhecidas|desafiar
|Bloquear tentativa de explorações contra Imgmagik CVE-2016-3714 |bloquear
|Bloquear tentativa de explorações contra GraphicsMagick CVE-2016-5118 |bloquear
|RCE PHPMailer - CVE-2016-10033 Tipo A|bloquear
|RCE PHPMailer - CVE-2016-10033 Tipo B|bloquear
|Bloquear tentativas de exploração de CVE-2017-5638 (Content-Type)|bloquear
|Evitar tentativas de IIS RCE CVE-2017-7269|bloquear
|Tentativa de inclusão de SSI Struts / OGNL (CVE-2017-9791 etc.)|bloquear
|Bloquear tentativas de injeção de SQL 'drop table ...' []|simular
|Bloquear solicitações de HTTP com agente do usuário que corresponde apenas a 26 caracteres alfabéticos|bloquear
|Eliminar solicitações com X-Requested-With tendo um ID do APK do ataque de resistência|simular
|Descartar solicitações de correspondência de CVE-2017-9805|bloquear
|Análise de comentário de SQLi|simular
|Tentativa de SQLi []|simular
|Tentativa de SQLi []|bloquear
|Comentários de parâmetro cruzado de SQLi []|simular
|Análise de XSS com eventos Javascript|simular
|Proteção de RFI executável|simular
|Proteção de RFI redirecionada|simular
|SQLi para UNION SELECT ALL NULL|simular
|CVE-2017-7525 - RCE Struts / Jackson|bloquear
|UA falsificada :: Tentativa de Força Bruta|desafiar
|UA falsificada :: usado em bruteforce do Wordpress|desafiar
|UA falsificada :: usado em bruteforce do Wordpress|desafiar
|UA falsificada :: usado em bruteforce do Wordpress|desafiar
|UA falsificada :: usado em bruteforce do Wordpress|desafiar
|UA falsificada :: usado em bruteforce do Wordpress|desafiar
|UA falsificada :: usado em bruteforce do Wordpress|desafiar
|Bloqueio de vulnerabilidade mfunc do WordPress|bloquear
|Bloco de favicon CDorked.A|bloquear
|Regra para Minimizar Atlassian Confluence Security Advisory 2015-01-21|desafiar
|Explorar SQLi de Login de DB 28129 Practico CMS|bloquear
|WebHive LOIC|desafiar
|Script de ataque UITSEC|bloquear
|CVE-2013-2251 - Apache Struts RCE|simular
|Eliminar solicitações que tentam explorar CloudBees Jenkins RCE (CVE-2017-1000353)|simular
|Mitigação para Apache Tomcat CVE-2016-6816|bloquear
|Bloquear Solicitações Grandes para xmlrpc.php para Drupal CMS|bloquear
|Bloquear solicitações com argumentos de matriz estranhos|bloquear
|Bloquear atualização de Rosetta|desafiar
|Bloquear atualização de Rosetta|desafiar
|Exploração de JCE Joomla|bloquear
|Eliminar tentativa de RCE Usuer-Agent/X-Forwarded-For contra Joomla. CVE-2015-8562|bloquear
|Bloquear registro do usuário não autorizado em Joomla CVE-2016-8870|bloquear
|Bloquear registro do usuário não autorizado em Joomla CVE-2016-8869|bloquear
|Bloquear elevação de privilégio baseada em grupo CVE-2016-9838|bloquear
|Bloquear com_fields SQLI em Joomla|bloquear
|Bloquear com_fields SQLI em Joomla|bloquear
|Bloqueia a exploração de Magento rotulada como SUPEE-5344|bloquear
|Desaprovar arquivos de configuração Magento de serem atingidos APPSEC-1421|bloquear
|Desaprovar RCE apesar da API Magento APPSEC-1420 (Tipo A)|bloquear
|Desaprovar RCE apesar da API Magento APPSEC-1420 (Tipo B)|bloquear
|Exploração de Execução de Código Remota Apache / PHP 5.x|desafiar
|Desaprovar URIs php:// para evitar RCE e LFI|bloquear
|Desaprovar PHP ofuscado para evitar RCE|bloquear
|Solicitação Plone proibida|bloquear
|Vulnerabilidade de WHMCS 5.2.7|bloquear
|Vulnerabilidade de WHMCS 5.2.8|bloquear
|Vulnerabilidade do WHMCS 2.5.10|bloquear
|Bloqueador Pingback do WordPress|desafiar
|Desativar WAF para wp-admin|ativar
|Desativar WAF para post.php do WordPress|ativar
|Explorar Injeção de SQL DB 28485 Blind|bloquear
|Proteção do Jetpack do Wordpress|bloquear
|Desaprovar timthumb em pull de arquivos php|bloquear
|Bloquear scripts dinâmicos em diretórios de cache|bloquear
|Desaprovar timthumb em pull de origens externas|simular
|Yoast WordPress - SQLi Blind|bloquear
|Bloquear nomes de host anormalmente longos em pingbacks|bloquear
|Bloquear comentários anormalmente longos|bloquear
|Bloquear Ataque TwentyFifteen DOM XSS|bloquear
|Impedir Injeção de SQL CVE-2015-2213 no sistema de comentários|bloquear
|Corrigir RCE em EWWW Image Optimizer para WordPress|bloquear
|Desativar WAF para solicitações de backup do VaultPress verificado|ativar
|Evitar Mailport RCE por meio de upload de arquivo|bloquear
|Evitar RCE via upload na Régua de Controle de Revolução|bloquear
|Evitar que arquivos em unpackers de atualização sejam executados|bloquear
|Evitar RCE via upload em Formulários de Gravidade|bloquear
|Evitar abuso contra Tipo A da API wp-json|bloquear
|Evitar abuso contra Tipo B da API wp-json|bloquear
|Evitar abuso contra Tipo C da API wp-json|simular
|Proteção LFI de wp-config.php|bloquear
|Eliminar XML no campo de metadados de postagem do gabinete|bloquear
|CVE-2018-6389: descartando solicitações que tentam ataques de Amplificação DoS do script JS|simular
