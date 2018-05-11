---

copyright:
  years: 2018
lastupdated: "2018-03-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Configure el Sistema de nombres de dominio (DNS) para IBM CIS

Este documento contiene algunas instrucciones específicas sobre cómo configurar los registros DNS de IBM CIS, incluyendo cómo configurar DNS seguro.

## DNS seguro

**DNSSec** es una tecnología para 'firmar' digitalmente datos DNS para poder asegurarse de que sean válidos. Para eliminar la vulnerabilidad de Internet, DNSSec debe desplegarse en cada paso de la búsqueda, desde la zona raíz al nombre de dominio final (por ejemplo, www.icann.org).

## Configuración y gestión de DNS seguro 

DNSSec añade una capa de autenticación a la infraestructura DNS de Internet, que de lo contrario no es segura. DNS seguro garantiza que los visitantes se dirijan a **su** servidor web cuando escriban su nombre de dominio en un navegador web. Todo lo que tiene que hacer es habilitar DNSSec en su página DNS desde la cuenta de IBM CIS y añadir el registro DS a su registrador.

![DNS seguro](images/dns/secure-dns.png)

Puede seleccionar el botón **Ver registros DS** para abrir un recuadro de diálogo que explique cómo añadir el registro DS a su registrador. Debe copiar partes del registro DS y pegarlas en el panel de control del registrador. Cada registrador es diferente, y el registrador solo puede necesitar que especifique información para algunos de los campos disponibles.

## Adición de registros DNS

Puede utilizar el desplegable **Tipo** para seleccionar el tipo de registro que desee crear. Cada tipo de registro de DNS tiene un Nombre y un TTL (Time-To-Live) asociado con él. 

Todo lo que se especifique en el campo Nombre tendrá un nombre de dominio añadido al mismo a menos que el nombre de dominio ya esté añadido manualmente en el campo (p. ej., si se escribe `www` o `www.example.com` en el campo, la API manejará los dos como `www.example.com`). Si el nombre de dominio exacto se escribe en el campo de nombre, no se añadirá en sí mismo (p. ej., `example.com` se manejará como `example.com`). Sin embargo, la lista de registros DNS solo mostrará los nombres sin el nombre de dominio agregado, por lo que `www.example.com` se muestra como `www` y `example.com` se mostrará como `example.com`. El TTL tendrá un valor predeterminado de `Automatic`, pero el usuario lo puede cambiar. Un registro DNS proxy siempre tendrá un TTL de `Automatic`, de modo que un nuevo registro de proxy cambiará a esta configuración durante este cambio.

### Registro de Tipo A

Para añadir este tipo de registro, deben existir valores válidos en los campos **Nombre** y **Dirección IPv4**. Un **TTL** también se puede especificar desde el menú desplegable, con un valor predeterminado de 'Automatic'.

![Crear registro de Tipo A](images/dns/create-a-type-record.png)

    Campos obligatorios: Nombre, Dirección IPv4
    Campo opcional: TTL (El valor predeterminado es Automatic)

### Registro de Tipo AAAA

Para añadir este tipo de registro, deben existir valores válidos en los campos **Nombre** y **Dirección IPv6**. Un **TTL** también se puede especificar desde el menú desplegable, con el valor predeterminado de 'Automatic'.

![Crear registro de Tipo AAAA](images/dns/create-aaaa-type-record.png)

    Campos obligatorios: Nombre, Dirección IPv6
    Campo opcional: TTL (El valor predeterminado es Automatic)

### Registro de Tipo CNAME

Para añadir este tipo de registro, debe existir un valor válido en el campo **Nombre** y un nombre de dominio completo debe estar en el campo **Nombre de dominio** (FQDN). Un **TTL** también se puede especificar desde el menú desplegable, con el valor predeterminado de 'Automatic'.


![Crear registro de Tipo CNAME](images/dns/create-cname-type-record.png)

    Campos obligatorios: Nombre, Nombre de dominio (para CNAME)
    Campo opcional: TTL (El valor predeterminado es Automatic)


### Registro de Tipo MX

Para añadir este tipo de registro, debe existir un valor válido en el campo **Nombre** y debe existir una dirección válida en el campo **Servidor de correo**. Un **TTL** también se puede especificar desde el menú desplegable, con el valor predeterminado de 'Automatic'.

![Crear registro de Tipo MX](images/dns/create-mx-type-record.png)

    Campos obligatorios: Nombre, Servidor de correo
    Campos opcionales: TTL (El valor predeterminado es Automatic), Prioridad (El valor predeterminado es 1)

