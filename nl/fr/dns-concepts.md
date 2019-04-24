---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: domain name system, DNS servers, match domain names, DNS Concepts

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}


# Concepts DNS
{:#dns-concepts}

Ce document présente certains concepts et définitions liés au système de noms de domaine (DNS) Internet et à la façon dont il affecte votre déploiement IBM Cloud Internet Services (CIS). 

Le système DNS (Domain Name System, système de noms de domaines), vous l'utilisez tous les jours quand vous naviguez sur Internet. Il s'exécute en arrière-plan de manière totalement autonome, et convertit le nom des sites Web en adresses IP conformément à la [RFC 1918 pour les adresses IPv4 et à la RFC 4193 pour les adresses IPv6](https://en.wikipedia.org/wiki/Private_network). En résumé, les serveurs DNS font correspondre les noms de domaine, tels que `ibm.com`, à leurs adresses IP associées, qu'une grande majorité d'utilisateurs n'a pas forcément besoin de connaître.

Le système DNS va aller chercher cette adresse IP et les informations relatives au nom d'hôte auprès d'un réseau de serveurs DNS sur Internet, de la même manière que les personnes recherchent une adresse sur un annuaire ou une carte.

## Serveurs de noms
{:#dns-concepts-nameservers}

Un **serveur de noms** implémente les services qui permettent de fournir une réponse aux requêtes via un service d'annuaire. Il convertit un identificateur hôte ou Web en une adresse IP.

La **délégation de serveur de noms** intervient lorsqu'un serveur de noms de domaine reçoit une requête provenant d'un enregistrement d'un sous-domaine et répond avec la référence du serveur de nom sur le serveur délégué. Vous pouvez ainsi décentraliser la gestion d'un grand domaine (par exemple, `ibm.com`).

Un **serveur de noms de domaine personnalisés** permet d'utiliser les serveurs du fournisseur DNS avec le nom de référence personnalisé de votre propre domaine. Par exemple, vous pouvez utiliser le serveur de noms `ns1.cloud.ibm.com` en lieu et place de `ns1.acme.com`.

## DNS sécurisé
{:#dns-concepts-secure-dns}

La technologie **DNSSec** permet d'apposer une "signature" numérique aux données DNS et garantit ainsi à l'utilisateur la validité de ces données. Afin d’éliminer cette vulnérabilité de l'Internet, il faut déployer DNSSec à chaque étape de consultation, de la consultation de la zone racine à celle du nom de domaine final, comme www.icann.org.

## Mise à plat de CNAME pour enregistrement racine 
{:#dns-concepts-root-record-cname-flattening}

IBM CIS prend en charge une fonctionnalité appelée "Mise à plat de CNAME". A l'aide de cette méthode, les enregistrements racine peuvent surmonter la restriction RFC de l'IETF, à savoir que si un enregistrement racine est un CNAME, il ne peut contenir aucun autre enregistrement pour ce domaine. Les serveurs CIS faisant autorité surmontent cette restriction en renvoyant les enregistrements A correspondant à la cible CNAME au lieu de renvoyer le CNAME lui-même, masquant ainsi le CNAME. Cette technique permet d'ajouter d'autres enregistrements au domaine, tels que des enregistrements MX, même si l'enregistrement racine est un CNAME. 

## Enregistrements DNS avec proxy activé 
{:#dns-concepts-proxying-dns-records}

IBM CIS prend en charge la possibilité d'indiquer si le proxy est activé ou non sur un enregistrement. Lorsque le proxy est activé sur un enregistrement, cela signifie que son trafic s'exécute directement via IBM CIS. Actuellement, le proxy peut être activé sur les enregistrements avec les types **A**, **AAAA** ou **CNAME**.
