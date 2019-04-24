---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: WAF Custom Rules, Custom WAF Rules

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# Reglas personalizadas de WAF
{:#waf-custom-rules}

Para ir a las Reglas personalizadas de Cortafuegos de aplicaciones web (WAF), seleccione **Seguridad > Cortafuegos de aplicaciones web > Reglas personalizadas**. Las reglas de WAF están disponibles en los planes de empresa y se crean en función de los requisitos exclusivos de ese cliente y/o de los patrones de tráfico de su sitio web. Esto significa que puede pedirnos que bloqueemos virtualmente cualquier combinación de características de una solicitud. 

Las reglas personalizadas de WAF tienen en cuenta situaciones para las que IBM WAF todavía no tiene una regla, y el atacante utiliza un patrón o un agente de usuario específico pensado específicamente para la estructura de su sitio web. En estas situaciones, puede crear una regla personalizada para su propiedad web.

## Solicitar una regla personalizada
{:#request-a-custom-rule}

Para solicitar una regla, envíe un correo electrónico a wafsup@us.ibm.com con los requisitos de la regla o los patrones de tráfico. 

Proporcione la mayor cantidad de información posible, incluyendo:
* Registros de acceso que muestren un ejemplo de unas 100 solicitudes maliciosas confirmadas.
* Una solicitud POST de ejemplo que incluya los datos POST (si las solicitudes tienen un cuerpo POST) para determinar si la solicitud contiene algo que podamos bloquear o activar.
* Si desea que las solicitudes sean totalmente bloqueadas, o que sean impugnadas, en caso de potenciales positivos falsos.
* Los dominios específicos a los que desea aplicar estas reglas.
* Si desea que las reglas estén activadas o desactivadas de forma predeterminada.

Después de crear las reglas WAF personalizadas, debe habilitar todas las reglas personalizadas para que entren en vigor.
{:note}
