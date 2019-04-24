---
copyright:
  years: 2018
lastupdated: "2018-03-17"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Gestion de votre déploiement IBM Cloud Internet Services (CIS)

Vous allez utiliser l'écran Vue d'ensemble comme base de travail. Vous trouverez dans cet écran l'ensemble des paramètres actuels de votre déploiement.

Une fois que vous avez installé et configuré votre DNS, vous pouvez commencer à l'utiliser. 

## Utilisation de l'écran Vue d'ensemble

Dans cet écran, vous pouvez voir le statut de toutes vos sélections. Vous pouvez modifier les paramètres directement dans l'écran Vue d'ensemble en cliquant simplement sur le nom souligné du paramètre que vous souhaitez modifier ; par exemple, vous pouvez cliquer sur la zone `Equilibreurs de charge` pour ajouter un équilibreur de charge.

Sur l'écran Vue d'ensemble, vous pouvez voir que le statut de la configuration de votre nom de domaine est **En attente** ou **Actif**, comme illustré dans la  figure ci-dessous.

![Image d'écran Vue d'ensemble](images/overview-screen-configuration-summary.png)


## Configuration et gestion du DNS

Accédez à votre page DNS et ajoutez un enregistrement (vraisemblablement un enregistrement de type A). Entrez les informations relatives à votre enregistrement DNS, puis cliquez sur `Ajouter un enregistrement` pour implémenter vos changements.

![Ajout DNS](images/dns/create-a-type-record.png)

## Configuration et gestion de la mise en cache

Vous pouvez maintenant configurer la mise en cache. 

![IMAGE](images/caching-screen.png)

Vous avez la possibilité de choisir entre trois options de mise en cache à partir du menu déroulant correspondant : 

 * Aucune chaîne de requête :  Seules les ressources du cache sont distribuées lorsqu'il n'y a aucune chaîne de requête.
 * Indépendamment de la chaîne de requête : La même ressource est distribuée, peu importe la chaîne de requête. (Remarque : Le paramètre **Ignorer la chaîne de requête** s'applique uniquement aux extensions de fichier statique. Ce paramètre supprime la chaîne de requête lors de la génération de la clé de cache, de sorte qu'une demande pour `style.css?something` est normalisée au format `style.css` lorsqu'elle provient de la mémoire cache.)
 * Selon la chaîne de requête : Une ressource différente est distribuée chaque fois que la chaîne de requête est modifiée.
  
## Vider le cache
 
Vous pouvez vider le cache pour préparer les mises à jour à tout moment, en saisissant simplement l'adresse URL dans la zone de purge du cache. Vous pouvez purger un seul fichier ou plusieurs fichiers simultanément (jusqu'à 30 fichiers).
 
 ## Expiration du navigateur
 
Utilisez le menu déroulant pour sélectionner une durée d'expiration de votre navigateur, par exemple, 8 heures ou 1 jour.
 
 ## Utilisation du mode développement
 
L'option **Mode développement** est destinée à être utilisée lorsque vous devez procéder à des mises à jour majeures, lorsque de nouveaux téléchargements de fichiers sont requis, ou chaque fois que vous ne voulez pas que les utilisateurs finaux travaillent à partir de la mémoire cache, mais extraient les fichiers directement à partir des serveurs d'origine. Pour commencer à utiliser le **Mode développement**, déplacez le commutateur sur la position `Activé`. Pour arrêter de l'utiliser, replacez le commutateur sur la position `Désactivé`. Le **Mode développement** expire automatiquement au bout de 3 heures. 

## Gestion de vos règles de page
 
Vous pouvez activer jusqu'à 50 règles de page. Servez-vous des menus déroulants pour les configurer. Les paramètres de règle sont divisés en trois catégories : **Sécurité**, **Performances** et **Fiabilité**.

Notez que certaines règles de page sont activées tandis que d'autres sont grisées, si ces options entrent en conflit avec les autres règles que vous venez de sélectionner. Après avoir sélectionné les règles de page de votre choix, cliquez sur **Provisionner** pour les activer. Les nouvelles règles prennent effet immédiatement et sont aussitôt visibles dans l'écran Règles de page.
 
 ![MENUS REGLES DE PAGE](images/page-rule-dropdown-settings.png)
 
Vous pouvez également activer ou désactiver vos règles de page depuis le tableau affiché dans l'écran Règles de page. Pour plus d'informations, voir [Utilisation des règles de page](using-page-rules.html).
 
 ## Paramètres de sécurité
 
Par défaut, la protection DDoS est activée pour tous les enregistrements DNS avec proxy, ce qui peut également être effectué depuis le tableau **Enregistrements** de la page DNS. Placez le commutateur WAF sur la position Activé. Lorsque vous activez ou désactivez les règles, les modifications sont appliquées immédiatement.

