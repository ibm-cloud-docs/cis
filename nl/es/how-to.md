---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Overview page, page rules, Service Mode

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Gestión del despliegue de IBM Cloud Internet Services (CIS)
{:#manage-your-cis-deployment}

Comenzará utilizando la pantalla Visión general como su base de operaciones de trabajo. Muestra todos los parámetros actuales para el despliegue.

Una vez que haya configurado su DNS y lo haya configurado, estará listo para empezar.

## Uso de la pantalla Visión general
{:#using-the-overview-screen}

Al utilizar la pantalla Visión general, puede ver el estado de todas las selecciones. Cada valor se enlaza con la sección de la interfaz de usuario donde se configura el valor. Para modificar cualquier selección, pulse en el enlace de ese valor. Por ejemplo, para cambiar la configuración del equilibrador de carga o añadir un nuevo equilibrador de carga, pulse en el campo `Equilibrador de carga`.

En la pantalla Visión general, puede ver que la configuración del nombre de dominio se encuentra en estado **Pendiente**, o en estado **Activo**, tal como se muestra en la figura siguiente.


![imagen de la pantalla visión general](images/overview-screen-configuration-summary.jpg)

El estado **Pendiente** indica que el dominio aún no se ha configurado completamente. Tiene que actualizar el proveedor de DNS o el registrador con los servidores de nombres que se proporcionan como parte del proceso de configuración.

**Sólo Empresa**: la sección **Detalles de servicio** de la Visión general también le permite añadir dominios adicionales a su instancia de CIS y conmutar entre diversos dominios.

## Cambiar la modalidad de servicio
{#changing-the-service-mode}

En la página Visión general, en la sección Modalidad de servicio, hay una lista desplegable para seleccionar uno modalidad de entre dos:

* **Modalidad de defensa** ayuda a proteger frente a los ataques DNS existentes o previstos. Esta modalidad impide que el tráfico llegue a sus servidores de origen a través de su dominio.
* **Poner servicio en pausa** inhabilita todas las ventajas de seguridad y rendimiento de su dominio. Las funciones DNS se siguen resolviendo en su sitio web, pero el tráfico se envía directamente a los orígenes configurados. 

### Pasos para establecer la modalidad de servicio
{:#steps-to-set-service-mode}

1. Seleccione la modalidad deseada en el menú desplegable.
1. Pulse el botón `Activar`.
1. Confirme o cancele la selección en la ventana emergente de confirmación.

Aparecerá una notificación en todas las páginas para mostrar que Poner servicio en pausa o Modalidad de defensa están activos.
Para volver al funcionamiento normal, pulse `Desactivar modalidad` en el banner de notificación. ![imagen de botón Desactivar modalidad](images/deactivate-mode.png)


## Configuración y gestión del DNS
{:#configure-and-manage-your-dns}

Vaya a su página DNS y añada un registro (más probable, un registro A). Escriba la información sobre el registro DNS y luego pulse `Añadir registro` para implementar los cambios.

![add-DNS](images/dns/create-a-type-record.png)

Después de crear los registros, considere la posibilidad de activar el parámetro `Proxy`. La mayoría de las características de CIS requieren que el tráfico de Internet a su sitio fluya a través de la infraestructura de CIS. En otras palabras, sólo se aplica a registros redirigidos por proxy y a los equilibradores de carga. Para realmente aprovechar CIS, asegúrese de que los registros de DNS y los equilibradores de carga tienen el parámetro proxy habilitado.

## Configuración y gestión del almacenamiento en memoria caché
{:#set-up-and-manage-your-caching}

A continuación, puede configurar el almacenamiento en memoria caché. 

![IMAGE](images/caching-screen.png)

Tiene la opción de 3 tipos de almacenamiento en memoria caché, disponible desde el menú desplegable de la pantalla de almacenamiento en memoria caché: 

 * Sin serie de consulta: Solo ofrece recursos de memoria caché cuando no hay ninguna serie de consulta.
 * Serie de consulta independiente: Ofrece el mismo recurso a todo el mundo, independientemente de la serie de consulta. (Nota: El valor **Ignorar serie de consulta** solo se aplica a las extensiones de archivo estáticas. Este valor elimina la serie de consulta al generar la clave de la memoria caché, de forma que una solicitud para `style.css?something` se normaliza a `style.css` al servir desde la memoria caché).
 * Serie de consulta dependiente: Ofrece un recurso distinto cada vez que cambie la serie de consulta.
  
## Depurar caché
{:#purge-cache-overview}
 
Puede depurar la caché para prepararse para las actualizaciones en cualquier momento, tan solo especificando el URL en el campo depurar caché. Puede depurar un único archivo o varios archivos (un máximo de 30 a la vez).
 
 ## Caducidad del navegador
 {:#browser-expiration}
 
Puede utilizar el menú desplegable para seleccionar el momento de caducidad del navegador que necesite, por ejemplo 8 horas, o 1 día.

Sólo Empresa: también puede indicar a CIS que no sustituya el control de memoria caché de navegador estableciendo esta opción en **Respetar cabeceras existentes**.
 
 ## Uso de la modalidad de desarrollo
 {:#using-development-mode}
 
La **modalidad de desarrollo** está pensada para utilizarse cuando son necesarias actualizaciones importantes o cargas de archivos nuevas, o en cualquier momento que no desee que los usuarios finales trabajen desde la memoria caché, sino recuperar archivos directamente desde los servidores de origen. Para empezar a utilizar **Modelo de desarrollo**, cambie el conmutador a la posición `Habilitado`. Para dejar de utilizar **Modalidad de desarrollo**, cambie el conmutador a la posición `Inhabilitado`. **Modalidad de desarrollo** caduca automáticamente después de 3 horas. 

## Gestión de las reglas de página
{:#managing-your-page-rules}
 
Puede utilizar reglas de página para especificar valores particulares que se apliquen únicamente a ciertos URL, por ejemplo para tener distintos valores de control de memoria caché para ciertas vías de acceso de URL. Utilice los menús desplegables para configurar la Regla de página. Los valores de las reglas se dividen en tres categorías: **Seguridad**, **Rendimiento** y **Fiabilidad**.

Tenga en cuenta que cuando están habilitadas determinadas reglas, otras opciones pasarán a estar inactivas, si esas opciones están en conflicto con el resto de las reglas que acabe de seleccionar. Después de haber seleccionado las Reglas de página que deseara, pulse **Suministro** para habilitarlas. Las nuevas reglas entrarán en vigor inmediatamente, y pueden verse inmediatamente en la pantalla Reglas de página.
 
 ![PAGE RULES MENUS](images/page-rule-dropdown-settings.png)
 
También puede habilitar o inhabilitar las Reglas de página desde la tabla que se muestra en la pantalla Reglas de página. Consulte [Uso de Reglas de página](/docs/infrastructure/cis?topic=cis-use-page-rules) para obtener más información.
 
 ## Valores de seguridad
 {:#security-settings-overview}
 
De forma predeterminada, la protección DDoS está habilitada para cualquier registro DNS o equilibrador de carga que tenga proxy activado. 
Los valores de seguridad son: 

* Active WAF utilizando el conmutador en la página **Cortafuegos de aplicación web**. Cuando active o desactive las reglas, los cambios se aplicarán inmediatamente.

* **Sólo Empresa**: la página **Limitación de velocidad** le permite configurar reglas para limitar la velocidad para evitar problemas de vecinos ruidosos y repeler DDoS.

* En la página **Cortafuegos de IP**, puede configurar reglas de acceso basadas en IP, código de país o ASN. También puede configurar reglas para bloquear agentes de usuario. La sección de bloqueo de dominio de esta página le permite limitar el acceso a su dominio a determinadas direcciones IP.

* Puede revisar los sucesos relacionados con el cortafuegos en la página **Sucesos**.

## Certificados
{:#certificates-overview}

Al configurar un dominio, IBM CIS despliega automáticamente un certificado universal para ese dominio. Así pues, no necesita hacer nada para tener protección basada en certificado en ese dominio. Si lo desea, puede cargar su propio certificado. Necesitará un certificado independiente para cada dominio, y verá un mensaje de error si el certificado que está cargando no coincide con el dominio. También puede solicitar certificados personalizados en esta página. 

![IMAGE](images/certificates-table.png)
 
 
