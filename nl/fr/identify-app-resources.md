---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: origin pools, application resources, Origin Pools section

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Identifier vos ressources d'application
{:#identify-your-application-resources}

Identifiez les ressources de votre application, par exemple, les pools d'origines et les mécanismes de contrôle de santé.
 
1. Accédez à la section **Pools d'origines** et cliquez sur **Créer un pool** afin de définir un nouveau pool d'origines. 

   Les pools d'origines sont des ressources serveur qui fournissent des applications à vos clients. 
   
2. Affectez un nom à votre pool d'origines et sélectionnez le mécanisme de contrôle de santé défini précédemment. Ajoutez votre serveur d'applications comme origine. Vous pouvez ajouter une ou plusieurs origines en cliquant sur **Ajouter une origine**. 

   Si vos serveurs d’applications se trouvent derrière un équilibreur de charge local, tel qu’un équilibreur de charge IBM Cloud, ajoutez alors votre nom de domaine complet (FQDN) ou votre adresse IP virtuelle en tant qu’origine, au lieu d’ajouter vos serveurs individuels.
{:note}
   
3. Cliquez sur **Mettre à disposition une ressource** pour finaliser la création de votre pool d'origines.  

   <img src="images/reliability8.png" alt="dessin" style="width: 300px;"/>
   
   Au départ, le pool d'origines est à l'état **Défaillant**. Il passe à l'état **Sain** après un contrôle de santé réussi réalisé par le système. Vous devrez peut-être actualiser votre navigateur pour voir le changement d'état. 
   
   <img src="images/reliability9.png" alt="dessin" style="width: 300px;"/>
   
   Si votre pool d'origines contient plusieurs origines, utilisez le seuil d'origine saine pour spécifier le nombre minimal d'origines devant être saines avant de déclarer le pool sain. {:note}
   
4. Définissez autant de pools d'origines que de parcs d'applications dont vous disposez. Ces parcs peuvent se trouver dans la même région ou dans des régions différentes. Dans notre exemple, nous allons créer deux pools d'origines représentant un parc d'applications situé sur les côtes Ouest et Est des Etats-Unis. 

   <img src="images/reliability10.png" alt="dessin" style="width: 300px;"/>
