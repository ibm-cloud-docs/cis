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

# HIPAA 勧告
{:#hipaa-advisory}

規制データ (例えば PHI、ITAR など) でのキャッシング (CDN) の使用は**禁止**されています。CIS を使用するすべての規制データ・フローは、**キャッシュなし**に設定する必要があります。
{:important}

CIS CDN によるコンテンツのキャッシングを無効にするには、いくつかの方法があります。 
- 起点サーバーは規制コンテンツに対して **Cache-Control** ヘッダーに **no-cache** を設定できます。
- 起点が **Cache-Control** ヘッダーで **no-cache** を送信しないときでも、CIS ページ・ルールを使用して、指定されたパスにあるすべてのコンテンツのキャッシングを無効にします。 
