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


# Paramètres WAF
{:#waf-settings}

Le tableau suivant indique les actions que peuvent effectuer les pare-feux d'applications Web (WAF).  


|Action| Définition|
|---|---|
|Blocage | Le blocage d'une attaque arrête toute action avant qu'elle ne soit publiée sur votre site Web.|
|Simulation| Pour tester les faux positifs, définissez le WAF sur le mode Simulation, ce qui enregistre la réponse aux attaques éventuelles sans demande d'authentification, ni blocage.|
|Demande d'authentification | Une page de demande d'authentification demande aux visiteurs de soumettre un CAPTCHA pour continuer sur votre site Web.|
|Paramètre de seuil ou de sensibilité | Définissez les règles pour se déclencher plus ou moins fréquemment, en fonction de la sensibilité.|

## Jeu de règles CIS pour WAF 
{:#cis-ruleset-for-waf}

Sélectionnez **Afficher les règles CIS** pour afficher les jeux de règles de ce package. Les jeux de règles sont les suivants :
  * Drupal
  * Flash
  * Joomla
  * Magento
  * Divers
  * PHP
  * Plone
  * Spéciales
  * WHMCS
  * Wordpress

Le jeu de règles **Spéciales** contient un certain nombre de règles adaptées à pratiquement toutes les applications et les sites Web sur Internet. Ce jeu de règles constitue le coeur de la sécurité offerte par WAF, avec des règles qui ciblent les attaques courantes telles que SQLi, XSS et LFI. Nous vous recommandons de toujours laisser les règles Spéciales activées. 

Activez uniquement les jeux de règles correspondant à votre pile technologique. Par exemple, si vous utilisez Wordpress mais aucune des autres technologies, activez uniquement les jeux de règles Spéciales et Wordpress. Evitez d'activer des jeux de règles qui ne sont pas pertinents pour votre pile technologique. 

Sélectionnez l'un des jeux de règles spécifiques pour obtenir plus de détails sur chacune des règles incluses. 

Le jeu de règles CIS vous permet d'effectuer quatre actions sur chaque règle :
  1. **Désactivation** : désactive la règle.
  2. **Simulation** : enregistre l'événement et ne bloque pas le visiteur, ni ne lui demande de s'authentifier (vous pouvez toujours décider de définir un blocage ou une demande d'authentification après avoir examiné vos journaux).
  3. **Blocage** : bloque simplement la requête entièrement, sans possibilité de la contourner.
  4. **Demande d'authentification** : affiche une page de demande d'authentification (CAPTCHA) qui doit être complétée avant que l'accès à la demande en question ne soit autorisé.

Vous pouvez remarquer que les noms des règles ne révèlent pas exactement leur fonctionnement et qu’ils constituent essentiellement un récapitulatif général de leur fonction. Ce procédé est délibéré. Pour des raisons de sécurité, nous ne révélons pas le code (ou toute autre information exacte) que nous utilisons pour filtrer le trafic. Cela empêche les acteurs malveillants de l’ingénierie inverse de contourner nos défenses. 