### Registro de Tipo LOC

Para añadir este tipo de registro, debe existir un valor válido en el campo **Nombre**. Si necesita información más específica, seleccione el botón **Configurar opciones LOC**. Un **TTL** también se puede especificar desde el menú desplegable, con el valor predeterminado de 'Automatic'.

![Crear registro de Tipo LOC](images/dns/create-loc-type-record-1.png)

    Campos obligatorios: Nombre
    Campos opcionales: opciones de LOC (pulse el botón para configurar)

![Crear registro de Tipo LOC](images/dns/create-loc-type-record-2.png)

### Registro de Tipo CAA

Para añadir este tipo de registro, deben existir valores válidos en los campos **Nombre** y **Valor**. El campo Valor se correlacionará con el valor del campo desplegable **Código**, cuyo valor predeterminado es "Send violation reports to URL". Un **TTL** también puede especificarse desde el desplegable, con el valor predeterminado de 'Automatic'.

![Crear registro de Tipo CAA](images/dns/create-caa-type-record.png)

    Campos obligatorios: Nombre, Valor (asociado a etiqueta)
    Campos opcionales: TTL (el valor predeterminado es Automatic), Etiqueta (el valor predeterminado es send violation reports to URL)

### Registro de Tipo SRV

Para añadir este tipo de registro, deben existir valores válidos en los campos **Nombre**, **Nombre de servicio** y **Destino**. Utilice el menú desplegable para seleccionar un **protocolo**, que tiene como valor predeterminado el protocolo UDP. Adicionalmente, puede especificar **Prioridad**, **Peso** y **Puerto**. Estos tres campos tienen como valor predeterminado un valor de 1. Un **TTL** también se puede especificar desde el menú desplegable, con el valor predeterminado de 'Automatic'.

![Crear registro de Tipo SRV](images/dns/create-srv-type-record.png)

    Campos obligatorios: Nombre, Nombre de servicio, Destino
    Campos opcionales: TTL (el valor predeterminado es Automatic), Protocolo (el valor predeterminado es UDP), Prioridad (el valor predeterminado es 1), Peso (el valor predeterminado es 1), Puerto (el valor predeterminado es 1)

### Registro de Tipo SPF

Para añadir este tipo de registro, deben existir valores válidos en los campos **Nombre** y **Contenido**. Un **TTL** también se puede especificar desde el menú desplegable, con el valor predeterminado de 'Automatic'.

![Crear registro de Tipo SPF](images/dns/create-spf-type-record.png)

    Campos obligatorios: Nombre, Contenido
    Campo opcional: TTL (el valor predeterminado es Automatic)

### Registro de Tipo TXT

Para añadir este tipo de registro, deben existir valores válidos en los campos **Nombre** y **Contenido**. Un **TTL** también se puede especificar desde el menú desplegable, con el valor predeterminado de 'Automatic'.

![Crear registro de Tipo TXT](images/dns/create-txt-type-record.png)

    Campos obligatorios: Nombre, Contenido
    Campo opcional: TTL (el valor predeterminado es Automatic)

### Registro de Tipo NS

Para añadir este tipo de registro, deben existir valores válidos en los campos **Nombre** y **Servidor de nombres**. Un **TTL** también se puede especificar desde el menú desplegable, con el valor predeterminado de 'Automatic'.

![Crear registro de Tipo NS](images/dns/create-ns-type-record.png)

    Campos obligatorios: Nombre, Servidor de nombres
    Campo opcional: TTL (el valor predeterminado es Automatic)

## Actualización de registros DNS

En cada fila de registro, puede pulsar la opción **Editar registro** desde el menú, lo que abrirá un recuadro de diálogo, que puede utilizar para actualizar el registro.

![Editar registro de DNS](images/dns/edit-dns-record.png)

Por ejemplo, este es el diálogo de actualización para el registro de tipo **A**. Cuando haya terminado de realizar los cambios, seleccione **Actualizar registro** para guardarlos.

![Editar diálogo de registro de DNS](images/dns/update-dns-dialog.png)

## Supresión de registros

En cada fila de registro, puede seleccionar la opción **Suprimir registro** desde el menú, lo que abre un recuadro de diálogo para confirmar el proceso de supresión.

![Suprimir registro de DNS](images/dns/delete-record.png)

Puede seleccionar el botón **Suprimir** para confirmar la acción de supresión. Seleccione **Cancelar** si no desea suprimir.

![Suprimir diálogo de registro de DNS](images/dns/delete-record-dialog.png)
