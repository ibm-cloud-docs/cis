---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: health checks, Free Trial plan, dedicated certificate, known issues

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"} 
{:note: .note} 
{:important: .important} 
{:deprecated: .deprecated} 
{:generic: data-hd-programlang="generic"}

# Limitations connues
{:#known-limitations}

 * Nous vous recommandons d'utiliser Chrome.
 
 * Le forfait Essai gratuit est limité à une instance par compte. Une fois que vous avez créé une instance de ressource et que vous lui avez ajouté un domaine, vous n'êtes pas autorisé à ajouter de nouvelles instances de ressources pour CIS. Cette restriction s'applique même lorsque vous supprimez un domaine d'essai et que vous essayez ensuite d'ajouter à nouveau un domaine à la même instance de ressource. Une erreur sera générée si vous tentez de le faire.

 * Pour ce service, nous prenons en charge uniquement la délégation de sous-domaine à l'aide d'enregistrements NS provenant d'un autre fournisseur. La délégation CNAME n'est pas prise en charge.
  
 * Les enregistrements à caractères génériques A, AAAA et CNAME (*) ne peuvent pas être transmis par proxy. 

 * Lorsque vous supprimez un certificat dédié, celui-ci peut réapparaître dans la liste quelques instants avant sa suppression. 
 
 * Pour modifier les noms d’hôte de votre certificat dédié personnalisé après la commande, vous devez commander un nouveau certificat, puis supprimer l’ancien.  
 
 * Les règles IP créées avec des codes de pays à deux lettres ne peuvent être créées qu'avec l'action `Demande d'authentification`. Si vous souhaitez bloquer les visiteurs d'un pays, effectuez une mise à niveau vers le forfait Enterprise ou définissez des règles sur votre serveur pour bloquer complètement les visiteurs. 

## Equilibreur de charge global
{:#known-limitations-glb}

 * Cloud Internet Services vous permet d’utiliser le caractère `_` dans les noms d’hôte de l’équilibreur de charge. Toutefois, les clusters Kubernetes ne peuvent pas utiliser le caractère `_`. 

 * Le forfait Standard autorise un maximum de 5 équilibreurs de charge, pools et contrôles de santé. Chaque pool peut comporter un total de 6 origines, mais seules 6 origines uniques sont autorisées dans chaque instance CIS. 

* Les événements de contrôle de santé pour les pools et les origines supprimés ne peuvent pas être filtrés, mais ils apparaissent toujours dans le tableau. 

* Si vous filtrez les Evénements de contrôle de santé par `Santé de pool`, les pools `Dégradés` sont inclus car ils sont techniquement sains, mais peuvent contenir une ou plusieurs origines critiques. 

* Lorsque vous ajoutez le nom d'en-tête de demande pour un contrôle de santé, utilisez `Hôte`. L'utilisation du mot `hôte` en minuscule pour un contrôle de santé échoue. 

## DNS
{:#known-limitations-dns}

 * L'exportation des enregistrements DNS inclut les enregistrements Cloudflare CNAME qui doivent être masqués. Ces enregistrements commencent par `_` et ont généralement un second enregistrement du même nom mais le signe `_` est supprimé.
   ```
   Ex.
   _cf.generate.yourdomain.com 0	IN	CNAME address.alias.com
   cf.generate.yourdomain.com 0	IN	CNAME address2.alias.com
   ```
 
   Ces enregistrements doivent être supprimés du fichier de zone pour pouvoir être importés correctement. 
 
 * L'exportation des enregistrements DNS CAA ne fonctionne pas correctement. `<tag>` et `<value>` sont au format hexadécimal. 
 
    CAA `<flags>` `<tag>` `<value>`
  {:note}
   ```
   Ex.
   Original CAA record
   caa.yourdomain.com.	1	IN	CAA	0 issue "letsencrypt.org"
 
   Exported CAA record
   caa.yourdomain.com.	1	IN	CAA	0 6973737565 "6c657473656e63727970742e6f7267"
   ```
Ces enregistrements doivent être convertis du format hexadécimal en chaîne ou supprimés et ajoutés manuellement avant importation. 

## Règles de page
{:#known-limitations-pagerules}

   * La mise à jour des paramètres de règles de page à l'aide du plug-in CIS pour IBM Cloud CLI peut générer une erreur si l'ID de règle de page n'est pas inclus dans la chaîne JSON ni dans le fichier JSON de la mise à jour. Pour résoudre ce problème, soumettez la mise à jour à l'aide d'un fichier de configuration JSON complet pour la règle de page, y compris l'ID. 
   * La suppression des paramètres de règle de page à l'aide de l'interface utilisateur CIS peut ne pas supprimer le paramètre, même si l'interface indique une mise à jour réussie. Pour contourner ce problème, utilisez le plug-in CIS pour la CLI IBM Cloud afin de supprimer le paramètre et inclure l'ID de règle de page dans le document de mise à jour JSON :
      ```
      $> ibmcloud cis page-rule-update <domain-id> <rule-id> -j <file>
      ```
      Le fichier JSON doit inclure la configuration complète de la règle de page, y compris l'ID, avec les mises à jour nécessaires.
