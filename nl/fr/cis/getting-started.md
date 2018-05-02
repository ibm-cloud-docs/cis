---
copyright:
  years: 2018
lastupdated: "2018-03-19"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Initiation à IBM Cloud Internet Services (CIS)

IBM Cloud Internet Services (CIS) propose trois grandes fonctionnalités pour optimiser votre flux de travail : [sécurité](/docs/infrastructure/cis/managing-for-security.html), [fiabilité](/docs/infrastructure/cis/managing-for-reliability.html) et [performances](/docs/infrastructure/cis/managing-for-performance.html). Chacune de ces fonctionnalités est représentée dans la barre de navigation à gauche de votre écran lorsque l'application IBM CIS est ouverte.

IBM CIS vous permet d'optimiser ces fonctions afin de répondre à vos besoins spécifiques, y compris :

 * Serveurs DNS faisant autorité
 * Equilibrage de charge global et local
 * Pare-feu d'application Web (WAF)
 * Protection contre les DDoS
 * Mise en cache et règles de page



## Avant de commencer
Pour pouvoir utiliser IBM CIS, vous devez tout d'abord disposer d'un [IBMid](https://www.ibm.com/account/us-en/signup/register.html). Ensuite, vous pourrez commander vos services via IBM Cloud Account, ou le nouveau portail [IBM Cloud Internet Services Portal](https://console.bluemix.net/catalog/services/internet-services), selon vos préférences.

Si vous avez besoin d'aide pour ouvrir un compte permettant d'utiliser IBM Cloud Internet Services, [contactez votre représentant commercial IBM](https://www.ibm.com/cloud-computing/bluemix/contact-us) pour en savoir plus sur la mise en route.

Si vous possédez déjà un compte Softlayer, vous pouvez [lier votre compte](https://console.bluemix.net/docs/account/softlayerlink.html#unifyingaccounts) à votre IBMid. 

## Présentation du processus

Vous pouvez commencer à utiliser IBM CIS pour vos connexions à Internet en seulement quelques étapes.

 * Ouvrez l'application IBM CIS à partir de votre tableau de bord IBM Cloud.
 * Ajoutez le domaine que vous souhaitez gérer.
 * Configurez vos informations DNS avec les serveurs de noms que nous vous avons fourni.
 * Familiarisez-vous avec IBM CIS, en regardant un tutoriel ou en configurant d'autres fonctionnalités.

### Etape 1 : Ouvrez l'application IBM CIS

Ouvrez votre [tableau de bord IBM Cloud](https://console.bluemix.net/catalog/). Accédez ensuite à l'icône de l'application IBM CIS en sélectionnant la catégorie **Plateforme -> Réseau** située dans la barre de navigation à gauche du tableau de bord. Ouvrez l'application IBM Cloud Internet Services en cliquant sur l'icône qui apparaît près du milieu de l'écran. 

![Catalogue](images/catalog-cis-tile.png)

**Ecran Vue d'ensemble**

Lorsque l'application IBM CIS démarre, l'écran **Vue d'ensemble** s'ouvre avec les onglets **Sécurité**, **Fiabilité** et **Performances** à gauche de l'interface.

**Quel plan dois-je choisir ?**

En ce qui concerne la version _Accès anticipé_, un seul plan est disponible, et il est gratuit. Cliquez sur le bouton **Créer** situé dans l'angle inférieur gauche de l'écran **Vue d'ensemble** pour commencer la mise à disposition de votre compte.

**Commencer la mise à disposition**

Le premier écran de l'application IBM CIS s'affiche, à partir duquel vous allez cliquer sur le bouton **Ajouter un domaine**.

|**Notez qu'une seule instance par compte est autorisée avec le programme d'accès anticipé.** |
|-------------------------------------------------------------------|
| Après avoir créé une instance de ressource et lui avoir ajouté un domaine, vous ne pouvez pas ajouter de nouvelles instances de ressources pour IBM CIS. Cette restriction s'applique même lorsque vous supprimez un domaine d'essai et que vous essayez ensuite d'ajouter à nouveau un domaine à la même instance de ressource. Une erreur sera générée si vous tentez de le faire.|

### Etape 2. Ajoutez et configurez votre domaine.

Commencez à protéger et à améliorer les performances de votre service Web en entrant votre domaine ou un sous-domaine.

**Remarque :** Veuillez renseigner les zones DNS. Vous pouvez configurer les serveurs de noms de ces domaines ou sous-domaines au niveau du registre ou du fournisseur DNS du domaine. N'utilisez pas les CNAME.

![Initiation](images/overview-add-domain.png)
L'écran Vue d'ensemble affiche votre domaine à l'état `En attente`. Il restera dans cet état jusqu'à ce que vous ayez terminé l'étape 3.

**Remarque :** L'instance IBM CIS ne peut pas être supprimée une fois qu'un domaine a été ajouté. Pour supprimer l'instance, supprimez d'abord le domaine de l'instance.

### Etape 3. Configurez vos serveurs de noms au niveau du registre ou du fournisseur DNS existant.

Pour profiter des avantages d'IBM CIS, configurez votre registre ou votre fournisseur de nom de domaine de manière à utiliser les serveurs de noms répertoriés dans la liste. Si vous déléguez un domaine (`example.com`, par exemple), configurez les serveurs de noms répertoriés dans les paramètres de votre domaine, à l'emplacement à partir duquel ils sont gérés par votre registre (par exemple, sur le portail Web du registre). Si vous n'êtes pas sûr du registre de votre domaine, consultez la liste à l'adresse https://whois.icann.org/. Si vous déléguez un sous-domaine (par exemple, `subdomain.example.com`) à partir d'un autre fournisseur DNS, vous devez ajouter un enregistrement de serveur de noms (NS) à chacun des serveurs figurant dans la liste.

Lorsque vous avez configuré votre registre ou fournisseur DNS, un délai de 24 heures peut être requis pour que les modifications soient prises en compte. Après avoir vérifié que les serveurs de noms ont été correctement configurés pour votre domaine ou sous-domaine, le statut du domaine passe de `En attente` à `Actif`. Une fois les noms de serveurs configurés, vous pouvez cliquer sur le lien "Revérifier les serveurs de noms" dans la page `Vue d'ensemble` pour accélérer potentiellement l'activation de votre domaine (cette vérification ne peut être exécutée qu'une fois par heure).

### Etape 4. Assurez-vous qu'IBM Cloud Internet Services effectue la résolution des informations de domaine pour votre application, nom d'hôte ou site Web.

Pour continuer, sélectionnez l'onglet **Fiabilité** dans la barre de navigation de gauche et choisissez l'option **DNS**. Veillez à ajouter les _Enregistrements DNS_ appropriés. Ajoutez l'**enregistrement A** ainsi que toutes les entrées **AAAA** ou **MX** qui sont renseignées. Si vous oubliez d'ajouter ces enregistrements avant que la délégation de registre ne soit terminée, IBM Cloud Internet Services ne peut pas résoudre les informations de domaine pour vos applications Internet.  

![Initiation](images/dns-records.png)

### Etape 5. Pendant ce temps, vous pouvez commencer à gérer d'autres fonctionnalités IBM CIS.

Pour en savoir plus sur la gestion des autres fonctionnalités, voir les [instructions détaillées](/docs/infrastructure/cis/how-to.html).
