---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: domain Input information, IBM Cloud Internet Service, Domain Name

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Especificar información sobre su dominio
{:#input-information-about-your-domain}

Especifique información sobre el dominio que desea proteger y al que desea proporcionar equilibrio de carga global.

1. Pulse **Visión general** en el lado izquierdo de la pantalla Cómo empezar. Especifique el nombre de dominio (o el nombre de subdominio) y pulse **Añadir dominio**. 
    
    <img src="images/reliability3.png" alt="dibujo" style="width: 300px;"/>
    
    IBM Cloud Internet Service no es un registrador DNS, por lo que este dominio (o subdominio) debe haberse creado previamente.
    {:note}

    En la sección Detalles de servicio, observará que el dominio recién añadido se mostrará inicialmente con un estado Pendiente. 

    <img src="images/reliability4.png" alt="dibujo" style="width: 300px;"/>    

2. Vaya a la página de administración del dominio con el registrador de DNS respectivo y delegue el dominio/subdominio a los servidores de nombres de IBM definiendo los registros NS.

Es posible que tenga que esperar hasta 24 horas para que su información se replique en la base de datos de DNS. Una vez lo haga, el estado del dominio cambiará a Activo. 

<img src="images/reliability5.png" alt="dibujo" style="width: 300px;"/>    
