---
copyright:
  years: 2018
lastupdated: "2018-03-19"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Iniciación a IBM Cloud Internet Services (CIS)

IBM Cloud Internet Services (CIS) ofrece tres funciones principales para mejorar su flujo de trabajo: [seguridad](/docs/infrastructure/cis/managing-for-security.html), [fiabilidad](/docs/infrastructure/cis/managing-for-reliability.html) y [rendimiento](/docs/infrastructure/cis/managing-for-performance.html). Cada área de funcionalidad está representada en la barra de navegación izquierda de la pantalla, una vez que haya abierto la aplicación de IBM CIS.

Para cada funcionalidad, IBM CIS le ayuda a ajustar sus características para que se ajusten a sus necesidades específicas, entre las que se incluye:

 * Servidores DNS autorizados
 * Equilibrio de carga global y local
 * Cortafuegos de aplicaciones web (WAF)
 * Protección DDoS
 * Almacenamiento en memoria y reglas de páginas



## Antes de empezar
Antes de empezar a utilizar IBM CIS, primero necesitará un [IBMid](https://www.ibm.com/account/us-en/signup/register.html). Entonces, podrá pedir sus servicios mediante su Cuenta de IBM Cloud, o mediante el nuevo [IBM Cloud Internet Services Portal](https://console.bluemix.net/catalog/services/internet-services), dependiendo de su preferencia.

Si necesita ayuda al obtener una cuenta para utilizar IBM Cloud Internet Services, [póngase en contacto con el representante de ventas de IBM](https://www.ibm.com/cloud-computing/bluemix/contact-us) para obtener orientación adicional sobre cómo empezar.

Si tiene una cuenta de Softlayer existente, puede [enlazar la cuenta](https://console.bluemix.net/docs/account/softlayerlink.html#unifyingaccounts) con el IBMid. 

## Visión general del proceso

Puede empezar a utilizar IBM CIS para su tráfico de Internet con solo unos pasos.

 * Abra la aplicación IBM CIS desde el panel de control de IBM Cloud.
 * Añada el dominio que desea gestionar.
 * Configure la información de DNS con los servidores de nombres que hemos proporcionado.
 * Continúe iniciándose a IBM CIS, siguiendo una guía de aprendizaje o configurando otras características.

### Paso 1: Abra la aplicación IBM CIS

Abra el [panel de control de IBM Cloud](https://console.bluemix.net/catalog/). A continuación, vaya al icono de aplicación de IBM CIS seleccionando la categoría **Plataforma -> Red** en la barra de navegación izquierda del panel de control. Abra la aplicación IBM Cloud Internet Services pulsando el icono que verá cerca de la mitad de la pantalla. 

![Catálogo](images/catalog-cis-tile.png)

**La pantalla Visión general**

Una vez que se inicie la aplicación IBM CIS, verá la pantalla **Visión general** de IBM CIS, y encontrará los separadores para **Seguridad**, **Fiabilidad** y **Rendimiento** en el área izquierda de la pantalla IU.

**¿Qué plan puedo elegir?**

Para el release _Early Access_, solo hay un plan para elegir, y es gratuito. Pulse el botón **Crear** en la parte inferior izquierda de la pantalla **Vista previa** para empezar a suministrar su cuenta.

**Empezar a suministrar**

Verá la primera pantalla de la aplicación IBM CIS, donde seleccionará el botón **Añadir dominio** para empezar.

|**Tenga en cuenta que el programa Early Access está limitado a una instancia por cuenta.** |
|-------------------------------------------------------------------|
| Una vez que haya creado una instancia de recursos y que haya añadido un dominio a la misma, no se le permitirá añadir nuevas instancias de recursos para IBM CIS. Esta restricción se aplica incluso si suprime un dominio de prueba y luego intenta añadir un dominio de nuevo a la misma instancia de recursos. Encontrará un error si intenta hacerlo.|

### Paso 2. Añada y configure su Dominio.

Empiece a proteger y a mejorar el rendimiento de su servicio web especificando su dominio o un subdominio.

**Nota:** Especifique zonas DNS. Puede configurar los servidores de nombres para estos dominios o subdominios en el registrador del dominio o en el proveedor de DNS. No utilice CNAME.

![Cómo empezar](images/overview-add-domain.png)
La pantalla Visión general mostrará el dominio en el estado `Pendiente`. Su dominio seguirá `Pendiente` hasta que complete el Paso 3.

**Nota:** La instancia de IBM CIS no se puede suprimir una vez que se haya añadido un dominio. Para suprimir la instancia, suprima el dominio de la instancia en primer lugar.

### Paso 3. Configure los Servidores de nombres con el Registrador o un Proveedor DNS existente.

Para empezar a recibir los beneficios de IBM CIS, configure el registrador o el proveedor de nombres de dominio para utilizar los servidores de nombres listados. Si está delegando un dominio (algo parecido a `example.com`), configure los servidores de nombres listados en la configuración del dominio, donde están gestionados por el registrador (por ejemplo, en el portal web del registrador). Si no está seguro de quién es el registrador para el dominio, puede buscarlo en https://whois.icann.org/. Si delega un subdominio (por ejemplo, `subdomain.example.com`) desde otro proveedor de DNS, debe añadir un registro de NS (Name Server, servidor de nombres) para cada uno de los servidores de nombres listados.

Después de haber configurado el registrador o proveedor de DNS, puede necesitar hasta 24 horas para que los cambios entren en vigor. Una vez que verifique que se hayan configurado correctamente los servidores de nombres especificados para el dominio o subdominio, el estado del dominio cambiará de `Pendiente` a `Activo`. Después de configurar los servidores de nombres, puede pulsar en el enlace "Volver a comprobar los servidores de nombres" en la página `Visión general` para acelerar potencialmente la activación del dominio (puede realizar esta comprobación solo una vez cada hora).

### Paso 4. Asegúrese de que IBM Cloud Internet Services esté resolviendo la información de dominio para su aplicación, nombre de host o sitio web.

Para continuar, seleccione el separador **Fiabilidad** desde la barra de navegación de la izquierda y, a continuación, seleccione la opción **DNS**. Asegúrese de añadir los _Registros DNS_ apropiados. Añada el **Registro A** y cualquier entrada **AAAA** o **MX** que se rellene. Si se olvida de añadir estos registros antes de que la delegación del registrador se haya completado, IBM Cloud Services Internet no podrá resolver la información de dominio para sus aplicaciones conectadas a Internet.  

![Cómo empezar](images/dns-records.png)

### Paso 5. Mientras tanto, puede empezar a gestionar otras funciones y características de IBM CIS.

Para obtener más detalles sobre la gestión de otras funciones y características, consulte las [instrucciones paso a paso](/docs/infrastructure/cis/how-to.html).
