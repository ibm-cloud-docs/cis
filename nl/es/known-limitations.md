---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: health checks, Free Trial plan, dedicated certificate, known issues

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"} 
{:note: .note} 
{:important: .important} 
{:deprecated: .deprecated} 
{:generic: data-hd-programlang="generic"}

# Limitaciones conocidas
{:#known-limitations}

 * Recomendamos utilizar Chrome.
 
 * El plan Prueba gratuita está limitado a una instancia por cuenta. Después de crear una instancia de recursos y de añadir un dominio a la misma, no se le permitirá añadir nuevas instancias de recursos para CIS. Esta restricción se aplica incluso si suprime un dominio de prueba y luego intenta añadir un dominio de nuevo a la misma instancia de recursos. Encontrará un error si intenta hacerlo.

 * Para este servicio, sólo se admite la delegación de subdominios utilizando registros NS desde otro proveedor. La delegación CNAME no está soportada.
  
 * Los registros comodín A, AAAA y CNAME (*) no se pueden redirigir por proxy.

 * Cuando se suprime un certificado dedicado, puede volver a aparecer en la lista durante un breve periodo de tiempo hasta que se complete la supresión.
 
 * Para modificar los nombres de host de su certificado personalizado dedicado después de realizar el pedido, debe solicitar un nuevo certificado y después suprimir el antiguo. 
 
 * Sólo se pueden crear reglas de IP con códigos de país de dos letras con la acción `Desafío`. Si desea bloquear a los visitantes de un país, actualice al plan de Empresa o coloque reglas en el servidor para bloquearlos completamente.

## Equilibrador de carga global
{:#known-limitations-glb}

 * Cloud Internet Services le permite utilizar el carácter `_` en los nombres de host del equilibrador de carga; sin embargo, los clústeres de Kubernetes no pueden utilizar `_`. 

 * El plan estándar permite un máximo de 5 equilibradores de carga, agrupaciones y comprobaciones de estado. Cada agrupación puede tener un total de 6 orígenes, pero sólo se permiten 6 orígenes exclusivos en cada instancia de CIS.

* No se pueden filtrar los sucesos de comprobación de estado de las agrupaciones y los orígenes suprimidos, pero todavía aparecen en la tabla.

* Si filtra sucesos de comprobación de estado por `Estado de agrupación`, se incluyen las agrupaciones `Degradadas` porque técnicamente están en buen estado, pero pueden contener 1 o más orígenes críticos.

* Al añadir el nombre de cabecera de solicitud de una comprobación de estado, utilice `Host`. Si se utiliza `host` en minúscula para una comprobación de estado, da un error.

## DNS
{:#known-limitations-dns}

 * La exportación de registros de DNS incluye registros CNAME de Cloudflare que deben estar ocultos. Estos registros comienzan por `_` y normalmente tienen un segundo registro con el mismo nombre pero se elimina `_`.
   ```
   Por ejemplo,
   _cf.generate.yourdomain.com 0	IN	CNAME address.alias.com
   cf.generate.yourdomain.com 0	IN	CNAME address2.alias.com
   ```
 
   Estos registros deben eliminarse del archivo de zona para una correcta importación.
 
 * La exportación de registros DNS de CAA no funciona correctamente. `<tag>` y `<value>` están codificados en hexadecimal. 
 
    CAA `<flags>` `<tag>` `<value>`
  {:note}
   ```
   Por ejemplo,
   Original CAA record
   caa.yourdomain.com.	1	IN	CAA	0 issue "letsencrypt.org"
 
   Exported CAA record
   caa.yourdomain.com.	1	IN	CAA	0 6973737565 "6c657473656e63727970742e6f7267"
   ```
   Estos registros se deben convertir de hexadecimal a serie o eliminarlos y añadirlos manualmente antes de la importación.

## Reglas de página
{:#known-limitations-pagerules}

   * Si se actualizan las reglas de página con el plugin de CIS para la CLI de IBM Cloud, se puede producir un error si no se incluye el ID de regla de página en la serie JSON o el archivo JSON para la actualización. Como solución temporal, envíe la actualización utilizando un archivo de configuración de JSON completo para la regla de página, que incluya el ID.
   * Puede ser que al eliminar los valores de regla de página utilizando la interfaz de usuario de CIS no se elimine el valor, aunque la interfaz de usuario indique que la actualización ha sido satisfactoria. Como solución temporal para este problema, utilice el plugin de CIS para la CLI de IBM Cloud para eliminar el valor e incluya el ID de regla de página en el documento de actualización de JSON:
      ```
      $> ibmcloud cis page-rule-update <domain-id> <rule-id> -j <file>
      ```
      El archivo JSON debe incluir la configuración de regla de página completa, incluyendo el ID, con las actualizaciones necesarias.
