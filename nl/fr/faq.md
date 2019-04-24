---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: configuration domain, Free Trial plan, CIS instance

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:faq: data-hd-content-type='faq'}



# Foire aux questions
{:#faq}

## Qu'en est-il du forfait Accès anticipé qui figurait dans le catalogue ? 
{:#cis-faq-early-access-plan}
{: faq}

Le forfait Accès anticipé a été supprimé du catalogue le 31 mai 2018. Il a été remplacé par le forfait Standard payant et par un nouveau forfait Essai gratuit de 30 jours. Si vous disposez d'une instance du forfait Accès anticipé, passez immédiatement au forfait Standard pour éviter toute perte de données ; vous ne serez pas autorisé à créer une instance Essai gratuit si vous avez participé au programme bêta Accès anticipé. 

## A quoi ai-je droit avec le forfait Essai gratuit ? 
{:#cis-faq-free-trial-plan}
{: faq}

Le forfait Essai gratuit, de par sa conception, autorise une seule zone par compte. Nous vous conseillons de créer une seule instance par compte et de vérifier le nom de la zone. Il est essentiel de vérifier le nom de la zone avant de l'ajouter. Si une zone est supprimée, il est impossible d'ajouter une autre zone ou la même zone pendant le forfait Essai gratuit.

## De combien d'instances Essai gratuit puis-je bénéficier ? 
{:#cis-faq-free-trial-instances}
{: faq}

Vous pouvez avoir au plus une instance Essai gratuit par compte pour la durée de vie du compte. Si vous disposez déjà d'une instance Essai gratuit, ou si vous supprimez une instance Essai gratuit, ou si la version Essai gratuit est arrivée à expiration, vous ne serez pas autorisé à créer une autre instance Essai gratuit. Cependant, vous pouvez créer des instances d'autres types de forfait payant (par exemple, Standard), indépendamment des instances Essai gratuit que vous avez éventuellement créées. 

## J'ai une instance de service souscrite avec le forfait Accès anticipé. Puis-je la remplacer par une instance Essai gratuit ? 
{:#cis-faq-early-access-to-free-trial-plan}
{: faq}

Non. Le forfait Accès anticipé ne peut être mis à niveau que vers un forfait payant, qui est le forfait Standard pour le moment. 

## J'ai eu une instance Accès anticipé que j'ai peut-être supprimée ou peut-être pas. Puis-je créer une instance Essai gratuit maintenant ? 
{:#cis-faq-early-access-and-free-trial-plan}
{: faq}

Non, chaque compte n'a droit qu'à une seule instance gratuite. Le forfait Accès anticipé et le forfait Essai gratuit qui l'a remplacé sont considérés comme des forfaits gratuits. Cela signifie également que vous pouvez avoir au plus une instance Essai gratuit. 

## Puis-je descendre de la version Standard vers la version Essai gratuit ? 
{:#cis-faq-downgrade-standard-to-free-plan}
{: faq}

Non, cette opération n'est pas autorisée. 

## Mon forfait Essai gratuit est arrivé à expiration. Quelles sont mes possibilités ?  
{:#cis-faq-free-trial-plan-expired}
{: faq}

Pour éviter toute perte de données, vous devez effectuer une mise à niveau du forfait Essai gratuit au forfait Standard avant la date d'expiration. Après quoi, nous prenons en charge uniquement la mise à niveau du forfait ou la suppression de l'instance CIS. Si l'instance n'est pas supprimée ou mise à niveau après 45 jours (à compter du lancement de l'instance), le domaine de configuration, le GLB, les pools et les contrôles de santé sont automatiquement supprimés. 

## Comment puis-je supprimer mon instance CIS ? 
{:#{:#cis-faq-delete-instance}
{: faq}

Pour supprimer une instance CIS, vous devez d'abord supprimer tous les GLB, les pools et les contrôles de santé. Supprimez ensuite le domaine associé (zone). Accédez à la page **Vue d'ensemble** et cliquez sur l'icône de la corbeille en regard du nom de domaine situé dans la section **Détails du service** pour lancer le processus de suppression. 

## J'ai ajouté un utilisateur à mon compte et lui ai donné l'autorisation de gérer la ou les instances Internet Services. Pourquoi cet utilisateur est-il confronté à des problèmes d'authentification ? 
{:#cis-faq-user-authentication-issue}
{: faq}

Il est possible que vous n'ayez pas attribué de "rôles d'accès au service" à l'utilisateur. Notez qu'il existe deux jeux de rôles distincts : "accès à la plateforme" et "accès au service". Les rôles d'accès à la plateforme sont nécessaires pour créer et gérer les instances de service, mais les rôles d'accès aux services sont nécessaires pour effectuer des opérations spécifiques au service sur les instances de service. Dans la console, ces paramètres peuvent être mis à jour à partir du menu **Gérer > Sécurité > Identité et accès**.

## Pourquoi mon domaine est-il en attente ? Comment l'activer ?
{:#cis-faq-pending-domain}
{: faq}

Lorsque vous ajoutez un domaine à CIS, nous vous fournissons quelques serveurs de noms à configurer au niveau de votre registre (ou de votre fournisseur de DNS si vous ajoutez un sous-domaine). Le domaine ou le sous-domaine reste en attente jusqu'à ce que vous ayez correctement configuré les serveurs de noms. Assurez-vous de bien ajouter les deux serveurs de noms dans votre registre ou votre fournisseur DNS. Nous analysons régulièrement le système DNS public afin de vérifier que les serveurs de noms ont été configurés conformément aux instructions. Dès que nous avons vérifié vos modifications (dans un délai de 24 heures), nous activons votre domaine. Vous pouvez soumettre une nouvelle demande de vérification des serveurs de noms en cliquant sur l'option **Revérifier les serveurs de noms** dans la page de vue d'ensemble.

## Qui est le registre de mon domaine ?
{:#cis-faq-who-is-registrar}
{: faq}

Consultez la page https://whois.icann.org/ pour en savoir plus à ce sujet. **Remarque** : Vous devez disposer de privilèges d'administration pour modifier la configuration de votre domaine au niveau du registre en vue de mettre à jour ou d'ajouter les serveurs de noms fournis pour votre domaine lorsque vous l'ajoutez à CIS. Si vous ne connaissez pas le nom du registre associé au domaine que vous essayez d'ajouter au CIS, il est peu probable que vous disposiez des autorisations requises pour mettre à jour la configuration de votre domaine au niveau du registre. Prenez contact avec le propriétaire du domaine dans votre organisation afin d'effectuer les modifications nécessaires.

## Je souhaite conserver mon fournisseur DNS actuel pour mon domaine (example.com). Puis-je déléguer un sous-domaine (subdomain.example.com) depuis mon fournisseur DNS actuel vers CIS ?
{:#cis-faq-keep-current-dns-provider}
{: faq}

Oui. Le processus est similaire à l'ajout d'un domaine, si ce n'est qu'à la place du registre, vous avez à faire au fournisseur DNS pour le domaine de niveau supérieur. Lorsque vous ajoutez un sous-domaine à CIS, vous devez configurer deux serveurs de noms, comme d'habitude. Vous configurez un enregistrement serveur de noms (NS) pour chaque serveur de noms en tant qu'enregistrement DNS au sein du domaine actuellement géré par l'autre fournisseur DNS. Dès que nous avons vérifié que les enregistrements DNS requis ont été ajoutés, nous activons votre sous-domaine. Si vous ne gérez pas le domaine de niveau supérieur au sein de votre organisation, vous devez prendre contact avec le propriétaire du domaine de niveau supérieur pour bénéficier des enregistrements NS que vous avez ajoutés.

## Qu'est-ce que TLS ?
{:#cis-faq-what-is-tls}
{: faq}

TLS est un protocole de sécurité standard qui crée un canal sécurisé entre un serveur Web et un navigateur au cours d'une communication en ligne. Un certificat TLS est requis pour créer une connexion TLS avec un site Web, et se compose du nom de domaine, du nom de la société et de données supplémentaires, telles que l'adresse, la ville, le code postal et le pays de la société. En outre, le certificat indique la date d'expiration, ainsi que les détails concernant l'autorité de certification émettrice.

## Comment fonctionne TLS ?
{:#cis-faq-how-does-tls-work}
{: faq}

Lorsqu'un navigateur initie une connexion avec un site Web sécurisé TLS, il va d'abord chercher le certificat TLS du site pour vérifier sa validité. Il vérifie que l'autorité de certification est de confiance et que le certificat est bien utilisé pour le site Web pour lequel il a été émis. Si l'une de ces conditions n'est pas vérifiée, un message avertissement s'affiche vous indiquant que le site Web n'est pas sécurisé par un certificat valide.

Lorsqu'un certificat TLS est installé sur un serveur Web, il permet d'établir une connexion sécurisée entre le serveur Web et le navigateur qui s'y connecte. Le préfixe 'https' remplace 'http' dans l'adresse du site Web et un cadenas s'affiche dans la barre d'adresse. Si le site Web utilise un certificat à validation étendue (EV), le navigateur peut également afficher la barre d'adresse en vert.

## Pourquoi un avertissement de confidentialité s'affiche-t-il ?
{:#cis-faq-privacy-warning}
{: faq}

Les certificats TLS émis par IBM Cloud CIS couvrent le domaine racine (`example.com`) et un niveau du sous-domaine (`*.example.com`). Si vous tentez d'atteindre un second niveau du sous-domaine (`*.*.example.com`), un avertissement de confidentialité s'affiche dans votre navigateur, car les noms d'hôte n'ont pas été ajoutés au SAN.

En outre, veuillez compter jusqu'à 15 minutes pour que l'une de nos autorités de certification partenaires émette un nouveau certificat. Un avertissement de confidentialité s'affichera dans votre navigateur si le nouveau certificat n'a pas encore été émis.

## Pourquoi une erreur de certificat SSL non valide s'affiche-t-elle ? 
{:#cis-faq-invalid-ssl-cert-error}
{: faq}

Si vous voyez "Error 526, Invalid SSL Certificate" lors de la visite de votre site, cela signifie peut-être que votre certificat d'origine n'est pas valide. Lorsque le proxy CIS est activé, un certificat valide signé par une autorité de certification est requis à l'origine en mode SSL par défaut, à savoir le certificat "Signé CA de bout en bout". Notez que le paramètre par défaut du mode SSL était auparavant "Souple de bout en bout", qui ne tient pas compte de la validité du certificat présenté par l'origine. La nouvelle valeur par défaut est appliquée uniquement aux domaines ajoutés à nouveau. Si votre domaine a été ajouté alors que le mode SSL par défaut était Souple de bout en bout, ce paramètre n'est pas écrasé. Vous pouvez remplacer le mode par un mode moins strict, mais cela n’est pas recommandé pour les environnements de production. 

## Qu'est-ce qu'une attaque DDoS ?
{:#cis-faq-what-is-ddos}
{: faq}

Une attaque par déni de service distribué (DDoS) est une tentative de rendre un service en ligne indisponible en le surchargeant d'un important trafic provenant de nombreuses sources. Dans une attaque DDoS, plusieurs systèmes informatiques compromis attaquent une cible, telle qu'un serveur, un site Web ou toute autre ressource réseau, ce qui a des répercussions sur l'utilisation de la ressource cible.

Le flux de messages entrants, requêtes de connexion ou paquets mal formés vers le système cible a pour conséquence de ralentir, voire de bloquer et d'arrêter le système cible, empêchant ainsi les utilisateurs ou systèmes légitimes d'un service de l'utiliser. Les attaques DDoS sont menées par divers auteurs, allant du simple pirate informatique aux réseaux de criminels organisés et agences gouvernementales.

## Que faire en cas d'attaque DDoS ?
{:#cis-faq-what-to-do-in-ddos}
{: faq}

**Etape 1 :** Activez le “Mode défense" dans l'écran **Vue d'ensemble**. 

![Mode défense](images/defense-mode.png)

**Etape 2 :** Paramétrez vos enregistrements DNS sur la sécurité maximale.

**Etape 3 :** N'appliquez pas de limite de débit ni de régulateurs de demandes dans IBM CIS, car vous avez besoin de bande passante pour vous en sortir.

**Etape 4 :** Bloquez certains pays ou visiteurs, si nécessaire.

## J'ai reçu une erreur 522, que dois-je faire ?
{:#cis-faq-522-error}
{: faq}

Une erreur 522 signifie que nous n'avons pas pu établir de connexion à votre serveur d'origine (à savoir, votre hôte). Si la connexion n'est pas établie au bout de 15 secondes, la page d'erreur 522 s'affiche.

Ce problème est généralement causé par un pare-feu ou logiciel de sécurité qui bloque accidentellement nos adresses IP. CIS agissant en tant que proxy inverse, les connexions à votre site donneront l'impression de provenir de diverses adresses IP CIS. Ainsi, certains pare-feux peuvent bloquer ces connexions, nous empêchant ainsi d'afficher correctement le contenu du site à vos visiteurs.

Pour corriger ce problème, demandez à votre hôte d'établir une liste blanche de toutes les adresses IP CIS, consultable [ici](/docs/infrastructure/cis?topic=cis-ibm-cloud-cis-whitelisted-ip-addresses).

Toutes ces adresses IP doivent être répertoriées dans la liste blanche pour éviter les erreurs 522. De même, il convient de vérifier qu'aucune de ces adresses n'est bloquée.

Les erreurs 522 peuvent également être causées par des problèmes de connectivité. Par conséquent, assurez-vous que votre serveur et votre réseau sont sains et qu'ils ne sont pas surchargés.

Si, malgré toutes ces mesures, vous continuez à recevoir des erreurs, contactez le support et confirmez les points suivants :

* Vos adresses IP sont sur liste blanche
* Votre serveur/réseau est en ligne et n'a pas subi d'altération majeure

Si vous contactez notre équipe de support, veuillez fournir le Ray ID d'une erreur 522 récente. Nous l'utiliserons pour déterminer le centre de données CIS concerné et exécuter des tests supplémentaires.

## Qu'est-ce qu'un enregistrement proxy et pourquoi en ai-je besoin ?
{:#cis-faq-proxied-record}
{: faq}

Les enregistrements proxy sont des enregistrements qui acheminent leur trafic via le proxy d'IBM CIS. Seuls les enregistrements proxy bénéficient des avantages CIS, à l'instar du masque IP, où une adresse IP CIS remplace l'adresse IP d'origine afin de la protéger :

```
$ whois 104.28.22.57 | grep OrgName
OrgName:        IBM
```

Si vous préférez ignorer CIS sur un domaine (une résolution DNS est quand même appliquée), il est possible de ne pas utiliser l'enregistrement comme proxy.

## J'ai reçu une erreur de validation DNS : 1004, que dois-je faire ?
{:#cis-faq-dns-validation-error}
{: faq}

Pour que les règles de page fonctionnent, le système DNS de votre zone doit être résolu. Par conséquent, vous devez disposer d'un enregistrement DNS proxy pour votre zone. 

## Puis-je ajouter un CNAME pour un enregistrement racine ? 
{:#cis-faq-add-cname-root-record}
{: faq}

Oui. IBM CIS prend en charge une fonctionnalité appelée "mise à plat de CNAME" qui permet à nos utilisateurs d'ajouter un CNAME en tant qu'enregistrement racine. Nos serveurs DNS faisant autorité énumèrent les enregistrements de la cible CNAME et répondent avec ces enregistrements et non avec le CNAME même, masquant ainsi le fait que l'utilisateur a configuré un CNAME à la racine du domaine. 

## Quel est le délai par défaut d'un contrôle de santé ? 
{:#cis-faq-default-health-check-timeout}
{: faq}

Le délai d'attente par défaut d'un contrôle de santé pour les forfaits Essai gratuit et Standard est de 60 secondes. 

## Les contrôles de santé peuvent-ils être configurés pour le trafic non HTTP/HTTPS ? 
{:#cis-faq-health-check-non-http-traffic}
{: faq}

Non, ils ne peuvent être configurés qu'avec HTTP/HTTPS. 

## Les GLB peuvent-ils être configurés pour le trafic non HTTP/HTTPS ? 
{:#cis-faq-glb-non-http-traffic}
{: faq}

Non, ils ne peuvent être configurés qu'avec HTTP/HTTPS. 

## La désactivation de toutes mes origines dans un pool d'origines désactivera-t-elle l'intégralité du pool d'origines ? 
{:#cis-faq-disabling-origins-disable-origin-pool}
{: faq}

Oui, si le pool d'origines est utilisé dans un équilibreur de charge, le trafic est acheminé vers le pool suivant dont la priorité est la plus élevée ou le pool de repli. 

## Mon entrée Kubernetes contient une erreur, que dois-je faire ? 
{:#cis-faq-kubernetes-ingress-error}
{: faq}

Le nom d'hôte d'une entrée Kubernetes doit être composé de caractères alphanumériques en minuscule, '-' ou '.', et doit commencer et se terminer par un caractère alphanumérique. L'utilisation du caractère `_` dans le nom de l'équilibreur de charge, bien qu'autorisée, peut entraîner une erreur d'entrée dans les clusters Kubernetes. Nous vous recommandons de ne pas utiliser le caractère `_` dans le nom de l'équilibreur de charge pour éviter les problèmes liés aux clusters Kubernetes. 

## Une erreur 502 s'affiche lorsque je tente de sauvegarder d'une action de fonctions Edge. Que dois-je faire ? 
{:#cis-faq-502-error}
{: faq}

Contactez le [support IBM](/docs/infrastructure/cis?topic=cis-getting-help-and-support) et indiquez le script que vous avez tenté de sauvegarder.
