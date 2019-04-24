---
copyright:
  years: 2018
lastupdated: "2018-28-03"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Preguntas más frecuentes

## ¿Cómo obtengo un Plan Early Access?
El programa Early Access, por diseño, solo permite una zona por cuenta. Se recomienda crear solamente una instancia por cuenta y el nombre de zona se verificará. Es muy importante verificar el nombre de zona antes de añadirlo. Si una zona se suprime, no se podrá añadir otra zona o la misma zona durante el programa Early Access.

## ¿Por qué está mi dominio en estado Pendiente? ¿Cómo lo activo?
Al añadir un dominio a CIS, le damos un par de servidores de nombres para configurar en el registrador (o en su proveedor de DNS, si está añadiendo un subdominio). El dominio o el subdominio sigue en estado pendiente hasta que configure los servidores de nombres correctamente. Asegúrese de añadir ambos servidores de nombres a su registrador o proveedor de DNS. Exploramos periódicamente el sistema de DNS público para comprobar si se han configurado los servidores de nombres como se instruyó. Tan pronto como podamos comprobar el cambio en el servidor de nombres (esto puede tardar hasta 24 horas), activaremos su dominio. Puede enviar una solicitud para volver a comprobar los servidores de nombres pulsando en **Volver a comprobar servidores de nombres** en la página de visión general.

## ¿Quién es el registrador para mi dominio?
Consulte https://whois.icann.org/ para ver esta información. **Nota**: Debe tener el privilegio administrativo para editar la configuración del dominio en el registrador para actualizar o añadir los servidores de nombres proporcionados para el dominio al añadirlo a CIS. Si no sabe quién es el registrador para el dominio que está intentando añadir a CIS, es improbable que tenga el permiso para actualizar la configuración del dominio en el registrador. Trabaje con el propietario del dominio en su organización para realizar los cambios necesarios.

## Quiero mantener mi actual proveedor DNS para mi dominio (example.com). ¿Puedo delegar un subdominio (subdomain.example.com) desde mi proveedor DNS actual a CIS?
Sí. El proceso es similar a añadir un dominio, pero en lugar del registrador, trabaja con el proveedor de DNS para el dominio de nivel superior. Al añadir un subdominio a CIS, se le dan dos servidores de nombres para configurar, como siempre. Configure un registro de NS (Name Server, servidor de nombres) para cada uno de los dos servidores de nombres como registros DNS dentro de su dominio gestionados por el otro proveedor de DNS. Cuando pueda verificar que se han añadido los registros NS necesarios, se activará el subdominio. Si no gestiona el dominio de nivel superior dentro de su organización, debe trabajar con el propietario del dominio de nivel superior para obtener los registros NS añadidos.

## ¿Qué es TLS?
TLS es un protocolo de seguridad estándar para establecer enlaces cifrados entre un servidor web y un navegador en una comunicación en línea. Un certificado TLS es necesario crear una conexión TLS con un sitio web, y consta del nombre de dominio, el nombre de la empresa, y datos adicionales como dirección de la empresa, ciudad, estado y país. El certificado también muestra la fecha de caducidad y los detalles de la emisión de la entidad emisora de certificados (CA, Certificate Authority).

## ¿Cómo funciona TLS?
Cuando un navegador inicia una conexión con un sitio web seguro TLS, primero recupera el Certificado TLS del sitio para comprobar si el certificado sigue siendo válido. Verifica que la entidad emisora de certificados es una en la que confía el navegador, y que el certificado lo utiliza el sitio web para el que se ha emitido. Si falla cualquiera de estas comprobaciones, recibirá un aviso que indica que el sitio web no está garantizado por un certificado válido.

Cuando un certificado TLS está instalado en un servidor web, permite una conexión segura entre el servidor web y el navegador que se conecta a él. El URL del sitio web tiene como prefijo "https" en lugar de "http" y se muestra un candado en la barra de direcciones. Si el sitio web utiliza un certificado de validación extendida (EV), el navegador también puede mostrar una barra de direcciones verde.

