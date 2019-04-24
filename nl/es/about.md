---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Caching, IBM Cloud Internet Services, Web Application Firewall

subcollection: cis

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"} 

# Acerca de IBM Cloud Internet Services (CIS)
{:#about-ibm-cloud-internet-services-cis}

IBM Cloud Internet Services (CIS), basado en Cloudflare, proporciona un servicio de Internet rápido, muy eficiente, fiable y seguro para clientes que gestionan su negocio en IBM Cloud.   

IBM CIS le pone en marcha rápidamente estableciendo valores predeterminados, que pueden cambiar fácilmente utilizando la API o IU. Estos son algunos parámetros comúnmente cambiados:

 * **Valores de DNS**: puede utilizar IBM CIS para alojar su DNS o puede crear registros de CNAME.
 * **Valores criptográficos (TLS)**: el valor predeterminado es la modalidad `flexible`, que cifra la conexión entre el host y el servidor perimetral de IBM CIS, pero no cifra la comunicación entre el servidor perimetral de IBM CIS y el servidor de origen.

## Cortafuegos de aplicaciones web (WAF)
{:#about-waf}

IBM CIS proporciona la función de Cortafuegos de aplicaciones web (WAF), que examina el tráfico web para buscar actividad sospechosa. Puede filtrar el tráfico ilegítimo automáticamente (basado en conjuntos de reglas) para buscar en las solicitudes web GET y basadas en POST. Puede utilizar varios conjuntos de reglas para determinar qué tráfico bloqueará, desafiará o dejará pasar. Nuestro WAF puede bloquear correo no deseado de comentarios, ataques de script entre sitios e inyecciones de SQL.

Puede habilitar o inhabilitar WAF a su discreción. Le recomendamos que siempre lo deje encendido.

## Protección contra ataques DDoS
{:#ddos-protection}

IBM CIS proporciona protección DDoS que está entre el sitio web y los atacantes, independientemente del tamaño o de la duración del ataque.

## Equilibrio de carga
{:#about-load-balancing}

IBM CIS Load Balancing funciona a nivel de DNS autorizado. Incorpora comprobaciones de estado avanzadas para supervisar el estado de los orígenes, y ajusta de forma dinámica las respuestas de DNS. Además, puede configurar Geopolíticas para Global Load Balancing (GLB).

### Comprobaciones de estado
{:#about-health-checks}

Load Balancing Health Checks se realizan en URL específicas mediante solicitudes HTTP o HTTPS periódicas, y se configuran con intervalos, tiempos de espera y códigos de estado personalizables. Cuando un servidor de origen se marca como insalubre, se direcciona a los visitantes lejos de las anomalías, utilizando nuestras rutas de migración rápida.
 
### Geopolíticas y Global Load Balancing (GLB)
{geo-policies-and-glb}

Las geopolíticas le dan el control de los servidores de origen a los que se dirigirá un cliente determinado, basadas en la ubicación geográfica de dicho cliente. Por ejemplo, podría configurar sus Geopolíticas para que los visitantes de Europa se envíen al origen europeo más próximo para su sitio web o aplicación, los visitantes de EE.UU. se enviarán a un origen de América del Norte, y así sucesivamente.

## Almacenamiento en memoria caché
{:#about-caching}

El almacenamiento en memoria caché es una forma de almacenar su contenido web estático más cerca de los visitantes de su sitio, mejorando así significativamente el rendimiento del sitio web. Nuestro entorno de entrega distribuido globalmente permite a los propietarios de contenido web proporcionar una experiencia perfecta, en todo el mundo.  
 
## Cifrado con TLS
{:#encryption-with-tls}

Comunicación cifrada a y desde su sitio web utilizando Transport Layer Security (TLS). Se puede tardar hasta 24 horas después de que el sitio esté activo para que se emitan sus nuevos certificados.

Puede encontrar más información sobre TLS en nuestras [Preguntas frecuentes](/docs/infrastructure/cis?topic=cis-faq).
