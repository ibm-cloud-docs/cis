---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: OWASP Rule Set, Rule Set

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# Conjunto de reglas OWASP para WAF
{:#owasp-rule-set-for-waf}

El conjunto de reglas OWASP contiene reglas de detección de ataques genéricos. Las reglas OWASP protegen contra muchas categorías de ataque comunes, incluyendo la inyección de SQL, los scripts entre sitios y la inclusión de archivos de entorno local, entre otros. IBM CIS proporciona pero no organiza estas reglas. OWASP es un estándar del sector que proporciona una buena línea base de seguridad. Consulte los enlaces siguientes para obtener más información:
  * [OWASP en Github](https://github.com/SpiderLabs/owasp-modsecurity-crs)
  * [OWASP.org](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project)

## Gestión de OWASP
{:#managing-owasp}

A diferencia del [conjunto de reglas de CIS](/docs/infrastructure/cis?topic=cis-cis-rule-set-for-waf), OWASP le permite establecer la sensibilidad.
Una solicitud puede desencadenar un conjunto de reglas OWASP que tienen una puntuación de gravedad asociada desde alta hasta baja. La puntuación final se calcula en función de todas las reglas desencadenadas. Después de calcular la puntuación final, CIS la compara con el umbral de sensibilidad seleccionado al principio y, a continuación, bloquea o permite la solicitud.

|Puntuación de sensibilidad| Umbral de desencadenante|
|------|---------------|
|Baja   |  60 y superior|
|Media|  40 y superior|
|Alta  |  25 y superior|

Sugerimos que establezca la sensibilidad OWASP en `low` (baja). Si la establece en `high` (alta), compruebe los registros en CIS, y ajuste el conjunto de reglas OWASP para que funcionen para su aplicación.

Tenga presente que las reglas de OWASP sólo se pueden establecer en _on_ u _off_, a diferencia de las reglas de los conjuntos de reglas de CIS, que se pueden establecer en _Disable_, _Simulate_, _Challenge_ o _Block_.

## ¿Cómo tratar los falsos positivos?
{:#owasp-false-positives}

Se pueden producir falsos positivos cuando la variable o el valor se evalúa como _true_ o _positivo_, pero en realidad es un valor negativo. En el contexto de nuestro WAF, un falso positivo significa que una solicitud está bloqueada porque se ha evaluado por error como maliciosa.

Para tratar los falsos positivos y asegurarse de evitarlos en el futuro, debe saber cómo detectarlos y corregirlos. Revise los registros de las solicitudes bloqueadas y evalúe si estas solicitudes se han bloqueado de forma razonable en el contexto del tráfico esperado y el tráfico normal de su sitio web.
