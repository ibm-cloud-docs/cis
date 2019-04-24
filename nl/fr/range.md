---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: range application, tls encryption, ddos protection, global tcp proxy

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Fonctionnalité Range 
{:#cis-range}

La fonctionnalité Range apporte la protection DDoS, l'équilibrage de charge et l'accélération de contenu à tout protocole basé sur TCP. La fonctionnalité Range est un proxy TCP global s'exécutant sur les noeuds périphériques de CIS/Cloudflare.  

La fonctionnalité Range peut être utilisée pour : 
* Protéger vos ports et protocoles TCP contre les attaques **DDoS des couches 3 et 4.**. 
* Réduire la capacité des attaquants à espionner et à dérober des données sensibles en activant le **chiffrement TLS**.
* Intégrer le pare-feu IP de CIS, ce qui vous permet d'empêcher ou de défier les adresses IP, ou des plages d'IP entières, d'atteindre vos services TCP.  
* Configurer des équilibreurs de charge avec des contrôles de santé TCP, le basculement et des règles de pilotage pour déterminer le flux du trafic. 

## Mise en route de la fonctionnalité Range 
{:#getting-started-with-range}

La fonctionnalité Range n'est disponible que pour les clients Enterprise moyennant un coût supplémentaire et son prix dépend de l'utilisation de la bande passante. {:note}

### Ajout d'une application 
{:#range-add-an-application}
Procédez comme suit pour ajouter une application. 

1. Accédez à **Sécurité > Range**
1. Cliquez sur le bouton **Ajouter une application**  
1. Entrez le nom de l'application dans la première zone de saisie. Votre application est associée à un nom DNS sur votre domaine CIS. 
1. Entrez le port de périphérie dans la zone de saisie suivante. Nous serons à l'écoute des connexions entrantes vers ces adresses sur ce port. Les connexions à ces adresses sont transmises par proxy à votre origine. (La transmission par proxy est prise en charge sur tous les ports sauf le port 21.) 
1. Dans la section Origine, entrez l'adresse IP d'origine et le port de votre application TCP. Vous pouvez également sélectionner un équilibreur de charge existant. 
1. Activez le pare-feu IP. Lorsqu'elles sont activées, les règles de pare-feu avec une action "bloquer" ou "liste blanche" sont appliquées pour cette application. Les règles basées sur les pays ou l'ASN ne sont pas encore prises en charge. 
1. Activez le protocole proxy si un proxy en ligne prend en charge PROXY Protocol v1. Cette fonctionnalité est utile si vous exécutez un service nécessitant une connaissance de la véritable adresse IP du client. Dans la plupart des cas, ce paramètre doit rester désactivé. 
1. Cliquez sur **Mettre à disposition**

Le protocole proxy ajoute à chaque connexion un en-tête indiquant l'adresse IP et le port du client. Un en-tête de protocole proxy est au format suivant : 
  * PROXY_STRING + espace unique + INET_PROTOCOL + espace unique + CLIENT_IP + espace unique + PROXY_IP + espace unique + CLIENT_PORT + espace unique + PROXY_PORT + "\r\n"
  * Voici un exemple de ligne de protocole proxy pour une adresse IPv4 :
    `PROXY TCP4 192.0.2.0 192.0.2.255 42300 443\r\n`
  * Voici un exemple de ligne de protocole proxy pour une adresse IPv6 :
    `PROXY TCP6 2001:db8:: 2001:db8:ffff:ffff:ffff:ffff:ffff:ffff 42300 443\r\n`
   
La mise à disposition d'une application Range entraîne des coûts supplémentaires, en fonction de la quantité de bande passante utilisée par application. {:note}

Votre application est maintenant visible dans une mosaïque avec les propriétés suivantes : 
  * Nom de l'application
  * Port de périphérie
  * Origine & port
  * Connexions de l'heure écoulée (interrogées toutes les minutes) 
  * Débit de l'heure écoulée (interrogé toutes les minutes) 
  * Le menu déroulant dynamique (coin supérieur droit) permet de :  
    * Modifier l'application 
    * Afficher les métriques pour l'application spécifiée 
    * Supprimer l'application  
    
Lorsqu'une application Range est créée, une adresse IPv4 et IPv6 unique lui est attribuée. Ces adresses IP ne sont pas statiques et peuvent être modifiées. Vous pouvez déterminer l'adresse IP attribuée à l'aide de DNS. Le nom DNS renvoie toujours l'adresse IP attribuée à l'application.      
    
### Affichage de métriques 
{:#range-view-metrics}
Votre application est maintenant prête à utiliser le trafic TCP par proxy via Cloudflare/CIS.

Accédez à **Métriques > Range** pour afficher le nombre de connexions aux applications et le trafic à haut débit.
Les graphiques montrent les métriques pour un maximum de 10 applications. {:note}

Les métriques d'application peuvent être basculées via la touche Graphique ou en cliquant sur le bouton **Sélectionner des applications**. La période des données métriques peut être modifiée à l'aide du menu déroulant. 

## Mosaïque d'applications Range
{:#range-apptiles}
Après la création d'applications, la page **Sécurité > Range** est complétée avec une mosaïque d'applications. La mosaïque d'applications contient les informations suivantes : 
* Nom de l'application
* Port de périphérie
* Origine & port
* Connexions de l'heure écoulée (interrogées toutes les minutes) 
* Débit de l'heure écoulée (interrogé toutes les minutes) 


La mosaïque d'applications contient également un menu déroulant dynamique dans le coin supérieur (3 points). Le menu déroulant dynamique offre aux utilisateurs la possibilité de : 
* Modifier l'application 
* Afficher les métriques pour l'application spécifiée
  * Cela conduit l'utilisateur à la page **Métriques > Range** qui affiche les métriques uniquement pour cette application
* Supprimer l'application 


## Exemples d'utilisation de l'API 
{:#range-api-usage-examples}
Il s'agit d'exemples pour créer et répertorier des applications en utilisant Range. 

### Création d'une application Range
{:#create-range-app}
Il existe deux manières de désigner une origine dans une application Range. 
1. Adresse IP d'origine - à l'aide du paramètre `origin_direct`
2. Equilibreur de charge - à l'aide des paramètres `origin_dns` et `origin_port`

**Demande :**
```
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps \
  -H 'X-Auth-User-Token: <token>' \
  -d '{"protocol":"tcp/22","dns":{"type":"CNAME","name":"ssh.example.com"},"origin_direct":["tcp://172.0.2.1:22"],"proxy_protocol":true,"ip_firewall":true}'

```
**Réponse :**
```
{
    "result": {
        "id": "4f70c3d4f20576b79135b898295e8093",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_direct": [
            "tcp://172.0.2.1:22"
        ],
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-09T17:33:09.190606Z",
        "modified_on": "2019-01-09T17:33:09.190606Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}
```

**Demande :**
```
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps \
  -H 'X-Auth-User-Token: <token>' \
  -d '{"protocol":"tcp/22","dns":{"type":"CNAME","name":"ssh.example.com"},"origin_dns": {"name": "test"},"proxy_protocol":true,"ip_firewall":true, "origin_port": 43}'

```
**Réponse :**
```
{
    "result": {
        "id": "4f70c3d4f20576b79135b898295e8093",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_dns": {
          "name": "test"
        },
        "origin_port": 43,
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-09T17:39:09.190606Z",
        "modified_on": "2019-01-09T17:39:09.190606Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}
```

**Nom DNS :** votre application est associée à un nom DNS sur votre domaine.

**Protocole/port de périphérie :** il s'agit du port sur lequel votre application est en cours d'exécution. Les connexions à ces adresses sont transmises par proxy à votre origine. 

**Origine directe :** il s'agit de l'adresse IP sur laquelle votre application est exécutée et du port sur lequel vous souhaitez que le trafic circule de la périphérie vers votre origine.

**Pare-feu IP :** si cette option est activée, les règles de pare-feu avec une action de blocage sont appliquées pour cette application Range.

**Protocole PROXY :** activez le protocole PROXY si un proxy en ligne prend en charge PROXY Protocol v1. Dans la plupart des cas, ce paramètre reste désactivé.

**DNS d'origine :** il s'agit du nom de l'équilibreur de charge que vous souhaitez définir comme origine.

**Port d'origine :** il s'agit du port de votre service. 

### Liste de toutes les applications
{:#range-list-all-apps}

**Demande :**
```
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps
```

**Réponse :**
```
{
    "result": [
        {
            "id": "4f70c3d4f20546b79135b898295e8093",
            "protocol": "tcp/22",
            "dns": {
                "type": "CNAME",
                "name": "ssh.example.com"
            },
            "origin_direct": [
                "tcp://172.0.2.1:22"
            ],
            "ip_firewall": true,
            "proxy_protocol": true,
            "created_on": "2019-01-09T17:33:09.190606Z",
            "modified_on": "2019-01-09T17:33:09.190606Z"
        }
    ],
    "success": true,
    "errors": [],
    "messages": []
}
```

### Affichage d'une application Range spécifique 
{:#range-list-a-specific-range-app}
**Demande :**
```
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps/4f70c3d4f20546b79135b898295e8093
```

**Réponse :**
application utilisant l'adresse IP d'origine
```
{
    "result": {
        "id": "4f70c3d4f20546b79135b898295e8093",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_direct": [
            "tcp://172.0.2.1:22"
        ],
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-09T17:33:09.190606Z",
        "modified_on": "2019-01-09T17:33:09.190606Z"
    },
    "success": true,
    "errors": [],
    "messages": []
} 
```

Application utilisant l'équilibreur de charge
```
{
    "result": {
        "id": "555359036e7f4acc82d69b916f62caba",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_dns": {
            "name": "test_update"
        },
        "origin_port": 76,
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-10T22:26:47.167008Z",
        "modified_on": "2019-01-10T22:26:47.167008Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}

```
