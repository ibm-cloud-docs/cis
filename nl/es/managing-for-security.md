---
copyright:
  years: 2018
lastupdated: "2018-03-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Gestión de IBM CIS para una seguridad óptima

Los valores de seguridad de IBM Cloud Internet Services (CIS) incluyen valores predeterminados seguros diseñados para evitar falsos positivos e influencia negativa en el tráfico. Sin embargo, estos valores predeterminados seguros no proporcionan la mejor postura de seguridad para cada cliente. Siga estos pasos para asegurarse de que su cuenta de CIS esté configurada de forma segura:

**Recomendaciones y mejores prácticas:**

* Proteja las direcciones IP de origen redirigiendo y aumentando la ofuscación
* Configure su Nivel de seguridad de forma selectiva
* Active su Cortafuegos de aplicaciones web (WAF) de forma segura

## Mejor práctica 1: Proteger sus direcciones IP de origen

Cuando se redirige un subdominio utilizando IBM CIS, se protegerá todo el tráfico porque respondemos de forma activa con direcciones IP específicas de IBM CIS (por ejemplo, todos sus clientes se conectan a proxies de CIS en primer lugar, y sus direcciones IP de origen se ocultarán).

### Uso de los proxies de IBM CIS para todos los Registros DNS para tráfico HTTP(S) desde su origen

Para mejorar la seguridad de su dirección IP de origen, todo el tráfico HTTP(S) se debería redirigir.

**Consulte la diferencia por sí mismo: Consulte un registro no redirigido y otro redirigido:**

```
$ dig greycloud.theburritobot.com +short
1.2.3.4 (The origin IP address)

$ dig orangecloud.theburritobot.com +short
104.16.22.6 , 104.16.23.6 (CIS IP addresses)
```

### Ocultación de registros de origen no redirigidos con nombres no estándares
Los registros que no se pueden redirigir mediante IBM CIS, y que todavía utilizan su IP de origen, como FTP, se pueden proteger creando ofuscación adicional. En particular, si necesita un registro para su origen que no se pueda redirigir mediante IBM CIS, utilice un nombre no estándar. Por ejemplo, en lugar de `ftp.example.com`, utilice `[random word or-random characters].example.com`. Esta ofuscación hace menos probable que las exploraciones de diccionario de sus registros DNS expongan las direcciones IP de origen.

### Utilice rangos de IP distintos para tráfico HTTP y no HTTP si es posible
Algunos clientes utilizan rangos de IP distintos para tráfico HTTP y no HTTP, permitiéndoles así redirigir todos los registros que apuntan a su rango de IP HTTP, y ocultar todo el tráfico no HTTP con una subred IP distinta.

## Mejor práctica 2: Configurar el Nivel de seguridad de forma selectiva
Su **Nivel de seguridad** establece la sensibilidad de nuestra **Base de datos de reputación de IP**. IBM CIS ve más de mil millones de direcciones IP exclusivas cada mes, de más de 7 millones de sitios web, lo que permite a nuestro sistema identificar actores maliciosos y evitar que lleguen a sus activos web. Para evitar interacciones negativas o falsos positivos, configure su **Nivel de seguridad** por dominio para aumentar la seguridad donde sea necesario, y para bajarla donde sea apropiado.

### Aumento del nivel de seguridad para áreas sensibles a 'Alto'
Puede aumentar este valor añadiendo una **Regla de página** para las páginas de administración o las páginas de inicio de sesión, para reducir los intentos por la fuerza:

1. Cree una **Regla de página** con el patrón de URL de la API (por ejemplo, `www.example.com/wp-login`). 
2. Identifique el valor **Nivel de seguridad**.
3. Marque el valor como **Alto**.
4. Seleccione **Suministro de recursos**.

### Reducción del Nivel de seguridad para vías de acceso no sensibles o API para reducir falsos positivos
Este valor puede ser reducido para páginas generales y tráfico de API: 

1. Cree una **Regla de páginas** con el patrón URL de la API (por ejemplo, `www.example.com/api/*`).
2. Identifique el valor **Nivel de seguridad**.
3. Coloque el Nivel de seguridad en **Bajo** o en **Esencialmente desactivado**.
4. Seleccione **Suministro de recursos**.

