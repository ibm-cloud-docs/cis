---
copyright:
  years: 2018
lastupdated: "2018-03-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Gestion de votre déploiement IBM CIS pour une sécurité optimale

Les paramètres de sécurité IBM Cloud Internet Services (CIS) utilisent des valeurs par défaut sécurisées destinées à éviter les faux positifs et les influences négatives sur votre trafic. Toutefois, ces paramètres de sécurité par défaut ne sont pas forcément adaptés aux besoins de chaque client. Suivez les étapes suivantes pour vérifier que votre compte CIS est configuré de manière sûre et sécurisée :

**Recommandations et meilleures pratiques :**

* Sécurisez vos adresses IP d'origine en établissant des connexions proxy et en augmentant le brouillage.
* Configurez votre niveau de sécurité de manière sélective.
* Activez votre pare-feu d'application Web (WAF) en toute sécurité.

## Meilleure pratique 1 : Sécurisez vos adresses IP d'origine

Lorsqu'un sous-domaine est utilisé comme proxy à l'aide d'IBM CIS, l'ensemble du trafic est protégé, car nous répondons activement avec des adresses IP spécifiques à IBM CIS (par exemple, tous nos clients se connectent d'abord aux proxy et vos adresses IP d'origine sont dissimulées).

### Utilisez les proxy IBM CIS pour tous les enregistrements DNS sur le trafic HTTP(S) provenant de votre origine

Pour améliorer la sécurité de l'adresse IP de votre origine, l'ensemble du trafic HTTP(S) doit être acheminé par proxy.

**Constatez la différence par vous-même, en contactant un enregistrement qui utilise un proxy et un autre qui n'en utilise pas :**

```
$ dig greycloud.theburritobot.com +short
1.2.3.4 (Adresse Ip d'origine)

$ dig orangecloud.theburritobot.com +short
104.16.22.6 , 104.16.23.6 (Adresses IP CIS)
```

### Masquez les enregistrements d'origine sans proxy par des noms non standard
Tous les enregistrements qui ne peuvent pas être traités comme proxy à l'aide d'IBM CIS, et qui continuent à utiliser votre IP d'origine, telle que FTP, peuvent être sécurisés en créant un brouillage supplémentaire. En particulier, si vous avez besoin d'un enregistrement pour votre origine qui ne peut pas être traité comme proxy par IBM CIS, utilisez un nom qui ne soit pas standard. Par exemple, au lieu d'utiliser `ftp.example.com`, utilisez `[mot aléatoire ou-caractères aléatoires].example.com.` Ainsi, les analyses de dictionnaire de vos enregistrements DNS sont moins susceptibles d'exposer les adresses IP de votre origine.

### Utilisez des plages IP distinctes pour le trafic HTTP et non HTTP si possible
Certains clients utilisent des plages IP séparées pour le trafic HTTP et non HTTP afin de leur permettre de passer tous les enregistrements pointant vers leur plage IP HTTP par un proxy, et de masquer l'ensemble du trafic non HTTP à l'aide d'un sous-réseau IP différent.

## Meilleure pratique 2 : Configurez votre niveau de sécurité de manière sélective
Votre **Niveau de sécurité** définit la sensibilité de votre **base de données de réputation IP**. IBM CIS reçoit plus d'un milliard d'adresses IP uniques chaque mois,  provenant de plus de 7 millions de sites Web, ce qui permet à notre système d'identifier les acteurs malveillants et de les empêcher d'accéder à vos actifs Web. Afin d'éviter les interactions négatives ou les faux positifs, configurez votre **niveau de sécurité** par domaine de manière à renforcer ou diminuer la sécurité en fonction des besoins.

### Augmentez le niveau de sécurité des zones sensibles sur 'Haut'
Vous pouvez augmenter ce paramètre en ajoutant une **Règle de page** aux pages d'administration ou de connexion, afin de réduire les tentatives d'intrusion illicites :

1. Créez une **règle de page** avec le masque d'URL de votre API (par exemple, `www.example.com/wp-login`). 
2. Recherchez le paramètre **Niveau de sécurité**.
3. Définissez-le sur la valeur **Haut**.
4. Sélectionnez **Provisionner 1 ressource**.

### Diminuez le niveau de sécurité des chemins d'accès ou API non sensibles afin de réduire les faux positifs
Vous pouvez diminuer ce paramètre pour les pages générales et le trafic d'API : 

1. Créez une **règle de page** avec le masque d'URL de votre API (par exemple, `www.example.com/api/*`).
2. Recherchez le paramètre **Niveau de sécurité**.
3. Définissez-le sur la valeur **Bas** ou **Essentiellement désactivé**.
4. Sélectionnez **Provisionner 1 ressource**.

