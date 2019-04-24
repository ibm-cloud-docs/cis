---
copyright:
  years: 2018
lastupdated: "2018-03-16"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Comment IBM Cloud Internet Services (CIS) sécurise-t-il vos activités ?

IBM CIS est un service Cloud distribué dans le monde entier qui bloque les menaces et limite les bots et autres moteurs d'exploration malveillants, susceptibles de gaspiller votre bande passante et vos ressources serveur. IBM CIS fonctionne en tant que proxy inverse HTTP(S) global et en tant que prestataire de services DNS gérés. Votre trafic Web est acheminé sur notre réseau global intelligent afin d'optimiser à la fois vos performances et votre sécurité.

![security-graphic.png](images/security-graphic.png)

Voici un bref aperçu des fonctionnalités :

## Caractéristiques de sécurité

 * Pare-feu d'application Web (WAF)
 * Atténuation des attaques DDoS illimitées

## Normes et plateforme de sécurité

 * TLS (SHA2 et SHA1)
 * IPv6
 * HTTP/2 et SPDY

## DNS

 * Réseau anycast global
 * DNSSEC

## Attaques réseau et mesures d'atténuation

En règle générale, les attaques peuvent être classées en deux catégories

| Attaques de la couche 3 ou 4 | Attaques de la couche 7 |
|------------------------------|-----------------|
|Ces attaques consistent à saturer le trafic au niveau de la couche 3 du modèle OSI (couche réseau), telles que les inondations ICMP, ou au niveau de la couche 4 (couche transport), telles que les inondations SYN TCP ou les inondations SYN par réflexion |Ces attaques envoient des demandes malveillantes au niveau de la couche 7 du modèle OSI (couche application), telles que des inondations GET. |
| Ces attaques sont bloquées automatiquement au niveau de notre serveur de périphérie | Nous traitons ces attaques à l'aide du “Mode défense”, du pare-feu d'application Web (WAF) et des paramètres de niveau de sécurité |

## Récapitulatif

 * Le mode défense teste les fonctionnalités du navigateur qui font défaut à un grand nombre de clients malveillants
 * Le pare-feu d'application Web (WAF) bloque les masques de demandes connus susceptibles d'être malveillants, ou demande une authentification
