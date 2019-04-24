---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Use Page Rules, Page Rule

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# Uso de las Reglas de página
{:#use-page-rules}

Una Regla de página especifica algunas configuraciones y valores que se pueden aplicar a un patrón de URL específico que hace referencia a su dominio. Las Reglas de página ayudan a gestionar la seguridad, el rendimiento y la fiabilidad en función de cada URL individual del sitio. La tabla siguiente describe las Reglas de página que están disponibles para todos los clientes, los comportamientos que producen, y cualquier consideración especial que debería tener en cuenta antes de utilizarlas.

## Seguridad
{:#page-rules-security}

| **Valor** | **Comportamiento** | **Consideraciones** |
|-----------|----------|----------------|
|**Comprobación de integridad del navegador**|Busca cabeceras HTTP comunes de las que abusan los emisores de spam, y niega el acceso a su página. También bloquea a los visitantes que no tienen un agente de usuario o que añaden un agente de usuario no estándar (también comúnmente utilizado por los bots, los rastreadores o las API de abuso). | |
|**Inhabilitar seguridad**|Inhabilita las características siguientes: <ul><li>Ofuscación de correo electrónico</li> <li>Exclusiones del lado del servidor</li> <li>WAF</li></ul>|Si se establece una regla para inhabilitar la seguridad, y se establece otra regla para habilitar el WAF, la regla de WAF tendrá prioridad, independientemente del orden en el que aparezcan.|
|**Ofuscación de correo electrónico**|Activa o desactiva la Ofuscación de correo electrónico. | |
|**Cabecera de geolocalización de IP**|Incluye el código de país de la ubicación del visitante con todas las solicitudes en su sitio web. La información se puede encontrar en la cabecera HTTP `CF-IPCountry`. | |  
|**Nivel de seguridad**|Controla cómo de alta debe ser la puntuación de amenazas de un cliente para que un cliente encuentre una página de solicitud. Este valor se puede utilizar para que su sitio siempre presente a los visitantes la solicitud **Modalidad de defensa** cuando visitan su sitio. | |
|**Exclusiones del lado del servidor**|Activa o desactiva las Exclusiones del lado del servidor.  | |
|**TLS**|Controla cuál de las modalidades TLS se utiliza. | |
|**WAF**|Activa o desactiva WAF. | |  
|**Reescrituras HTTPS automáticas**|Activa o desactiva las Reescrituras HTTPS automáticas.  | |
|**Cifrado oportunista**|Activa o desactiva el Cifrado oportunista.  | |
|**Escudo de engaño de memoria caché**|Activa o desactiva el Escudo de engaño de memoria caché.  | |
|**Utilizar siempre HTTPS**|Convierte cualquier URL `http://` en un URL `https://` creando una redirección `301`.|Utilizar este valor inhabilita la configuración del resto de los valores para la regla, porque IBM CIS fuerza a una redirección a `HTTPS` para la solicitud, que se convierte en una nueva solicitud que se evaluará en Reglas de página. |
|**Cabecera True Client IP**|CIS enviará la dirección IP del usuario final en la cabecera `True-Client-IP`.  |Sólo Empresa |

## Rendimiento
{:#page-rules-performance}

| **Valor** | **Comportamiento** | **Consideraciones** |
|-----------|----------|----------------|
|**TTL de memoria caché de navegador**|Controla cuánto tiempo seguirán siendo válidos los recursos almacenados por navegadores de clientes. | |
|**Omitir memoria caché en la cookie**|Servir un objeto almacenado en la memoria caché a menos que se vea una cookie de un nombre específico, por ejemplo, servir una versión almacenada en memoria caché de la página de inicio a menos que se vea una cookie `SessionID` que indica que el cliente ha iniciado sesión y, por lo tanto, debería presentársele contenido personalizado. | |
|**Nivel de memoria caché**|**Omitir**: Los recursos que coinciden con dicha Regla de página no se almacenan en la memoria caché.<br>**Sin serie de consulta**: Solo ofrece recursos de memoria caché cuando no hay ninguna serie de consulta.<br>**Ignorar serie de consulta**: Ofrece el mismo recurso a todo el mundo, independientemente de la serie de consulta.<br>**Estándar**: Ofrece un recurso distinto cada vez que cambie la serie de consulta.<br> **Almacenar todo en la memoria caché**: Los recursos que coinciden con la Regla de página se almacenan en la memoria caché.|De forma predeterminada, el contenido HTML no se almacena en la memoria caché. Se debe escribir una Regla de página para almacenar en la memoria caché contenido HTML estático. |
|**TTL límite de almacenamiento en memoria caché**|Controla cuánto tiempo IBM CIS conservará archivos en nuestra memoria caché. |Este valor es opcional al especificar el nivel de memoria caché. |
|**Resolver sustitución**|Cambie el URL o la IP a la que se resuelve la solicitud que coincide con la regla de la página.||
|**Memoria caché en Cookie**|Aplique la opción `Almacenar todo en la memoria caché` (parámetro `Nivel de memoria caché`) basada en una coincidencia de expresión regular con un nombre de cookie. Si añade este parámetro y `Omitir memoria caché en la cookie` a la misma regla de página, `Memoria caché en Cookie` tiene prioridad sobre `Omitir memoria caché en la cookie`.|Sólo Empresa |
|**Inhabilitar rendimiento**|Desactivar:<ul><li>`Minificar contenido web`</li><li>`Optimización de carga de imagen`</li><li>`Optimización de tamaño de imagen`</li><li>`Optimización de carga de script`</li></ul> |Sólo Empresa |
|**Minificar contenido web**|Minificar los archivos HTML, CSS y/o JavaScript eliminando todos los caracteres no necesarios de estos archivos. |Sólo Empresa |
|**Optimización de carga de imagen**|Mejora el tiempo de carga de las páginas que incluyen imágenes basándose en la conexión de red y el tipo de dispositivo mediante:<ul><li>**Virtualización de imágenes** - Sustituye las imágenes por imágenes de marcador de posición de baja resolución que tienen las mismas dimensiones que las originales (incluyendo imágenes de terceros). Una vez la página se ha representado completamente, se cargan por carga diferida (lazy-load) las imágenes en su resolución completa (priorizando las imágenes que se encuentren en la zona de observación del navegador). Este proceso permite que las páginas se representen rápidamente y se reduce al mínimo el reflujo del navegador.</li><li>**Optimización de solicitudes** - Combina varias solicitudes de red individuales de imágenes en una sola.</li></ul> |Sólo Empresa |
|**Optimización de tamaño de imagen**|Reducir el tamaño de archivo de imagen eliminando metadatos (fecha y hora, fabricante y modelo de la cámara, etc.)y comprimiendo las imágenes cuando sea posible. Unos tamaños de archivo más pequeños suponen tiempos de carga más rápidos para las imágenes y las páginas web. |Sólo Empresa |
|**Ordena series de consulta**|Trata los archivos con las mismas series de consulta como el mismo archivo en la memoria caché, independientemente del orden de las series de consulta. |Sólo Empresa |
|**Almacenamiento intermedio de respuesta**|Habilite o inhabilite el almacenamiento intermedio de respuestas desde el servidor de origen. De forma predeterminada, CIS envía paquetes al cliente a medida que los recibimos. Habilitar el almacenamiento intermedio de respuesta supone que CIS esperará hasta que tenga el archivo completo antes de reenviarlo al usuario final. |Sólo Empresa |
|**Optimización de carga de script**|Mejore los tiempos de pintura (paint time) cargando de forma asíncrona los Javascripts, incluyendo los scripts de terceros, de modo que no bloqueen la representación del contenido de las páginas. |Sólo Empresa |

## Fiabilidad
{:#page-rules-reliability}

| **Valor** | **Comportamiento** | **Consideraciones** |
|-----------|----------|----------------|
|**Servir contenido obsoleto**|Mantiene una versión limitada del sitio en línea si el servidor se desactiva. |Para obtener más información, vea [Gestión del despliegue de CIS para una fiabilidad óptima](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-deployment-for-optimal-reliability) |
|**Control de memoria caché de origen**|Determinar qué contenido se almacena en la memoria caché desde el origen y con cuánta frecuencia se actualiza el contenido |Para obtener más información, vea [Gestión del despliegue de CIS para una fiabilidad óptima](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-deployment-for-optimal-reliability) |
|**URL de reenvío** |URL que se utilizará en caso de que el sitio no esté disponible. | Esto inhabilita la configuración de los demás valores porque está reenviando la solicitud a otro lugar. Para obtener más información, vea [Gestión del despliegue de CIS para una fiabilidad óptima](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-deployment-for-optimal-reliability)|
|**Sustituir cabecera de host**|Sustituye la cabecera de host por el URI que coincide con la regla de página por el valor especificado. Esto se utiliza normalmente para el contenido alojado en un contenedor S3.|
|**Inhabilitar apps**|Desactivar todas las apps de CIS. | Sólo Empresa |
|**Paso de página de error de origen**|Inhabilita las páginas de error de CIS que se desencadenarían para los problemas enviados desde el servidor de origen y en su lugar muestra las páginas de error establecidas en el origen. |Sólo Empresa ||

## Patrones de URL de Regla de página
{:#page-rule-url-patterns}

Una Regla de página entrará en vigor en un patrón de URL determinado, coincidiendo con el siguiente formato:

`<scheme>://<hostname><:port>/<path>`

Un ejemplo que utilice cada componente sería el siguiente:

`https://www.example.com:80/image.png`

Los componentes *scheme* y *port* son opcionales. Si el esquema se omite, cubrirá ambos protocolos `http://` y `https://`. Si el puerto no está especificado, la regla coincidirá con todos los puertos. Puede realizar coincidencias básicas de comodines utilizando un símbolo ‘*’ en el patrón de reglas, permitiéndole coincidir con una serie de patrones similares en lugar de solo con uno.

Aquí hay tres cosas importantes que recordar con las Reglas de página:

 * Solo tendrá efecto una Regla de páginas en cualquier solicitud determinada.
 * Las Reglas de página tienen prioridad en un orden de arriba abajo.
 * Una vez que un URL coincida con una regla, solo se aplicará esa regla; es decir, si una Regla de página ya se ha desencadenado en una solicitud, las reglas posteriores que también coincidan con el patrón de URL no entrará en vigor. Como regla general, recomendamos ordenar las reglas de _más específicas_ a _menos específicas_.

Las Reglas de páginas se pueden inhabilitar, en cuyo caso no tendrán ninguna acción. Se pueden seguir viendo en la lista y editarse. El establecimiento del conmutador **Habilitado** en **Off** creará una Regla de página que está inhabilitada inicialmente.

Para obtener más información, consulte el [documento ilustrativo Almacenamiento en memoria y reglas de páginas](/docs/infrastructure/cis?topic=cis-use-page-rules-with-caching).
