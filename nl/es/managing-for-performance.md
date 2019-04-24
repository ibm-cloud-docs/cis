---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Page Rule Use, Cache-Tag Purge, web content

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Gestión del despliegue de CIS para un mejor rendimiento
{:#manage-your-cis-deployment-for-best-performance}

IBM Cloud Internet Services (CIS) puede proporcionar la experiencia más rápida para sus clientes porque optimiza sus imágenes, y almacena el contenido web lo más cerca posible a los usuarios finales. El contenido se carga desde servidores perimetrales con proxy (lo que reduce la latencia).

Con IBM CIS, puede mejorar aún más el rendimiento del sitio utilizando las mejores prácticas para acelerar la carga de su contenido web. Estas son algunas de las mejores prácticas específicas para mejorar en rendimiento del contenido web dentro de CIS.

**Recomendaciones y mejores prácticas:**

 * Guarde en la memoria caché tanto contenido web estático como semiestático como sea posible
 * Para el contenido gestionado por sucesos, depure la memoria caché utilizando la API
 
## Mejor práctica 1: Guardar en la memoria caché tanto contenido estático como semiestático como sea posible
{:#best-practice-cache-static-content}

  * Habilite **Almacenar todo en la memoria caché** para las páginas web HTML estáticas
  * Utilice **Tiempo de duración (TTL)** conservador para el contenido que cambie ocasionalmente

### Utilización de TTL (Tiempos de duración) conservadores para el contenido que cambie ocasionalmente
{:#utilize-conservative-ttl}

Si el contenido cambia raramente, puede establecer un TTL conservador para utilizar nuestra memoria caché tanto como sea posible. Si tiene un alto porcentaje de solicitudes de revalidación, podría aumentar los TTL del contenido sin que afecte negativamente a sus clientes. Al utilizar la memoria caché de forma más efectiva, aumentará el rendimiento porque revalidará con menor frecuencia.

### ¿Cómo sé si los elementos están en la memoria caché?
{:#how-do-i-tell-if-items-are-being-cached}

IBM CIS añade la cabecera de respuesta `CF-Cache-Status` cuando intenta almacenar en caché un objeto. Si el almacenamiento en memoria caché es correcto, el valor de esta cabecera indicará su estado con una de estas palabras clave:

* **MISS:** El activo todavía no estaba en la memoria caché o el TTL ha caducado (es decir, ha llegado a la edad mínima de control de memoria caché de 0).
* **HIT:** El activo se entregó desde la memoria caché.
* **EXPIRED:** Este activo se entregó desde la memoria caché, pero la solicitud siguiente necesitará revalidación.
* **REVALIDATED:** El activo se entregó desde la memoria caché. El TTL ha caducado, pero una solicitud `If-Modified-Since` al origen indicaba que el activo no se había modificado. Por lo tanto, la versión de la memoria caché se considera válida de nuevo.

## Mejor práctica 2: Para contenido gestionado por sucesos, utilice la API para depurar la memoria caché
{:#best-practice-api-purge-cache}

Por ejemplo, cada vez que se añada una publicación nueva a su blog, podría depurar fácilmente la memoria caché de CIS utilizando un mandato de API. Es común ver contenido gestionado por sucesos, y lo hacemos fácil para garantizar que ningún contenido obsoleto llegue a los usuarios. Los mandatos para depurar la memoria caché inmediatamente en toda nuestra red global se listan a continuación. Puede utilizar nuestra aplicación de almacenamiento en memoria caché o la API.

  * Depuración de la memoria caché mediante un código de caché
  * Depuración de la memoria caché globalmente
  * Depuración de la memoria caché mediante Regla de páginas
  * Utilización de características de almacenamiento en memoria caché avanzadas

### Depuración de la memoria caché mediante un código de caché
{:#purge-cache-by-cache-tag}

Los códigos de caché le permiten definir grupos de contenido que desea depurar. Es una forma excelente de combinar objetos que se suelen cambiar juntos. Por lo tanto, una publicación de blog HTML, por ejemplo, y todo su contenido de imagen se podría etiquetar junto. El contenido solo móvil también podría ser empaquetado utilizando códigos de caché, de modo que pueda depurarlo todo al enviar por push una nueva actualización a su dominio móvil.

### Depuración de la memoria caché globalmente
{:#purge-cache-globally}

También tiene la opción de forzar toda nuestra memoria caché para revalidar. Puede restablecer todos los objetos almacenados en nuestra memoria caché para que cada solicitud se direccione al servidor de origen.

### Depuración de la memoria caché mediante Regla de páginas
{:#purge-cache-by-page-rule}

Las reglas de páginas le permiten depurar toda la memoria caché basándose en una expresión regular. Puede utilizar una regla de página predefinida y volver a validar todas las coincidencias en dicha Regla de página. Puede crear hasta 50 reglas de páginas por página.

### Utilización de características de almacenamiento en memoria caché avanzadas
{:#use-advanced-caching-features}

**Omitir memoria caché en la cookie:** Configurada en una Regla de página, esta característica le permite servir un objeto en memoria caché a menos que exista una cookie de un nombre específico. Por ejemplo, puede servir una versión en la memoria caché de la página inicial a menos que encuentre una cookie `SessionID` que indique que el cliente ha iniciado sesión, y por lo tanto debería presentarse con contenido personalizado.
