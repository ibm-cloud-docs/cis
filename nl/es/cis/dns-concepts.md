---

copyright:
  years: 2018
lastupdated: "2018-03-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}


# Conceptos de DNS

Este documento contiene algunos conceptos y definiciones relacionados con el Sistema de nombres de dominio (DNS) de Internet y cómo afecta al despliegue de IBM Cloud Internet Services (CIS). 

El Sistema de nombres de dominio (DNS) respalda la web que utilizamos todos los días. Funciona de forma transparente en segundo plano, convirtiendo los nombres de sitios webs legibles por humanos en legibles por el sistema, direcciones IP numéricas que siguen las [directrices RFC 1918 de Internet para IPv4 y RFC 4193 para IPv6](https://en.wikipedia.org/wiki/Private_network). En resumen, los servidores DNS hacen coincidir los nombres de dominio, como 'ibm.com', con sus direcciones IP asociadas, que la mayoría de las personas no necesitan saber.

El sistema DNS busca esta información de dirección IP y nombre de host en una red de servidores DNS enlazados a través de Internet, de forma similar a cómo pueden buscar las personas un lugar utilizando una guía telefónica o un mapa.

## Servidores de nombres
Un **servidor de nombres** implementa servicios que proporcionan respuestas a preguntas en un servicio de directorio. Convierte la web significativa basada en texto o los identificadores de host en direcciones IP.

**Delegación de servidor de nombres** tiene lugar cuando un servidor de nombres para un dominio recibe una solicitud para los registros de un subdominio y responde con la referencia del servidor de nombres al servidor delegado. Esta función le permite descentralizar la gestión de un gran dominio (como, por ejemplo, `ibm.com`).

Un **servidor de nombres de dominio personalizado** le permite utilizar los servidores del proveedor de DNS con el nombre de referencia personalizado de su propio dominio. Por ejemplo, puede definir el servidor de nombres para que sea `ns1.cloud.ibm.com` en lugar `ns1.acme.com`.

## DNS seguro

**DNSSec** es una tecnología para 'firmar' digitalmente datos DNS para poder asegurarse de que sean válidos. Para eliminar la vulnerabilidad de Internet, DNSSec debe desplegarse en cada paso de la búsqueda, desde la zona raíz al nombre de dominio final (por ejemplo, www.icann.org).
