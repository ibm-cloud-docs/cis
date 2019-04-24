---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-26"

keywords: IBM CIS, optimal security, Security Level

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Gestión de IBM CIS para una seguridad óptima
{:#manage-your-ibm-cis-for-optimal-security}
Los valores de seguridad de IBM Cloud Internet Services (CIS) incluyen valores predeterminados seguros diseñados para evitar falsos positivos e influencia negativa en el tráfico. Sin embargo, estos valores predeterminados seguros no proporcionan la mejor postura de seguridad para cada cliente. Siga estos pasos para asegurarse de que su cuenta de CIS esté configurada de forma segura.

**Recomendaciones y mejores prácticas:**

* Proteja las direcciones IP de origen redirigiendo y aumentando la ofuscación
* Configure su Nivel de seguridad de forma selectiva
* Active su Cortafuegos de aplicaciones web (WAF) de forma segura

## Mejor práctica 1: Proteger sus direcciones IP de origen
{:#best-practice-secure-origin-ip-address}

Cuando se redirige un subdominio utilizando IBM CIS, se protegerá todo el tráfico porque respondemos de forma activa con direcciones IP específicas de IBM CIS (por ejemplo, todos sus clientes se conectan a proxies de CIS en primer lugar, y sus direcciones IP de origen se ocultarán).

### Uso de los proxies de IBM CIS para todos los Registros DNS para tráfico HTTP(S) desde su origen
{:#use-cis-proxies-for-dns-records}

Para mejorar la seguridad de su dirección IP de origen, todo el tráfico HTTP(S) se debería redirigir.

**Consulte la diferencia por sí mismo: Consulte un registro no redirigido y otro redirigido:**

```
$ dig nonproxied.theburritobot.com +short
1.2.3.4 (The origin IP address)

$ dig proxied.theburritobot.com +short
104.16.22.6 , 104.16.23.6 (CIS IP addresses)
```

### Ocultación de registros de origen no redirigidos con nombres no estándares
{:#obsure-non-proxied-origin-records-with-non-standard-names}
Los registros que no se pueden redirigir mediante IBM CIS, y que todavía utilizan su IP de origen, como FTP, se pueden proteger creando ofuscación adicional. En particular, si necesita un registro para su origen que no se pueda redirigir mediante IBM CIS, utilice un nombre no estándar. Por ejemplo, en lugar de `ftp.example.com`, utilice `[random word or-random characters].example.com`. Esta ofuscación hace menos probable que las exploraciones de diccionario de sus registros DNS expongan las direcciones IP de origen.

### Utilice rangos de IP distintos para tráfico HTTP y no HTTP si es posible
{:#use-separate-ipranges-for-traffic}
Algunos clientes utilizan rangos de IP distintos para tráfico HTTP y no HTTP, permitiéndoles así redirigir todos los registros que apuntan a su rango de IP HTTP, y ocultar todo el tráfico no HTTP con una subred IP distinta.

## Mejor práctica 2: Configurar el Nivel de seguridad de forma selectiva
{:#best-practice-configure-security-level-selectively}
Su **Nivel de seguridad** establece la sensibilidad de nuestra **Base de datos de reputación de IP**. Para evitar interacciones negativas o falsos positivos, configure su **Nivel de seguridad** por dominio para aumentar la seguridad donde sea necesario, y para bajarla donde sea apropiado.

### Aumento del nivel de seguridad para áreas sensibles a 'Alto'
{:#increase-security-level-for-sensitive-areas}
Puede aumentar este valor en la página Seguridad avanzada de su dominio añadiendo una **Regla de página** para las páginas de administración o las páginas de inicio de sesión, para reducir los intentos por la fuerza:

1. Cree una **Regla de página** con el patrón de URL de la API (por ejemplo, `www.example.com/wp-login`). 
2. Identifique el valor **Nivel de seguridad**.
3. Marque el valor como **Alto**.
4. Seleccione **Suministro de recursos**.

### Reducción del Nivel de seguridad para vías de acceso no sensibles o API para reducir falsos positivos
{:#decrease-security-level-non-sensitive-paths-reduce-false-positives}
Este valor puede ser reducido para páginas generales y tráfico de API: 

1. Cree una **Regla de páginas** con el patrón URL de la API (por ejemplo, `www.example.com/api/*`).
2. Identifique el valor **Nivel de seguridad**.
3. Coloque el Nivel de seguridad en **Bajo** o en **Esencialmente desactivado**.
4. Seleccione **Suministro de recursos**.

### ¿Qué significan los valores de Nivel de seguridad?
{:#what-do-security-level-settings-mean}
Nuestros valores de Nivel de seguridad están alineados con las puntuaciones de amenazas que adquieren determinadas direcciones IP de comportamiento malicioso en nuestra red. Una puntuación de amenazas superior a 10 se considera alta.

* **HIGH**: Se necesitan puntuaciones de amenazas mayores que 0.
* **MEDIUM**: Se necesitan puntuaciones de amenazas mayores que 14.
* **LOW**: Se necesitan puntuaciones de amenazas mayores que 24.
* **ESSENTIALLY OFF**: Se necesitan puntuaciones de amenazas mayores que 49.
* **OFF**: *Solo empresa* 
* **UNDER ATTACK**: Sólo debe utilizarse cuando el sitio web esté bajo un ataque DDoS. Los visitantes reciben una página intercalada durante unos cinco segundos, mientras CIS analiza el tráfico y el comportamiento para asegurarse de que quien está intentando acceder a su sitio web es un visitante legítimo. **UNDER ATTACK** puede afectar a algunas acciones de su dominio, como por ejemplo, utilizar una API. Puede establecer un nivel de seguridad personalizado para la API o cualquier otra parte del dominio mediante la creación de una regla de página para dicha sección.

Le recomendamos que revise sus valores de Nivel de seguridad periódicamente, y puede encontrar instrucciones en nuestras [Mejores prácticas para el documento de configuración de CIS](/docs/infrastructure/cis?topic=cis-best-practices-for-cis-setup)

## Mejor práctica 3: Activar su Cortafuegos de aplicaciones web (WAF) de forma segura
{:#best-practice-activate-waf-safely}
Su WAF está disponible en la sección **Seguridad**. Le guiaremos por estos valores en orden inverso para asegurarse de que su WAF esté configurado de la forma lo más segura posible antes de activarlo para todo su dominio. Estos valores iniciales pueden reducir falsos positivos cumplimentando los **Sucesos de seguridad** para un maejor ajuste. El WAF se actualiza automáticamente para manejar nuevas vulnerabilidades a medida que se identifican.

El WAF le protege frente a los siguientes tipos de ataques:
* Ataque de inyección de SQL
* Script entre sitios
* Falsificación entre sitios

El WAF contiene un conjunto de reglas predeterminadas que incluye reglas para detener los ataques más comunes. En este momento, le permitimos habilitar o inhabilitar el WAF y ajustar reglas específicas en los conjuntos de reglas de WAF. Consulte el documento [Conjunto de reglas predeterminadas de WAF](/docs/infrastructure/cis?topic=cis-waf-default-rule-set) para obtener más detalles sobre el conjunto de reglas predeterminadas y el comportamiento de cada regla.

Para obtener más información sobre el WAF, consulte el [documento Conceptos de WAF](/docs/infrastructure/cis?topic=cis-web-application-firewall-concepts-q-a)

## Mejor práctica 4: Configurar los valores de TLS
{:#best-practice-configure-tls-settings}
IBM CIS proporciona algunas opciones para cifrar el tráfico. Como proxy inverso, cerramos las conexiones TLS en nuestros centros de datos y abrimos una nueva conexión TLS a su servidor de origen.

TLS ofrece cuatro modalidades de funcionamiento:
* **Desactivado**: TLS está inhabilitado en esta modalidad, no se recomienda.
* **Cliente a extremo**: TLS cifra el tráfico de CIS a sus clientes, pero no de CIS a su(s) servidor(es) de origen.
* **Extremo a extremo flexible**: TLS cifra todo el tráfico; sin embargo, puede utilizar un certificado firmado automáticamente para proteger el tráfico entre CIS y su(s) servidor(es) de origen.
* **Firmado por una entidad emisora de certificados de extremo a extremo**: TLS cifra todo el tráfico; debe utilizar un certificado firmado por una entidad emisora de certificados.

Para obtener más detalles sobre las opciones de TLS, consulte [este documento](/docs/infrastructure/cis?topic=cis-tls-options).

IBM CIS le permite utilizar certificados personalizados, o puede utilizar un certificado comodín proporcionado para usted por CIS.

### Cargar certificados personalizados
{:#upload-custom-certs}
Puede cargar el certificado personalizado pulsando el botón **Añadir certificado** y especificando el certificado, la clave privada y el método del paquete. Si carga su propio certificado, obtendrá compatibilidad inmediata con tráfico cifrado, y mantendrá el control sobre su certificado (por ejemplo, un certificado Validación ampliada (EV)). Recuerde que será responsable de gestionar el certificado si carga un certificado personalizado. Por ejemplo, IBM CIS no realizará el seguimiento de la fecha de caducidad del certificado. 

![certificado personalizado](images/upload-custom-certificate.png)

### Solicitar certificados dedicados
{:#order-dedicated-certs}
CIS facilita la gestión de los certificados al ofrecer certificados dedicados. Ya no es necesario generar claves privadas, crear solicitudes de firma de certificados (CSR) ni acordarse de renovar los certificados. Puede solicitar un certificado dedicado pulsando el botón **Añadir certificado** y solicitando un certificado comodín o especificando nombres de host para solicitar un certificado personalizado dedicado. Los tipos de certificados son:

 * Certificado firmado SHA-2/ECDSA utilizando la clave P-256, 
 * Certificado firmado SHA-2/RSA utilizando la clave RSA 2048-bit, y 
 * Certificado firmado SHA-1/RSA utilizando la clave RSA 2048-bit. 
 
CIS puede emitir para todos los TLD excepto para `.cu`, `.iq`, `.ir`, `.kp`, `.sd`, `.ss` y `.ye`. CIS gestiona la fecha de caducidad. Para editar los nombres de host en el certificado personalizado dedicado, debe volver a volver a solicitarlo y después suprimirlo. Por ejemplo, puede solicitar un certificado personalizado dedicado con el nombre de host `alpha.yourdomain.com`. Para añadir el nombre de host `beta.yourdomain.com` al certificado personalizado dedicado, solicite otro certificado personalizado dedicado con los nombres de host `alpha.yourdomain.com` y `beta.yourdomain.com`. Después, _tiene que_ suprimir el certificado personalizado dedicado original.

La primera vez que solicita un certificado dedicado, se produce un proceso de Validación de control de dominio (DCV) que genera en correspondiente registro TXT. Si suprime el registro TXT, se producirá otra vez el proceso DCV cuando ordene otro certificado dedicado. Si suprime un certificado dedicado, el registro de TXT correspondiente al proceso DCV no se suprime.
{:note}

A continuación se indican los errores más frecuentes que se producen al solicitar certificados dedicados:
* `Error al conectar con el servicio de certificados.`
* `Error al solicitar al servicio de certificados.`
{:note}

Si recibe un error al solicitar certificados, actualice la página e inténtelo de nuevo.

![certificado dedicado](images/order-dedicated-certificate.png)

### Utilización de un certificado suministrado
{:#utilize-provisioned-certificate}
IBM ha colaborado con varias entidades emisoras de certificados (CA) para proporcionar certificados comodín de dominio para nuestros clientes. La verificación manual podría ser necesaria para configurar estos certificados. Su equipo de soporte puede ayudarle a realizar estos pasos adicionales.

### Prioridad de certificados en nuestros límites
{:#certificate-prioirity-at-our-edge}
La prioridad con la que se visualizan los certificados en nuestros límites es:
1. Personalizado cargado
2. Dedicado personalizado
3. Comodín dedicado
4. Universal

### Versión de TLS mínima
{:#security-minimum-tls-version}
Consulte [Versión de TLS mínima](/docs/infrastructure/cis?topic=cis-tls-options#minimum-tls-version). Los niveles más altos de TLS proporcionan más seguridad, pero pueden impedir que los clientes se conecten a su sitio.
