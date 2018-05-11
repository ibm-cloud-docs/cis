---
copyright:
  years: 2018
lastupdated: "2018-03-16"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Conceptos de ataques DDoS (Distributed Denial of Service)

Los ataques DDoS se encuentran entre los tipos más comunes de ataques en Internet que puede sufrir su sitio web o host.

## ¿Qué es un ataque DDoS?
Un ataque DDoS (Distributed Denial of Service) es un intento malicioso de interrumpir el tráfico normal de un servidor, un servicio o una red sobrecargando el destino o su infraestructura circundante con una ola de tráfico de Internet. Los ataques DDoS se vuelven eficaces utilizando muchos sistemas informáticos comprometidos como orígenes de tráfico de ataque. Entre las máquinas explotadas se pueden incluir sistemas y otros recursos en la red como dispositivos IoT. Desde un nivel alto, un ataque DDoS es como un atasco de tráfico en una carretera, que impide que el tráfico normal llegue a su destino deseado.

## ¿Cómo funciona un ataque DDoS?
Un atacante obtiene el control de una red de máquinas en línea para llevar a cabo un ataque DDoS. Los sistemas y otras máquinas (como dispositivos IoT) están infectados con malware, lo que los convierte en un bot (o zombie). El atacante controla el grupo de bots, lo que se denomina _botnet_. 

Después de establecer un botnet, el atacante dirige las máquinas enviando instrucciones actualizadas a cada bot mediante control remoto. Una dirección IP de destino puede recibir solicitudes de una multitud de bots, haciendo que el servidor o la red de destino desborde su capacidad. Esto crea una denegación de servicio al tráfico normal. Dado que cada bot es un dispositivo de Internet legítimo, separar el tráfico de ataque del tráfico normal puede ser difícil. 

## ¿Cuáles son los tipos comunes de ataques DDoS?
Los vectores de ataque de DDoS tienen como objetivo componentes diversos de una conexión de red. Aunque casi todos los ataques DDoS implican sobrecargar un dispositivo o a una red de destino con tráfico, los ataques se pueden dividir en tres categorías. Un atacante puede utilizar uno o varios vectores de ataque, y puede incluso recorrer estos vectores de ataque en función de las contramedidas adoptadas por el destino.

Los tipos comunes son:

 * Ataques de capa de aplicación (capa 7)
 * Ataques de protocolo (capas 3 y 4)
 * Ataques volumétricos (ataques de amplificación)

###	Ataques de capa de aplicación
Un ataque de capa de aplicación a veces se denomina _ataque DDoS de capa 7_ (en referencia a la séptima capa del modelo OSI). El objetivo de estos ataques es agotar los recursos de la víctima, atacando la capa donde se generan las páginas web en el servidor y son entregadas a los visitantes en respuesta a solicitudes HTTP (es decir, la capa de aplicación). Los ataques de capa 7 son difíciles, porque puede ser difícil identificar el tráfico como malicioso.

###	Ataques de protocolo
Los ataques de protocolo utilizan las debilidades de la capa 3 y 4 de la pila del protocolo ISO para convertir el destino en inaccesible. Estos ataques, también conocidos como ataques de agotamiento de estado, provocan una interrupción del servicio al consumir toda la capacidad de _tabla de estado_ disponible de los servidores de aplicaciones web, o de recursos intermedios como cortafuegos y equilibradores de carga. 
  
###	Ataques volumétricos
Esta categoría de ataques intenta crear congestión consumiendo todo el ancho de banda disponible entre el destino e Internet. Se envían grandes cantidades de datos a un destino utilizando una forma de amplificación, o mediante otros medios de creación de tráfico masivo, como solicitudes de un botnet. 


## ¿Qué puedo hacer si sufro un ataque DDoS?

**Paso 1:** Active “Modalidad de defensa" desde la pantalla **Visión general**. 

![Modalidad de defensa](images/defense-mode.png)

**Paso 2:** Establezca los registros DNS para máxima seguridad.

**Paso 3:** No limite por velocidad ni regule las solicitudes desde IBM CIS, necesitamos el ancho de banda para ayudarle con su situación.

**Paso 4:** Bloquee países y visitantes específicos si es necesario.
