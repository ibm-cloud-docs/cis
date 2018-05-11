---

copyright:
  years: 2018
lastupdated: "2018-03-05"

---

# Conceptos del Equilibrador de carga global (GLB)

Este documento contiene algunos conceptos y definiciones relacionados con el Equilibrador de carga global (GLB) y cómo afecta su despliegue de IBM CIS.

## Equilibrador de carga global

El Equilibrador de carga global (GLB) gestiona el tráfico entre recursos de servidores localizados en varias regiones. La GLB utiliza una agrupación que permite al tráfico distribuirse en varios orígenes. Esto proporciona muchos beneficios, como:

  * Minimizar el tiempo de respuesta
  * Mayor disponibilidad mediante redundancia
  * Maximizar el rendimiento del tráfico

## Agrupación

Una agrupación es un grupo de servidores de origen al que se direcciona el tráfico de forma inteligente al adjuntarse a un GLB. El número mínimo de servidores de origen disponibles para la agrupación que se marcará como en buen estado es configurable por el usuario junto con la comprobación de estado específica que se utilizará. La agrupación de origen se puede asociar con una región específica o se puede convertir en disponible para todas las regiones.

## Comprobación de estado

Una comprobación de estado ayuda a obtener información sobre la disponibilidad de las agrupaciones para que el tráfico se pueda direccionar a las que están en buen estado. Estas comprobaciones envían solicitudes HTTP/HTTPS periódicamente y supervisan las respuestas. Se pueden configurar con intervalos, tiempos de espera, códigos de estado, etc. personalizados. Tan pronto como se marque una agrupación como en mal estado, el tráfico se redireccionará de forma inteligente a otra agrupación disponible, si está disponible.
