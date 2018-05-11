---
copyright:
  years: 2018
lastupdated: "2018-03-06"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Cómo IBM Cloud Internet Services (CIS) mantiene su trabajo fiable

IBM Cloud Internet Services (CIS) le ayuda a mejorar la fiabilidad de los servicios web y aplicaciones, porque le ayuda a evitar el tiempo de inactividad causado por las interrupciones de aplicaciones e infraestructura. Por ejemplo, con el Equilibrio de carga global, puede desplegar los servicios web y las aplicaciones en varias regiones. IBM CIS direcciona las solicitudes del cliente a las regiones más próximas disponibles al habilitar el Equilibrio de carga global. Si falla alguna región, las solicitudes se direccionarán a la siguiente ubicación más próxima, de modo que los clientes no estarán afectados por el tiempo de inactividad. Si el sitio web o la API falla, IBM CIS le enviará notificaciones automáticamente, y le notificará cuando se haya restaurado.


![reliability-graphic.png](images/reliability-graphic.png)

Aquí hay una visión general de características rápida:

## Características de fiabilidad

 * Equilibrio de carga global 
 * Opciones de proxy y de no proxy para el equilibrio de carga
 * Agrupaciones de origen y supervisores de estado
 * Gestión de DNS
 
### Resumen
 
  * Los supervisores de estado comprueban si las agrupaciones de origen están en buen estado.
  * En caso de fallo del supervisor de estado, sus solicitudes se redireccionarán a orígenes en buen estado.
  * Estará informado de cuándo falla su servicio web o API y cuándo se restaura.
