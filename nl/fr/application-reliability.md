---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: domain Input information, IBM Cloud Internet Services, Global Load balancing

subcollection: cis

---


{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Amélioration de la fiabilité et de l'évolutivité des applications à l'aide de l'équilibrage de charge global d'IBM Cloud Internet Services
{:#improving-application-reliability-and-scalability-with-global-load-balancing-from-ibm-cloud-internet-services}

Si vous possédez un site Web d'e-commerce ou si vous hébergez une application à laquelle vos utilisateurs finaux doivent pouvoir accéder en permanence, la disponibilité et les performances 24*7 de votre application sont sûrement des enjeux majeurs pour vous. 

Les fonctionnalités d'équilibrage de charge global disponibles avec IBM Cloud Internet Services (CIS) permettent d'améliorer et l'évolutivité de vos applications tout en fournissant la meilleure expérience d'utilisateur final qui soit. Ce guide fournit une revue de projet relative à la configuration de l'équilibrage de charge global.  

## Ce que vous allez faire
{:#what-you-accomplish}

Au cours de cette procédure détaillée, vous apprendrez à configurer une opération d'installation et configuration semblable à celle illustrée ci-dessous.

<img src="images/reliability1.png" alt="dessin" style="width: 300px;"/>

Dans cet exemple, les ressources d'application sont déployées dans deux emplacements de centre de données, l'un situé sur la côte Ouest des Etats-Unis et l'autre sur la côte Est des Etats-Unis. Les utilisateurs finaux sont susceptibles d'accéder à cette application partout dans le monde. 

Tâche  | Description
------------- | -------------
[Créer une instance CIS](/docs/infrastructure/cis?topic=cis-create-your-ibm-cloud-internet-services-cis-instance) | Commencez par créer votre instance IBM Cloud Internet Services (CIS) à l'aide du portail client IBM.|
[Entrer des informations relatives à votre domaine](/docs/infrastructure/cis?topic=cis-input-information-about-your-domain) | Entrez des informations sur le domaine que vous souhaitez protéger et pour lequel vous souhaitez fournir un équilibrage de charge global.
[Commencer la configuration de l'équilibreur de charge global](/docs/infrastructure/cis?topic=cis-begin-global-load-balancer-configuration) | Commencez à configurer votre équilibreur de charge global.
[Identifier vos ressources d'application](/docs/infrastructure/cis?topic=cis-identify-your-application-resources) |Identifiez les ressources de votre application, par exemple, les pools d'origines et les mécanismes de contrôle de santé.
[Définir l'équilibreur de charge global](/docs/infrastructure/cis?topic=cis-define-the-global-load-balancer) | Définissez la configuration de votre équilibreur de charge global en spécifiant un nom d'hôte, en ajoutant et en ajustant vos pools d'origines et en définissant des règles supplémentaires pour contrôler la façon dont le trafic est acheminé aux clients.