## ¿Por qué veo un aviso de privacidad?
Los Certificados TLS emitidos por IBM Cloud CIS cubren el dominio raíz (`example.com`) y un nivel de subdominio (`*.example.com`). Si está tratando de llegar a un subdominio de segundo nivel (`*.*.example.com`), verá un aviso de privacidad en el navegador, porque estos nombres de host no están añadidos al SAN.

Además, deje hasta 15 minutos para que una de nuestras autoridades emisoras de certificados (CAs) asociadas emita un nuevo certificado. Verá un aviso de privacidad en el navegador si el nuevo certificado aún no se ha emitido.

## ¿Qué es DDoS?
Un ataque de denegación de servicio distribuido (DDoS) es un intento de convertir en no disponible un servicio en línea sobrecargándolo con tráfico de varias fuentes. En un ataque DDoS, varios sistemas comprometidos atacan un destino como un servidor, un sitio web, u otros recursos de red, y que afecta a los usuarios del recurso de destino.

La ola de mensajes entrantes, de solicitudes de conexión, o de paquetes mal formados en el sistema de destino lo fuerza a ralentizarse o incluso a colgarse y a cerrarse, negando así el servicio a los usuarios o sistemas legítimos. Los ataques DDoS han sido realizados por diversos actores de amenazas, desde hackers individuales a bandas criminales de la delincuencia organizada y agencias gubernamentales.

## ¿Qué puedo hacer si sufro un ataque DDoS?

**Paso 1:** Active “Modalidad de defensa" en la pantalla **Visión general**. 

![Modalidad de defensa](images/defense-mode.png)

**Paso 2:** Establezca los registros DNS para máxima seguridad.

**Paso 3:** No limite por velocidad ni regule las solicitudes desde IBM CIS, necesitamos el ancho de banda para ayudarle con su situación.

**Paso 4:** Bloquee países y visitantes específicos si es necesario.

## Tuve un error 522, ¿qué hago ahora?

Un error 522 indica que no hemos podido establecer una conexión con el servidor de origen (es decir, su host). Después de 15 segundos de no conexión, se cierra la conexión y se visualiza una página de error 522.

Este problema es causado generalmente por cortafuegos o software de seguridad que accidentalmente bloquea nuestras direcciones IP. Puesto que CIS actúa como un proxy inverso, las conexiones a su sitio parecerán provenir de un rango de IP de CIS. Este comportamiento puede causar que determinados cortafuegos bloqueen estas conexiones, lo que nos impide servir contenido a los visitantes del sitio correctamente.

Para solucionar este problema, pida a su host incluir en la lista blanca todos los rangos de IP de CIS, que se listan [aquí](whitelisted-ips.html).

Todas estas IP deben estar en la lista blanca para evitar errores 522. También vale la pena comprobar si cualquiera de las IP de estos rangos están bloqueadas.

Los errores 522 también pueden estar causados por problemas de conectividad de red, así que confirme que el servidor y la red estén generalmente en buen estado y no sobrecargados.

Si después de realizar los pasos anteriores sigue recibiendo errores, póngase en contacto con el soporte de IBM CIS y confirme lo siguiente:

* Ha incluido en la lista blanca nuestros rangos de IP
* El servidor/red está en línea y generalmente en buen estado

Si se pone en contacto con nuestro equipo de soporte, proporcione un ray ID desde un error 522 reciente. Podemos utilizar esto para determinar a qué Centro de datos de CIS llegó y ejecutar más pruebas.

## ¿Qué es un registro de proxy y por qué lo necesito?

Los registros con proxy son registros que redirigen su tráfico mediante IBM CIS. Solo los registros con proxy recibirán beneficios de CIS, como el enmascaramiento de IP, donde una IP de CIS se sustituye por su IP de origen para protegerla:

```
$ whois 104.28.22.57 | grep OrgName
OrgName:        IBM
```

Si prefiere omitir CIS en un dominio (seguiremos resolviendo DNS), no representar el registro sería una posible solución.

## Tuve un error DNS Validation: 1004; ¿qué puedo hacer ahora?

Para que las reglas de páginas funcionen, DNS necesita resolverse para su zona. Como resultado, debe tener un registro DNS con proxy para su zona. 