### A quoi correspondent les différents niveaux de sécurité ?
Nos paramètres de niveau de sécurité sont alignés sur les scores de menace obtenus par certaines adresses IP sur la base des comportements malveillants sur notre réseau. Un score supérieur à 10 est considéré comme élevé.

* **HAUT** : Les scores de menace supérieurs à 0 font l'objet d'une demande d'authentification.
* **MOYEN** : Les scores de menace supérieurs à 14 font l'objet d'une demande d'authentification.
* **BAS** : Les scores de menace supérieurs à 24 font l'objet d'une demande d'authentification.
* **ESSENTIELLEMENT DESACTIVE** : Les scores de menace supérieurs à 49 font l'objet d'une demande d'authentification.

Nous vous conseillons d'examiner régulièrement vos paramètres de niveau de sécurité. Vous trouverez toutes les informations nécessaires dans le document [Meilleures pratiques pour la configuration CIS](best-practices.html). 

## Meilleure pratique 3 : Activez votre pare-feu d'application Web (WAF) en toute sécurité
Votre WAF est disponible dans la section **Sécurité**. Nous examinerons ces paramètres dans l'ordre inverse afin de vous assurer que votre WAF est configuré de la façon la plus sûre possible avant de l'activer sur la totalité de votre domaine. Ces paramètres initiaux peuvent permettre de réduire les faux positifs en renseignant l'application Trafic avec les événements WAF pour de meilleurs réglages. Des mises à jour automatiques assurent une parfaite protection contre les nouvelles menaces, à mesure qu'elles sont identifiées.

Le pare-feu d'application Web (WAF) vous protège contre les types d'attaques suivants :
* Injection SQL
* Cross-site Scripting
* Falsification intersite

Le WAF contient un ensemble de règles par défaut qui inclut les règles permettant de stopper les attaques les plus courantes. A l'heure actuelle, vous avez la possibilité d'activer ou de désactiver le WAF. Voir [Jeu de règles WAF par défaut](waf-rule-set.html) pour en savoir plus sur le jeu de règles par défaut et le comportement de chacune des règles.

Pour plus d'informations sur le pare-feu d'application Web (WAF), voir le document relatif aux [concepts du pare-feu d'application Web (WAF)](waf-concept.html). 

## Meilleure pratique 4 : Configurez vos paramètres TLS
IBM CIS prévoit un certain nombre d'options de chiffrement de votre trafic. En tant que proxy inverse, nous fermons les connexions TLS au niveau de nos centres de données et nous ouvrons une nouvelle connexion TLS vers votre serveur d'origine.

Le protocole TLS offre quatre modes de fonctionnement :
* **Désactivé** : Le protocole TLS étant désactivé dans ce mode, il n'est pas recommandé.
* **Client à périphérie** : Le protocole TLS chiffre le trafic depuis CIS vers vos clients, mais pas depuis CIS vers vos serveurs d'origine.
* **Souple de bout en bout** : Le protocole TLS chiffre l'ensemble du trafic et vous pouvez utiliser un certificat autosigné pour sécuriser le trafic entre CIS et vos serveurs d'origine.
* **Signé CA de bout en bout** : Le protocole TLS chiffre l'ensemble du trafic et vous devez obligatoirement utiliser un certificat signé par l'autorité de certification.

Pour en savoir plus sur les options TLS, voir [ce document](ssl-options.html).

IBM CIS vous permet soit d'utiliser des certificats personnalisés, soit d'utiliser un certificat générique mis à votre disposition par CIS.

### Téléchargez un certificat personnalisé
Vous pouvez télécharger votre certificat personnalisé en cliquant sur le bouton **Ajouter un certificat** et en indiquant votre certificat, votre clé privée et la méthode de regroupement. Si vous téléchargez votre propre certificat, vous êtes immédiatement assuré de sa compatibilité avec le trafic chiffré et vous gardez le contrôle sur votre certificat, par exemple, un certificat à confirmation étendue (EV). Rappelez-vous que vous êtes responsable de la gestion de votre certificat si vous devez télécharger un certificat personnalisé. Par exemple, IBM CIS ne contrôlera pas la date d'expiration de vos certificats. 

![certificat-personnalisé](images/upload-custom-certificate.png)

### Utilisez un certificat personnalisé
IBM s'est associé à un grand nombre d'autorités de certification (CA) pour fournir des certificats génériques à vos clients. Une vérification manuelle peut être requise pour configurer ces certificats. Votre équipe de support peut vous aider à réaliser ces étapes supplémentaires.
