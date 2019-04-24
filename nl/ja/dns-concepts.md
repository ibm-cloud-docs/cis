---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: domain name system, DNS servers, match domain names, DNS Concepts

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}


# DNS の概念
{:#dns-concepts}

この資料には、インターネットのドメイン・ネーム・システム (DNS) に関連した概念と定義や、DNS が IBM Cloud Internet Services (CIS) デプロイメントに与える影響について記載されています。 

ドメイン・ネーム・システム (DNS) は、毎日使用する Web の基礎となります。 バックグラウンドで透過的に働き、人間が読める Web サイト名をコンピューターが読める数値の IP アドレスに変換します。このアドレスは、[IPv4 の場合はインターネットの RFC 1918 の指針、IPv6 の場合は RFC 4193 の指針](https://en.wikipedia.org/wiki/Private_network)に従っています。 手短に言えば、DNS サーバーは、`ibm.com` などのドメイン・ネームを、ほとんどの人は知る必要のない、それと関連する IP アドレスと一致させます。

DNS システムは、インターネットでリンクされている DNS サーバーのネットワーク上でこの IP アドレスとホスト名の情報を検索します。これは人間が電話帳や地図を使って特定の場所を探すのに似ています。

## ネーム・サーバー
{:#dns-concepts-nameservers}

**ネーム・サーバー**は、ディレクトリー・サービスに対する照会への応答を提供するサービスを実装しています。 意味のあるテキスト・ベースの Web やホストの ID を IP アドレスに変換します。

**ネーム・サーバー代行**は、ドメインのネーム・サーバーがサブドメインのレコードに関する要求を受け取る際に行われ、ネーム・サーバーは要求側に対して代行サーバーの参照で応答します。 この機能を使用すると、大きなドメイン (`ibm.com` など) の管理を分散できます。

**カスタム・ドメイン・ネーム・サーバー**を使用すると、独自のドメインのカスタマイズ済みの参照名が付けられた DNS プロバイダーのサーバーを利用できます。 例えば、ネーム・サーバーが `ns1.acme.com` ではなく `ns1.cloud.ibm.com` になるように定義できます。

## 保護 DNS
{:#dns-concepts-secure-dns}

**DNSSec** は、DNS データにデジタル「署名」して、データが有効であることを証明するテクノロジーです。 インターネットから脆弱性を除外するために、ルート・ゾーンから最終的なドメイン・ネーム (www.icann.org など) までの検索の各ステップで DNSSec をデプロイしなければなりません。

## ルート・レコードの CNAME フラット化
{:#dns-concepts-root-record-cname-flattening}

IBM CIS は「CNAME フラット化」と呼ばれる機能をサポートしています。この方式を使用すると、ルート・レコードは IETF RFC 制限 (ルート・レコードが CNAME の場合、そのドメインにはその他のレコードがあってはならない) を克服することができます。CIS 権限サーバーは、CNAME 自体を戻さずに、CNAME のターゲットに対応する A のレコードを戻すことによって、CNAME を効果的に隠して、この制限を克服します。この手法により、ルート・レコードが CNAME の場合でも、MX レコードなどのその他のレコードをドメインに追加できます。

## DNS レコードのプロキシー接続
{:#dns-concepts-proxying-dns-records}

IBM CIS は、レコードをプロキシー接続するかどうかを切り替える機能をサポートしています。レコードをプロキシー接続すると、そのトラフィックは IBM CIS により直接実行されることになります。現在 **A**、**AAAA**、または **CNAME** タイプのレコードをプロキシー接続できます。
