---
copyright:
  years: 2018
lastupdated: "2018-03-01"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Ferramentas úteis para gerenciar sua implementação do CIS

Existem algumas ferramentas de administração do sistema UNIX de domínio público que podem ajudá-lo a gerenciar sua implementação do IBM CIS.

## Ferramentas sysadmin

 * whois (ferramenta de identificação de domínio)
 * dig (ferramenta de DNS)
 * curl (ferramenta de HTTP e HTTPS)
 * netcat (ferramenta de IP e porta)
 * traceroute (ferramenta de rede)

## Ferramentas comerciais para testes externos e remotos:

 * GTMetrix (http)
 * Teste de página da web (http)
 * WhatsMyDNS (ferramenta de DNS)
 * G Suite Toolbox (DNS e HTTP)

## Ferramentas para examinar logs e histórico

 * Archives HTTP (arquivos HAR)


### Usando `whois`

`whois` é uma ferramenta de linha de comandos do sistema UNIX que pode ser usada para consultar informações de registro para um determinado nome de domínio ou endereço IP, por exemplo, os servidores autorizados fornecidos do domínio ou o proprietário de um endereço IP específico.

Exemplos:

`whois example.com`

`whois 8.8.8.8`

### Usando `dig`

`dig` é uma ferramenta de linha de comandos do UNIX que pode executar consultas DNS e verificar registros de DNS para um domínio específico. Ela é semelhante a `nslookup`.

O esquema desse comando é: dig <recordtype. <domainname> <options>

**Exemplos:**

`dig example.com`

`dig my.example.com`

`dig example.com +trace`

`dig NS example.com`

`dig example.com @ns.example.com`

### Usando `cURL`

`cURL` é uma ferramenta de linha de comandos do UNIX que permite transmitir dados usando a sintaxe de URL. Ela é comumente usada para fazer solicitações de HTTP ou comparar respostas do servidor.

O esquema para esse comando é: curl -option1 -option2 http://example.com/url

**Exemplos:**

`curl -svo /dev/null http://www.example.com`

`curl -svo /dev/null -A “USER_AGENT_STRING” http://www.example.com`

`curl -svo /dev/null -H “host: www.example.com” http://ORIGIN_IP`

`curl -svo /dev/null -H https://www.example.com --resolve www.example.com:443:ORIGIN_IP`

### Usando o `mtr` e `traceroute`

MTR e `traceroute` são ferramentas de linha de comandos do UNIX que permitem medir o desempenho ou a latência em um caminho de rede específico para um host ou servidor de destino especificado.

**Exemplos:**

`mtr -rwc 20 example.com -T -4`
`mtr -rwc 20 8.8.8.8 -T -6`

`traceroute example.com -T -4`

`traceroute 8.8.8.8 -T -6`

| Opção | Definição |
|---------|-----------|
| -c | Configura o número de pings enviados |
| -T | Força um rastreio de rotas TCP (normalmente ICMP) |
| -4 | Força o uso de IPv4 |
| -6 | Força o uso de IPv6 |

### Gerando um arquivo HAR

Um arquivo HAR é uma gravação de solicitações de HTTP de um navegador da web. Navegadores como o Chrome têm uma seção Ferramentas do Desenvolvedor que pode ajudá-lo a configurar e criar um arquivo HAR.
