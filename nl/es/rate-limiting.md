---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Bypass, header responses, brute-force login attempts

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Limitación de velocidad
{:#cis-rate-limiting}

Limitación de velocidad (sólo el plan de Empresa) protege contra ataques de denegación de servicio, intentos de inicio de sesión de fuerza bruta y otros tipos de comportamiento abusivo que apunten a la capa de aplicación.

Seleccione el tipo de regla de limitación de velocidad, ya sea una **Regla personalizada** o **Proteger inicio de sesión**

## Crear una regla de limitación de velocidad personalizada
{:#create-a-custom-rate-limiting-rule}

Especifique un nombre de regla que le ayude a recordar lo que hace la regla. Este campo es opcional.

**Criterios de coincidencia de tráfico** utiliza la operación AND. Especifique un URL del cual esté limitando la velocidad y, después, cuando las solicitudes del **Mismo IP superen** el número que ha especificado de **Solicitudes por segundo**, se desencadenará la regla especificada.

La opción **Criterios avanzados** permite especificar qué métodos HTTP, respuestas de cabecera y códigos de respuesta de origen restringen aún más los criterios de coincidencia. 

Seleccione un valor en el menú desplegable **Método** (ANY es el valor predeterminado).  

Actualice la **cabecera de respuesta HTTP**.  También puede **Añadir cabecera de respuesta** para incluir las cabeceras devueltas por el servidor web de origen. 

Si tiene más de una cabecera en **Cabecera de respuesta HTTP**, se aplica una lógica booleana _AND_.  Para excluir una cabecera de ser coincidente, utilice la opción _No igual a_. Además, cada cabecera debe ser una coincidencia exacta. No obstante, no se aplica la sensibilidad a mayúsculas y minúsculas.
{:note}

En **Código de respuesta de origen**, escriba el valor numérico válido de cada código de respuesta HTTP para que coincida.  Para incluir dos o más códigos de respuesta, separe cada valor con una coma. Por ejemplo, puede especificar `401, 403` si desea que sólo cuenten estos dos códigos de error. 

### Configurar respuesta
{:#rate-limiting-configure-response}

Seleccione entre las acciones de la lista y especifique el periodo de tiempo de espera. En este caso, el tiempo de espera hace referencia al periodo en que se realiza la acción. Un tiempo de espera de 60 segundos significa que la acción se aplica durante 60 segundos.

|Acción| Descripción|
|------|------------|
|Bloque | Emite un error 429 cuando se sobrepasa el umbral|
|Desafío | El usuario debe pasar un desafío de ReCaptcha de Google para poder continuar. Si tiene éxito, aceptamos la solicitud. De lo contrario, se bloquea la solicitud.| 	
|Desafío JS |	El usuario debe pasar un desafío de Javascript para poder continuar. Si tiene éxito, aceptamos la solicitud. De lo contrario, se bloquea la solicitud.
|Simulación| Puede utilizar esta opción para probar la regla antes de aplicar cualquiera de las otras opciones en el entorno activo.

**Respuesta avanzada**

Especifique el tipo de respuesta a dar cuando se sobrepasa el umbral de una regla. 

### Ignorar
{:#rate-limiting-bypass}

Ignorar le permite crear el equivalente de una lista blanca o una excepción para un conjunto de URL.  No hay ningún desencadenante de acciones para dichos URL, incluso si hay coincidencia con la regla de Limitación de tarifas.

## Proteger inicio de sesión
{:#rate-limiting-protect-login}

Proteger inicio de sesión crea una regla estándar que protege las páginas de inicio de sesión contra ataques de fuerza bruta. Los clientes que intenten iniciar sesión más de 5 veces en 5 minutos se bloquearán durante 15 minutos. 

Especifique un nombre para la regla y el URL de inicio de sesión.
