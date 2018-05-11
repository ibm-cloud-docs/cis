---
copyright:
  years: 2018
lastupdated: "2018-03-17"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Gestión del despliegue de IBM Cloud Internet Services (CIS)

Comenzará utilizando la pantalla Visión general como su base de operaciones de trabajo. Muestra todos los parámetros actuales para el despliegue.

Una vez que haya configurado su DNS y lo haya configurado, estará listo para empezar.

## Uso de la pantalla Visión general

Al utilizar la pantalla Visión general, puede ver el estado de todas las selecciones. Puede cambiar los valores directamente desde la pantalla Visión general, tan solo pulsando en el nombre subrayado del valor que desea cambiar; por ejemplo, podría pulsar el campo `Equilibradores de carga` para añadir un Equilibrador de carga.

En la pantalla Visión general, puede ver que la configuración del nombre de dominio se encuentra en estado **Pendiente**, o en estado **Activo**, tal como se muestra en la figura siguiente.

![imagen de la pantalla visión general](images/overview-screen-configuration-summary.png)


## Configuración y gestión del DNS

Vaya a su página DNS y añada un registro (más probable, un registro A). Escriba la información sobre el registro DNS y luego pulse `Añadir registro` para implementar los cambios.

![add-DNS](images/dns/create-a-type-record.png)

## Configuración y gestión del almacenamiento en memoria caché

A continuación, puede configurar el almacenamiento en memoria caché. 

![IMAGE](images/caching-screen.png)

Tiene la opción de 3 tipos de almacenamiento en memoria caché, disponible desde el menú desplegable de la pantalla de almacenamiento en memoria caché: 

 * Sin serie de consulta: Solo ofrece recursos de memoria caché cuando no hay ninguna serie de consulta.
 * Serie de consulta independiente: Ofrece el mismo recurso a todo el mundo, independientemente de la serie de consulta. (Nota: El valor **Ignorar serie de consulta** solo se aplica a las extensiones de archivo estáticas. Este valor elimina la serie de consulta al generar la clave de la memoria caché, de forma que una solicitud para `style.css?something` se normaliza a `style.css` al servir desde la memoria caché).
 * Serie de consulta dependiente: Ofrece un recurso distinto cada vez que cambie la serie de consulta.
  
## Depurar caché
 
Puede depurar la caché para prepararse para las actualizaciones en cualquier momento, tan solo especificando el URL en el campo depurar caché. Puede depurar un único archivo o varios archivos (un máximo de 30 a la vez).
 
 ## Caducidad del navegador
 
Puede utilizar el menú desplegable para seleccionar el momento de caducidad del navegador que necesite, por ejemplo 8 horas, o 1 día.
 
 ## Uso de la modalidad de desarrollo
 
La **modalidad de desarrollo** está pensada para utilizarse cuando son necesarias actualizaciones importantes o cargas de archivos nuevas, o en cualquier momento que no desee que los usuarios finales trabajen desde la memoria caché, sino recuperar archivos directamente desde los servidores de origen. Para empezar a utilizar **Modelo de desarrollo**, cambie el conmutador a la posición `Habilitado`. Para dejar de utilizar **Modalidad de desarrollo**, cambie el conmutador a la posición `Inhabilitado`. **Modalidad de desarrollo** caduca automáticamente después de 3 horas. 

## Gestión de las reglas de página
 
Puede habilitar hasta 50 Reglas de página. Utilice los menús desplegables para configurar la Regla de página. Los valores de las reglas se dividen en tres categorías: **Seguridad**, **Rendimiento** y **Fiabilidad**.

Tenga en cuenta que cuando están habilitadas determinadas reglas, otras opciones pasarán a estar inactivas, si esas opciones están en conflicto con el resto de las reglas que acabe de seleccionar. Después de haber seleccionado las Reglas de página que deseara, pulse **Suministro** para habilitarlas. Las nuevas reglas entrarán en vigor inmediatamente, y pueden verse inmediatamente en la pantalla Reglas de página.
 
 ![PAGE RULES MENUS](images/page-rule-dropdown-settings.png)
 
También puede habilitar o inhabilitar las Reglas de página desde la tabla que se muestra en la pantalla Reglas de página. Consulte [Uso de Reglas de página](using-page-rules.html) para obtener más información.
 
 ## Valores de seguridad
 
De forma predeterminada, la protección DDoS está habilitada para cualquier registro DNS que tenga proxy, lo que se puede hacer desde la tabla **Registros** en la página DNS. Active WAF utilizando el conmutador. Cuando active o desactive las reglas, los cambios se aplicarán inmediatamente.

![IMAGE](images/ddos-waf-ssl-screen.png)

## Certificados

