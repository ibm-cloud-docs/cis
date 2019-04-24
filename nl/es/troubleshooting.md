---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM CIS connection, CIS network connection, Origin web server, troubleshooting

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Resolución de problemas de la conexión de red CIS
{:#troubleshooting-your-cis-network-connection}

## ¿Cómo sé si mis datos pasan a través de mi conexión IBM CIS?
{:#how-do-i-know-if-my-data-is-passing-through-my-cis-connection}

IBM Cloud Internet Services (CIS) utiliza cabeceras HTTP, que puede leer, añadir o modificar. La cabecera nos permite rastrear cómo se ha direccionado una solicitud, utilizando un número CF-Ray. El número CF-Ray se puede encontrar mediante un mandato `curl` o con un plugin de Google Chrome llamado "Claire".

Para saber si los datos se pasan a través de IBM CIS, localice el `Ray ID` que estará presente en cada paquete.

**Herramientas de línea de mandato de Unix:**

 * curl for HTTP:
`$ curl -vso /dev/null http://example.com`

 * dig for DNS:
`$ dig www.example.com`

 * traceroute for network:
`$ traceroute example.com`

**Por ejemplo:**

Mandato terminal: `curl -svo /dev/null YOUR_URL_HERE. -L`

Resultados en: `CF-RAY: 1ca349b6c1300da3-SJC`

## Adición de cabeceras CF-Ray

La cabecera CF-RAY se añade para ayudar a rastrear una solicitud a un sitio web a través de la red. Utilícela al trabajar con el equipo de soporte para ayudar a resolver problemas relacionados con la conectividad. Puede revelar este "ID de Ray" en los registros editando los archivos de configuración de Apache y nginx.

### Apache
{:#troubleshooting-cis-apache}

```
LogFormat "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-agent}i\" %{CF-Ray}i" cf_custom

CustomLog log/access_log cf_custom
```

### nginx
{:#troubleshooting-cis-nginx}

```
log_format cf_custom '$remote_addr - $remote_user [$time_local]  '
                    '"$request" $status $body_bytes_sent '
                    '"$http_referer" "$http_user_agent" '
                    '$http_cf_ray';

access_log  /var/log/nginx/access.log cf_custom;
```

## ¿Cómo rastreo una ruta?
{:#how-do-i-trace-a-route}

Para ver si una ruta pasa a través de su vía de acceso de IBM CIS, puede realizar una ‘profundización’ en una ventana del Terminal para Mac o Linux
o utilizar `nslookup` en el indicador de mandatos de Windows para Windows.

Si el paquete tiene un valor de CF-Ray, habrá viajado a través de CIS.

El mandato `traceroute` muestra toda la vía de acceso que ha tomado una solicitud IP.

El equipo de soporte hace uso de estos mandatos para ayudarle.

## Si ve un aviso de privacidad
{:#troubleshooting-cis-privacy-warning}

Los certificados emitidos por IBM CIS cubren el dominio raíz (`example.com`) y un nivel de subdominio (`*.example.com`). Si está tratando de llegar a un subdominio de segundo nivel (`*.*.example.com`), verá un aviso de privacidad en el navegador, porque estos nombres de host no están añadidos al SAN.

Además, deje hasta 15 minutos para que una de nuestras autoridades emisoras de certificados (CA) asociadas emita un nuevo certificado. Verá un aviso de privacidad en el navegador si el nuevo certificado aún no se ha emitido.

## ¿Qué puedo hacer si sufro un ataque DDoS?
{:#troubleshooting-cis-ddos-attack}

 * **Paso 1:** Active "Modalidad de defensa" desde su panel de control
 * **Paso 2:** Establezca los registros DNS para máxima seguridad
 * **Paso 3:** No limite por velocidad ni regule las solicitudes desde IBM CIS
 
Durante la "Modalidad de defensa", cada nuevo visitante obtuvo una solicitud de seguridad "Captcha", que debe pasar antes de recibir una cookie para el acceso sin desafío. De esta forma, el tráfico botnet se bloquea hasta que la "Modalidad de defensa" se desactiva. Los visitantes que no cumplan la solicitud de seguridad se añadirán a la Base de datos de (mala) reputación de IP.

## Otros problemas que puede encontrar
{:#troubleshooting-cis-other-problems}

Estos son algunos mensajes de error comunes que usted o su equipo de soporte puede ver:

| Código de error    | Motivo |
| ------------- | ------------- |
| 1001  | Error de resolución DNS. El cliente ha firmado recientemente y su información DNS todavía no se ha propagado, o la persona que está gestionando el DNS tiene un error. |
| 521  | El servidor web de origen ha rechazado la conexión desde CIS. El servidor web de origen no se está ejecutando, o algo está bloqueando las direcciones IP de IBM CIS. |
| 522  | La conexión ha superado el tiempo de espera en el servidor de origen (valor predeterminado de 30 segundos). CIS puede tener la velocidad limitada, el servidor web puede estar consumiendo todos los recursos (servidor compartido), o puede haber problemas de conectividad de red entre el servidor web e IBM CIS. |
| 523  | No se puede llegar al servidor de origen. Asegúrese de que la dirección IP de origen para el registro DNS sea la misma que la que aparece en la página Configuración de DNS de CIS. |
| 524  | IBM CIS podría realizar una conexión TCP pero no ha recibido ninguna respuesta del servidor web. Una consulta de una aplicación o de una base de datos de larga ejecución está interfiriendo. |

### No vemos ningún tráfico de red
{:#troubleshooting-cis-network-traffic}

Si no ve tráfico, y está utilizando un CNAME, asegúrese de que haya una redirección en su lugar, de modo que el tráfico no se direccione al dominio raíz. Recuerde que algunas propagaciones DNS pueden tardar hasta 48 horas en completarse.

### Sitio web fuera de línea
{:#troubleshooting-cis-website-offline}

Aquí le decimos lo que podría ver:

`IBM CIS no puede conectarse al servidor de origen (error 521, 522, 523)`.

**Sitio web fuera de línea - sin versión en la memoria caché**

1. El servidor está en línea, pero está bloqueando la solicitud de IBM CIS.
2. El servidor de origen está fuera de línea e IBM CIS no tiene ninguna imagen de sitio web de copia de seguridad 

Lo que puede hacer:

* Verificar que las direcciones IP de IBM CIS estén incluidas en la lista blanca.
* Asegurarse de que las IP de IBM CIS no tengan limitaciones de velocidad.
* Esta es la lista de [IP a añadir en la lista blanca](/docs/infrastructure/cis?topic=cis-ibm-cloud-cis-whitelisted-ip-addresses)

### Error 502 “fatal 502”
{:#troubleshooting-cis-502-error}

Este error es uno de los más comunes que puede ver. Normalmente se produce cuando una parte de una red no está disponible, por ejemplo, en el inicio de un ataque DDoS. Un centro de datos en particular podría no estar disponible durante un tiempo. El tráfico será desviado. Ejecute una ruta de rastreo. 

Aquí le decimos lo que podría ver: `Error 502 - error de pasarela errónea`

Lo que sucedió:

* Una parte de la red de IBM CIS está teniendo un problema.
* Normalmente, el problema se limita a un servidor en un centro de datos.
* Solo afecta a una parte de los visitantes del sitio.
* El equipo de operaciones técnico de IBM CIS lo trata.

Lo que puede hacer:

* Enviar los resultados de `www.YOUR_DOMAIN.com/cdn-cgi/trace` en una incidencia a [Soporte](/docs/get-support?topic=get-support-getting-customer-support).
* Desactivar temporalmente los Registros de DNS (sin proxy).

