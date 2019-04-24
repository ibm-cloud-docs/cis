---
copyright:
  years: 2018
lastupdated: "2018-03-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Sobre o IBM Cloud Internet Services (CIS)
O IBM Cloud Internet Services (CIS) fornece um serviço da Internet rápido, altamente eficaz, confiável e seguro para clientes que executam seus negócios no IBM Cloud.   

O IBM CIS permite avançar rapidamente, estabelecendo para você padrões que podem ser mudados facilmente usando a API ou a IU. Aqui estão alguns parâmetros comumente mudados:

 * **Configurações de DNS**: é possível usar o IBM CIS para hospedar seu DNS ou você pode criar registros CNAME.
 * **Configurações de criptografia (TLS)**: o padrão é o modo `flexible`, que criptografa a conexão entre o host e o servidor de borda do IBM CIS, mas não criptografa a comunicação entre o servidor de borda do IBM CIS e o servidor de origem.

## Web Application Firewall (WAF)
O IBM CIS fornece o recurso Web Application Firewall (WAF), que examina o tráfego da web para procurar atividade suspeita. Ele pode filtrar o tráfego ilegítimo automaticamente, com base em conjuntos de regras, para ver solicitações da web baseadas em GET e POST. É possível usar vários conjuntos de regras para determinar qual tráfego bloquear, desafiar ou deixar passar. Nosso WAF pode bloquear spam de comentário, ataques cross-site scripting e injeções de SQL.

É possível ativar ou desativar o WAF ao seu critério. Recomendamos que você sempre o deixe ativado.

## Proteção contra ataques DDoS
O IBM CIS fornece proteção DDoS que se posiciona entre seu website e os invasores, independentemente do tamanho ou da duração do ataque.

## Balanceamento de carga
O Balanceamento de Carga do IBM CIS opera no nível DNS de autoridade. Ele incorpora verificações de funcionamento avançadas para monitorar o funcionamento das origens e ajusta dinamicamente as respostas de DNS. Além disso, é possível configurar políticas Geo para Balanceamento de Carga Global (GLB).

### Verificações de funcionamento
As Verificações de Funcionamento do Balanceamento de Carga são realizadas em URLs específicas por meio de solicitações de HTTP ou HTTPS periódicas e são configuradas com intervalos, tempos limites e códigos de status customizáveis. Quando um servidor de origem está marcado como inoperante, os visitantes são roteados para longe de falhas, usando nossas rotas de failover rápido.
 
### Políticas Geo e balanceamento de carga (GLB)
As políticas Geo fornecem o controle dos servidores de origem para os quais um determinado cliente é direcionado, com base no local geográfico desse cliente. Por exemplo, você poderia configurar suas políticas Geo para que os visitantes da Europa fossem enviados para a origem europeia mais próxima de seu website ou aplicativo, os visitantes dos EUA seriam enviados para uma origem na América do Norte, e assim por diante.

## Armazenamento em cache
O armazenamento em cache é uma maneira de armazenar seu conteúdo da web estático mais próximo dos visitantes de seu site, melhorando de maneira significativa o desempenho do website. Nosso ambiente de entrega distribuído globalmente permite que os proprietários de conteúdo da web forneçam uma experiência contínua, em todo o mundo.  
 
## Criptografia com TLS
A comunicação criptografada para seu website e a partir dele usando a Segurança da Camada de Transporte (TLS). Pode levar até 24 horas após o site se tornar ativo para que seus novos certificados sejam emitidos.

É possível localizar mais informações sobre TLS em nossa [FAQ](faq.html).