![IMAGE](images/ddos-waf-ssl-screen.png)

## Certificats

Lorsque vous effectuez le déploiement dans une zone, IBM CIS déploie automatiquement un certificat universel pour cette zone. Par conséquent, vous n'avez rien à faire pour que la protection basée sur certificat soit activée. Si vous le souhaitez, vous pouvez télécharger votre propre certificat. Vous aurez besoin d'un certificat distinct pour chaque zone, et un message d'erreur s'affiche si le certificat que vous téléchargez ne correspond pas à votre zone.

![IMAGE](images/certificates-table.png)
 
 ## Installation et gestion des équilibreurs de charge
 
 IBM CIS fournit un équilibrage de charge global en tant que service.

![IMAGE](images/glb-screen.png)

### Tableau de bord GLB
Votre tableau de bord comporte trois listes qui affichent respectivement les équilibreurs de charge, les pools d'origine et les contrôles de santé. Les listes affichent l'équilibreur de charge global nouveau ou mis à jour, ou l'un de ses composants après l'avoir mis à disposition ou mis à jour. Les listes sont initialement vides, et vous devez prendre quelques mesures avant de créer un équilibreur de charge.

#### Création
**Remarque **: Le signe <sup>`*`</sup> indique que cette étape est facultative.

1) <sup>`*`</sup>Pour mettre en place un contrôle de santé, cliquez sur "Créer un contrôle de santé".
  ![IMAGE](images/glb-health-check-list.png)
    <ul>
      <li>* **Chemin** : Chemin du noeud final sur lequel effectuer le contrôle de santé.</li> 
      <li>* **Type** : Protocole à utiliser pour le contrôle de santé.</li>
      <li>* **Description** : Description fournie par l'utilisateur.</li>
    </ul>

2) Pour créer un pool, cliquez sur "Créer un pool".
  ![IMAGE](images/glb-pool-list.png)
    <ul>
      <li>* **Santé** : Statut du pool.</li>
      <li>* **Nom** : Nom fourni par l'utilisateur.</li>
      <li>* **Origines** : Nombre d'origines saines dans le pool.</li>
      <li>* **Contrôle de santé** : Chemin du contrôle de santé associé, le cas échéant.</li>
    </ul>

3) Pour créer un équilibreur de charge, cliquez sur "Créer un équilibreur de charge".
  ![IMAGE](images/glb-load-balancer-list.png)
    <ul>
      <li>* **Santé** : Statut de l'équilibreur de charge.</li>
      <li>* **Nom d'hôte** : Nom ajouté en préfixe au nom de domaine.</li>
      <li>* **Pools disponibles** : Nombre de pools sains.</li>
      <li>* **TTL** : Durée de vie.</li>
      <li>* **Proxy** : Active ou désactive le flux de trafic du proxy.</li>
      <li>* **Etat** : Active ou désactive l'équilibreur de charge.</li>
    </ul>

#### Edition/Suppression
Pour éditer ou supprimer l'équilibreur de charge ou l'un de ses composants, cliquez sur le bouton du menu déroulant dynamique situé à l'extrémité de chaque ligne.

Bouton déroulant dynamique :

![IMAGE](images/overflow.png)

Les options suivantes sont disponibles pour chaque liste.

* Contrôle de santé
    * **Modifier le contrôle de santé** : Cette option redirige l'utilisateur vers le flux d'édition. 
    * **Supprimer le contrôle de santé** : Cette option ouvre la boîte de dialogue de confirmation de suppression du flux.

* Pool
    * **Afficher les détails du pool** : Cette option ouvre une boîte de dialogue modale comportant des informations sur le pool.
    * **Modifier le pool** : Cette option redirige l'utilisateur vers le flux d'édition.
    * **Supprimer le pool** : Cette option ouvre une boîte de dialogue de confirmation de suppression du flux.

* Equilibreur de charge
    * **Désactiver/Activer** : Active ou désactive un équilibreur de charge.
    * **Modifier l'équilibreur de charge** : Redirige l'utilisateur vers le flux d'édition. 
    * **Supprimer l'équilibreur de charge** : Ouvre la boîte de dialogue de confirmation de suppression du flux.

### Ajout d'un contrôle de santé

Les contrôles de santé constituent des pièces jointes facultatives aux pools d'origine. Ils utilisent un intervalle de répétition personnalisé pour analyser un corps de réponse spécifique, ou un code de statut, afin de surveiller la santé du pool. Une fois créés, les contrôles de santé peuvent être ajoutés à un nouveau pool d'origine ou à un pool d'origine qui existe déjà.

Lors de la création d'un contrôle de santé, une seule zone est requise :
 * **Code réponse** : Code ou plage de code de réponse HTTP attendu(e) pour le contrôle de santé. Cette valeur doit être comprise entre 200 et 299 avec des caractères génériques représentés par un caractère 'x'.

