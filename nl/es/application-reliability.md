---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: domain Input information, IBM Cloud Internet Services, Global Load balancing

subcollection: cis

---


{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Mejora de la fiabilidad y la escalabilidad de las aplicaciones con el Equilibrio de carga global de IBM Cloud Internet Services
{:#improving-application-reliability-and-scalability-with-global-load-balancing-from-ibm-cloud-internet-services}

Si tiene un sitio web de comercio electrónico o aloja una aplicación que necesita ser accesible para los usuarios finales en todo momento, es probable que le preocupe la disponibilidad 24*7 y el rendimiento de su aplicación. 

Las funciones globales de equilibrio de carga disponibles con IBM Cloud Internet Services (CIS) pueden ayudar a mejorar la fiabilidad y la escalabilidad de las aplicaciones a la vez que ofrecen la mejor experiencia de usuario final posible. Esta guía proporciona una guía paso a paso de la configuración de equilibrio de carga global.  

## Lo que conseguirá
{:#what-you-accomplish}

En esta guía paso a paso, aprenderá a configurar una configuración similar a la que se muestra a continuación.

<img src="images/reliability1.png" alt="dibujo" style="width: 300px;"/>

En este ejemplo, los recursos de aplicación se despliegan en dos ubicaciones de centro de datos, una en el Oeste de EE.UU. y otra en la Costa Este de EE.UU. Es posible que los usuarios finales estén accediendo a esta aplicación desde todo el mundo. 

Tarea  | Descripción
------------- | -------------
[Crear una instancia de CIS](/docs/infrastructure/cis?topic=cis-create-your-ibm-cloud-internet-services-cis-instance) | Empiece por crear su instancia de IBM Cloud Internet Services (CIS) utilizando el portal de clientes de IBM.|
[Especificar información sobre su dominio](/docs/infrastructure/cis?topic=cis-input-information-about-your-domain) | Especifique información sobre el dominio que desea proteger y al que desea proporcionar equilibrio de carga global.
[Iniciar la configuración del equilibrador de carga global](/docs/infrastructure/cis?topic=cis-begin-global-load-balancer-configuration) | Empiece a configurar el equilibrador de carga global.
[Identificar los recursos de la aplicación](/docs/infrastructure/cis?topic=cis-identify-your-application-resources) | Identifique los recursos de la aplicación como, por ejemplo, las agrupaciones de origen y los mecanismos de comprobación de estado.
[Definir el equilibrador de carga global](/docs/infrastructure/cis?topic=cis-define-the-global-load-balancer) | Defina la configuración del equilibrador de carga global especificando un nombre de host, añadiendo y ajustando las agrupaciones de origen y definiendo reglas adicionales para controlar cómo se sirve el tráfico a los clientes.
