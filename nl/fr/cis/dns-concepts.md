---

copyright:
  years: 2018
lastupdated: "2018-03-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}


# Concepts DNS

Ce document présente certains concepts et définitions liés au système de noms de domaine (DNS) Internet et à la façon dont il affecte votre déploiement IBM Cloud Internet Services (CIS). 

Le système DNS (Domain Name System, système de noms de domaines), vous l'utilisez tous les jours quand vous naviguez sur Internet. Il s'exécute en arrière-plan de manière totalement autonome, et convertit le nom des sites Web en adresses IP conformément à la [RFC 1918 pour les adresses IPv4 et à la RFC 4193 pour les adresses IPv6](https://en.wikipedia.org/wiki/Private_network). En résumé, les serveurs DNS font correspondre les noms de domaine, tels que 'ibm.com', à leurs adresses IP associées, qu'une grande majorité d'utilisateurs n'a pas forcément besoin de connaître.

Le système DNS va aller chercher cette adresse IP et les informations relatives au nom d'hôte auprès d'un réseau de serveurs DNS sur Internet, de la même manière que les personnes recherchent une adresse sur un annuaire ou une carte.

## Serveurs de noms
Un **serveur de noms** implémente les services qui permettent de fournir une réponse aux requêtes via un service d'annuaire. Il convertit un identificateur hôte ou Web en une adresse IP.

La **délégation de serveur de noms** intervient lorsqu'un serveur de noms de domaine reçoit une requête provenant d'un enregistrement d'un sous-domaine et répond avec la référence du serveur de nom sur le serveur délégué. Vous pouvez ainsi décentraliser la gestion d'un grand domaine (par exemple, `ibm.com`).

Un **serveur de noms de domaine personnalisés** permet d'utiliser les serveurs du fournisseur DNS avec le nom de référence personnalisé de votre propre domaine. Par exemple, vous pouvez utiliser le serveur de noms `ns1.cloud.ibm.com` en lieu et place de `ns1.acme.com`.

## DNS sécurisé

La technologie **DNSSec** permet d'apposer une "signature" numérique aux données DNS et garantit ainsi à l'utilisateur la validité de ces données. Afin d’éliminer cette vulnérabilité de l'Internet, il faut déployer DNSSec à chaque étape de consultation, de la consultation de la zone racine à celle du nom de domaine final, comme www.icann.org.