Zones facultatives supplémentaires :
 * **Chemin** : Chemin de noeud final sur lequel effectuer le contrôle de santé (valeur par défaut /).
 * **Type** : Protocole à utiliser pour le contrôle de santé (valeur par défaut HTTP).
 * **Description** : Description du contrôle de santé.
 * **Intervalle** : Intervalle (en secondes) entre chaque contrôle de santé. Un intervalle plus court permet d'améliorer la reprise en ligne, mais augmente la charge sur les origines, car les contrôles proviennent de plusieurs emplacements (valeur par défaut 60).
 * **Méthode** : Méthode HTTP à utiliser pour le contrôle de santé (valeur par défaut GET).
 * **Délai d'attente** : Délai (en secondes) avant que le contrôle de santé ne soit considéré comme ayant échoué (valeur par défaut 5).
 * **Nouvelles tentatives** : Nombre de tentatives à effectuer en cas de dépassement du délai avant que l'origine ne soit marquée comme défectueuse. Les tentatives sont réalisées immédiatement (valeur par défaut 2).
 * **Corps de la réponse** : Sous-chaîne insensible à la casse pour permettre les comparaisons dans le corps de réponse. Si la chaîne est introuvable, l'origine est marquée comme non intègre.
 * **En-têtes de demande** : En-têtes de demande HTTP à envoyer dans le contrôle de santé. Nous vous conseillons de définir un en-tête d'hôte par défaut. L'en-tête `User-Agent` ne peut pas être remplacé.

### Ajout d'un pool

Au moins un pool est requis pour chaque équilibreur de charge mis à disposition. Les pools regroupent vos origines pour l'équilibreur de charge à utiliser.

Lors de la création d'un pool, deux zones sont requises :
 * **Nom** : Un abrégé (balise) pour le pool. Seuls les caractères alphanumériques, les traits d'union et les traits de soulignement sont autorisés.
 * **Origines** : Liste des origines au sein du pool. Le trafic acheminé vers ce pool est équilibré entre toutes les origines actuellement intègres, à condition que le pool  lui-même soit intègre.

Zones facultatives supplémentaires :
 * **Description** : Description lisible du pool.
 * **Activé** : Indique si ce pool doit être activé (valeur par défaut). Les pools désactivés ne reçoivent aucun trafic et sont exclus des contrôles d'intégrité. La désactivation d'un pool entraîne le basculement des équilibreurs de charge qui l'utilisent vers le pool suivant, le cas échéant (valeur par défaut true).
 * **Seuil d'origine saine** : Nombre minimum d'origines devant être intègres pour que ce pool distribue le trafic. Si le nombre est inférieur à cette valeur, le pool est marqué comme étant non intègre et bascule vers le prochain pool disponible (valeur par défaut 1)
 * **Régions du contrôle de santé** : Région à partir de laquelle le contrôle de santé effectue la surveillance.
 * **Contrôle de santé** : Contrôle de santé à utiliser pour vérifier les origines au sein du pool (aucun contrôle de santé par défaut ).
 * **E-mail de notification** : Adresse électronique devant recevoir les notifications relatives à l'état de santé. Cette adresse peut être une boîte aux lettres individuelles ou une liste de diffusion.

 ### Ajout d'un équilibreur de charge

Les équilibreurs de charge aident à répartir le trafic par proxy entre plusieurs pools d'origine en utilisant une distribution de façon circulaire.

Lors de la création d'un équilibreur de charge, les zones requises sont les suivantes :
 * **Nom** : Nom d'hôte DNS à associer à votre équilibreur de charge. Si ce nom d'hôte existe déjà en tant qu'enregistrement DNS dans le DNS IBM, l'équilibreur de charge est prioritaire et l'enregistrement DNS n'est pas utilisé.
 * **Pools par défaut** : Liste d'ID pool. La liste est classée selon leur priorité de basculement. Les pools définis ici sont utilisés par défaut, ou lorsque les pools de région n'ont pas été configurés pour une région donnée.

Les zones suivantes peuvent être configurées en option :
 * **Proxy** : Achemine le trafic à l'aide du service des performances et mesures d'IBM.
 * **Affinité de session** : Achemine toujours le trafic via la même instance de performances et de mesures. Cette option est disponible uniquement si le proxy est activé.
 * **TTL** : Durée de vie (TTL) de l'entrée DNS associée à l'adresse IP renvoyée par cet équilibreur de charge. Cette option s'applique uniquement aux équilibreurs de charge qui n'utilisent pas de proxy. Sinon, elle prend la valeur par défaut `Automatique`.
 * **Pools de région** : Mappage des codes de région ou de pays vers une liste de pools (classés selon leur priorité de basculement) pour la région donnée. Toutes les régions qui ne sont pas explicitement définies utiliseront alors les pools par défaut.
