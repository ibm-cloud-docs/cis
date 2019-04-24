---
copyright:
  years: 2018
lastupdated: "2018-03-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Preguntas y respuestas de los conceptos del Cortafuegos de aplicaciones web

El cortafuegos de aplicaciones web protege contra ataques de ISO Capa 7, que pueden ser algunos de los más difíciles. Este documento ofrece algunos detalles.

## ¿Qué es un Cortafuegos de aplicaciones web (WAF)?
Un WAF o Cortafuegos de aplicaciones web ayuda a proteger las aplicaciones web filtrando y supervisando el tráfico HTTP entre una aplicación web e Internet. Un WAF es una defensa de capa 7 del protocolo ISO (en el [modelo de OSI ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://en.wikipedia.org/wiki/OSI_model)), no está diseñado para defenderse frente a todos los tipos de ataques. 

El despliegue de un WAF frente a una aplicación web es como colocar un escudo entre la aplicación web e Internet. Un servidor proxy protege la identidad de la máquina de un cliente utilizando un intermediario (para tráfico saliente), pero un WAF es un tipo de proxy inverso que protege al servidor de la exposición haciendo que el tráfico del cliente pase por el WAF antes de llegar al servidor (para tráfico entrante).

## ¿Qué tipos de ataques puede evitar un WAF?
Un WAF normalmente protege las aplicaciones web de ataques como la falsificación entre sitios, los scripts entre sitios (XSS), la inclusión de archivos y la inyección SQL, entre otros. Un WAF normalmente forma parte de una suite de herramientas, que juntas pueden crear una defensa holística contra una serie de vectores de ataque.

## ¿Cómo funciona un WAF?

Un WAF funciona mediante un conjunto de reglas a menudo llamadas políticas. Estas políticas tienen como objetivo proteger contra las vulnerabilidades en la aplicación filtrando el tráfico malicioso. 

El valor de un WAF proviene de la velocidad y de la facilidad con las que se pueden implementar las modificaciones de su política, permitiendo así una respuesta más rápida a distintos vectores de ataque. Por ejemplo, durante un [ataque DDoS ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://en.wikipedia.org/wiki/Denial-of-service_attack), la limitación de velocidad se puede implementar modificando las políticas de WAF.
