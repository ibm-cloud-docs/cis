---
copyright:
  years: 2018
lastupdated: "2018-03-13"
---

# Conceptos de almacenamiento en memoria caché

Este documento contiene algunos conceptos y definiciones relacionados con el almacenamiento en memoria caché y cómo afecta a su despliegue de IBM CIS.

## ¿Qué es el almacenamiento en memoria caché?

El almacenamiento en memoria caché es el proceso de almacenamiento de archivos en nuestros servidores perimetrales, lo que se puede hacer para el fin de mejorar el tiempo de respuesta al servir esos archivos a los clientes. Al almacenar los archivos más cerca de los clientes, se puede reducir el tiempo que se tarda en que los datos se secuencien en la red, lo que comúnmente se conoce como la **latencia**.

De forma predeterminada, almacenamos en la memoria caché **archivos estáticos**, lo que incluye muchos tipos de archivos de imagen y de texto (archivos no HTML). De forma predeterminada, no se almacenan en la memoria caché los archivos HTML porque no los consideramos como estáticos; sin embargo, es posible almacenar en la memoria caché archivos HTML [utilizando la característica Reglas de página](using-page-rules.html).

Los archivos almacenados en la memoria caché tienen una hora de caducidad específica, **TTL (Time-To-Live)** tras la cual se depuran de la memoria caché. También es posible depurar archivos de la memoria caché manualmente. Una vez que los archivos se eliminen de la memoria caché, CIS vuelve al servidor de origen para volver a cargar los archivos y actualizar la memoria caché con las versiones más recientes.

Se puede encontrar una explicación más profunda de la configuración de la memoria caché y de las opciones de almacenamiento en memoria caché en la [guía de aprendizaje Almacenamiento en memoria caché y reglas de páginas](caching-with-page-rules.html).
