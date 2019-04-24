---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Web Application Firewall Concepts, web application firewall

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Questions-réponses relatives aux concepts de pare-feu d'application Web
{:#waf-q-and-a}

Le pare-feu d'application Web offre une protection contre les attaques de la couche 7 du modèle OSI, qui peuvent être les plus difficiles. Vous trouverez davantage de renseignements dans ce document.

## Qu'est-ce qu'un pare-feu d'application Web (WAF) ?
{:#what-is-a-waf}

Un WAF, ou pare-feu d'application Web, permet de protéger les applications Web en filtrant et en surveillant le trafic HTTP entre une application Web et Internet. Un WAF est une protection de la couche protocole 7 du modèle OSI ([Modèle OSI ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://en.wikipedia.org/wiki/OSI_model)). Il n'est pas conçu pour offrir une protection contre tous les types d'attaques. 

Déployer un WAF en amont d'une application Web revient au même que placer un bouclier entre l'application Web et Internet. Un serveur proxy protège l'identité d'une machine client en utilisant un intermédiaire (pour le trafic sortant), tandis qu'un WAF est un type de proxy inverse qui évite de trop exposer le serveur en acheminant le trafic du client via le pare-feu avant d'atteindre le serveur (pour le trafic entrant).

## Quels sont les types d'attaques pouvant être bloqués par un WAF ?
{:#what-types-of-attacks-can-waf-prevent}

Un WAF protège normalement les applications Web des attaques de type falsification intersite, Cross-site-Scripting (XSS), inclusion de fichier, injection SQL, entre autres. Un WAF fait généralement partie d'une suite d'outils, qui conjugués peuvent créer une défense globale contre toute une série de vecteurs d'attaque.

## Comment fonctionne un WAF ?
{:#how-does-waf-work}

Un WAF fonctionne via un ensemble de règles souvent appelées stratégies. Ces stratégies ont pour objectif de prévenir les vulnérabilités de l'application en filtrant le trafic malveillant. 

La valeur ajoutée d'un WAF provient de la facilité et de la vitesse avec lesquelles peuvent être modifiées les stratégies, permettant ainsi une réponse plus rapide aux différents vecteurs d'attaques. Par exemple, pendant une [Attaque DDoS ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://en.wikipedia.org/wiki/Denial-of-service_attack), une limitation de débit peut être mise en place en modifiant les stratégies WAF.

## Quels sont les principaux avantages du pare-feu d'application web IBM Cloud CIS ? 
{:#key-benefits-of-cis-waf}

Le WAF IBM Cloud CIS simplifie la configuration, la gestion et la personnalisation des règles de sécurité pour protéger vos applications Web des menaces Web courantes. Consultez la liste suivante pour connaître les fonctionnalités clés : 

 * **Facilité d'installation** : le WAF CIS fait partie de notre service global, qui ne prend que quelques minutes à mettre en place. Une fois que vous avez redirigé votre DNS vers nous, vous pouvez activer le WAF et configurer les règles dont vous avez besoin. 

 * **Rapports détaillés** Consultez les détails dans les rapports, par exemple sur les menaces bloquées par une règle ou un groupe de règles. 
