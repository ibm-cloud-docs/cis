---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: CIS Rule Set, WAF settings, WAF CIS Rules

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# Valores de WAF
{:#waf-settings}

En la tabla siguiente se muestran las acciones que pueden llevar a cabo los cortafuegos de aplicación web (WAF). 


|Acción| Definición|
|---|---|
|Bloqueo | Bloquear un ataque detendrá cualquier acción antes de que se publique en su sitio web.|
|Simulación | Para probar los falsos positivos, establezca WAF a modalidad Simular, que registra la respuesta a posibles ataques sin bloquear ni presentar un desafío.|
|Desafío | Una página de desafío pide a los visitantes que envíen un CAPTCHA para continuar en el sitio web.|
|Valor de umbral o de sensibilidad | Establezca las reglas para desencadenar más o menos, en función de la sensibilidad.|

## Conjunto de reglas de CIS para WAF
{:#cis-ruleset-for-waf}

Seleccione **Ver reglas de CIS** para revelar los conjuntos de reglas de este paquete. Los conjuntos de reglas son los siguientes:
  * Drupal
  * Flash
  * Joomla
  * Magento
  * Miscellaneous
  * PHP
  * Plone
  * Specials
  * WHMCS
  * Wordpress

**Specials** contiene una serie de reglas adecuadas para virtualmente todas las aplicaciones y sitios web en Internet. Este conjunto de reglas es el núcleo de la seguridad que ofrece nuestro WAF, con reglas que se dirigen a ataques comunes como SQLi, XSS y LFI. Le recomendamos que deje siempre Specials habilitado.

Únicamente habilite los conjuntos de reglas que correspondan a su pila de tecnología. Por ejemplo, si utiliza Wordpress pero ninguna de las otras tecnologías, habilite sólo los conjuntos de reglas Specials y Wordpress. Evite habilitar conjuntos de reglas que no sean relevantes para su pila de tecnología.

Seleccione cualquiera de los conjuntos de reglas específicos para ver detalles adicionales sobre cada una de las reglas incluidas.

Los conjuntos de reglas CIS le permiten llevar a cabo cuatro acciones en cada regla:
  1. **Inhabilitar**: Desactiva la regla.
  2. **Simular**: Registra el suceso y no bloquea ni presenta un desafío al visitante (puede decidir establecer un bloqueo o un desafío al revisar los registros).
  3. **Bloquear**: Simplemente bloquea la solicitud completamente, sin ninguna opción de omitirla para esa solicitud.
  4. **Desafío**: Muestra una página de desafío (CAPTCHA) que se debe completar para que a la solicitud en cuestión se le permita el acceso.

Puede observar cuenta de que los nombres de las reglas no revelan exactamente cómo funcionan y que en su mayoría son un resumen general de su función. Esto es deliberado.  Por motivos de seguridad, no revelamos el código (ni otra información exacta) que utilizamos para filtrar el tráfico. Esto evita que actores maliciosos de ingeniería inversa se salten nuestras defensas.
