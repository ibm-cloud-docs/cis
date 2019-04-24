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


# Jeu de règles OWASP pour WAF 
{:#owasp-rule-set-for-waf}

Le jeu de règles OWASP contient des règles de détection d'attaque génériques. Les règles OWASP protègent contre de nombreuses catégories d'attaques courantes, notamment l'injection SQL, les scripts intersites et l'inclusion de fichiers de paramètres régionaux. IBM CIS fournit ces règles, mais ne les gère pas. OWASP est une norme de l'industrie qui fournit une bonne base de sécurité. Consultez les liens suivants pour plus d'informations :
  * [OWASP sur Github](https://github.com/SpiderLabs/owasp-modsecurity-crs)
  * [OWASP.org](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project)

## Gestion d'OWASP
{:#managing-owasp}

Contrairement au [jeu de règles CIS](/docs/infrastructure/cis?topic=cis-cis-rule-set-for-waf), OWASP vous permet de définir la sensibilité.
Une demande peut déclencher un jeu de règles OWASP auxquelles un indice de gravité élevé à faible est associé. L'indice final est calculé en fonction de toutes les règles déclenchées. Après avoir calculé l'indice final, CIS le compare au seuil de sensibilité sélectionné au début, puis bloque ou autorise la demande. 

|Indice de sensibilité| Seuil de déclenchement|
|------|---------------|
|Faible   |  60 et plus|
|Intermédiaire |  40 et plus|
|Elevé  |  25 et plus|

Nous vous suggérons de régler la sensibilité OWASP sur `faible`. Si vous la définissez sur `élevé`, consultez les journaux sur CIS et ajustez le jeu de règles OWASP pour l'adapter à votre application. 

N'oubliez pas que les règles OWASP peuvent uniquement être activées (_on_) ou désactivées (_off_), contrairement aux règles des jeux CIS, qui peuvent être définies sur _Désactiver_, _Simuler_, _Authentifier_ ou _Bloquer_.

## Comment traiter les faux positifs ? 
{:#owasp-false-positives}

De faux positifs peuvent se produire lorsque la variable ou la valeur est évaluée comme étant vraie (_true_) ou _positive_, alors qu'elle est en réalité négative. Dans le contexte de notre WAF, un faux positif signifie qu'une demande est bloquée car elle a été évaluée à tort comme malveillante. 

Pour traiter les faux positifs et les éviter à l'avenir, vous devez savoir les repérer et les corriger. Consultez les journaux des demandes bloquées, puis déterminez si ces demandes ont été raisonnablement bloquées dans le contexte du trafic attendu et normal de votre site Web. 
