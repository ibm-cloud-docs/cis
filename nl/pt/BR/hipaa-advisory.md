---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Advisory, Use of Caching, content caching, Cache-Control header

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Recomendação do HIPAA
{:#hipaa-advisory}

O uso do Armazenamento em Cache (CDN) para dados regulados (por exemplo, PHI, ITAR) é **proibido**. Todos os fluxos de dados regulados que usam o CIS devem ser configurados para **não armazenar em cache**.
{:important}

Há diversas maneiras de desativar o armazenamento em cache de conteúdo pelo CDN do CIS. 
- O servidor de origem pode configurar **no-cache** no cabeçalho **Cache-Control** para o conteúdo regulamentado
- Use as Regras de página do CIS para desativar o armazenamento em cache para qualquer conteúdo em um caminho especificado, mesmo se a origem não enviar um cabeçalho **no-cache** **Cache-Control**. 
