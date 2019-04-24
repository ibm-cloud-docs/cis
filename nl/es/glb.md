---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: origin server, pool implementation, origin servers

subcollection: cis

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"} 
{:note: .note}

# Conceptos del Equilibrador de carga global (GLB)
{:#global-load-balancer-glb-concepts}

Este documento contiene algunos conceptos y definiciones relacionados con el Equilibrador de carga global (GLB) y cómo afecta su despliegue de IBM CIS.

## Equilibrador de carga global
{:#global-load-balancer-cis}

El Equilibrador de carga global (GLB) gestiona el tráfico entre recursos de servidores localizados en varias regiones. El servidor de origen puede servir todo el contenido de un sitio web, siempre que el tráfico web no se extienda más allá de las capacidades de proceso del servidor y la latencia no sea una problema. El GLB utiliza una implementación de _agrupación_ que permite que el tráfico se distribuya a varios orígenes. Esta funcionalidad de agrupación ofrece muchas ventajas, entre ellas:

  * Minimiza el tiempo de respuesta
  * Crea una mayor disponibilidad mediante la redundancia
  * Maximiza el rendimiento del tráfico

El GLB direcciona el tráfico a la agrupación con la prioridad más alta, distribuyendo la carga entre sus servidores de origen. Consulte la siguiente sección _Agrupación_ para ver cómo se distribuye el tráfico dentro de una agrupación. Si la agrupación primaria pasa a estar no disponible, el tráfico se direcciona automáticamente a la siguiente agrupación de la lista basándose en la prioridad.

Si se configuran agrupaciones para regiones específicas, el tráfico se envía primero desde esas regiones a las agrupaciones de la región especificada. Únicamente si todas las agrupaciones de una región determinada están inactivas, el tráfico vuelve a las agrupaciones predeterminadas. En este caso, la agrupación de reserva es la agrupación con la prioridad más baja. 

### Cómo funciona
{:#how-glb-works}
Cuando se crea el GLB, se añade automáticamente un registro de DNS para el mismo con el nombre del equilibrador de carga. A continuación, el GLB devuelve una de las direcciones IP de origen a un cliente que realiza una solicitud de DNS.

Por ejemplo, se crea una agrupación de origen con dos orígenes que identifican las direcciones IP `169.61.244.18` y `169.61.244.19`. Si se crea un equilibrador de carga global con el nombre `glbcust.ibmmo.com` utilizando la agrupación de origen, un cliente en Internet puede ejecutar el mandato:
```
$ ping glbcust.ibmom.com
PING glbcust.ibmom.com (169.61.244.18): 56 data bytes
```
Es este ejemplo, CIS:

    * ha creado un registro de DNS denominado `glbcust.ibmmo.com`
    * ha utilizado el GLB para resolver el nombre DNS a una de las direcciones IP identificadas en la agrupación de origen

Tenga en cuenta que el equilibrador de carga global no termina la conexión TCP.
{:note}

Si se establece un elemento DNS o un GLB para "redireccionar" se cambia el comportamiento.
Si, por ejemplo, activa el proxy y establece **Seguridad > TLS > Modalidad** a algo distinto de `Off`, CIS termina la conexión TCP y establece una segunda conexión entre CIS y el originador.

Es este ejemplo, CIS:

    * ha creado un registro de DNS denominado: `glbcust.ibmmo.com`
    * ha utilizado el GLB para resolver el nombre DNS a una dirección IP proporcionada por CIS
    
Ahora, CIS termina las conexiones a `glbcust.ibmmo.com`, y aloja los certificados HTTPS (lo que es obligatorio para la terminación de TCP).

Después de que el cliente se conecte a la aplicación, el aspecto es el siguiente:

`[cliente]<--tls-->[cis]<-->[servidor de origen]`

## Agrupación
{:#glb-pools}

Una agrupación es un grupo de servidores de origen al que se direcciona el tráfico de forma inteligente al adjuntarse a un GLB. El número mínimo de servidores de origen disponibles para la agrupación que se marcará como en buen estado es configurable por el usuario junto con la comprobación de estado específica que se utilizará. La agrupación de origen se puede asociar con una región específica o se puede convertir en disponible para todas las regiones.

### Distribución del tráfico dentro de una agrupación
{:#distribution-of-traffic-within-a-pool}

De forma predeterminada, todo el tráfico se distribuye uniformemente entre los orígenes de la agrupación utilizando el protocolo de round robin. Esto también es válido para los GLB no redirigidos.

Los orígenes se pueden configurar con pesos, y para los GLB redirigidos, los pesos determinan la cantidad de tráfico que recibe cada servidor de origen con relación a otros orígenes de la agrupación. Los pesos se configuran como números entre 0 y 1 y especifican la fracción de tráfico que va a ir al origen. 

Por cada origen: 

` Porcentaje de tráfico al origen = peso del origen / suma de los pesos de todos los orígenes`

Si todos los orígenes tienen un peso de `1`, el tráfico se distribuye uniformemente. 

Los orígenes con un peso de `0` no reciben nada de tráfico de esta agrupación. No obstante, la afinidad de sesiones puede alterar temporalmente esto hasta que todas las sesiones estén cerradas. Si el origen es un miembro de otra agrupación, es posible que siga recibiendo tráfico para dicha agrupación.

**Ejemplo:** 

Una agrupación de origen se configura con 3 orígenes que tienen los siguientes pesos: origin-A: 0.4, origin-B: 0.3 y origin-C: 0.3. 

* Inicialmente, todos los orígenes están en buen estado. La cantidad de tráfico que recibe cada origen es: origin-A: 40%, origin-B: 30%, y origin-C: 30%.
* A continuación, origin-A pasa crítico; deja de recibir tráfico. El resto de orígenes tienen el mismo peso y, por lo tanto, el tráfico se distribuye uniformemente entre ellos y cada uno recibe el 50%.
* El administrador cambia el peso de origin-C a `0`. Ahora, el 100% del tráfico nuevo va a origin-B. Pero con la afinidad de sesión activada, el tráfico de las sesiones existentes en origin-C continúa yendo a origin-C hasta que se cierran esas sesiones (máx. 24 horas).

### Agrupación de reserva
{:#fallback-pool}

La agrupación de origen con la prioridad más baja (el número más grande) es la "agrupación de reserva" designada. Cuando todas las agrupaciones de una región están inactivas, el tráfico se direcciona a la agrupación de reserva, independientemente de su estado.

Cuando todas las agrupaciones están inhabilitadas, la agrupación de reserva no está disponible.
{:note}

## Comprobación de estado
{:#cis-health-check}

Una comprobación de estado ayuda a obtener información sobre la disponibilidad de las agrupaciones para que el tráfico se pueda direccionar a las que están en buen estado. Estas comprobaciones envían periódicamente solicitudes HTTP, HTTPS o TCP y supervisan las respuestas. Se pueden configurar con un puerto, intervalo, código de estado y más personalizados. Tan pronto como una agrupación se marca como en mal estado, el tráfico se redirecciona de forma inteligente a otra agrupación disponible, si está disponible.
Tenga en cuenta que los registros tienen referencias a Cloudflare debido a la asociación de IBM con Cloudflare para CIS.
{:note}

### Sucesos de comprobación de estado
{:#health-check-events}

Los sucesos de comprobación de estado son cambios de estado de las agrupaciones con comprobaciones de estado conectadas y sus servidores de origen asociados. Si el estado de un origen se degrada, aparece un nuevo elemento en una tabla, con la descripción del suceso. Vaya a **Fiabilidad > Equilibrador de carga global > Sucesos de comprobación de estado** para ver una tabla de los Sucesos de comprobación de estado. Puede filtrar por fecha, por estado u origen de la agrupación, por nombre de agrupación y por nombre de origen seleccionando los parámetros de filtro en los menús desplegables. Se pueden ordenar las columnas de la tabla pulsando en el nombre de columna.
![Tabla de Sucesos de comprobación de estado](images/health-check-events-table.png)

Las filas individuales dentro de la tabla se expanden con más información sobre la entrada. Si la agrupación está en buen estado, sólo se puede ver el mosaico **Detalles de agrupación**. Cuando la fila tiene un origen crítico, o una agrupación degradada, también aparece el mosaico **Detalles del origen afectado**. 

![Detalles de Sucesos de comprobación de estado](images/health-check-events-details.png)

#### Detalles de la agrupación:
* Nombre de agrupación - Nombre de la agrupación
* Orígenes en buen estado - Proporción de orígenes en buen estado/total de orígenes de una agrupación
* Umbral de buen estado - Número de orígenes que tiene que haber en buen estado para poder considerar que la agrupación está en buen estado
* Orígenes en buen estado - Nombres de los orígenes en buen estado
* Orígenes críticos - Nombres de los orígenes en mal estado

#### Detalles de origen afectado:
* Nombre de origen - Nombre del origen
* Dirección de origen - Dirección del origen
