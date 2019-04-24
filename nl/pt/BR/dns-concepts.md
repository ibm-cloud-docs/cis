---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: domain name system, DNS servers, match domain names, DNS Concepts

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}


# Conceitos de DNS
{:#dns-concepts}

Este documento contém alguns conceitos e definições relacionados ao sistema de nome de domínio (DNS) da Internet e como ele afeta sua implementação do IBM Cloud Internet Services (CIS). 

O Sistema de Nomes de Domínio (DNS) impulsiona a web que usamos todos os dias. Ele funciona de forma transparente no segundo plano, convertendo nomes de website legíveis para humanos em nomes legíveis para computador, endereços IP numéricos que seguem as [diretrizes RFC 1918 da Internet para IPv4 e RFC 4193 para IPv6](https://en.wikipedia.org/wiki/Private_network). Em resumo, os servidores DNS correspondem a nomes de domínio, como `ibm.com`, para seus endereços IP associados, mas a maioria das pessoas não precisa saber disso.

O sistema DNS procurará essas informações de endereço IP e nome do host em uma rede de servidores DNS vinculados pela Internet, de forma semelhante a como as pessoas podem procurar um lugar usando uma lista telefônica ou um mapa.

## Servidores de nome
{:#dns-concepts-nameservers}

Um **servidor de nomes** implementa serviços que fornecem respostas para consultas com relação a um serviço de diretório. Ele converte identificadores da web ou de host baseados em texto significativos em endereços IP.

A **delegação de servidor de nomes** ocorre quando um servidor de nomes para um domínio recebe uma solicitação para registros de um subdomínio e responde com a referência do servidor de nomes ao servidor delegado. Esse recurso permite descentralizar o gerenciamento de um domínio grande (tal como `ibm.com`).

Um **servidor de nomes de domínio customizado** permite que você utilize os servidores do provedor DNS com o nome de referência customizado de seu próprio domínio. Por exemplo, é possível definir o servidor de nomes para ser `ns1.cloud.ibm.com` em vez de `ns1.acme.com`.

## DNS seguro
{:#dns-concepts-secure-dns}

**DNSSec** é uma tecnologia para 'assinar' digitalmente dados DNS para garantir sua validade. Para eliminar a vulnerabilidade da Internet, DNSSec deve ser implementado em cada etapa na consulta, da zona raiz para o nome do domínio final (por exemplo, www.icann.org).

## Compressão de CNAME do registro raiz
{:#dns-concepts-root-record-cname-flattening}

O IBM CIS suporta um recurso chamado "Compressão de CNAME". Usando esse método, os registros raiz podem superar a restrição IETF RFC que considera que, se um registro raiz for um CNAME, não poderá ter nenhum outro registro para esse domínio. Os servidores Autoritativos do CIS superam essa restrição retornando os registros A correspondentes ao destino do CNAME em vez de retornar o CNAME em si, ocultando efetivamente o CNAME. Essa técnica permite que outros registros, como os MX, sejam incluídos no domínio, mesmo que o registro raiz seja um CNAME.

## Incluindo um proxy para registros de DNS
{:#dns-concepts-proxying-dns-records}

O IBM CIS suporta a capacidade de alternar se um registro tem ou não proxy. Quando um registro tem proxy, isso significa que seu tráfego é executado diretamente por meio do IBM CIS. Atualmente, os registros com os tipos **A**, **AAAA** ou **CNAME** podem ter proxies.
