---
copyright:
  years: 2018
lastupdated: "2018-03-01"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Herramientas útiles para gestionar el despliegue de CIS

Existen algunas herramientas de administración del sistema unix de dominio público que pueden ayudar a gestionar su despliegue de IBM CIS.

## Herramientas de sysadmin

 * whois (herramienta de identificación del dominio)
 * dig (herramienta de DNS)
 * curl (herramienta de HTTP y HTTPS)
 * netcat (herramienta de IP y puerto)
 * traceroute (herramienta de red)

## Herramientas comerciales para la prueba externa y remota:

 * GTMetrix (http)
 * Prueba de páginas web (http)
 * WhatsMyDNS (herramienta de DNS)
 * G Suite Toolbox (DNS y HTTP)

## Herramientas para buscar en los registros y en el historial

 * Archivos de archivado HTTP (archivos HAR)


### Uso de `whois`

`whois` es una herramienta de línea de mandatos del sistema unix que puede utilizar para buscar información del registrador para un nombre de dominio o una dirección IP determinados, por ejemplo, los servidores a los que se da autoridad del dominio o el propietario de una dirección IP en particular.

Ejemplos:

`whois example.com`

`whois 8.8.8.8`

### Uso de `dig`

`dig` es una herramienta de línea de mandatos de unix que puede realizar consultas DNS y comprobar registros DNS para un dominio específico. Es similar a `nslookup`.

El esquema de este mandato es: dig <tiporegistro. <nombredominio> <opciones>

**Ejemplos:**

`dig example.com`

`dig my.example.com`

`dig example.com +trace`

`dig NS example.com`

`dig example.com @ns.example.com`

### Uso de `cURL`

`cURL` es una herramienta de línea de mandatos de unix que permite transmitir datos utilizando sintaxis de URL. Se utiliza comúnmente para realizar solicitudes HTTP o comparar las respuestas del servidor.

El esquema para este mandato es: curl -option1 -option2 http://example.com/url

**Ejemplos:**

`curl -svo /dev/null http://www.example.com`

`curl -svo /dev/null -A “USER_AGENT_STRING” http://www.example.com`

`curl -svo /dev/null -H “host: www.example.com” http://ORIGIN_IP`

`curl -svo /dev/null -H https://www.example.com --resolve www.example.com:443:ORIGIN_IP`

### Uso de `mtr` y `traceroute`

MTR y `traceroute` son herramientas de línea de mandatos de unix que permiten medir el rendimiento o la latencia junto con una vía de acceso de la red específica a un host o servidor de destino especificado.

**Ejemplos:**

`mtr -rwc 20 example.com -T -4`
`mtr -rwc 20 8.8.8.8 -T -6`

`traceroute example.com -T -4`

`traceroute 8.8.8.8 -T -6`

| Opción | Definición |
|---------|-----------|
| -c | Establece el número de pings enviados |
| -T | Fuerza un traceroute de TCP (normalmente ICMP) |
| -4 | Fuerza el uso de IPv4 |
| -6 | Fuerza el uso de IPv6 |

### Generación de un archivo HAR

Un archivo HAR es un registro de solicitudes HTTP desde un navegador web. Los navegadores como Chrome tienen una sección Herramientas de desarrollador que puede ayudarle a configurar un archivo HAR.
