---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: health checks, origin pools, load balancers, IBM CIS

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# Installation et gestion des équilibreurs de charge
{:#set-up-and-configure-your-load-balancers}
 
 IBM CIS fournit un équilibrage de charge global en tant que service. Le tableau de bord de l'Equilibreur de charge global (GLB) se présente comme suit : 

![IMAGE](images/glb-screen.png)

## Tableau de bord GLB
{:#glb-dashboard}

Votre tableau de bord comporte trois listes qui affichent respectivement les équilibreurs de charge, les pools d'origine et les contrôles de santé. Les listes affichent l'équilibreur de charge global nouveau ou mis à jour, ou l'un de ses composants après l'avoir mis à disposition ou mis à jour. Les listes sont initialement vides, et vous devez prendre quelques mesures avant de créer un équilibreur de charge.

Reportez-vous au [guide de démarrage rapide](/docs/infrastructure/cis?topic=cis-global-load-balancer-quick-setup) si vous savez déjà ce que vous devez faire.

### Création
{:#create-health-check}

Le signe <sup>`*`</sup> indique que cette étape est facultative.
{:note}

1) <sup>`*`</sup>Pour mettre en place un contrôle de santé, cliquez sur **Créer un contrôle de santé**.
  ![IMAGE](images/glb-health-check-list.png)
    <ul>
      <li><b>Chemin</b> : Chemin du noeud final sur lequel effectuer le contrôle de santé.</li> 
      <li><b>Type</b> : Protocole à utiliser pour le contrôle de santé.</li>
      <li><b>Description</b> : Description fournie par l'utilisateur.</li>
    </ul>

2) Pour créer un pool, cliquez sur **Créer un pool**.
  ![IMAGE](images/glb-pool-list.png)
    <ul>
      <li><b>Santé</b> : Statut du pool.</li>
      <li><b>Nom</b> : Nom fourni par l'utilisateur.</li>
      <li><b>Origines</b> : Nombre d'origines saines dans le pool.</li>
      <li><b>Contrôle de santé</b> : Chemin du contrôle de santé associé, le cas échéant.</li>
    </ul>

3) Pour créer un équilibreur de charge, cliquez sur **Créer un équilibreur de charge**.
  ![IMAGE](images/glb-load-balancer-list.png)
    <ul>
      <li><b>Santé</b> : Statut de l'équilibreur de charge.</li>
      <li><b>Nom d'hôte</b> : Nom ajouté en préfixe au nom de domaine.</li>
      <li><b>Pools disponibles</b> : Nombre de pools sains.</li>
      <li><b>TTL</b> : Durée de vie.</li>
      <li><b>Proxy</b> : Active ou désactive le flux de trafic du proxy.</li>
      <li><b>Etat</b> : Active ou désactive l'équilibreur de charge.</li>
    </ul>

Les régions géographiques d'IBM diffèrent de celles de Cloudflare. Pour plus de détails sur les régions géographiques utilisées par Cloudflare, voir [Load Balancing: Geographic Regions ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://support.cloudflare.com/hc/en-us/articles/115000540888-Load-Balancing-Geographic-Regions){:new_window}.  
{:note}

