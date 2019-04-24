---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: origin server, pool implementation, origin servers

subcollection: cis

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"} 
{:note: .note}

# Concepts d'équilibreur de charge global (GLB)
{:#global-load-balancer-glb-concepts}

Ce document présente certains concepts et définitions liés à l'équilibreur de charge global (GLB) et à la façon dont il affecte votre déploiement IBM CIS.

## Equilibreur de charge global
{:#global-load-balancer-cis}

L'équilibreur de charge global (GLB) gère le trafic sur les ressources serveur installées dans différentes régions. Le serveur d'origine peut diffuser tout le contenu d'un site Web, à condition que le trafic Web ne dépasse pas les capacités de traitement du serveur et que le temps d'attente ne soit pas une préoccupation majeure. Le GLB utilise une implémentation de _pool_ qui permet de distribuer le trafic vers plusieurs origines. Cette capacité de pool offre de nombreux avantages, notamment : 

  * Minimise le temps de réponse 
  * Crée une plus grande disponibilité grâce à la redondance 
  * Maximise le débit du trafic 

Le GLB achemine le trafic vers le pool ayant la priorité la plus élevée, en répartissant la charge entre ses serveurs d'origine. Consultez la section _Pool_ ci-après pour savoir comment le trafic est réparti au sein d'un pool. Si le pool principal devient indisponible, le trafic est automatiquement acheminé vers le pool suivant dans la liste en fonction de la priorité. 

Si des pools sont configurés pour des régions spécifiques, le trafic provenant de ces régions est d'abord envoyé aux pools de la région spécifiée. Ce n'est que si tous les pools d'une région donnée sont en panne que le trafic est redirigé vers les pools par défaut. Dans ce cas, le pool de repli est le pool avec la priorité la plus basse.  

### Fonctionnement
{:#how-glb-works}
Lorsque le GLB est créé, un enregistrement DNS lui est automatiquement ajouté avec le nom de l'équilibreur de charge. Le GLB renvoie ensuite l'une des adresses IP d'origine à un client effectuant une demande DNS. 

Par exemple, un pool d'origines est créé avec deux origines identifiant les adresses IP `169.61.244.18` et `169.61.244.19`. Si un équilibreur de charge global est créé avec le nom `glbcust.ibmmo.com` à l'aide du pool d'origines, un client sur Internet peut exécuter la commande suivante : 
```
$ ping glbcust.ibmom.com
PING glbcust.ibmom.com (169.61.244.18): 56 data bytes
```
Dans cet exemple, CIS : 

    * a créé un enregistrement DNS nommé `glbcust.ibmmo.com`
    * a utilisé le GLB pour résoudre le nom DNS en l'une des adresses IP identifiées dans le pool d'origines 

Notez que l’équilibreur de charge global ne met pas fin à la connexion TCP.
{:note}

La définition d'un élément DNS ou du GLB sur "proxy" modifie le comportement. Si, par exemple, vous activez le proxy et les options **Sécurité > TLS > Mode** sur une autre option que `Désactivé`, le système CIS met désormais fin à la connexion TCP et établit une deuxième connexion entre le système CIS et l'émetteur. 

Dans cet exemple, CIS : 

    * a créé un enregistrement DNS nommé `glbcust.ibmmo.com`
    * a utilisé le GLB pour résoudre le nom DNS en une adresse IP fournie par le système CIS 
    
Désormais, les connexions vers `glbcust.ibmmo.com` sont achevées par CIS et les certificats HTTPS sont hébergés par CIS (requis pour l'achèvement de TCP). 

Une fois le client connecté à l'application, l'image ressemble à ceci : 

`[client]<--tls-->[cis]<-->[origin server]`

## Pool
{:#glb-pools}

Un pool est un groupe de serveurs d'origine vers lequel est acheminé le trafic lorsqu'il est associé à un GLB. Le nombre minimal de serveurs d'origine disponibles requis pour que le pool soit considéré comme étant sain peut être défini par l'utilisateur, ainsi que le contrôle de santé à utiliser. Le pool d'origines peut être associé à une région spécifique ou peut être disponible pour l'ensemble des régions.

### Répartition du trafic au sein d'un pool 
{:#distribution-of-traffic-within-a-pool}

Par défaut, tout le trafic est réparti de manière égale entre les origines du pool à l'aide du protocole round-robin. Cela est également le cas pour les GLB sans proxy. 

Les origines peuvent être configurées avec des pondérations. Pour les GLB avec proxy, les pondérations déterminent le volume de trafic que chaque serveur d'origine reçoit par rapport aux autres origines du pool. Les pondérations sont configurées sous forme de nombres compris entre 0 et 1 et spécifient quelle fraction du trafic sera envoyée à l'origine.  

Pour chaque origine : 

` Pourcentage du trafic vers l'origine = pondération d'origine / somme de toutes les pondérations d'origine`

Si toutes les origines ont la pondération `1`, le trafic est réparti de manière égale.  

Les origines avec pondération `0` ne reçoivent aucun trafic pour ce pool. Cependant, l'affinité de session peut toujours remplacer cette valeur jusqu'à ce que toutes les sessions soient fermées. Si l'origine est un membre d'un autre pool, elle peut toujours recevoir du trafic pour ce pool. 

**Exemple :** 

Un pool d’origines est configuré avec 3 origines ayant les pondérations suivantes : origine-A : 0,4, origine-B : 0,3 et origine-C : 0,3. 

* Au départ, toutes les origines sont saines. Le volume de trafic que chaque origine reçoit est le suivant : origine-A : 40 %, origine-B : 30 % et origine-C : 30 %.
* origine-A devient alors critique ; elle ne reçoit plus de trafic. Les autres origines ont la même pondération et, par conséquent, le trafic est réparti de manière égale, chaque origine recevant 50 %.
* L'administrateur modifie la pondération pour origine-C sur `0`. Désormais, 100 % du nouveau trafic est redirigé vers origine-B. Mais avec l'affinité de session activée, le trafic des sessions existantes sur origine-C continue d'être dirigé vers origine-C jusqu'à la fermeture de ces sessions (24 heures max.). 

### Pool de repli
{:#fallback-pool}

Le pool d'origines ayant la priorité la plus faible (le nombre le plus élevé) est le "pool de repli" désigné. Lorsque tous les pools d'une région donnée sont arrêtés, le trafic est routé vers le pool de repli, quelle que soit son état de santé.

Lorsque tous les pools sont désactivés, le pool de repli n'est pas disponible.
{:note}

## Contrôle de santé
{:#cis-health-check}

Le contrôle de santé vous aide à avoir un meilleur aperçu de la disponibilité des pools de manière à pouvoir rediriger le trafic vers les pools qui sont sains. Ces contrôles envoient régulièrement des requêtes HTTP, HTTPS ou TCP et surveillent les réponses. Ils peuvent être configurés avec un port personnalisé, un intervalle, un délai d'attente, un code d'état, etc. Dès qu'un pool est signalé comme étant malsain, le trafic est redirigé intelligemment vers un autre pool disponible. Sachez que vos journaux font référence à Cloudflare en raison du partenariat entre IBM et Cloudflare pour alimenter CIS. {:note}

### Evénements de contrôle de santé 
{:#health-check-events}

Les événements de contrôle de santé sont des changements d'état de pools dotés de contrôles de santé connectés et leurs serveurs d'origine associés. Si l'état d'une origine se dégrade, un nouvel élément apparaît dans une table, avec la description de l'événement. Accédez à **Fiabilité > Equilibreur de charge global > Evénements de contrôle de santé** pour afficher un tableau des événements de contrôle de santé. Vous pouvez filtrer les données par date, santé du pool ou de l'origine, nom du pool et nom de l'origine en sélectionnant les paramètres de filtrage dans les menus déroulants. Vous pouvez trier les colonnes du tableau en cliquant sur le nom de la colonne.
![Tableau Evénements de contrôle de santé](images/health-check-events-table.png)

Chaque ligne du tableau se développe avec plus d'informations sur l'entrée. Si le pool est sain, seule la vignette **Détails du pool** est visible. Lorsque la ligne comporte une origine critique ou un pool dégradé, la mosaïque **Détails de l'origine concernée** apparaît également.  

![Détails des Evénements de contrôle de santé](images/health-check-events-details.png)

#### Détails du pool :
* Nom de pool - Nom du pool
* Origines saines - Rapport d'origines de santé/origines totales dans un pool
* Seuil de santé - Nombre d'origines devant être saines pour pouvoir considérer que le pool est sain
* Origines saines - Noms des origines saines
* Origines critiques - Noms des origines malsaines 

#### Détails de l'origine concernée : 
* Nom d'origine - Nom de l'origine
* Adresse d'origine - Adresse de l'origine
