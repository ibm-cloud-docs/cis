---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: range application, tls encryption, ddos protection, global tcp proxy

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Range
{:#cis-range}

O recurso Range traz proteção DDoS, balanceamento de carga e aceleração de conteúdo para qualquer protocolo baseado em TCP.
O Range é um Proxy TCP global em execução nos nós de borda do CIS/Cloudflare. 

O intervalo pode ser usado para: 
* Proteja suas portas e protocolos TCP contra ataques **DDoS de camada 3 e 4**. 
* Reduza a capacidade dos invasores bisbilhotarem e roubarem dados sensíveis ativando a **criptografia do TLS**.
* Integre-se ao CIS IP Firewall, que permite bloquear ou desafiar endereços IP ou intervalos de IP inteiros ao acessarem seus serviços TCP. 
* Configure os balanceadores de carga com verificações de funcionamento de TCP, failover e políticas de direção para determinar onde o tráfego deve fluir.

## Introdução ao Range
{:#getting-started-with-range}

O Range está disponível somente para clientes Enterprise por um custo adicional e é precificado por uso de largura da banda.
{:note}

### Incluir um aplicativo
{:#range-add-an-application}
Siga essas etapas para incluir um aplicativo.

1. Navegue até **Segurança > Range**
1. Clique no botão **Incluir aplicativo** 
1. Insira o nome do aplicativo no primeiro campo de entrada. Seu aplicativo se torna associado a um nome DNS em seu domínio do CIS.
1. Insira a porta de borda no próximo campo de entrada. Atenderemos as conexões com esses endereços recebidas nessa porta. As conexões com esses endereços são roteadas por proxy para a sua origem (a inclusão de proxy é suportada em todas as portas, exceto na 21).
1. Na seção Origem, insira o IP de origem e a Porta de seu aplicativo TCP. Também é possível selecionar um Load Balancer existente
1. Ative o Firewall de IP. Quando ativado, as regras de firewall com uma ação "bloquear" ou "incluir na lista de desbloqueio" são aplicadas para esse aplicativo. As regras baseadas em país ou ASN ainda não são suportadas.
1. Ative o Protocolo de Proxy se tiver um proxy sequencial que suporta PROXY Protocol v1. Esse recurso é útil se você está executando um serviço que requer conhecimento do verdadeiro IP do cliente. Na maioria dos casos, essa configuração deve permanecer desativada. 
1. Clique em **Provisionar**

O Protocolo de Proxy precede cada conexão com um cabeçalho que relata o endereço IP e a porta do cliente. Um cabeçalho do Protocolo de Proxy tem o formato: 
  * PROXY_STRING + single space + INET_PROTOCOL + single space + CLIENT_IP + single space + PROXY_IP + single space + CLIENT_PORT + single space + PROXY_PORT + "\r\n"
  * Aqui está uma linha de Protocolo de Proxy de exemplo para um endereço IPv4:
    `PROXY TCP4 192.0.2.0 192.0.2.255 42300 443\r\n`
  * Aqui está uma linha de Protocolo de Proxy de exemplo para um endereço IPv6:
    `PROXY TCP6 2001:db8:: 2001:db8:ffff:ffff:ffff:ffff:ffff:ffff 42300 443\r\n`
   
O fornecimento de um aplicativo Range incorrerá em custos adicionais, com base na quantia de largura da banda usada por aplicativo.
{:note}

Seu aplicativo agora está visível em um tile com as propriedades a seguir:
  * Nome do aplicativo
  * Porta de borda
  * Origem e porta
  * Conexões da última hora (pesquisadas a cada minuto)
  * Rendimento da última hora (pesquisado a cada minuto)
  * O menu overflow (canto superior direito) permite o seguinte 
    * Editar o aplicativo
    * Visualizar métricas para o aplicativo especificado
    * Excluir o aplicativo 
    
Quando um aplicativo Range é criado, ele é designado a um endereço IPv4 e IPv6 exclusivo. Esses endereços IP não são estáticos e podem estar sujeitos a mudanças. É possível determinar o endereço IP designado usando o DNS. O nome do DNS sempre retornará o IP endereçado que foi designado ao aplicativo.     
    
### Visualizar métricas
{:#range-view-metrics}
Agora, seu aplicativo está pronto para incluir proxy no tráfego TCP por meio da Cloudflare/CIS.

Navegue até **Métricas > Range** para visualizar seu número de Conexões com aplicativos e o tráfego de Rendimento.
Os gráficos mostram métricas para até 10 aplicativos. 
{:note}

As métricas do aplicativo podem ser comutadas por meio da tecla Gráfico ou clicando no botão **Selecionar aplicativos**. O prazo de dados das Métricas pode ser mudado usando o menu suspenso.

## AppTiles do Range
{:#range-apptiles}
Após a criação de alguns aplicativos, a página **Segurança > Range** será preenchida com os tiles de aplicativos. Os tiles de aplicativos contêm as informações a seguir:
* Nome do aplicativo
* Porta de borda
* Origem e porta
* Conexões da última hora (pesquisadas a cada minuto)
* Rendimento da última hora (pesquisado a cada minuto)


O tile do aplicativo também contém um menu overflow no canto superior (3 pontos). O menu overflow fornece aos usuários a opção de:
* editar o aplicativo
* visualizar as métricas para o aplicativo especificado
  * isso leva o usuário à página **Métricas > Range**, que exibe as métricas para apenas esse aplicativo
* excluir o aplicativo


## Exemplos de uso da API
{:#range-api-usage-examples}
Esses são exemplos para criar e listar aplicativos usando o Range.

### Criar o aplicativo Range
{:#create-range-app}
Há duas maneiras possíveis de designar uma origem em um aplicativo Range
1. IP de origem - usando o parâmetro `origin_direct`
2. Load Balancer - usando os parâmetros `origin_dns` e `origin_port`

**Solicitação:**
```
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps \
  -H 'X-Auth-User-Token: <token>' \
  -d '{"protocol":"tcp/22","dns":{"type":"CNAME","name":"ssh.example.com"},"origin_direct":["tcp://172.0.2.1:22"],"proxy_protocol":true,"ip_firewall":true}'

```
**Resposta:**
```
{
    "result": {
        "id": "4f70c3d4f20576b79135b898295e8093",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        }, "origin_direct": [
            "tcp://172.0.2.1:22"
        ],
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-09T17:33:09.190606Z",
        "modified_on": "2019-01-09T17:33:09.190606Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}
```

**Solicitação:**
```
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps \
  -H 'X-Auth-User-Token: <token>' \
  -d '{"protocol":"tcp/22","dns":{"type":"CNAME","name":"ssh.example.com"},"origin_dns": {"name": "test"},"proxy_protocol":true,"ip_firewall":true, "origin_port": 43}'

```
**Resposta:**
```
{
    "result": {
        "id": "4f70c3d4f20576b79135b898295e8093",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_dns": {
          "name": "test"
        },
        "origin_port": 43,
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-09T17:39:09.190606Z",
        "modified_on": "2019-01-09T17:39:09.190606Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}
```

**Nome do DNS:** seu aplicativo está associado a um nome do DNS em seu Domínio.

**Porta do protocolo/de borda:** essa é a porta na qual seu aplicativo está em execução. As conexões com esses endereços são roteadas por proxy para a sua origem.

**Origem direta:** Este é o IP no qual seu aplicativo está em execução e a porta que você deseja que o tráfego flua da borda para a sua origem.

**Firewall de IP:** se ativado, as regras de firewall com uma ação Bloquear são aplicadas para esse aplicativo Range.

**Protocolo de PROXY:** ative se tiver um proxy sequencial que suporte o PROXY Protocol v1. Na maioria dos casos, essa configuração permanece desativada.

**DNS de origem:** esse é o nome do balanceador de carga que você deseja configurar como sua origem.

**Porta de origem:** essa é a porta de seu serviço. 

### Listar todos os aplicativos
{:#range-list-all-apps}

**Solicitação:**
```
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps
```

**Resposta:**
```
{
    "result": [
        {
            "id": "4f70c3d4f20546b79135b898295e8093",
            "protocol": "tcp/22",
            "dns": {
                "type": "CNAME",
                "name": "ssh.example.com"
            }, "origin_direct": [
                "tcp://172.0.2.1:22"
            ],
            "ip_firewall": true,
            "proxy_protocol": true,
            "created_on": "2019-01-09T17:33:09.190606Z",
            "modified_on": "2019-01-09T17:33:09.190606Z"
        }
    ],
    "success": true,
    "errors": [],
    "messages": []
}
```

### Listar um aplicativo Range específico
{:#range-list-a-specific-range-app}
**Solicitação:**
```
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/ < url-encoded-crn>/zones/ < zona-d>/range/apps/apps/4f70c3d4f20546b79135b898295e8093
```

**Resposta:**
Aplicativo que usa o IP de Origem
```
{
    "result": {
        "id": "4f70c3d4f20546b79135b898295e8093",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        }, "origin_direct": [
            "tcp://172.0.2.1:22"
        ],
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-09T17:33:09.190606Z",
        "modified_on": "2019-01-09T17:33:09.190606Z"
    },
    "success": true,
    "errors": [],
    "messages": []
} 
```

Aplicativo que usa o Load Balancer
```
{
    "result": {
        "id": "555359036e7f4acc82d69b916f62caba",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_dns": {
            "name": "test_update"
        },
        "origin_port": 76,
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-10T22:26:47.167008Z",
        "modified_on": "2019-01-10T22:26:47.167008Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}

```
