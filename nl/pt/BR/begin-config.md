---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: global load balancer configuration, glb configuration

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}

# Iniciar a configuração do balanceador de carga global 
{:#begin-global-load-balancer-configuration}

Inicie a configuração de seu balanceador de carga global.

1. Na seção **Confiabilidade**, selecione **Balanceador de carga global**. 
    
    <img src="images/reliability6.png" alt="desenho" style="width: 300px;"/>

2. Role para baixo até a seção Verificações de funcionamento. 

   Essa configuração é opcional. Se não definir nenhuma verificação de funcionamento customizada, o sistema usará "/" como seu caminho de verificação de funcionamento padrão.
   {:note}

3. Clique no botão **Criar verificação de funcionamento** para definir uma verificação de funcionamento customizada.   

   Forneça o caminho no qual deseja conduzir suas verificações de funcionamento. É possível usar os protocolos HTTP ou HTTPS para suas verificações de funcionamento. 
   
4. Em **Opções avançadas**, é possível customizar outros parâmetros, como o intervalo de verificação de funcionamento, o número de novas tentativas, o método de solicitação e o corpo de resposta. 
   
   <img src="images/reliability7.png" alt="desenho" style="width: 300px;"/>
   
5. Clique em **Provisionar recurso** para concluir a configuração da verificação de funcionamento. 
