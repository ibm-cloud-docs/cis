---
copyright:
  years: 2018
lastupdated: "2018-02-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Options TLS
Les options TLS vous permettent de contrôler si les visiteurs peuvent naviguer ou non sur votre site Web au moyen d'une connexion sécurisée, et le cas échéant, d'indiquer la manière dont CIS se connecte à votre serveur d'origine.

Ces options sont énumérées de la moins sécurisée (Désactivé) à la plus sécurisée (Signé CA de bout en bout). 

Les modes de chiffrement TLS sont les suivants :

 * Désactivé (valeur non recommandée)
 * Client à périphérie (absence de chiffrement entre le serveur de périphérie et le serveur d'origine, absence de prise en charge des certificats autosignés) 
 * Souple de bout en bout (les certificats entre le serveur de périphérie et le serveur d'origine peuvent être autosignés) 
 * Signé CA de bout en bout (valeur recommandée)

## Désactivé 
Aucune connexion sécurisée entre votre visiteur et CIS, et aucune connexion sécurisée entre CIS et votre serveur Web. Les visiteurs peuvent seulement consulter votre site Web sur HTTP, et les visiteurs qui essaient de se connecter via HTTPS recevront un code de statut de redirection `HTTP 301 Redirect` vers la version HTTP simple de votre site Web.

## Client à périphérie
Une connexion sécurisée entre votre visiteur et CIS est établie, mais pas entre CIS et votre serveur Web. Vous n'avez pas besoin d'un certificat TLS sur votre serveur Web, mais vos visiteurs continueront de voir le site comme étant marqué HTTPS. Cette option n'est pas recommandée si votre site Web comporte des informations sensibles. Ce paramètre fonctionne uniquement sur le port 443->80. Il ne doit être utilisé qu'en dernier recours si vous ne pouvez pas configurer le protocole TLS sur votre propre serveur Web. Cette option est la _moins sécurisée_ de toutes (même l'option “Désactivé”) et risque de vous poser un problème si vous décidez d'en changer.

## Souple de bout en bout
Une connexion sécurisée est établie entre votre visiteur et CIS, et une connexion sécurisée (mais pas authentifiée) est établie entre CIS et votre serveur Web. Votre serveur doit être configuré pour pouvoir répondre aux connexions HTTPS, avec au moins un certificat autosigné. L'authenticité du certificat n'est pas vérifiée : du point de vue de CIS (lorsqu'il se connecte à votre serveur Web d'origine), cela équivaut à ignorer le message d'erreur. Tant que l'adresse de votre serveur Web d'origine est correcte dans vos paramètres DNS, vous êtes assuré que la connexion est établie par IBM CIS et pas quelqu'un d'autre.

## Signé CA de bout en bout
Valeur recommandée. Une connexion sécurisée est établie entre le visiteur et CIS, et une connexion sécurisée et authentifiée est établie entre CIS et votre serveur Web. Votre serveur doit être configuré de manière à pouvoir répondre aux connexions HTTPS, avec un certificat TLS valide. Ce certificat doit être signé par une autorité de certification, doit avoir une date d'expiration valide et doit répondre au nom de domaine de la demande (nom d'hôte).
