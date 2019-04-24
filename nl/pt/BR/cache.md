---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM CIS deployment, query strings, HTML files

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Conceitos de armazenamento em cache
{:#caching-concepts}

Este documento contém alguns conceitos e definições relacionados ao armazenamento em cache e como ele afeta sua implementação do IBM CIS.

## O que é armazenamento em cache?
{:#what-is-caching}

O armazenamento em cache é o processo de armazenar arquivos em nossos servidores de borda, o que fazemos com o objetivo de melhorar o tempo de resposta ao servir esses arquivos para os clientes. Armazenando os arquivos mais perto dos clientes, podemos diminuir o tempo que leva para que os dados sejam transmitidos ao longo da rede, o que geralmente é chamado de **latência**.

Os arquivos armazenados em cache têm um tempo de expiração especificado, **Tempo de vida (TTL)** após o qual eles são eliminados do cache. Também é possível limpar arquivos do cache manualmente. Depois que os arquivos são removidos do cache, o CIS volta ao seu servidor de origem para recarregar seus arquivos e atualizar o cache com as versões mais recentes.

Uma explicação mais profunda das configurações de cache e de suas opções de armazenamento em cache pode ser localizada no [tutorial Armazenamento em cache e regras de página](/docs/infrastructure/cis?topic=cis-use-page-rules-with-caching).

### Qual conteúdo é armazenado em cache?
{:#what-content-is-cached}

Por padrão, nós armazenamos em cache **arquivos estáticos**, que incluem muitos tipos de arquivos de imagem e texto (arquivos não HTML). Isso inclui somente arquivos de seus websites e não recursos de terceiros de sites de rede social, etc. Além disso, atualmente, não armazenamos em cache por tipo MIME.

### Como armazenar em cache o HTML? 
{:#how-do-i-cache-html}

Não armazenamos em cache arquivos HTML por padrão porque não os consideramos estáticos, no entanto, se o HTML estático puder ser claramente distinguido do dinâmico, será possível armazenar em cache seus arquivos [usando o recurso Regras de Página](/docs/infrastructure/cis?topic=cis-use-page-rules).


## Classificação de sequências de consulta
{:#query-string-sorting}

O CIS **Apenas corporativo** trata as URLs que possuem sequências de consultas em ordens diferentes como arquivos separados no cache. Isso significa que se um usuário solicitar:

`/video/123456?title=0&byline=0&portrait=0&color=987654`

E outro usuário solicita:

`/video/123456?byline=0&color=987654&portrait=0&title=0`

O CIS volta para a origem, mesmo que tenhamos o arquivo em nosso cache.

A Sequência de Consultas Classifica as sequências de consultas _antes_ de atingem nosso cache, resultando em uma taxa de acertos de cache mais alta. Ative a Classificação de sequências de consultas usando a alternância na página **Armazenamento em cache**.

## Fornecer conteúdo antigo
{:#serve-stale-content-caching}

Mantém uma versão limitada do site on-line se o servidor fica inativo. Mesmo se tiver expirado, o CIS continuará entregando o conteúdo em cache aos usuários quando os servidores de origem estiverem off-line.
