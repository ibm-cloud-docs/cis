---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Glossary, load balancer, pool, health check

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Glosario
{:#glossary}

Este glosario contiene definiciones para los términos comunes que puede encontrar al trabajar con el Equilibrador de carga global (GLB).

## Equilibrador de carga
{:#glossary-load-balancer}

Un equilibrador de carga es un dispositivo que actúa como un proxy inverso y distribuye el tráfico de red o de aplicaciones entre varios servidores. Los equilibradores de carga se utilizan para aumentar la capacidad del sistema (el número de usuarios simultáneos) y para mejorar la fiabilidad de las aplicaciones.

## Agrupación
{:#glossary-pool}

Una agrupación es un grupo de servidores de origen al que se direcciona el tráfico de forma inteligente al adjuntarse a un GLB. El número mínimo de servidores de origen disponibles para la agrupación que se marcará como en buen estado es configurable por el usuario junto con la comprobación de estado específica que se utilizará. La agrupación de origen se puede asociar con una región específica o se puede convertir en disponible para todas las regiones.

## Comprobación de estado
{:#glossary-health-check}

Una comprobación de estado ayuda a obtener información sobre la disponibilidad de las agrupaciones para que el tráfico se pueda direccionar a las que están en buen estado. Estas comprobaciones envían solicitudes HTTP/HTTPS periódicamente y supervisan las respuestas. Se pueden configurar con intervalos, tiempos de espera, códigos de estado, etc. personalizados. Tan pronto como se marque una agrupación como en mal estado, el tráfico se redireccionará de forma inteligente a otra agrupación disponible, si está disponible.

## Servidores de origen
{:#glossary-origin-servers}

Un servidor de origen procesa y responde a las solicitudes entrantes de los clientes, y se utiliza normalmente con servidores de almacenamiento en memoria caché. Los servidores de origen ejecutan uno o más programas diseñados para escuchar y procesar las solicitudes entrantes de Internet. La distancia física entre el servidor de origen y el cliente que realiza una solicitud añade latencia a la conexión, aumentando el tiempo de carga. Si se utilizan servidores de almacenamiento en memoria caché, se reduce esta latencia.


