---
copyright:
  years: 2018
lastupdated: "2018-03-16"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Cómo IBM Cloud Internet Services (CIS) mantiene su trabajo seguro

IBM CIS es un servicio en la nube distribuido globalmente que bloquea las amenazas y limita los bots y los rastreadores abusivos, que pueden hacer perder el ancho de banda y los recursos del servidor. IBM CIS funciona como un proxy inverso HTTP(S) global y un proveedor de servicios DNS gestionado. El tráfico web se direcciona mediante nuestra red global inteligente para optimizar el rendimiento y la seguridad.

![security-graphic.png](images/security-graphic.png)

Aquí hay una visión general de características rápida:

## Características de seguridad

 * Cortafuegos de aplicaciones web (WAF)
 * Mitigación de DDoS ilimitado

## Estándares de seguridad y plataforma

 * TLS (SHA2 y SHA1)
 * IPv6
 * HTTP/2 y SPDY

## DNS

 * Red anycast global
 * DNSSEC

## Ataques de red y mitigación

Generalmente, vemos ataques que están en dos categorías

| Ataques de Capa 3 o de Capa 4 | Ataques de Capa 7 |
|------------------------------|-----------------|
|Estos ataques consisten en un desbordamiento de tráfico en ISO Capa 3 (la capa de red), como los desbordamientos de ICMP) o en la Capa 4 (la capa de transporte), como por ejemplo los desbordamientos de TCP SYN o los desbordamientos UDP reflejados) |Estos son ataques que envían solicitudes de ISO Capa 7 maliciosas (la capa de aplicación), como por ejemplo desbordamientos GET. |
| Se ha bloqueado automáticamente en nuestros límites | Los manejamos con “Modalidad de defensa”, WAF, y los Valores de nivel de seguridad |

## Resumen

 * La Modalidad de defensa prueba características de navegador que les faltan a muchos clientes maliciosos
 * WAF bloquea o cambia patrones de solicitudes conocidos que es probable que sean maliciosos
