---
copyright:
  years: 2018
lastupdated: "2018-03-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Limitaciones conocidas

 * Nuestra recomendación es utilizar Chrome.

 * En Firefox y Safari, las fechas *cargado*, *modificado* y *caduca* para un certificado no se pueden visualizar.

 * La edición de la coincidencia de URL para una regla de páginas hace que dicha regla se coloque en la prioridad más baja.
 
 * Sin un dominio configurado, puede navegar a **Fiabilidad > Equilibradores de carga globales** para crear sus agrupaciones de equilibrador de carga y sus comprobaciones de estado. Sin embargo, si selecciona **Crear equilibrador de carga**, configurar el equilibrador de carga y pulsar **Suministrar 1 recurso** rechazará la solicitud porque se necesita un dominio. Esta limitación funcional ayuda al usuario a entender la finalidad de las agrupaciones y supervisores en el flujo de creación del equilibrador de carga.
 
 * El programa Early Access está limitado a una instancia por cuenta. Después de crear una instancia de recursos y de añadir un dominio a la misma, no se le permitirá añadir nuevas instancias de recursos para CIS. Esta restricción se aplica incluso si suprime un dominio de prueba y luego intenta añadir un dominio de nuevo a la misma instancia de recursos. Encontrará un error si intenta hacerlo.

 * Cuando añada un dominio nuevo, nuestro sistema no recopila ni importa actualmente sus registros de dominio existentes.

 * Para este programa Early Access, apoyamos la delegación de subdominios utilizando solamente registros NS desde otro proveedor. La delegación CNAME no está soportada.
