---
copyright:
  years: 2018
lastupdated: "2018-03-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Limitations connues

 * Nous vous recommandons d'utiliser Chrome.

 * Sous Firefox et Safari, les dates de *téléchargement*, de *modification* et d'*expiration* relatives à un certificat ne peuvent pas être affichées.

 * Lorsque vous modifiez une adresse URL de sorte qu'elle corresponde à une règle de page, la priorité la plus faible est accordée à cette règle.
 
 * Si vous ne possédez pas de domaine configuré, accédez à **Fiabilité > Equilibreurs de charge globaux** pour créer vos pools d'équilibrage de charge et vos contrôles de santé. Toutefois, si vous sélectionnez l'option **Créer un équilibreur de charge**, que vous configurez l'équilibreur de charge et que vous cliquez sur **Provisionner 1 ressource**, la demande est refusée, car un domaine est obligatoire. Cette limite fonctionnelle aide les utilisateurs à mieux comprendre l'objectif des pools et surveillances dans le flux de création de l'équilibreur de charge.
 
 * Le programme Accès anticipé est limité à une seule instance par compte. Une fois que vous avez créé une instance de ressource et que vous lui avez ajouté un domaine, vous n'êtes pas autorisé à ajouter de nouvelles instances de ressources pour CIS. Cette restriction s'applique même lorsque vous supprimez un domaine d'essai et que vous essayez ensuite d'ajouter à nouveau un domaine à la même instance de ressource. Une erreur sera générée si vous tentez de le faire.

 * A l'heure actuelle, lorsque vous ajoutez un nouveau domaine, le système ne collecte pas et n'importe pas vos enregistrements de domaine existants.

 * Dans le cadre du programme d'accès anticipé, nous ne prenons en charge que la délégation de sous-domaine qui utilise des enregistrements NS provenant d'un autre fournisseur. La délégation CNAME n'est pas prise en charge.
