---
copyright:
  years: 2018
lastupdated: "2018-03-13"
---

# Conceitos de armazenamento em cache

Este documento contém alguns conceitos e definições relacionados ao armazenamento em cache e como ele afeta sua implementação do IBM CIS.

## O que é armazenamento em cache?

O armazenamento em cache é o processo de armazenar arquivos em nossos servidores de borda, o que fazemos com o objetivo de melhorar o tempo de resposta ao servir esses arquivos para os clientes. Armazenando os arquivos mais perto dos clientes, podemos diminuir o tempo que leva para que os dados sejam transmitidos ao longo da rede, o que geralmente é chamado de **latência**.

Por padrão, nós armazenamos em cache **arquivos estáticos**, que incluem muitos tipos de arquivos de imagem e texto (arquivos não HTML). Por padrão, nós não armazenamos arquivos HTML em cache, porque não os consideramos estáticos; no entanto, é possível armazenar arquivos HTML em cache [usando o recurso de Regras de Página](using-page-rules.html).

Os arquivos armazenados em cache têm um tempo de expiração especificado, **Tempo de vida (TTL)** após o qual eles são eliminados do cache. Também é possível limpar arquivos do cache manualmente. Depois que os arquivos são removidos do cache, o CIS volta ao seu servidor de origem para recarregar seus arquivos e atualizar o cache com as versões mais recentes.

Uma explicação mais detalhada das configurações de cache e de suas opções de armazenamento em cache pode ser localizada no [tutorial Armazenamento em cache e regras de página](caching-with-page-rules.html).
