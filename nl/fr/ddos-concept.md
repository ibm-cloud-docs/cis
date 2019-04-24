---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Attack Concepts, Application layer attacks, common types of internet attacks

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Concepts des attaques DDoS
{:#distributed-denial-of-service-ddos-attack-concepts}

Les attaques par déni de service distribué (DDos, Distributed Denial of Service) représentent la forme d'attaque Internet la plus courante contre les sites Web ou les hôtes.

## Qu'est-ce qu'une attaque DDoS ?
{:#what-is-a-ddos-attack}

Une attaque par déni de service distribué (DDoS) est une tentative de perturbation du trafic normal d'un serveur, d'un service ou d'un réseau qui consiste à saturer la cible ou ses infrastructures environnantes via un volume de trafic Internet important. D'une efficacité redoutable, ces attaques s'appuient sur une multitude de machines infectées comme sources du trafic d'attaque. Les machines exploitées peuvent inclure des ordinateurs et d'autres ressources réseau, telles que les équipements IoT. Globalement, une attaque DDoS est comparable à un embouteillage au niveau d'une grande route, qui empêche le trafic normal d'atteindre sa destination.

## Comment fonctionne une attaque DDoS ?
{:#how-does-a-ddos-attack-work}

Une attaque DDoS implique qu'un pirate prenne le contrôle d'un réseau de machines en ligne à l'insu des véritables propriétaires des ordinateurs. Les ordinateurs et autres machines (comme les appareils IoT) sont infectés par un logiciel malveillant qui transforme chaque appareil en bot (ou zombie). L'auteur de l'attaque contrôle alors à distance le réseau d'ordinateurs infectés, appelé un _botnet_. 

Une fois qu'un botnet a été mis en place, le pirate est en mesure de diriger les machines en envoyant des instructions mises à jour à chaque bot via une méthode de contrôle à distance. Lorsqu'une adresse IP est prise pour cible, elle reçoit des requêtes de la part d'un multitude de bots, ce qui peut saturer le serveur ou le réseau ciblé, entraînant un déni de service pour le trafic normal. Chaque bot étant un périphérique Internet légitime, il peut s'avérer difficile de séparer le trafic malveillant du trafic normal. 

## Quels sont les types d'attaques DDoS les plus courants ?
{:#what-are-common-types-of-ddos-attacks}

Différents vecteurs d'attaque DDoS ciblent des composants distincts d'une connexion réseau. Si la majorité des attaques DDoS impliquent de submerger de trafic une unité ou un réseau cible, ces attaques peuvent toutefois être divisées en trois catégories. Un pirate informatique peut utiliser un ou plusieurs vecteurs d'attaque différents, ou appliquer des vecteurs d'attaque selon un cycle potentiellement déterminé par les contre-mesures prises par la cible.

Les trois grandes familles d'attaques DDoS sont les suivantes :

 * Attaques au niveau des applications (couche 7)
 * Attaques au niveau des protocoles (couches 3 et 4)
 * Attaques au niveau de la volumétrie (attaques par amplification)

### Attaques sur la couche d'application
{:#application-layer-attacks}

Parfois appelées _attaques DDoS de la couche 7_ (en référence à la 7e couche du modèle OSI), l'objectif de ces attaques est d'épuiser les ressources de la cible. Les attaques ciblent la couche où les pages Web sont générées sur le serveur et fournies en réponse aux requêtes HTTP (c'est-à-dire la couche d'application). Les attaques de la couche 7 sont difficiles à contrecarrer, car il peut être difficile d'identifier le trafic comme malveillant.

### Attaques protocolaires
{:#protocol-attacks}

Les attaques protocolaires exploitent des faiblesses des couches 3 et 4 de la pile du modèle OSI pour rendre la cible inaccessible. Ces attaques, également connues sous la notion d'attaques par épuisement des tables d'état (state-exhaustion attacks), provoquent une interruption de service en consommant toute la capacité des _tables d'état_ des serveurs d'application Web ou des ressources intermédiaires comme les pare-feux et les équilibreurs de charge. 
  
### Attaques volumétriques
{:#volumetric-attacks}

Cette catégorie d'attaques tente de créer une saturation en consommant toute la bande passante disponible entre la cible et Internet. De grandes quantités de données sont envoyées vers la cible en utilisant une forme d'amplification ou un autre moyen de créer un trafic massif, comme des demandes provenant d'un botnet. 


## Que faire en cas d'attaque DDoS ?
{:#under-ddos-attack}

**Etape 1 :** Activez le “Mode défense" dans l'écran **Vue d'ensemble**. 

![Mode défense](images/defense-mode.png)

**Etape 2 :** Paramétrez vos enregistrements DNS sur la sécurité maximale.

**Etape 3 :** N'appliquez pas de limite de débit ni de régulateurs de demandes dans IBM CIS, car vous avez besoin de bande passante pour vous en sortir.

**Etape 4 :** Bloquez certains pays ou visiteurs, si nécessaire.
