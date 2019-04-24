---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: global load balancer, global load balancer configuration

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Definir el equilibrador de carga global
{:#define-the-global-load-balancer}

Defina la configuración del equilibrador de carga global especificando un nombre de host, añadiendo y ajustando las agrupaciones de origen y definiendo reglas adicionales para controlar cómo se sirve el tráfico a los clientes.

1. Cree el equilibrador de carga global pulsando el botón Crear equilibrador de carga de la derecha.  

2. Especifique el nombre de host para el dominio y ajuste el valor de TTL si lo desea (el valor predeterminado es de 60 segundos) y utilice **Añadir agrupación** para añadir las agrupaciones de origen. 

   <img src="images/reliability11.png" alt="dibujo" style="width: 300px;"/>
   
   **NOTA:** Los nombres de host combinados con nombres de dominio forman nombres de dominio completos (FQDN) para la aplicación. Los usuarios finales se conectan a la aplicación utilizando este FQDN. 
   
3. Ajuste las prioridades relativas de las agrupaciones de origen pulsando las flechas hacia arriba y hacia abajo de la parte izquierda de la agrupación. Estas agrupaciones de origen sirven las solicitudes de aplicación de los usuarios finales de forma round robin. 
   
   <img src="images/reliability12.png" alt="dibujo" style="width: 300px;"/>   
   
4. Opcionalmente, puede definir reglas adicionales para controlar cómo se sirve el tráfico a los clientes de distintas regiones geográficas. En el ejemplo siguiente, los clientes que llegan desde la región sur de América del Sur se dirigen a la agrupación de origen de la Costa Oeste de Estados Unidos. Puede utilizar estas reglas para dirigir a los clientes a su región más próxima. Si alguna de estas regiones falla, las solicitudes se direccionan a otras ubicaciones en buen estado disponibles, de modo que los usuarios finales no se vean afectados por el tiempo de inactividad. 

   <img src="images/reliability13.png" alt="dibujo" style="width: 300px;"/>   
   
5. Pulse **Suministrar recursos** para completar la configuración del equilibrador de carga global. 
6. Por último, verifique la conectividad con la aplicación escribiendo el `URL del FQDN` en una ventana de navegador móvil. Verá un mensaje de bienvenida si se puede conectar.