Al desplegar en una Zona, IBM CIS desplegará automáticamente un certificado universal para esa zona. Así, no necesita hacer nada para tener protección basada en certificado en esa zona. Si lo desea, puede cargar su propio certificado. Necesitará un certificado independiente para cada zona, y verá un mensaje de error si el certificado que está cargando no coincide con la zona.

![IMAGE](images/certificates-table.png)
 
 ## Establecimiento y configuración de los equilibradores de carga
 
 IBM CIS proporciona equilibrio de carga global como un servicio.

![IMAGE](images/glb-screen.png)

### Panel de control de GLB
En el panel de control, verá tres listas que muestran los equilibradores de carga, las agrupaciones de origen y las comprobaciones de estado. Las listas muestran el equilibrador de carga global nuevo o actualizado o uno de sus componentes cuando lo suministre o lo actualice. Inicialmente, las listas están vacías, y antes de crear un equilibrador de carga debe realizar algunas acciones.

#### Crear
**Nota**: <sup>`*`</sup> indica que este paso es opcional

1) <sup>`*`</sup>Crear una comprobación de estado, pulse "Crear comprobación de estado".
  ![IMAGE](images/glb-health-check-list.png)
    <ul>
      <li>* **Vía de acceso**: La vía de acceso de punto final en la que comprobar el estado.</li> 
      <li>* **Tipo**: El protocolo que se utilizará para la comprobación de estado.</li>
      <li>* **Descripción**: Descripción proporcionada por el usuario.</li>
    </ul>

2) Crear una agrupación, pulse "Crear agrupación".
  ![IMAGE](images/glb-pool-list.png)
    <ul>
      <li>* **Estado**: Estado de la agrupación.</li>
      <li>* **Nombre**: Nombre proporcionado por el usuario.</li>
      <li>* **Orígenes**: Recuento de orígenes de estado en la agrupación.</li>
      <li>* **Comprobación de estado**: Vía de acceso de la comprobación de estado adjunta, si la hay.</li>
    </ul>

3) Crear un equilibrador de carga, pulse "Crear equilibrador de carga".
  ![IMAGE](images/glb-load-balancer-list.png)
    <ul>
      <li>* **Estado**: Estado del equilibrador de carga.</li>
      <li>* **Nombre de host**: Nombre preañadido al nombre de dominio.</li>
      <li>* **Agrupaciones disponibles**: Recuento de agrupaciones en buen estado.</li>
      <li>* **TTL**: Tiempo de duración.</li>
      <li>* **Proxy**: Habilitar o inhabilitar el flujo de tráfico de proxy.</li>
      <li>* **Estado**: Habilitar o inhabilitar el equilibrador de carga.</li>
    </ul>

#### Editar/suprimir
Para editar o suprimir un equilibrador de carga o uno de sus componentes, pulse el botón de menú de desbordamiento ubicado en el extremo derecho de cada fila.

Botón de menú de desbordamiento:

![IMAGE](images/overflow.png)

Las opciones siguientes se proporcionan para cada lista.

* Comprobación de estado
    * **Editar comprobación de estado**: Esta opción redirige al usuario al flujo de edición. 
    * **Suprimir comprobación de estado**: Esta opción abre el recuadro de diálogo de confirmación para el flujo de supresión.

* Agrupación
    * **Ver detalles de la agrupación**: Esta opción abre un recuadro de diálogo modal con información sobre la agrupación.
    * **Editar agrupación**: Esta opción redirige al usuario al flujo de edición.
    * **Suprimir agrupación**: Esta opción abre el recuadro de diálogo de confirmación para el flujo de supresión.

* Equilibrador de carga
    * **Inhabilitar/Habilitar**: Habilitar o inhabilitar un equilibrador de carga.
    * **Editar equilibrador de carga**: Redirige al flujo de edición. 
    * **Suprimir equilibrador de carga**: Abre el recuadro de diálogo de confirmación para el flujo de supresión.

### Adición de una comprobación de estado

Las comprobaciones de estado son archivos adjuntos opcionales para agrupaciones de origen. Utilizan un intervalo de repetición personalizado para probar un cuerpo de respuesta específico, o para un código de estado, para supervisar el estado de la agrupación. Una vez creadas, las comprobaciones de estado se pueden añadir a una agrupación de origen nueva o existente.

Al crear una comprobación de estado, solo se necesita un campo:
 * **Código de respuesta**: El código de respuesta HTTP esperado o el rango de códigos de la comprobación de estado. Este valor debe estar entre 200 y 299 con comodines indicados por una 'x'.

