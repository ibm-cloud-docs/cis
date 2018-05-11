---
copyright:
  years: 2018
lastupdated: "2018-03-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Uso de las Reglas de página

Una Regla de página especifica algunas configuraciones y valores que se pueden aplicar a un patrón de URL específico que hace referencia a su dominio. Las Reglas de página ayudan a gestionar la seguridad, el rendimiento y la fiabilidad en función de cada URL individual del sitio. La tabla siguiente describe las Reglas de página que están disponibles para todos los clientes, los comportamientos que producen, y cualquier consideración especial que debería tener en cuenta antes de utilizarlas.

## Seguridad

| **Valor** | **Comportamiento** | **Consideraciones** |
|-----------|----------|----------------|
|**Comprobación de integridad del navegador**|Busca cabeceras HTTP comunes de las que abusan los emisores de spam, y niega el acceso a su página. También bloquea a los visitantes que no tienen un agente de usuario o que añaden un agente de usuario no estándar (también comúnmente utilizado por los bots, los rastreadores o las API de abuso). | |
|**Inhabilitar seguridad**|Inhabilita las características siguientes: <ul><li>Ofuscación de correo electrónico</li> <li>Exclusiones del lado del servidor</li> <li>WAF</li></ul>|Si se establece una regla para inhabilitar la seguridad, y se establece otra regla para habilitar el WAF, la regla de WAF tendrá prioridad, independientemente del orden en el que aparezcan.|
|**Ofuscación de correo electrónico**|Activa o desactiva la Ofuscación de correo electrónico. | |
|**Cabecera de geolocalización de IP**|Incluye el código de país de la ubicación del visitante con todas las solicitudes en su sitio web. La información se puede encontrar en la cabecera HTTP `CF-IPCountry`. | |  
|**Nivel de seguridad**|Controla cómo de alta debe ser la puntuación de amenazas de un cliente para que un cliente encuentre una página de solicitud. Este valor se puede utilizar para que su sitio siempre presente a los visitantes la solicitud **Modalidad de defensa** cuando visitan su sitio. | |
|**Exclusiones del lado del servidor**|Activa o desactiva las Exclusiones del lado del servidor. | |
|**TLS**|Controla cuál de las modalidades TLS se utiliza. | |
|**WAF**|Activa o desactiva WAF. | |  
|**Reescrituras HTTPS automáticas**|Activa o desactiva las Reescrituras HTTPS automáticas. | |
|**Cifrado oportunista**|Activa o desactiva el Cifrado oportunista. | |
|**Escudo de engaño de memoria caché**|Activa o desactiva el Escudo de engaño de memoria caché. | |
|**Utilizar siempre HTTPS**|Convierte cualquier URL `http://` en un URL `https://` creando una redirección `301`.|Utilizar este valor inhabilita la configuración del resto de los valores para la regla, porque IBM CIS fuerza a una redirección a `HTTPS` para la solicitud, que se convierte en una nueva solicitud que se evaluará en Reglas de página. |

## Rendimiento
| **Valor** | **Comportamiento** | **Consideraciones** |
|-----------|----------|----------------|
|**TTL de memoria caché de navegador**|Controla cuánto tiempo seguirán siendo válidos los recursos almacenados por navegadores de clientes. | |
|**Omitir memoria caché en la cookie**|Servir un objeto almacenado en la memoria caché a menos que se vea una cookie de un nombre específico, por ejemplo, servir una versión almacenada en memoria caché de la página de inicio a menos que se vea una cookie `SessionID` que indica que el cliente ha iniciado sesión y, por lo tanto, debería presentársele contenido personalizado. | |
|**Nivel de memoria caché**|**Omitir**: Los recursos que coinciden con dicha Regla de página no se almacenan en la memoria caché.<br>**Sin serie de consulta**: Solo ofrece recursos de memoria caché cuando no hay ninguna serie de consulta.<br>**Ignorar serie de consulta**: Ofrece el mismo recurso a todo el mundo, independientemente de la serie de consulta.<br>**Estándar**: Ofrece un recurso distinto cada vez que cambie la serie de consulta.<br> **Almacenar todo en la memoria caché**: Los recursos que coinciden con la Regla de página se almacenan en la memoria caché.|De forma predeterminada, el contenido HTML no se almacena en la memoria caché. Se debe escribir una Regla de página para almacenar en la memoria caché contenido HTML estático. |
|**TTL límite de almacenamiento en memoria caché**|Controla cuánto tiempo IBM CIS conservará archivos en nuestra memoria caché. |Este valor es opcional al especificar el nivel de memoria caché. |

## Fiabilidad
| **Valor** | **Comportamiento** | **Consideraciones** |
|-----------|----------|----------------|
|**Siempre en línea**|Mantiene una versión limitada del sitio en línea si el servidor se desactiva. |Para obtener más información, vea [Gestión del despliegue de CIS para una fiabilidad óptima](managing-for-reliability.html) |
|**Control de memoria caché de origen**|Determinar qué contenido se almacena en la memoria caché desde el origen y con cuánta frecuencia se actualiza el contenido |Para obtener más información, vea [Gestión del despliegue de CIS para una fiabilidad óptima](managing-for-reliability.html) |
|**URL de reenvío** |URL que se utilizará en caso de que el sitio no esté disponible. | Esto inhabilita la configuración de los demás valores porque está reenviando la solicitud a otro lugar. Para obtener más información, vea [Gestión del despliegue de CIS para una fiabilidad óptima](managing-for-reliability.html)|

## Patrones de URL de Regla de página

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

Para obtener más información, consulte el [documento ilustrativo Almacenamiento en memoria y reglas de páginas](caching-with-page-rules.html).
