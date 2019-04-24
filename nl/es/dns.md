---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM CIS DNS records, parts of the DS record, Type

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"} 
{:note: .note} 
{:important: .important} 
{:deprecated: .deprecated} 
{:generic: data-hd-programlang="generic"}

# Configure el Sistema de nombres de dominio (DNS) para IBM CIS
{:#set-up-your-dns-for-cis}

Este documento contiene algunas instrucciones específicas sobre cómo configurar los registros DNS de IBM CIS, incluyendo cómo configurar DNS seguro.

## DNS seguro
{:#secure-dns}

**DNSSec** es una tecnología para "firmar" digitalmente los datos de DNS y así asegurarse de que son válidos. Para eliminar la vulnerabilidad de Internet, DNSSec debe desplegarse en cada paso de la búsqueda, desde la zona raíz al nombre de dominio final (por ejemplo, www.icann.org).

## Configuración y gestión de DNS seguro 
{:#configuring-and-managing-your-secure-dns}

DNSSec añade una capa de autenticación a la infraestructura DNS de Internet, que de lo contrario no es segura. DNS seguro garantiza que los visitantes se dirijan a **su** servidor web cuando escriban su nombre de dominio en un navegador web.  Todo lo que tiene que hacer es habilitar DNSSec en su página DNS desde la cuenta de IBM CIS y añadir el registro DS a su registrador.

![DNS seguro](images/dns/secure-dns.png)

Puede seleccionar el botón **Ver registros DS** para abrir un recuadro de diálogo que explique cómo añadir el registro DS a su registrador. Debe copiar partes del registro DS y pegarlas en el panel de control del registrador. Cada registrador es diferente, y el registrador solo puede necesitar que especifique información para algunos de los campos disponibles.

## Adición de registros DNS
{:#adding-dns-records}

Puede utilizar el desplegable **Tipo** para seleccionar el tipo de registro que desee crear. Cada tipo de registro de DNS tiene un Nombre y un TTL (Time-To-Live) asociado con él. 

Todo lo que se especifique en el campo Nombre tendrá un nombre de dominio añadido al mismo a menos que el nombre de dominio ya esté añadido manualmente en el campo (p. ej., si se escribe `www` o `www.example.com` en el campo, la API manejará los dos como `www.example.com`). Si el nombre de dominio exacto se escribe en el campo de nombre, no se añadirá en sí mismo (p. ej., `example.com` se manejará como `example.com`). Sin embargo, la lista de registros DNS solo mostrará los nombres sin el nombre de dominio agregado, por lo que `www.example.com` se muestra como `www` y `example.com` se mostrará como `example.com`. El TTL tendrá un valor predeterminado de `Automatic`, pero el usuario lo puede cambiar. Un registro DNS proxy siempre tendrá un TTL de `Automatic`, de modo que un nuevo registro de proxy cambiará a esta configuración durante este cambio.

### Registro de Tipo A
{:#a-type-record}

Para añadir este tipo de registro, deben existir valores válidos en los campos **Nombre** y **Dirección IPv4**. También se puede especificar un **TTL** desde el menú desplegable, con el valor predeterminado `Automatic`.

![Crear registro de Tipo A](images/dns/create-a-type-record.png)

    Campos obligatorios: Nombre, Dirección IPv4
    Campo opcional: TTL (El valor predeterminado es Automatic)

### Registro de Tipo AAAA
{:#aaaa-type-record}

Para añadir este tipo de registro, deben existir valores válidos en los campos **Nombre** y **Dirección IPv6**. También se puede especificar un **TTL** desde el menú desplegable, con el valor predeterminado `Automatic`.

![Crear registro de Tipo AAAA](images/dns/create-aaaa-type-record.png)

    Campos obligatorios: Nombre, Dirección IPv6
    Campo opcional: TTL (El valor predeterminado es Automatic)

### Registro de Tipo CNAME
{:#cname-type-record}

Para añadir este tipo de registro, debe existir un valor válido en el campo **Nombre** y un nombre de dominio completo debe estar en el campo **Nombre de dominio** (FQDN). También se puede especificar un **TTL** desde el menú desplegable, con el valor predeterminado `Automatic`.


![Crear registro de Tipo CNAME](images/dns/create-cname-type-record.png)

    Campos obligatorios: Nombre, Nombre de dominio (para CNAME)
    Campo opcional: TTL (El valor predeterminado es Automatic)

Los planes de empresa pueden añadir un registro CNAME en otro dominio siempre y cuando ese dominio esté configurado dentro de CIS.
{:note}

```
Por ejemplo,
Dominios de CIS configurados:
  - example.com
  - different.com

test.example.com -CNAME-> test.different.com
```

### Registro de Tipo MX
{:#mx-type-record}

Para añadir este tipo de registro, debe existir un valor válido en el campo **Nombre** y debe existir una dirección válida en el campo **Servidor de correo**. También se puede especificar un **TTL** desde el menú desplegable, con el valor predeterminado `Automatic`.

![Crear registro de Tipo MX](images/dns/create-mx-type-record.png)

    Campos obligatorios: Nombre, Servidor de correo
    Campos opcionales: TTL (El valor predeterminado es Automatic), Prioridad (El valor predeterminado es 1)

### Registro de Tipo LOC
{:#loc-type-record}

Para añadir este tipo de registro, debe existir un valor válido en el campo **Nombre**. Si necesita información más específica, seleccione el botón **Configurar opciones LOC**. También se puede especificar un **TTL** desde el menú desplegable, con el valor predeterminado `Automatic`.

![Crear registro de Tipo LOC](images/dns/create-loc-type-record-1.png)

    Campos obligatorios: Nombre
    Campos opcionales: opciones de LOC (pulse el botón para configurar)

![Crear registro de Tipo LOC](images/dns/create-loc-type-record-2.png)

### Registro de Tipo CAA
{:#caa-type-record}

Para añadir este tipo de registro, deben existir valores válidos en los campos **Nombre** y **Valor**. El campo Valor se correlacionará con el valor del campo desplegable **Código**, cuyo valor predeterminado es "Send violation reports to URL". También se puede especificar un **TTL** desde el menú desplegable, con el valor predeterminado `Automatic`.

![Crear registro de Tipo CAA](images/dns/create-caa-type-record.png)

    Campos obligatorios: Nombre, Valor (asociado a etiqueta)
    Campos opcionales: TTL (el valor predeterminado es Automatic), Etiqueta (el valor predeterminado es send violation reports to URL)

### Registro de Tipo SRV
{:#srv-type-record}

Para añadir este tipo de registro, deben existir valores válidos en los campos **Nombre**, **Nombre de servicio** y **Destino**. Utilice el menú desplegable para seleccionar un **protocolo**, que tiene como valor predeterminado el protocolo UDP. Adicionalmente, puede especificar **Prioridad**, **Peso** y **Puerto**. Estos tres campos tienen como valor predeterminado el valor 1. También se puede especificar un **TTL** desde el menú desplegable, con el valor predeterminado `Automatic`.

![Crear registro de Tipo SRV](images/dns/create-srv-type-record.png)

    Campos obligatorios: Nombre, Nombre de servicio, Destino
    Campos opcionales: TTL (el valor predeterminado es Automatic), Protocolo (el valor predeterminado es UDP), Prioridad (el valor predeterminado es 1), Peso (el valor predeterminado es 1), Puerto (el valor predeterminado es 1)

### Registro de Tipo SPF
{:#spf-type-record}

Para añadir este tipo de registro, deben existir valores válidos en los campos **Nombre** y **Contenido**. También se puede especificar un **TTL** desde el menú desplegable, con el valor predeterminado `Automatic`.

![Crear registro de Tipo SPF](images/dns/create-spf-type-record.png)

    Campos obligatorios: Nombre, Contenido
    Campo opcional: TTL (el valor predeterminado es Automatic)

### Registro de Tipo TXT
{:#txt-type-record}

Para añadir este tipo de registro, deben existir valores válidos en los campos **Nombre** y **Contenido**. También se puede especificar un **TTL** desde el menú desplegable, con el valor predeterminado `Automatic`.

![Crear registro de Tipo TXT](images/dns/create-txt-type-record.png)

    Campos obligatorios: Nombre, Contenido
    Campo opcional: TTL (el valor predeterminado es Automatic)

La primera vez que solicita un certificado dedicado, se produce un proceso de Validación de control de dominio (DCV) que genera en correspondiente registro TXT. Si suprime el registro TXT, se producirá otra vez el proceso DCV cuando ordene otro certificado dedicado. Si suprime un certificado dedicado, el registro de TXT correspondiente al proceso DCV no se suprime.
{:note}

### Registro de Tipo NS
{:#ns-type-record}

Para añadir este tipo de registro, deben existir valores válidos en los campos **Nombre** y **Servidor de nombres**. También se puede especificar un **TTL** desde el menú desplegable, con el valor predeterminado `Automatic`.

![Crear registro de Tipo NS](images/dns/create-ns-type-record.png)

    Campos obligatorios: Nombre, Servidor de nombres
    Campo opcional: TTL (el valor predeterminado es Automatic)

## Actualización de registros DNS
{:#updating-dns-records}

En cada fila de registro, puede pulsar la opción **Editar registro** desde el menú, lo que abrirá un recuadro de diálogo, que puede utilizar para actualizar el registro.

![Editar registro de DNS](images/dns/edit-dns-record.png)

Por ejemplo, este es el diálogo de actualización para el registro de tipo **A**. Cuando haya terminado de realizar los cambios, seleccione **Actualizar registro** para guardarlos.

![Editar diálogo de registro de DNS](images/dns/update-dns-dialog.png)

## Supresión de registros
{:#deleting-dns-records}

En cada fila de registro, puede seleccionar la opción **Suprimir registro** desde el menú, lo que abre un recuadro de diálogo para confirmar el proceso de supresión.

![Suprimir registro de DNS](images/dns/delete-record.png)

Puede seleccionar el botón **Suprimir** para confirmar la acción de supresión. Seleccione **Cancelar** si no desea suprimir.

![Suprimir diálogo de registro de DNS](images/dns/delete-record-dialog.png)

## Importar y exportar registros
{:#import-export-records}

Los registros de DNS pueden importarse y exportarse desde CIS. Todos los archivos se importan y exportan como archivos .txt en formato BIND. Más información sobre el [formato BIND](https://en.wikipedia.org/wiki/Zone_file).
Pulse en el menú de desbordamiento y seleccione importar o exportar registros.
![Opción de registros DNS](images/dns/import-export-records.png)

### Importar registros
{:#import-dns-records}

De forma predeterminada, se permiten un total de 3500 registros de DNS (importados y creados en CIS). Puede importar varios archivos, uno cada vez, siempre y cuando el número total de registros esté por debajo del límite máximo. Después de la importación, se muestra un resumen con el número de registros añadidos satisfactoriamente y el número que ha fallado, junto con el motivo por el que ha fallado cada registro.
![Resumen de importación de registros de DNS](images/dns/import-records-summary.png)

### Exportar registros
{:#export-dns-records}

Utilice `Exportar registros` para crear una copia de seguridad de su archivo de zona, o exportarlo para utilizarlo con otro proveedor de DNS. Cuando se pulsa esta opción de menú, los registros se descargan en la ubicación especificada en los valores del navegador (normalmente en la carpeta Descargas). Para seleccionar otra ubicación de carpeta, cambie los valores de su navegador para que le solicite una ubicación en cada descarga.
