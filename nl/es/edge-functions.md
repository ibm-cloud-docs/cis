---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: edge functions beta, edge functions

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Edge Functions (Beta)
{: #edge-functions}

CIS Edge Functions le permite crear aplicaciones nuevas o modificar aplicaciones existentes, sin tener que configurar ni mantener la infraestructura, utilizando un entorno de ejecución sin servidor. Las funciones de Edge se pueden definir y cargar en la nube para procesar las solicitudes antes de que éstas lleguen al origen. Las CIS Edge Functions se pueden utilizar para modificar solicitudes y respuestas HTTP, realizar solicitudes paralelas o generar respuestas desde la nube.

## Cómo funcionan las funciones Edge
{: #how-edge-functions-work}

Edge Functions asocia **acciones** a URI en base a un dominio definido. Esta asociación se conoce como un **desencadenante**. Las solicitudes de entrada a su sitio serán interceptadas en la nube y comparadas con los desencadenantes de su cuenta o dominio. Si el URL de la solicitud coincide con el URI del desencadenante, se ejecuta la acción asociada al mismo. 

Las funciones Edge se modelan en los [Trabajadores de servicio](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) disponibles en los navegadores web modernos, y utilizan la misma API siempre que sea posible.

La API de trabajador de servicio permite interceptar cualquier solicitud que se realice en el sitio. Cuando el JavaScript está manejando la solicitud, puede elegir hacer cualquier número de subsolicitudes a su sitio o a otros sitios y, finalmente, devolver cualquier respuesta que desee al visitante.

A diferencia de los trabajadores de servicio estándar, las funciones Edge se ejecutan en servidores Edge de CIS, no en el navegador del usuario. Esto significa que puede confiar en que el código se ejecutará en un entorno de confianza donde los clientes maliciosos no puedan eludirlo. También significa que el usuario no necesita utilizar un navegador moderno que admita trabajadores de servicio – incluso puede interceptar solicitudes de clientes de API que no sean navegadores.

Internamente, las funciones Edge utilizan el mismo motor de JavaScript V8 que se utiliza en el navegador Google Chrome para ejecutar los trabajadores en nuestra infraestructura. La V8 compila dinámicamente el código JavaScript en código de máquina ultra rápido, haciéndolo muy eficiente. Esto permite que el código se ejecute en microsegundos y que en nuestros límites se ejecuten miles de scripts por segundo.

Si Edge Functions utiliza V8, no utiliza Node.js. Las API de JavaScript disponibles dentro de los trabajadores están implementadas directamente por nosotros. Trabajar directamente con V8 permite que el código se ejecute de forma más eficiente y con los controles de seguridad necesarios para mantener seguros los clientes y la infraestructura.


## Acciones
{: #edge-functions-actions}

Las acciones se escriben en JavaScript y requieren que un escucha de sucesos responda a un suceso desencadenante. Las acciones no afectarán al tráfico a menos que las utilice un desencadenante. 

### Planes de empresa frente a planes estándar
{: #edge-functions-enterprise-v-standard-plans}

Los planes estándar tienen un máximo de una acción. A la acción se le asigna un nombre que es el mismo que el del dominio. Puede sustituir la acción cargando otro archivo o actualizarla utilizando el editor de código. Si se carga otro archivo, se elimina la acción existente.

Los planes de empresa pueden subir un número ilimitado de scripts. A estos se les pueden dar nombres exclusivos.

### Crear acciones
{: #edge-functions-create-actions}

Seleccione **Crear** para añadir una acción utilizando el editor de códigos. En los Planes de empresa, especifique un nombre para la acción. En los planes Estándar, el nombre no es editable y se utiliza el nombre del dominio. Tras añadir código Javascript, seleccione **Guardar** para crear la acción. 

### Cargar acciones
{: #edge-functions-upload-actions}

Utilice el botón **Cargar** para cargar un archivo Javascript. En los Planes de empresa, el nombre de la acción es el nombre del archivo. En los planes Estándar, para el nombre de la acción se utiliza el nombre del dominio.

Si se carga o se crea una acción con el mismo nombre que una acción que ya existe se sobrescribe la acción existente. Cambie el nombre del archivo de acción antes de cargarlo o especifique un nombre exclusivo en la entrada de texto al crear la acción para evitar este comportamiento.
{:note}

### Editar acciones
{: #edge-functions-edit-actions}

Al seleccionar una acción se abre la acción en el editor para modificarla. Al guardar los cambios, la acción se carga en la nube. Una vez hechas las actualizaciones deseadas, seleccione **Guardar**. Si la acción está en uso, los cambios entrarán en vigor inmediatamente. 

### Suprimir acciones
{: #edge-functions-delete-actions}

Para suprimir una acción, pulse el icono **suprimir** de la tabla **Acciones**. No se puede suprimir una acción mientras está en uso. Para suprimir la acción, primero debe eliminarla de los desencadenantes. En la columna **Usos** se muestra el número de desencadenantes asociados a esta acción. La acción de supresión no se puede deshacer.


### Desencadenantes asociados
{: #edge-functions-associated-triggers}

Puede añadir un desencadenante y asociarlo a una acción.

### Limitaciones conocidas de Edge Functions
{: #edge-functions-known-limitations}

Cargar una acción con el mismo nombre que una acción que ya existe. La acción existente se sobrescribe. Cambie el nombre del archivo de acción antes de cargarlo para evitar este comportamiento.


## Desencadenantes
{: #triggers}

### Acerca de los desencadenantes
{: #about-triggers}

Los desencadenantes (rutas) determinan el direccionamiento del tráfico del dominio a las Acciones. Los desencadenantes asocian ciertos patrones de URL, basados en un dominio de la cuenta, a una acción predefinida. El URL debe contener el dominio, pero puede contener comodines como prefijo del dominio o al final de la vía de acceso. Si no se proporciona ninguna vía de acceso en el patrón, se añade `/` de forma implícita. El patrón de URL no puede contener comodines como infijo ni parámetros de consulta. 

Debe añadir un dominio para añadir desencadenantes. Puede añadir desencadenantes sin tener acciones.

### Añadir desencadenantes
{: #add-triggers}

Vaya al separador **Desencadenantes** y pulse **Añadir desencadenante**. Especifique un patrón de URL y seleccione una acción en la lista de acciones existentes. 

Para una acción, también puede seleccionar **Evitar Edge Functions**. Esto permite que la vía de acceso del desencadenante permanezca activa, pero evite utilizar acciones de Edge Function. Por ejemplo, hay una acción denominada `my-function` y un desencadenante con la vía de acceso `beta.cistest-load.com/*`. Si la vía de acceso `beta.cistest-load.com/data` no debe utilizar la acción `my-function` cree otro desencadenante con la vía de acceso `beta.cistest-load.com/data` y la opción **Evitar Edge Functions**. Esto permite que la vía de acceso `beta.cistest-load.com/data` permanezca activa sin utilizar la acción `my-function`.

### Editar desencadenantes
{: #edit-triggers}

Puede actualizar un desencadenante utilizando la opción de menú de la fila de la tabla para un desencadenante seleccionado. Una vez hechas las actualizaciones deseadas, seleccione **Guardar**.

### Suprimir desencadenantes
{: #delete-triggers}

Puede suprimir un desencadenante utilizando la opción de menú de la fila de la tabla para un desencadenante seleccionado. Esta acción no se puede deshacer.


## Casos prácticos
{: #edge-functions-use-cases-examples}

Estos ejemplos son sólo para fines de demostración y no están pensados para utilizarlos en producción. 
{:important}
* [Pruebas A/B](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#ab-testing)
* [Añadir una cabecera de respuesta](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#add-response-header)
* [Agregar varias solicitudes](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#aggregate-multiple-requests)
* [Direccionamiento condicional](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#conditional-routing)
* [Protección de enlaces dinámicos](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#hot-link-protection)
* [Respuestas sin origen](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#originless-responses)
* [Solicitudes POST](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#post-requests)
* [Establecer una cookie](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#setting-cookies)
* [Solicitudes firmadas](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#signed-requests)
* [Respuestas en streaming](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#streaming-responses)
