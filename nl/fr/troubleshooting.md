---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM CIS connection, CIS network connection, Origin web server, troubleshooting

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Traitement des incidents liés à votre connexion CIS
{:#troubleshooting-your-cis-network-connection}

## Comment savoir si mes données sont bien transmises via la connexion IBM CIS ?
{:#how-do-i-know-if-my-data-is-passing-through-my-cis-connection}

IBM Cloud Internet Services (CIS) utilise des en-têtes HTTP, qu'il peut lire, ajouter ou modifier. Les en-têtes nous permettent de savoir comment une demande a été acheminée, en utilisant une valeur CF-Ray. Cette valeur peut être localisée à l'aide d'une commande `curl` ou d'un plug-in Chrome appelé "Claire".

Pour savoir si les données sont transmises via IBM CIS, recherchez la valeur `Ray ID` qui existe sur chaque paquet.

**Outils de ligne de commande Unix :**

 * curl pour HTTP :
`$ curl -vso /dev/null http://example.com`

 * dig pour DNS :
`$ dig www.example.com`

 * traceroute pour le réseau :
`$ traceroute example.com`

**Par exemple :**

La commande de terminal : `curl -svo /dev/null YOUR_URL_HERE. -L`

a pour résultat : `CF-RAY: 1ca349b6c1300da3-SJC`

## Ajout d'en-têtes CF-Ray 

L'en-tête CF-RAY est ajouté pour aider à suivre une demande adressée à un site Web via le réseau. Utilisez-le lorsque vous travaillez avec le support pour vous aider à résoudre tout problème lié à la connectivité. Vous pouvez afficher ce "Ray ID" dans vos journaux en apportant des modifications aux fichiers de configuration dans Apache et nginx. 

### Apache
{:#troubleshooting-cis-apache}

```
LogFormat "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-agent}i\" %{CF-Ray}i" cf_custom

CustomLog log/access_log cf_custom
```

### nginx
{:#troubleshooting-cis-nginx}

```
log_format cf_custom '$remote_addr - $remote_user [$time_local]  '
                    '"$request" $status $body_bytes_sent '
                    '"$http_referer" "$http_user_agent" '
                    '$http_cf_ray';

access_log  /var/log/nginx/access.log cf_custom;
```

## Comment puis-je tracer une route ?
{:#how-do-i-trace-a-route}

Pour savoir si une route passe par votre voie de communication IBM CIS, exécutez une commande ‘dig’ dans la fenêtre de terminal Mac ou Linux, ou une commande `nslookup` dans l'invite de commande Windows.

Si le paquet comporte une valeur CF-Ray, cela signifie qu'il a été acheminé via CIS.

La commande `traceroute` permet d'afficher le chemin complet de la demande IP.

L'équipe de support utilise ces commandes pour vous aider.

## Si un avertissement de confidentialité s'affiche
{:#troubleshooting-cis-privacy-warning}

Les certificats émis par IBM CIS couvrent le domaine racine (`example.com`) plus un niveau du sous-domaine (`*.example.com`). Si vous tentez d'atteindre un second niveau du sous-domaine (`*.*.example.com`), un avertissement de confidentialité s'affiche dans votre navigateur, car les noms d'hôte n'ont pas été ajoutés au SAN.

En outre, veuillez compter jusqu'à 15 minutes pour que l'une de nos autorités de certification partenaires émette un nouveau certificat. Un avertissement de confidentialité s'affichera dans votre navigateur si le nouveau certificat n'a pas encore été émis.

## Que faire en cas d'attaque DDoS ?
{:#troubleshooting-cis-ddos-attack}

 * **Etape 1 :** Activez le "mode défense" à partir de votre tableau de bord
 * **Etape 2 :** Définissez vos enregistrements DNS sur la sécurité maximale
 * **Etape 3 :** N'appliquez pas de limite de débit ni de régulateurs de demandes dans IBM CIS
 
En "mode défense", chaque nouveau visiteur doit passer le test de sécurité du "Captcha" pour obtenir un cookie d'accès sans demande d'authentification. Le trafic des botnets est ainsi bloqué tant que le mode défense n'est pas désactivé. Les visiteurs qui échouent au test de sécurité sont ajoutés à la base de données de réputation IP (incorrecte).

## Autres problèmes potentiels
{:#troubleshooting-cis-other-problems}

Vous trouverez ci-dessous quelques messages d'erreur communs que vous ou votre équipe de support pouvez recevoir :

| Code d'erreur    | Motif |
| ------------- | ------------- |
| 1001  | Erreur de résolution DNS. Soit le client s'est récemment inscrit et ses informations DNS n'ont pas encore été propagées, soit l'utilisateur qui gère le DNS a rencontré un incident. |
| 521  | Le serveur Web d'origine a refusé la connexion de CIS. Soit le serveur Web d'origine n'est pas en cours d'exécution, soit un événement quelconque bloque les adresses IP IBM CIS. |
| 522  | Le délai de connexion au serveur d'origine a été dépassé (30 secondes par défaut). Soit CIS a un débit limité et le serveur Web consomme toutes les ressources (serveur partagé), soit des problèmes de connectivité réseau existent entre le serveur Web et IBM CIS. |
| 523  | Le serveur d'origine est inaccessible. Assurez-vous que l'adresse IP d'origine associée à l'enregistrement DNS est la même que celle qui figure dans la page des paramètres DNS CIS. |
| 524  | IBM CIS a établi une connexion TCP mais n'a pas reçu de réponse du serveur Web. Une application à exécution longue ou une requête de base de données perturbe la connexion. |

### Absence de trafic réseau
{:#troubleshooting-cis-network-traffic}

Si vous ne voyez aucun trafic, et que vous utilisez un CNAME, vérifiez qu'une redirection est en place de sorte que le trafic ne soit pas réacheminé vers le domaine racine. Rappelez-vous que les propagations DNS peuvent durer jusqu'à 48 heures.

### Site Web hors ligne
{:#troubleshooting-cis-website-offline}

Ce que vous pouvez voir :

`IBM CIS cannot connect to the origin server (error 521, 522, 523)`.

**Site Web hors ligne - aucune version en mémoire cache**

1. Le serveur est en ligne, mais il bloque la demande IBM CIS.
2. Le serveur d'origine est hors ligne et IBM CIS ne possède pas d'image de sauvegarde du site Web 

Ce que vous pouvez faire :

* Vérifiez que les adresses IP IBM CIS sont sur liste blanche.
* Vérifiez que les adresses IP IBM CIS ne sont pas limitées au niveau du débit.
* Consultez la liste des [adresses IP sur liste blanche](/docs/infrastructure/cis?topic=cis-ibm-cloud-cis-whitelisted-ip-addresses)

### Erreur 502 “La redoutée erreur 502”
{:#troubleshooting-cis-502-error}

Cette erreur est l'une des erreurs les plus couramment rencontrées. Elle se produit généralement lorsqu'une portion du réseau est indisponible, par exemple, au début d'une attaque DDoS. Un centre de données particulier peut être indisponible pendant un certain temps. Le trafic est alors réacheminé et un routage est exécuté. 

Ce que vous pouvez voir : `Error 502 - bad gateway error`

Ce qui s'est passé :

* Une portion du réseau IBM CIS rencontre un problème.
* Généralement, le problème se limite à un serveur du centre de données.
* Il affecte seulement une partie des visiteurs du site.
* L'équipe des opérations techniques IBM CIS traite cette question.

Ce que vous pouvez faire :

* Envoyer les résultats de `www.YOUR_DOMAIN.com/cdn-cgi/trace` sous forme de ticket au [Support](/docs/get-support?topic=get-support-getting-customer-support).
* Désactiver temporairement vos enregistrements DNS (pas de proxy).

