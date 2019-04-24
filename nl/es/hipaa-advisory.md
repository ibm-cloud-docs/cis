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

# Advertencia de HIPAA
{:#hipaa-advisory}

El uso de almacenamiento en memoria caché (CDN) para datos regulados (por ejemplo, PHI, ITAR) está **prohibido**. Todos los flujos de datos regulados que utilizan CIS se deben establecer en **no guardar en caché**.
{:important}

Hay varias formas de inhabilitar el almacenamiento en memoria caché del contenido por parte de CIS CDN. 
- El servidor de origen puede establecer **no-cache** en la cabecera **Cache-Control** para el contenido regulado
- Utilice las reglas de página de CIS para inhabilitar el almacenamiento en memoria caché de cualquier contenido en una vía de acceso especificada, aunque el origen no envíe una cabecera **no-cache** **Cache-Control**. 
