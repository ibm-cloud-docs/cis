---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: domain Input information, IBM Cloud Internet Service, Domain Name

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Entrer des informations relatives à votre domaine
{:#input-information-about-your-domain}

Entrez des informations sur le domaine que vous souhaitez protéger et pour lequel vous souhaitez fournir un équilibrage de charge global.

1. Cliquez sur **Vue d'ensemble** sur le côté gauche de l'écran Démarrage. Entrez votre nom de domaine (ou votre nom de sous-domaine) et cliquez sur **Ajouter un domaine**. 
    
    <img src="images/reliability3.png" alt="dessin" style="width: 300px;"/>
    
    IBM Cloud Internet Service n'est pas un registraire DNS. Ce domaine (ou sous-domaine) doit donc avoir été créé auparavant. {:note}

    Sous la section Détails du service, vous constaterez que le domaine nouvellement ajouté est à l'état En attente. 

    <img src="images/reliability4.png" alt="dessin" style="width: 300px;"/>    

2. Accédez à la page d'administration pour votre domaine avec votre enregistreur DNS respectif et déléguez votre domaine/sous-domaine aux serveurs de noms IBM en définissant des enregistrements de serveur de noms.

Un délai de 24 heures peut s'écouler avant la réplication de vos informations dans la base de données DNS. Une fois ce processus terminé, votre domaine passe à l'état Actif. 

<img src="images/reliability5.png" alt="dessin" style="width: 300px;"/>    
