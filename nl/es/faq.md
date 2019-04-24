---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: configuration domain, Free Trial plan, CIS instance

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:faq: data-hd-content-type='faq'}



# Preguntas más frecuentes
{:#faq}

## ¿Qué ha sucedido con el Plan de acceso anticipado que solía haber en el catálogo?
{:#cis-faq-early-access-plan}
{: faq}

El plan de Acceso anticipado se eliminó del catálogo el 31 de mayo de 2018. Se sustituyó por el plan de pago Estándar y un nuevo plan de Prueba gratuita de 30 días. Si tiene una instancia del plan de Acceso anticipado, actualícelo de inmediato al plan Estándar para evitar la pérdida de datos; no se le permitirá crear una instancia de Prueba gratuita si ha participado en la versión beta de Acceso anticipado.

## ¿Qué obtengo con un plan de Prueba gratuita?
{:#cis-faq-free-trial-plan}
{: faq}

El plan de Prueba gratuita, por diseño, solo permite una zona por cuenta. Se recomienda crear solamente una instancia por cuenta y el nombre de zona se verificará. Es muy importante verificar el nombre de zona antes de añadirlo. Si se suprime una zona, no se podrá añadir otra zona o la misma zona durante el plan de Prueba gratuita.

## ¿Cuántas instancias de Prueba gratuita puedo tener?
{:#cis-faq-free-trial-instances}
{: faq}

Puede tener como máximo una instancia de Prueba gratuita por cuenta, durante el tiempo de vida de la cuenta. Si ya tiene una instancia de prueba gratuita, o si suprime una instancia de prueba gratuita, o si la prueba gratuita caduca, no se le permitirá crear otra instancia de prueba gratuita. Sin embargo, puede crear instancias de otros tipos de planes pagados (por ejemplo, Estándar), independientemente de las pruebas gratuita que pueda haber creado.

## Tengo una instancia de servicio que está suscrita al plan de Acceso anticipado. ¿Puedo cambiarlo a Prueba gratuita?
{:#cis-faq-early-access-to-free-trial-plan}
{: faq}

No, El plan de Acceso anticipado sólo se puede actualizar a un plan de pago, que en este momento es el plan Estándar.

## Tenía una instancia de Acceso anticipado que quizás he borrado (o quizás no). ¿Puedo crear una instancia de Prueba gratuita?
{:#cis-faq-early-access-and-free-trial-plan}
{: faq}

No, cada cuenta puede tener a una sola instancia gratuita. Tanto el plan de Acceso anticipado como el plan de Prueba gratuita que lo reemplaza cuentan como planes gratuitos. Esto también significa que puede tener como máximo una instancia de Prueba gratuita.

## ¿Puedo bajar de Estándar a Prueba gratuita?
{:#cis-faq-downgrade-standard-to-free-plan}
{: faq}

No, esto no está permitido.

## Mi Prueba gratuita ha caducado. ¿Qué opciones tengo?
{:#cis-faq-free-trial-plan-expired}
{: faq}

Para evitar cualquier pérdida de datos, debe actualizarse de Prueba gratuita a Estándar antes de la fecha de caducidad. Después de esa fecha, sólo damos soporte a la actualización del plan o a la supresión de la instancia de CIS. Si no se suprime o se actualiza la instancia en 45 días (desde la fecha de iniciación de la instancia) el dominio de configuración, GLB, las agrupaciones y las comprobaciones de estado se suprimen automáticamente.

## ¿Cómo puedo suprimir mi instancia de CIS?
{:#{:#cis-faq-delete-instance}
{: faq}

Para suprimir una instancia de CIS, primero debe suprimir todos los GLB, las agrupaciones y las comprobaciones de estado. A continuación, suprimir el dominio asociado (zona). Vaya a la página **Visión general** y pulse el icono de papelera situado junto al nombre de dominio situado en la sección **Detalles de servicio** para iniciar el proceso de supresión.

## He añadido un usuario a mi cuenta y le he dado permiso a ese usuario para gestionar la(s) instancia(s) de Servicios de Internet. ¿Por qué ese usuario tiene problemas de autenticación?
{:#cis-faq-user-authentication-issue}
{: faq}

Es posible que no haya asignado "roles de acceso al servicio" al usuario. Tenga en cuenta que hay dos conjuntos de roles distintos: "acceso a plataforma" y "acceso a servicio". Los roles de acceso a plataforma son necesarios para crear y gestionar instancias de servicio, pero los roles de acceso al servicio son necesarios para realizar operaciones específicas de servicio en instancias de servicio. En la consola, estos valores se pueden actualizar seleccionando **Gestionar > Seguridad > Identidad y acceso**.

## ¿Por qué está mi dominio en estado Pendiente? ¿Cómo lo activo?
{:#cis-faq-pending-domain}
{: faq}

Al añadir un dominio a CIS, le damos un par de servidores de nombres para configurar en el registrador (o en su proveedor de DNS, si está añadiendo un subdominio). El dominio o el subdominio sigue en estado pendiente hasta que configure los servidores de nombres correctamente. Asegúrese de añadir ambos servidores de nombres a su registrador o proveedor de DNS. Exploramos periódicamente el sistema de DNS público para comprobar si se han configurado los servidores de nombres como se instruyó. Tan pronto como podamos comprobar el cambio en el servidor de nombres (esto puede tardar hasta 24 horas), activaremos su dominio. Puede enviar una solicitud para volver a comprobar los servidores de nombres pulsando en **Volver a comprobar servidores de nombres** en la página de visión general.

## ¿Quién es el registrador para mi dominio?
{:#cis-faq-who-is-registrar}
{: faq}

Consulte https://whois.icann.org/ para ver esta información. **Nota**: Debe tener el privilegio administrativo para editar la configuración del dominio en el registrador para actualizar o añadir los servidores de nombres proporcionados para el dominio al añadirlo a CIS. Si no sabe quién es el registrador para el dominio que está intentando añadir a CIS, es improbable que tenga el permiso para actualizar la configuración del dominio en el registrador. Trabaje con el propietario del dominio en su organización para realizar los cambios necesarios.

## Quiero mantener mi actual proveedor DNS para mi dominio (example.com). ¿Puedo delegar un subdominio (subdomain.example.com) desde mi proveedor DNS actual a CIS?
{:#cis-faq-keep-current-dns-provider}
{: faq}

Sí. El proceso es similar a añadir un dominio, pero en lugar del registrador, trabaja con el proveedor de DNS para el dominio de nivel superior. Al añadir un subdominio a CIS, se le dan dos servidores de nombres para configurar, como siempre. Configure un registro de NS (Name Server, servidor de nombres) para cada uno de los dos servidores de nombres como registros DNS dentro de su dominio gestionados por el otro proveedor de DNS. Cuando pueda verificar que se han añadido los registros NS necesarios, se activará el subdominio. Si no gestiona el dominio de nivel superior dentro de su organización, debe trabajar con el propietario del dominio de nivel superior para obtener los registros NS añadidos.

## ¿Qué es TLS?
{:#cis-faq-what-is-tls}
{: faq}

TLS es un protocolo de seguridad estándar para establecer enlaces cifrados entre un servidor web y un navegador en una comunicación en línea. Un certificado TLS es necesario crear una conexión TLS con un sitio web, y consta del nombre de dominio, el nombre de la empresa, y datos adicionales como dirección de la empresa, ciudad, estado y país. El certificado también muestra la fecha de caducidad y los detalles de la emisión de la entidad emisora de certificados (CA, Certificate Authority).

## ¿Cómo funciona TLS?
{:#cis-faq-how-does-tls-work}
{: faq}

Cuando un navegador inicia una conexión con un sitio web seguro TLS, primero recupera el Certificado TLS del sitio para comprobar si el certificado sigue siendo válido. Verifica que la entidad emisora de certificados es una en la que confía el navegador, y que el certificado lo utiliza el sitio web para el que se ha emitido. Si falla cualquiera de estas comprobaciones, recibirá un aviso que indica que el sitio web no está garantizado por un certificado válido.

Cuando un certificado TLS está instalado en un servidor web, permite una conexión segura entre el servidor web y el navegador que se conecta a él. El URL del sitio web tiene como prefijo "https" en lugar de "http" y se muestra un candado en la barra de direcciones. Si el sitio web utiliza un certificado de validación extendida (EV), el navegador también puede mostrar una barra de direcciones verde.

## ¿Por qué veo un aviso de privacidad?
{:#cis-faq-privacy-warning}
{: faq}

Los Certificados TLS emitidos por IBM Cloud CIS cubren el dominio raíz (`example.com`) y un nivel de subdominio (`*.example.com`). Si está tratando de llegar a un subdominio de segundo nivel (`*.*.example.com`), verá un aviso de privacidad en el navegador, porque estos nombres de host no están añadidos al SAN.

Además, deje hasta 15 minutos para que una de nuestras autoridades emisoras de certificados (CA) asociadas emita un nuevo certificado. Verá un aviso de privacidad en el navegador si el nuevo certificado aún no se ha emitido.

## ¿Por qué veo un error de Certificado SSL no válido?
{:#cis-faq-invalid-ssl-cert-error}
{: faq}

Si ve el "Error 526, Certificado SSL no válido" al visitar el sitio, puede significar que el certificado de origen no es válido. Cuando el proxy de CIS está habilitado, se requiere un certificado válido firmado por una entidad emisora de certificados en el origen en la modalidad SSL predeterminada, que es "End-to-end CA Signed". Tenga en cuenta que el valor predeterminado para la modalidad SSL antes era "End-to-end Flexible", que ignora la validez del certificado presentado por el origen. El nuevo valor predeterminado se aplica sólo a los dominios añadidos. Si el dominio se ha añadido cuando el modo SSL predeterminado era End-to-end Flexible, este valor no se sobrescribe. Puede cambiar el modo a un modo menos estricto, pero no se recomienda para entornos de producción.

## ¿Qué es DDoS?
{:#cis-faq-what-is-ddos}
{: faq}

Un ataque de denegación de servicio distribuido (DDoS) es un intento de convertir en no disponible un servicio en línea sobrecargándolo con tráfico de varias fuentes. En un ataque DDoS, varios sistemas comprometidos atacan un destino como un servidor, un sitio web, u otros recursos de red, y que afecta a los usuarios del recurso de destino.

La ola de mensajes entrantes, de solicitudes de conexión, o de paquetes mal formados en el sistema de destino lo fuerza a ralentizarse o incluso a colgarse y a cerrarse, negando así el servicio a los usuarios o sistemas legítimos. Los ataques DDoS han sido realizados por diversos actores de amenazas, desde hackers individuales a bandas criminales de la delincuencia organizada y agencias gubernamentales.

## ¿Qué puedo hacer si sufro un ataque DDoS?
{:#cis-faq-what-to-do-in-ddos}
{: faq}

**Paso 1:** Active “Modalidad de defensa" en la pantalla **Visión general**. 

![Modalidad de defensa](images/defense-mode.png)

**Paso 2:** Establezca los registros DNS para máxima seguridad.

**Paso 3:** No limite por velocidad ni regule las solicitudes desde IBM CIS, necesitamos el ancho de banda para ayudarle con su situación.

**Paso 4:** Bloquee países y visitantes específicos si es necesario.

## Tuve un error 522, ¿qué hago ahora?
{:#cis-faq-522-error}
{: faq}

Un error 522 indica que no hemos podido establecer una conexión con el servidor de origen (es decir, su host). Después de 15 segundos de no conexión, se cierra la conexión y se visualiza una página de error 522.

Este problema es causado generalmente por cortafuegos o software de seguridad que accidentalmente bloquea nuestras direcciones IP. Puesto que CIS actúa como un proxy inverso, las conexiones a su sitio parecerán provenir de un rango de IP de CIS. Este comportamiento puede causar que determinados cortafuegos bloqueen estas conexiones, lo que nos impide servir contenido a los visitantes del sitio correctamente.

Para solucionar este problema, pida a su host incluir en la lista blanca todos los rangos de IP de CIS, que se listan [aquí](/docs/infrastructure/cis?topic=cis-ibm-cloud-cis-whitelisted-ip-addresses).

Todas estas IP deben estar en la lista blanca para evitar errores 522. También vale la pena comprobar si cualquiera de las IP de estos rangos están bloqueadas.

Los errores 522 también pueden estar causados por problemas de conectividad de red, así que confirme que el servidor y la red estén generalmente en buen estado y no sobrecargados.

Si después de realizar los pasos anteriores sigue recibiendo errores, póngase en contacto con el soporte de IBM CIS y confirme lo siguiente:

* Ha incluido en la lista blanca nuestros rangos de IP
* El servidor/red está en línea y generalmente en buen estado

Si se pone en contacto con nuestro equipo de soporte, proporcione un ray ID desde un error 522 reciente. Podemos utilizar esto para determinar a qué Centro de datos de CIS llegó y ejecutar más pruebas.

## ¿Qué es un registro de proxy y por qué lo necesito?
{:#cis-faq-proxied-record}
{: faq}

Los registros con proxy son registros que redirigen su tráfico mediante IBM CIS. Solo los registros con proxy recibirán beneficios de CIS, como el enmascaramiento de IP, donde una IP de CIS se sustituye por su IP de origen para protegerla:

```
$ whois 104.28.22.57 | grep OrgName
OrgName:        IBM
```

Si prefiere omitir CIS en un dominio (seguiremos resolviendo DNS), una posible solución es no actuar como proxy del registro.

## Tuve un error DNS Validation: 1004; ¿qué puedo hacer ahora?
{:#cis-faq-dns-validation-error}
{: faq}

Para que las reglas de páginas funcionen, DNS necesita resolverse para su zona. Como resultado, debe tener un registro DNS con proxy para su zona. 

## ¿Puedo agregar un CNAME de un registro raíz?
{:#cis-faq-add-cname-root-record}
{: faq}

Sí. IBM CIS admite una característica denominada "Simplificación de CNAME" que permite a nuestros usuarios añadir un CNAME como registro raíz. Nuestros servidores DNS autorizados enumeran los registros del destino de CNAME y responden con esos registros en vez del CNAME, ocultando el hecho de que el usuario ha configurado un CNAME en la raíz del dominio.

## ¿Cuál es el tiempo de espera predeterminado de una comprobación de estado?
{:#cis-faq-default-health-check-timeout}
{: faq}

El tiempo de espera predeterminado de una comprobación de estado para los planes Prueba gratuita y Estándar es de 60 segundos.

## ¿Se pueden configurar comprobaciones de estado para tráfico que no sea HTTP/HTTPS?
{:#cis-faq-health-check-non-http-traffic}
{: faq}

No, sólo se pueden configurar con HTTP/HTTPS.

## ¿Se puede configurar GLB para tráfico que no sea HTTP/HTTPS?
{:#cis-faq-glb-non-http-traffic}
{: faq}

No, sólo se pueden configurar con HTTP/HTTPS.

## ¿Si se inhabilitan todos los orígenes de una agrupación de origen, se inhabilita toda la agrupación de orígenes?
{:#cis-faq-disabling-origins-disable-origin-pool}
{: faq}

Sí, si se utiliza la agrupación de origen en un equilibrador de carga, el tráfico se direcciona a la siguiente agrupación de prioridad más alta o a la agrupación de reserva.

## Tengo un error mi entrada de Kubernetes, ¿qué hago?
{:#cis-faq-kubernetes-ingress-error}
{: faq}

El nombre de host de una entrada de Kubernetes debe estar formado por caracteres alfanuméricos en minúsculas, '-' o '.', y debe empezar y finalizar por un carácter alfanumérico. El uso de `_` en el nombre del equilibrador de carga, aunque está permitido, puede provocar un error de entrada en los clústeres de Kubernetes. Le recomendamos que no utilice `-` en el nombre del equilibrador de carga para evitar problemas con los clústeres de Kubernetes.

## Me ha salido un error 502 al intentar guardas una acción de Edge Functions, ¿qué hago?
{:#cis-faq-502-error}
{: faq}

Póngase en contacto con el [Servicio de soporte de IBM](/docs/infrastructure/cis?topic=cis-getting-help-and-support) y proporcione el script que estaba intentando guardar.