### ¿Qué significan los valores de Nivel de seguridad?
Nuestros valores de Nivel de seguridad están alineados con las puntuaciones de amenazas que adquieren determinadas direcciones IP de comportamiento malicioso en nuestra red. Una puntuación de amenazas superior a 10 se considera alta.

* **HIGH**: Se necesitan puntuaciones de amenazas mayores que 0.
* **MEDIUM**: Se necesitan puntuaciones de amenazas mayores que 14.
* **LOW**: Se necesitan puntuaciones de amenazas mayores que 24.
* **ESSENTIALLY OFF**: Se necesitan puntuaciones de amenazas mayores que 49.

Le recomendamos que revise sus valores de Nivel de seguridad periódicamente, y puede encontrar instrucciones en nuestras [Mejores prácticas para el documento de configuración de CIS](best-practices.html)

## Mejor práctica 3: Activar su Cortafuegos de aplicaciones web (WAF) de forma segura
Su WAF está disponible en la sección **Seguridad**. Le guiaremos por estos valores en orden inverso para asegurarse de que su WAF esté configurado de la forma lo más segura posible antes de activarlo para todo su dominio. Estos valores iniciales pueden reducir falsos positivos rellenando la Aplicación de tráfico con sucesos WAF para ajustar más. El WAF se actualiza automáticamente para manejar nuevas vulnerabilidades a medida que se identifiquen.

El WAF le protege frente a los siguientes tipos de ataques:
* Ataque de inyección de SQL
* Script entre sitios
* Falsificación entre sitios

El WAF contiene un conjunto de reglas predeterminadas que incluye reglas para detener los ataques más comunes. En este momento, le permitimos habilitar o inhabilitar el WAF. Consulte el documento [Conjunto de reglas predeterminadas de WAF](waf-rule-set.html) para obtener más detalles sobre el conjunto de reglas predeterminadas y el comportamiento de cada regla.

Para obtener más información sobre el WAF, consulte el [documento Conceptos de WAF](waf-concept.html)

## Mejor práctica 4: Configurar los valores de TLS
IBM CIS proporciona algunas opciones para cifrar el tráfico. Como proxy inverso, cerramos las conexiones TLS a nuestros centros de datos y abrimos una nueva conexión TLS en nuestro servidor de origen.

TLS ofrece cuatro modalidades de funcionamiento:
* **Desactivado**: TLS está inhabilitado en esta modalidad, no se recomienda.
* **Cliente a extremo**: TLS cifra el tráfico de CIS a sus clientes, pero no de CIS a su(s) servidor(es) de origen.
* **Extremo a extremo flexible**: TLS cifra todo el tráfico; sin embargo, puede utilizar un certificado firmado automáticamente para proteger el tráfico entre CIS y su(s) servidor(es) de origen.
* **Firmado por una entidad emisora de certificados de extremo a extremo**: TLS cifra todo el tráfico; debe utilizar un certificado firmado por una entidad emisora de certificados.

Para obtener más detalles sobre las opciones de TLS, consulte [este documento](ssl-options.html).

IBM CIS le permite utilizar certificados personalizados, o puede utilizar un certificado de comodines proporcionado para usted por CIS.

### Carga de un certificado personalizado
Puede cargar el certificado personalizado pulsando el botón **Añadir certificado** y especificando el certificado, la clave privada y el método del paquete. Si carga su propio certificado, obtendrá compatibilidad inmediata con tráfico cifrado, y mantendrá el control sobre su certificado (por ejemplo, un certificado Validación ampliada (EV)). Recuerde que será responsable de gestionar el certificado si carga un certificado personalizado. Por ejemplo, IBM CIS no realizará el seguimiento de las fechas de caducidad del certificado. 

![custom-certificate](images/upload-custom-certificate.png)

### Utilización de un certificado suministrado
IBM ha colaborado con varias entidades emisoras de certificados (CAs) para proporcionar certificados de comodines de dominio para nuestros clientes. La verificación manual podría ser necesaria para configurar estos certificados. Su equipo de soporte puede ayudarle a realizar estos pasos adicionales.
