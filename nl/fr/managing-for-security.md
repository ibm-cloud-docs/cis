---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-26"

keywords: IBM CIS, optimal security, Security Level

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Gestion de votre déploiement IBM CIS pour une sécurité optimale
{:#manage-your-ibm-cis-for-optimal-security}
Les paramètres de sécurité IBM Cloud Internet Services (CIS) utilisent des valeurs par défaut sécurisées destinées à éviter les faux positifs et les influences négatives sur votre trafic. Toutefois, ces paramètres de sécurité par défaut ne sont pas forcément adaptés aux besoins de chaque client. Suivez les étapes suivantes pour vérifier que votre compte CIS est configuré de manière sûre et sécurisée.

**Recommandations et meilleures pratiques :**

* Sécurisez vos adresses IP d'origine en établissant des connexions proxy et en augmentant le brouillage.
* Configurez votre niveau de sécurité de manière sélective.
* Activez votre pare-feu d'application Web (WAF) en toute sécurité.

## Meilleure pratique 1 : Sécurisez vos adresses IP d'origine
{:#best-practice-secure-origin-ip-address}

Lorsqu'un sous-domaine est utilisé comme proxy à l'aide d'IBM CIS, l'ensemble du trafic est protégé, car nous répondons activement avec des adresses IP spécifiques à IBM CIS (par exemple, tous nos clients se connectent d'abord aux proxy et vos adresses IP d'origine sont dissimulées).

### Utilisez les proxy IBM CIS pour tous les enregistrements DNS sur le trafic HTTP(S) provenant de votre origine
{:#use-cis-proxies-for-dns-records}

Pour améliorer la sécurité de l'adresse IP de votre origine, l'ensemble du trafic HTTP(S) doit être acheminé par proxy.

**Constatez la différence par vous-même, en contactant un enregistrement qui utilise un proxy et un autre qui n'en utilise pas :**

```
$ dig nonproxied.theburritobot.com +short
1.2.3.4 (The origin IP address)

$ dig proxied.theburritobot.com +short
104.16.22.6 , 104.16.23.6 (CIS IP addresses)
```

### Masquez les enregistrements d'origine sans proxy par des noms non standard
{:#obsure-non-proxied-origin-records-with-non-standard-names}
Tous les enregistrements qui ne peuvent pas être traités comme proxy à l'aide d'IBM CIS, et qui continuent à utiliser votre IP d'origine, telle que FTP, peuvent être sécurisés en créant un brouillage supplémentaire. En particulier, si vous avez besoin d'un enregistrement pour votre origine qui ne peut pas être traité comme proxy par IBM CIS, utilisez un nom qui ne soit pas standard. Par exemple, au lieu d'utiliser `ftp.example.com`, utilisez `[mot aléatoire ou-caractères aléatoires].example.com.` Ainsi, les analyses de dictionnaire de vos enregistrements DNS sont moins susceptibles d'exposer les adresses IP de votre origine.

### Utilisez des plages IP distinctes pour le trafic HTTP et non HTTP si possible
{:#use-separate-ipranges-for-traffic}
Certains clients utilisent des plages IP séparées pour le trafic HTTP et non HTTP afin de leur permettre de passer tous les enregistrements pointant vers leur plage IP HTTP par un proxy, et de masquer l'ensemble du trafic non HTTP à l'aide d'un sous-réseau IP différent.

## Meilleure pratique 2 : Configurez votre niveau de sécurité de manière sélective
{:#best-practice-configure-security-level-selectively}
Votre **Niveau de sécurité** définit la sensibilité de votre **base de données de réputation IP**. Afin d'éviter les interactions négatives ou les faux positifs, configurez votre **niveau de sécurité** par domaine de manière à renforcer ou diminuer la sécurité en fonction des besoins.

### Augmentez le niveau de sécurité des zones sensibles sur 'Haut'
{:#increase-security-level-for-sensitive-areas}
Vous pouvez augmenter ce paramètre depuis la page Sécurité avancée de votre domaine ou en ajoutant une **Règle de page** aux pages d'administration ou de connexion, afin de réduire les tentatives d'intrusion illicites :

1. Créez une **règle de page** avec le masque d'URL de votre API (par exemple, `www.example.com/wp-login`). 
2. Recherchez le paramètre **Niveau de sécurité**.
3. Définissez-le sur la valeur **Haut**.
4. Sélectionnez **Provisionner 1 ressource**.

### Diminuez le niveau de sécurité des chemins d'accès ou API non sensibles afin de réduire les faux positifs
{:#decrease-security-level-non-sensitive-paths-reduce-false-positives}
Vous pouvez diminuer ce paramètre pour les pages générales et le trafic d'API : 

1. Créez une **règle de page** avec le masque d'URL de votre API (par exemple, `www.example.com/api/*`).
2. Recherchez le paramètre **Niveau de sécurité**.
3. Définissez-le sur la valeur **Bas** ou **Essentiellement désactivé**.
4. Sélectionnez **Provisionner 1 ressource**.

### A quoi correspondent les différents niveaux de sécurité ?
{:#what-do-security-level-settings-mean}
Nos paramètres de niveau de sécurité sont alignés sur les scores de menace obtenus par certaines adresses IP sur la base des comportements malveillants sur notre réseau. Un score supérieur à 10 est considéré comme élevé.

* **HAUT** : les scores de menace supérieurs à 0 font l'objet d'une demande d'authentification.
* **MOYEN** : les scores de menace supérieurs à 14 font l'objet d'une demande d'authentification.
* **BAS** : les scores de menace supérieurs à 24 font l'objet d'une demande d'authentification.
* **ESSENTIELLEMENT DESACTIVE** : les scores de menace supérieurs à 49 font l'objet d'une demande d'authentification.
* **DESACTIVE** : *Enterprise uniquement* 
* **SOUS ATTAQUE** : à utiliser uniquement si votre site Web fait l'objet d'une attaque DDoS. Les visiteurs reçoivent une page interstitielle pendant environ cinq secondes, tandis que CIS analyse le trafic et le comportement pour s'assurer qu'il s'agit d'un visiteur légitime qui tente d'accéder à votre site Web. **SOUS ATTAQUE** peut affecter certaines actions sur votre domaine, telles que l'utilisation d'une API. Vous pouvez définir un niveau de sécurité personnalisé pour votre API ou toute autre partie de votre domaine en créant une règle de page pour cette section. 

Nous vous conseillons d'examiner régulièrement vos paramètres de niveau de sécurité. Vous trouverez toutes les informations nécessaires dans le document [Meilleures pratiques pour la configuration CIS](/docs/infrastructure/cis?topic=cis-best-practices-for-cis-setup).

## Meilleure pratique 3 : Activez votre pare-feu d'application Web (WAF) en toute sécurité
{:#best-practice-activate-waf-safely}
Votre WAF est disponible dans la section **Sécurité**. Nous examinerons ces paramètres dans l'ordre inverse afin de vous assurer que votre WAF est configuré de la façon la plus sûre possible avant de l'activer sur la totalité de votre domaine. Ces paramètres initiaux peuvent permettre de réduire les faux positifs en renseignant les **événements de sécurité** pour de meilleurs réglages. Des mises à jour automatiques assurent une parfaite protection contre les nouvelles menaces, à mesure qu'elles sont identifiées.

Le pare-feu d'application Web (WAF) vous protège contre les types d'attaques suivants :
* Injection SQL
* Cross-site Scripting
* Falsification intersite

Le WAF contient un ensemble de règles par défaut qui inclut les règles permettant de stopper les attaques les plus courantes. A l'heure actuelle, vous avez la possibilité d’activer ou de désactiver le WAF et d’affiner les règles spécifiques des jeux de règles WAF. Voir [Jeu de règles WAF par défaut](/docs/infrastructure/cis?topic=cis-waf-default-rule-set) pour en savoir plus sur le jeu de règles par défaut et le comportement de chacune des règles.

Pour plus d'informations sur le pare-feu d'application Web (WAF), voir le document relatif aux [concepts du pare-feu d'application Web (WAF)](/docs/infrastructure/cis?topic=cis-web-application-firewall-concepts-q-a).

## Meilleure pratique 4 : Configurez vos paramètres TLS
{:#best-practice-configure-tls-settings}
IBM CIS prévoit un certain nombre d'options de chiffrement de votre trafic. En notre qualité de proxy inverse, nous fermons les connexions TLS au niveau de nos centres de données et nous ouvrons une nouvelle connexion TLS vers votre serveur d'origine. 

Le protocole TLS offre quatre modes de fonctionnement :
* **Désactivé** : Le protocole TLS étant désactivé dans ce mode, il n'est pas recommandé.
* **Client à périphérie** : Le protocole TLS chiffre le trafic depuis CIS vers vos clients, mais pas depuis CIS vers vos serveurs d'origine.
* **Souple de bout en bout** : Le protocole TLS chiffre l'ensemble du trafic et vous pouvez utiliser un certificat autosigné pour sécuriser le trafic entre CIS et vos serveurs d'origine.
* **Signé CA de bout en bout** : Le protocole TLS chiffre l'ensemble du trafic et vous devez obligatoirement utiliser un certificat signé par l'autorité de certification.

Pour en savoir plus sur les options TLS, voir [ce document](/docs/infrastructure/cis?topic=cis-tls-options).

IBM CIS vous permet soit d'utiliser des certificats personnalisés, soit d'utiliser un certificat générique mis à votre disposition par CIS.

### Téléchargez des certificats personnalisés 
{:#upload-custom-certs}
Vous pouvez télécharger votre certificat personnalisé en cliquant sur le bouton **Ajouter un certificat** et en indiquant votre certificat, votre clé privée et la méthode de regroupement. Si vous téléchargez votre propre certificat, vous êtes immédiatement assuré de sa compatibilité avec le trafic chiffré et vous gardez le contrôle sur votre certificat, par exemple, un certificat à confirmation étendue (EV). Rappelez-vous que vous êtes responsable de la gestion de votre certificat si vous devez télécharger un certificat personnalisé. Par exemple, IBM CIS ne contrôlera pas la date d'expiration de vos certificats. 

![certificat-personnalisé](images/upload-custom-certificate.png)

### Commandez des certificats dédiés 
{:#order-dedicated-certs}
CIS facilite la gestion de vos certificats en proposant des certificats dédiés. Vous n'avez plus besoin de générer de clés privées, de créer des demandes de signature de certificat (CSR) ou de vous souvenir de renouveler les certificats. Vous pouvez commander un certificat dédié en cliquant sur le bouton **Ajouter un certificat** et en commandant un certificat générique ou en entrant un nom d'hôte pour commander un certificat personnalisé dédié. Les types de certificats sont : 

 * Certificat signé SHA-2/ECDSA utilisant la clé P-256,  
 * Certificat signé SHA-2/RSA utilisant une clé RSA 2048 bits, et  
 * Certificat signé SHA-1/RSA utilisant une clé RSA 2048 bits.  
 
CIS peut émettre des certificats pour tous les TLD à l'exception de `.cu`, `.iq`, `.ir`, `.kp`, `.sd`, `.ss` et `.ye`. CIS gère la date d'expiration. Pour modifier les noms d’hôte sur votre certificat personnalisé dédié, vous devez les réorganiser puis les supprimer. Par exemple, vous commandez un certificat personnalisé dédié avec le nom d’hôte `alpha.yourdomain.com`. Pour ajouter le nom d’hôte `beta.yourdomain.com` à votre certificat personnalisé dédié, commandez un autre certificat personnalisé dédié avec les noms d’hôte `alpha.yourdomain.com` et `beta.yourdomain.com`. Ensuite, vous _devez_ supprimer le certificat personnalisé dédié d'origine. 

La première fois que vous commandez un certificat dédié, un processus de validation de contrôle de domaine (DCV) se produit, ce qui génère un enregistrement TXT correspondant. Si vous supprimez l'enregistrement TXT, le processus DCV se répète lorsque vous commandez un autre certificat dédié. Si vous supprimez un certificat dédié, l'enregistrement TXT correspondant au processus DCV n'est pas supprimé. {:note}

Les erreurs courantes rencontrées lors de la commande de certificats dédiés sont les suivantes : 
* `Erreur de connexion au service de certificat.`
* `Erreur lors de la demande du service de certificat.`
{:note}

Si vous recevez une erreur lors de la commande de certificats, actualisez la page et réessayez. 

![certificat dédié](images/order-dedicated-certificate.png)

### Utilisez un certificat personnalisé
{:#utilize-provisioned-certificate}
IBM s'est associé à un grand nombre d'autorités de certification (CA) pour fournir des certificats génériques à vos clients. Une vérification manuelle peut être requise pour configurer ces certificats. Votre équipe de support peut vous aider à réaliser ces étapes supplémentaires.

### Priorité des certificats au niveau de notre serveur de périphérie  
{:#certificate-prioirity-at-our-edge}
La priorité d'affichage des certificats au niveau de notre serveur de périphérie est : 
1. Personnalisé téléchargé 
2. Personnalisé dédié 
3. Générique dédié 
4. Universel

### Version minimale de TLS 
{:#security-minimum-tls-version}
Voir [Version minimale de TLS](/docs/infrastructure/cis?topic=cis-tls-options#minimum-tls-version). Des niveaux supérieurs de TLS offrent plus de sécurité, mais peuvent empêcher les clients de se connecter à votre site. 