### Edition/Suppression
{:#edit-delete-load-balancer}
Pour éditer ou supprimer l'équilibreur de charge ou l'un de ses composants, cliquez sur le bouton du menu déroulant dynamique situé à l'extrémité de chaque ligne.

Bouton déroulant dynamique :

![IMAGE](images/overflow.png)

Les options suivantes sont disponibles pour chaque liste.

* Contrôle de santé
    * **Afficher le contrôle de santé** : Cette option affiche un bref récapitulatif du contrôle de santé, avec un lien menant au flux de modification..
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

## Ajout d'un contrôle de santé
{:#add-a-health-check}

Les contrôles de santé constituent des pièces jointes facultatives aux pools d'origine. Ils utilisent un intervalle de répétition personnalisé pour analyser un corps de réponse spécifique, ou un code de statut, afin de surveiller la santé du pool. Une fois créés, les contrôles de santé peuvent être ajoutés à un nouveau pool d'origines ou à un pool d'origines existant.

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

## Ajout d'un pool
{:#add-a-pool}

Au moins un pool est requis pour chaque équilibreur de charge mis à disposition. Les pools regroupent vos origines pour l'équilibreur de charge à utiliser.

Lors de la création d'un pool, deux zones sont requises :
 * **Nom** : Un abrégé (balise) pour le pool. Seuls les caractères alphanumériques, les traits d'union et les traits de soulignement sont autorisés.
 * **Origines** : Liste des origines au sein du pool. Le trafic acheminé vers ce pool est équilibré entre toutes les origines actuellement intègres, à condition que le pool lui-même soit intègre.

Zones facultatives supplémentaires :
 * **Description** : Description lisible du pool.
 * **Activé** : Indique si ce pool doit être activé (valeur par défaut). Les pools désactivés ne reçoivent aucun trafic et sont exclus des contrôles d'intégrité. La désactivation d'un pool entraîne le basculement des équilibreurs de charge qui l'utilisent vers le pool suivant, le cas échéant (valeur par défaut true).
 * **Seuil d'origine saine** : Nombre minimum d'origines devant être intègres pour que ce pool distribue le trafic. Si le nombre est inférieur à cette valeur, le pool est marqué comme étant non intègre et bascule vers le prochain pool disponible (valeur par défaut 1)
 * **Régions du contrôle de santé** : Région à partir de laquelle le contrôle de santé effectue la surveillance. **Remarque** : Les régions géographiques d'IBM diffèrent de celles de Cloudflare. Pour plus de détails sur les régions géographiques utilisées par Cloudflare, voir [Load Balancing: Geographic Regions ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://support.cloudflare.com/hc/en-us/articles/115000540888-Load-Balancing-Geographic-Regions){:new_window}. 
 * **Contrôle de santé** : Contrôle de santé à utiliser pour vérifier les origines au sein du pool (aucun contrôle de santé par défaut ).
 * **E-mail de notification** : Adresse électronique devant recevoir les notifications relatives à l'état de santé. Cette adresse peut être une boîte aux lettres individuelles ou une liste de diffusion.

## Ajout d'un équilibreur de charge
{:#add-a-load-balancer}

Les équilibreurs de charge aident à répartir le trafic par proxy entre plusieurs pools d'origine en utilisant une distribution de façon circulaire.

Lors de la création d'un équilibreur de charge, les zones requises sont les suivantes :
 * **Nom** : Nom d'hôte DNS à associer à votre équilibreur de charge. Si ce nom d'hôte existe déjà en tant qu'enregistrement DNS dans le DNS IBM, l'équilibreur de charge est prioritaire et l'enregistrement DNS n'est pas utilisé.
 * **Pools par défaut** : Liste d'ID pool. La liste est classée selon leur priorité de basculement. Les pools définis ici sont utilisés par défaut, ou lorsque les pools de région n'ont pas été configurés pour une région donnée.

Les zones suivantes peuvent être configurées en option :
 * **Proxy** : Achemine le trafic à l'aide du service des performances et mesures d'IBM.
 * **Affinité de session** : Achemine toujours le trafic via la même instance de performances et de mesures. Cette option est disponible uniquement si le proxy est activé.
 * **TTL** : Durée de vie (TTL) de l'entrée DNS associée à l'adresse IP renvoyée par cet équilibreur de charge. Cette option s'applique uniquement aux équilibreurs de charge qui n'utilisent pas de proxy. Sinon, elle prend la valeur par défaut `Automatique`.
 * **Pools de région** : Mappage des codes de région ou de pays vers une liste de pools (classés selon leur priorité de basculement) pour la région donnée. Toutes les régions qui ne sont pas explicitement définies utiliseront alors les pools par défaut. **Remarque** : Les régions géographiques d'IBM diffèrent de celles de Cloudflare. Pour plus de détails sur les régions géographiques utilisées par Cloudflare, voir [Load Balancing: Geographic Regions ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://support.cloudflare.com/hc/en-us/articles/115000540888-Load-Balancing-Geographic-Regions){:new_window}. 
 
Pour consulter les définitions des termes utilisés dans le présent document, qui sont généralement des termes courants dans l’ensemble du secteur d'activité, reportez-vous au [Glossaire](/docs/infrastructure/cis?topic=cis-glossary).
