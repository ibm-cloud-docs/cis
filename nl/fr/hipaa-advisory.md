---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Advisory, Use of Caching, content caching, Cache-Control header

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Avis HIPAA 
{:#hipaa-advisory}

L'utilisation de la mise en cache (CDN) pour les données réglementées (par exemple, PHI, ITAR) est **interdite**. Tous les flux de données réglementés qui utilisent CIS doivent être configurés pour **ne pas être mis en cache**. {:important}

Il existe plusieurs façons de désactiver la mise en cache du contenu par le CDN CIS.  
- Le serveur d'origine peut définir **no-cache** dans l'en-tête **Cache-Control** pour le contenu réglementé. 
- Utilisez les règles de page CIS pour désactiver la mise en cache de tout contenu sur un chemin spécifié, même si l'origine n'envoie pas d'en-tête **no-cache** **Cache-Control**.  