Campos opcionales adicionales:
 * **Vía de acceso**: La vía de acceso de punto final en la que se realizará la comprobación de estado (su valor predeterminado es /).
 * **Tipo**: El protocolo que se utilizará para la comprobación de estado (el valor predeterminado es HTTP).
 * **Descripción**: Descripción de la comprobación de estado.
 * **Intervalo**: El intervalo (en segundos) entre cada comprobación de estado. Los intervalos más cortos pueden mejorar el tiempo de migración tras error, pero aumentan la carga en los orígenes, ya que las comprobaciones provienen de varias ubicaciones (el valor predeterminado es 60).
 * **Método**: El método HTTP que se utilizará para la comprobación de estado (el valor predeterminado es GET).
 * **Tiempo de espera**: El tiempo (en segundos) antes de marcar la comprobación de estado como fallida (el valor predeterminado es 5).
 * **Reintentos**: El número de reintentos que se realizarán en caso de que se supere el tiempo de espera antes de marcar el origen como en mal estado. Los reintentos se realizarán inmediatamente (el valor predeterminado es 2).
 * **Cuerpo de respuesta**: Una subserie que no distingue entre mayúscula y minúscula para hacerla coincidir en el cuerpo de respuesta. Si esta serie no se encuentra, el origen se marcará como en mal estado.
 * **Cabeceras de solicitud**: Las cabeceras de solicitud HTTP que se enviarán en la comprobación de estado. Se recomienda establecer una cabecera Host de forma predeterminada. La cabecera `User-Agent` no se puede sobrescribir.

### Adición de una agrupación

Es necesaria al menos una agrupación para cada equilibrador de carga suministrado. Las agrupaciones agrupan sus orígenes para el equilibrador de carga que se utilizará.

Al crear una agrupación, serán necesarios dos campos:
 * **Nombre**: Un nombre abreviado (etiqueta) para la agrupación. Solo se permiten caracteres alfanuméricos, guiones y subrayados.
 * **Orígenes**: La lista de orígenes de esta agrupación. El tráfico dirigido a esta agrupación se equilibra entre todos los orígenes que están en buen estado actualmente, siempre que la agrupación lo esté también.

Campos opcionales adicionales:
 * **Descripción**: Una descripción legible por humanos de la agrupación.
 * **Habilitado**: Habilitar (valor predeterminado) o no esta agrupación. Las agrupaciones inhabilitadas no reciben tráfico y están excluidas de las comprobaciones de estado. La inhabilitación de una agrupación hace que cualquier equilibrador de carga que la utilice migre tras error a la siguiente agrupación, si la hay (el valor predeterminado es true).
 * **Umbral de origen en buen estado**: El número mínimo de orígenes que deben estar en buen estado para que esta agrupación sirva tráfico. Si el número de orígenes en buen estado está por debajo de este número, la agrupación se marcará como en mal estado y migrará tras error a la siguiente agrupación disponible (el valor predeterminado es 1).
 * **Regiones de comprobación de estado**: Región desde la que la comprobación de estado realizará la supervisión.
 * **Comprobación de estado**: La comprobación de estado que se utilizará para comprobar orígenes dentro de esta agrupación (el valor predeterminado es sin comprobación de estado).
 * **Correo electrónico de notificación**: La dirección de correo electrónico que debería recibir las notificaciones de estado. Esta dirección puede ser un buzón de correo individual o una lista de distribución.

 ### Adición de un equilibrador de carga

Los equilibradores de carga ayudan a distribuir el tráfico con proxy en varias agrupaciones de origen utilizando una distribución en rueda.

Al crear un equilibrador de carga, los campos necesarios son:
 * **Nombre**: El nombre de host de DNS que se asociará con el Equilibrador de carga. Si este nombre de host ya existe como un registro de DNS en el DNS de IBM, el Equilibrador de carga tendrá prioridad y el registro de DNS no se utilizará.
 * **Agrupaciones predeterminadas**: Una lista de ID de agrupación. La lista está ordenada por su prioridad de migración tras error. Las agrupaciones definidas aquí se utilizan de forma predeterminada, o cuando las agrupaciones de regiones no están configuradas para una región determinada.

Opcionalmente, se pueden configurar los campos siguientes:
 * **Proxy**: Direcciona el tráfico a través del servicio de rendimiento y de métricas de IBM.
 * **Afinidad de sesiones**: Direcciona siempre a través de la misma instancia de rendimiento y de métricas. Esta opción solo está disponible si el proxy está habilitado.
 * **TTL**: Tiempo de duración (TTL) de la entrada DNS para la dirección IP devuelta por este equilibrador de carga. Esta opción solo se aplica a los equilibradores de carga sin proxy; de lo contrario, tiene como valor predeterminado `Automatic`.
 * **Agrupaciones de región**: Una correlación de códigos de regiones o de países en una lista de agrupaciones (ordenadas por su prioridad de migración tras error) para la región determinada. Cualquier región no definida explícitamente volverá a utilizar las agrupaciones predeterminadas.
