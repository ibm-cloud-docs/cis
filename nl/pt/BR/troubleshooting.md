---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM CIS connection, CIS network connection, Origin web server, troubleshooting

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Solucionando problemas de conexão de rede do CIS
{:#troubleshooting-your-cis-network-connection}

## Como sei se meus dados estão passando pela minha conexão do IBM CIS?
{:#how-do-i-know-if-my-data-is-passing-through-my-cis-connection}

O IBM Cloud Internet Services (CIS) usa cabeçalhos de HTTP, que ele pode ler, incluir ou modificar. O cabeçalho nos permite rastrear como uma solicitação foi roteada, usando um número CF-Ray. O número CF-Ray pode ser localizado por um comando `curl` ou com um plug-in do Google Chrome chamado "Claire".

Para saber se os dados passaram pelo IBM CIS, localize o `Ray ID` que estará presente em cada pacote.

**Ferramentas de linha de comandos do UNIX:**

 * curl para HTTP:
`$ curl -vso /dev/null http://example.com`

 * dig para DNS:
`$ dig www.example.com`

 * traceroute para rede:
`$ traceroute example.com`

**Por exemplo:
        **

Comando do terminal: `curl -svo /dev/null YOUR_URL_HERE. -L`

Resultados em: `CF-RAY: 1ca349b6c1300da3-SJC`

## Incluindo cabeçalhos CF-Ray

O cabeçalho CF-RAY é incluído para ajudar a rastrear uma solicitação para um website por meio da rede. Use-o ao trabalhar com o Suporte para ajudar a solucionar quaisquer problemas relacionados à conectividade. É possível revelar esse "Ray ID" em seus logs fazendo algumas edições nos arquivos de configuração no Apache e no nginx.

### Apache
{:#troubleshooting-cis-apache}

```
LogFormat "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-agent}i\" %{CF-Ray}i" cf_custom

CustomLog log/access_log cf_custom
```

### nginx
{:#troubleshooting-cis-nginx}

```
log_format cf_custom '$remote_addr - $remote_user [$time_local]  '
                    '"$request" $status $body_bytes_sent '
                    '"$http_referer" "$http_user_agent" '
                    '$http_cf_ray';

access_log  /var/log/nginx/access.log cf_custom;
```

## Como rastrear uma rota?
{:#how-do-i-trace-a-route}

Para ver se uma rota passa por seu caminho do IBM CIS, é possível executar um 'dig' em uma janela do Terminal para Mac ou Linux
ou usar `nslookup` no prompt de comandos para o Windows.

Se o pacote tiver um valor CF-Ray, ele viajou por meio do CIS.

O comando `traceroute` mostra o caminho inteiro que uma solicitação de IP usou.

A equipe de suporte faz uso desses comandos para ajudá-lo.

## Ao ver um aviso de privacidade
{:#troubleshooting-cis-privacy-warning}

Os certificados emitidos pelo IBM CIS cobrem o domínio-raiz (`example.com`) e um nível de subdomínio (`*.example.com`). Se você está tentando atingir um subdomínio de segundo nível (`*.*.example.com`), verá um aviso de privacidade em seu navegador, porque esses nomes de host não são incluídos na SAN.

Além disso, permita até 15 minutos para que uma de nossas Autoridades de certificação (CAs) parceiras emita um novo certificado. Você verá um aviso de privacidade em seu navegador se o novo certificado ainda não tiver sido emitido.

## O que eu faço se estiver sob um ataque DDoS?
{:#troubleshooting-cis-ddos-attack}

 * **Etapa 1:** ative o "Modo de Defesa" de seu painel
 * **Etapa 2:** configure seus registros de DNS para segurança máxima
 * **Etapa 3:** não faça solicitações de limite de taxa ou regulagem por meio do IBM CIS
 
Durante o "Modo de Defesa", cada novo visitante é atendido com um desafio de segurança "Captcha", pelo qual ele deve passar antes de ser fornecido um cookie para acesso ilimitado. Dessa maneira, o tráfego de botnet é bloqueado até que o "Modo de Defesa" seja desligado. Visitantes que não atendem ao desafio de segurança são incluídos no banco de dados de Reputação de IP (inválido).

## Outros problemas que podem ser encontrados
{:#troubleshooting-cis-other-problems}

A seguir estão algumas mensagens de erro comuns que você ou sua equipe de suporte poderá ver:

| Código de Erro    | Razão |
| ------------- | ------------- |
| 1001  | Erro de resolução de DNS. O cliente recentemente se inscreveu e suas informações de DNS ainda não foram propagadas ou quem quer que esteja gerenciando o DNS tem uma falha. |
| 521  | Servidor da web de origem recusou a conexão do CIS. O servidor da web de origem não está em execução ou algo está bloqueando endereços IP do IBM CIS. |
| 522  | Tempo limite de conexão com o servidor de origem (padrão de 30 segundos). O CIS pode ter a taxa limitada, o servidor da web pode estar consumindo todos os recursos (servidor compartilhado) ou pode haver problemas de conectividade de rede entre o servidor da web e o IBM CIS. |
| 523  | O servidor de origem está inacessível. Assegure-se de que o endereço IP de origem para o registro de DNS seja o mesmo que aquele que aparece na página Configurações de DNS do CIS. |
| 524  | O IBM CIS pôde estabelecer uma conexão TCP, mas não recebeu uma resposta do servidor da web. Um aplicativo de longa execução ou consulta de banco de dados está interferindo. |

### Não vejo nenhum tráfego de rede
{:#troubleshooting-cis-network-traffic}

Se você não está vendo o tráfego e está usando um CNAME, certifique-se de que haja um redirecionamento em vigor, nesse caso, o tráfego não está sendo roteado para o domínio-raiz. Lembre-se de que algumas propagações de DNS podem levar até 48 horas para serem concluídas.

### Website off-line
{:#troubleshooting-cis-website-offline}

Aqui está o que você pode ver:

`IBM CIS cannot connect to the origin server (error 521, 522, 523)`.

**Website off-line - nenhuma versão em cache**

1. O servidor está on-line, mas está bloqueando a solicitação do IBM CIS.
2. O servidor de origem está off-line e o IBM CIS não tem uma imagem de website de backup. 

O que você pode fazer:

* Verifique se os endereços IP do IBM CIS estão incluídos na lista de desbloqueio.
* Certifique-se de que os IPs do IBM CIS não estejam sendo limitados por taxa.
* Aqui está a lista de [IPs para a lista de desbloqueio](/docs/infrastructure/cis?topic=cis-ibm-cloud-cis-whitelisted-ip-addresses)

### Erro 502 “O temido 502”
{:#troubleshooting-cis-502-error}

Esse erro é um dos mais comuns que você pode ver. Ele geralmente ocorre quando uma parte de uma rede está indisponível, por exemplo, no início de um ataque DDoS. Um data center específico pode estar indisponível por um tempo. O tráfego será roteado novamente. Execute um rastreio de rotas. 

Aqui está o que você pode ver: `Error 502 - bad gateway error`

O que aconteceu:

* Uma parte da rede do IBM CIS está tendo um problema.
* Geralmente, o problema é limitado a um servidor em um data center.
* Isso afeta apenas uma parte dos visitantes do site.
* A equipe IBM CIS Technical Operations lida com isso.

O que você pode fazer:

* Envie os resultados de `www.YOUR_DOMAIN.com/cdn-cgi/trace` em um chamado para [Suporte](/docs/get-support?topic=get-support-getting-customer-support).
* Alterne temporariamente seus Registros do DNS para desativado (sem proxy).

