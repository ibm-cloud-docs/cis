---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: global load balancer, global load balancer configuration

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Definir o balanceador de carga global
{:#define-the-global-load-balancer}

Defina a configuração de seu balanceador de carga global especificando um nome de host, incluindo e ajustando seus conjuntos de origem e definindo regras adicionais para controlar como o tráfego é entregue aos clientes.

1. Crie seu balanceador de carga global clicando no botão Criar balanceador de carga à direita.  

2. Especifique o nome do host para seu domínio e ajuste o valor TTL, se desejado (o padrão é 60 segundos), e use **Incluir conjunto** para incluir seus Conjuntos de Origem. 

   <img src="images/reliability11.png" alt="desenho" style="width: 300px;"/>
   
   **NOTA:** nomes de host combinados com nomes de domínio formam nomes de domínio completos (FQDN) para seu aplicativo. Seus usuários finais se conectam ao seu aplicativo usando esse FQDN. 
   
3. Ajuste as prioridades relativas de seus conjuntos de origem clicando nas setas para cima e para baixo à esquerda do conjunto. As solicitações de aplicativo de usuários finais são atendidas no modo round-robin por esses conjuntos de origem. 
   
   <img src="images/reliability12.png" alt="desenho" style="width: 300px;"/>   
   
4. Opcionalmente, é possível definir regras adicionais para controlar como o tráfego é entregue a clientes de diferentes regiões geográficas. No exemplo abaixo, os clientes que chegam da região sul da América do Sul são roteados para o conjunto de origem da Costa Oeste dos EUA. É possível usar essas regras para direcionar os clientes para sua região mais próxima possível. Se qualquer uma dessas regiões falhar, as solicitações serão roteadas para outros locais funcionais disponíveis, para que os usuários finais não sejam afetados pelo tempo de inatividade. 

   <img src="images/reliability13.png" alt="desenho" style="width: 300px;"/>   
   
5. Clique em **Provisionar recursos** para concluir a configuração do seu balanceador de carga global. 
6. Finalmente, verifique a conectividade com o seu aplicativo digitando `URL do FQDN` em uma janela do navegador móvel. Se você conseguir se conectar, verá uma mensagem de boas-vindas.
