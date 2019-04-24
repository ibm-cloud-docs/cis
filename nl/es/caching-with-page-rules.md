---
copyright:
  years: 2018
lastupdated: "2018-03-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Uso de reglas de páginas con almacenamiento en memoria caché

Las Reglas de páginas le ofrecen la posibilidad de realizar varias acciones basadas en el URL de la página, como crear redirecciones, ajustar el comportamiento del almacenamiento en memoria caché, o la habilitación e inhabilitación de servicios.

Una Regla de página tiene efecto en un patrón URL determinado que coincide con el formato siguiente:

`<scheme>://<hostname><:port>/<path>`

Por ejemplo:

`https://www.example.com:80/image.png`

Los componentes `scheme` y `port` son opcionales. Si se omite el componente `scheme`, el formato aceptará los protocolos `http://` y `https://`. Si el `port` no se especifica, la regla coincidirá con todos los puertos. Puede realizar coincidencias básicas de comodines utilizando un símbolo `*` en el patrón de reglas, permitiéndole coincidir con una serie de patrones similares.

**Cosas importantes que recordar con las Reglas de páginas:**

 * Solo tiene efecto una Regla de páginas en cualquier solicitud determinada.
 * Las Reglas de páginas tienen prioridad en un orden de arriba abajo. Una vez que un URL coincida con una regla, solo se aplicará esa regla; es decir, si una Regla de páginas ya se ha desencadenado en una solicitud, las reglas posteriores que también coincidan con el patrón de URL no entrará en vigor. 
 * Como regla general, recomendamos ordenar las reglas de más específicas a menos específicas.
 * Las Reglas de páginas se pueden inhabilitar, en cuyo caso no tendrán ninguna acción, pero se pueden seguir viendo en la lista y editarse. El establecimiento del conmutador *Habilitado* en "Off" crea una Regla de páginas que está inhabilitada inicialmente.


## Reenvío (Redirección de URL)
Redirige un URL a otro utilizando una redirección HTTP 301 o 302. Se puede hacer referencia al contenido de cualquier sección de un URL con el que coincide un comodín utilizando la sintaxis `$X`. La `X` indica el índice de un glob en el patrón: `$1` se sustituye por la primera coincidencia de comodín, `$2` por la segunda coincidencia de comodín, y así sucesivamente.

Por ejemplo, supongamos que establece la regla siguiente:

![imagen](images/url-redirection-example.png)

Aquí, una solicitud a "www.example.com/stuff/things" se redirigirá a "http://example.com/stuff/things".

**Nota:** Tenga cuidado para no crear una redirección en la que el dominio apunte a sí mismo como destino. Este error puede causar un error de redirección infinita, y los URL afectados no podrán resolverse.


## Redirección a HTTPS
Si desea redirigir los visitantes para utilizar HTTPS, utilice el valor **Utilizar siempre HTTPS** en su lugar:

![imagen2](images/url-matching-patterns.png)


## Almacenamiento en memoria caché personalizado
Establece el comportamiento del almacenamiento en memoria caché para cualquier URL que coincida con el patrón Regla de páginas, utilizando cualquiera de nuestros niveles de almacenamiento en la memoria caché estándares. El establecimiento de **Nivel de memoria caché** en **Almacenar todo en la memoria caché** almacena en la memoria caché cualquier contenido, incluso aunque no sea uno de nuestros tipos de archivos estáticos predeterminados. El establecimiento de **Nivel de memoria caché** en el valor **Ignorar** impide el almacenamiento en la memoria caché en dicho URL.

Al especificar el nivel de memoria caché utilizando Reglas de página, puede establecer un **TTL límite de almacenamiento en memoria caché**, que controla cuánto tiempo conservará CIS archivos en nuestra memoria caché.

**TTL de almacenamiento en memoria caché del navegador** controla cuánto tiempo seguirán siendo válidos los recursos almacenados por navegadores de clientes. Si un navegador solicita un recurso de nuevo y el TTL no ha caducado, el navegador recibirá una respuesta `HTTP 304 (Not Modified)`. Puede establecer TTL que van de 30 minutos a 1 año.

No todos los comportamientos de almacenamiento en memoria caché predeterminados están estrictamente conformes con RFC. El establecimiento del **Control de memoria caché de origen** mediante las Reglas de páginas utiliza un conjunto más reciente de reglas de almacenamiento en memoria caché que busca adherirse más a RFC, principalmente con respecto a la revalidación. Por ejemplo, nuestro comportamiento predeterminado con `max-age=0` es no almacenar en la memoria caché en absoluto, mientras que el valor **Control de memoria caché de origen** almacena en memoria caché, pero siempre revalida.

El ejemplo siguiente establece una Regla de páginas para almacenar en la memoria caché todo lo que se encuentre en la carpeta `/images`. Los recursos almacenados en la memoria caché caducan a los 30 minutos en el navegador del usuario, y caducarán después de un día en los centros de datos de IBM CIS:

![imagen3](images/url-example.png)
