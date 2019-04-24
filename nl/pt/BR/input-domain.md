---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: domain Input information, IBM Cloud Internet Service, Domain Name

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Inserir informações sobre seu domínio
{:#input-information-about-your-domain}

Insira informações sobre o domínio que deseja proteger e para o qual deseja fornecer o balanceamento de carga global.

1. Clique em **Visão geral** no lado esquerdo da tela Introdução. Insira seu Nome de Domínio (ou Nome de Subdomínio) e clique em **Incluir domínio**. 
    
    <img src="images/reliability3.png" alt="desenho" style="width: 300px;"/>
    
    O IBM Cloud Internet Service não é um registrador de DNS, portanto, esse domínio (ou subdomínio) deve ter sido criado anteriormente.
    {:note}

    Na seção Detalhes do serviço, você perceberá que o domínio incluído recentemente será inicialmente mostrado em um estado Pendente. 

    <img src="images/reliability4.png" alt="desenho" style="width: 300px;"/>    

2. Navegue até a página de administração de seu domínio com seu respectivo registrador de DNS e delegue seu domínio/subdomínio a servidores de nomes da IBM definindo registros de DNS.

É possível que você tenha que esperar até 24 horas para que suas informações sejam replicadas no banco de dados DNS. Assim que forem, o estado de seu domínio será mudado para Ativo. 

<img src="images/reliability5.png" alt="desenho" style="width: 300px;"/>    
