---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM CIS deployment, query strings, HTML files

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Conceptos de almacenamiento en memoria caché
{:#caching-concepts}

Este documento contiene algunos conceptos y definiciones relacionados con el almacenamiento en memoria caché y cómo afecta a su despliegue de IBM CIS.

## ¿Qué es el almacenamiento en memoria caché?
{:#what-is-caching}

El almacenamiento en memoria caché es el proceso de almacenamiento de archivos en nuestros servidores perimetrales, lo que se puede hacer para el fin de mejorar el tiempo de respuesta al servir esos archivos a los clientes. Al almacenar los archivos más cerca de los clientes, se puede reducir el tiempo que se tarda en que los datos se secuencien en la red, lo que comúnmente se conoce como la **latencia**.

Los archivos almacenados en la memoria caché tienen una hora de caducidad específica, **TTL (Time-To-Live)** tras la cual se depuran de la memoria caché. También es posible depurar archivos de la memoria caché manualmente. Una vez que los archivos se eliminen de la memoria caché, CIS vuelve al servidor de origen para volver a cargar los archivos y actualizar la memoria caché con las versiones más recientes.

Se puede encontrar una explicación más profunda de la configuración de la memoria caché y de las opciones de almacenamiento en memoria caché en la [guía de aprendizaje Almacenamiento en memoria caché y reglas de páginas](/docs/infrastructure/cis?topic=cis-use-page-rules-with-caching).

### ¿Qué contenido se almacena en memoria caché?
{:#what-content-is-cached}

De forma predeterminada, almacenamos en la memoria caché **archivos estáticos**, lo que incluye muchos tipos de archivos de imagen y de texto (archivos no HTML). Esto sólo incluye los archivos de los sitios web y no los recursos de terceros de sitios de red social, etc. Además, actualmente no almacenamos en memoria caché por tipo MIME.

### ¿Cómo puedo almacenar HTML en la memoria caché? 
{:#how-do-i-cache-html}

De forma predeterminada, no se almacenan en la memoria caché los archivos HTML porque no los consideramos estáticos; sin embargo, si se puede distinguir claramente el HTML estático del HTML dinámico, es posible almacenar en la memoria caché archivos HTML [utilizando la característica Reglas de página](/docs/infrastructure/cis?topic=cis-use-page-rules).


## Ordenación de series de consulta
{:#query-string-sorting}

El CIS **Solo empresa** trata los URL que tienen series de consulta en orden distinto como archivos separados en la memoria caché. Esto significa que si un usuario solicita:

`/video/123456?title=0&byline=0&portrait=0&color=987654`

Y otro usuario solicita:

`/video/123456?byline=0&color=987654&portrait=0&title=0`

CIS vuelve al origen, a pesar de que tenemos el archivo en nuestra memoria caché.

La opción Orden de series de consulta ordena las series de consulta _antes_ de que vayan a la memoria caché, lo que da como resultado un índice más alto de aciertos de memoria caché. Habilite Orden de series de consulta utilizando el conmutador de la página **Almacenamiento en memoria caché**.

## Servir contenido obsoleto
{:#serve-stale-content-caching}

Mantiene una versión limitada del sitio en línea si el servidor se desactiva. Incluso si el contenido ha caducado, el CIS seguirá sirviendo contenido almacenado en memoria caché a los usuarios cuando los servidores de origen estén fuera de línea.
