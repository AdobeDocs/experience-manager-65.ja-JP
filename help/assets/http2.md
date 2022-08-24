---
title: コンテンツの HTTP/2 配信
description: HTTP/2 によりブラウザーとサーバーの通信が改善され、必要な処理能力を抑えながら情報をより高速に転送できます。
uuid: d9deb945-bdf5-4d6b-95c8-8bae4442e618
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: c8e145ad-f021-4043-8190-62151775e296
role: User, Admin
exl-id: 9eb9f309-33e5-4694-84d2-fb2cd3de50a6
feature: Publishing,Configuration
source-git-commit: 65af6e33ae3897519491952f4d3a6832700f77b2
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 100%

---

# コンテンツの HTTP/2 配信 {#http-delivery-of-content}

アドビは、パフォーマンスの向上という全体的な利点をもたらすコンテンツの HTTP/2 配信に対応しました。

>[!NOTE]
>
>この機能を使用するには、Adobe Experience Manager Dynamic Media にバンドルされている標準搭載の CDN を使用する必要があります。この機能では、その他のカスタム CDN はサポートされません。

## HTTP/2 とは  {#what-is-http}

HTTP/2 によりブラウザーとサーバーの通信が改善され、必要な処理能力を抑えながら情報をより高速に転送できます。

HTTP/2 とその利点については、次の Web サイトで簡潔に説明されています。

[HTTP/2 について知っておく必要がある事項](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html)

## コンテンツ配信を HTTP/2 に移行する主なメリット  {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

パフォーマンスの向上は、大きく変化する可能性があります。web サイトのコード、Dynamic Media の使用方法、消費者のデバイス、画面、場所など、様々な要因があります。

アドビ独自のテストでは、以下の結果が出ています。

* 画像の場合、デバイスおよびブラウザーに応じて、応答時間が 7％～28％向上しました。パフォーマンスの向上は、iOS デバイスにおいて最も顕著でした。
* ビューアの場合、読み込み時間のパフォーマンスが 15％向上しました。

以下のデモは、HTTP/1 と HTTP/2 の読み込みの差異を示しています。

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## HTTP/2 に切り替えるには {#am-i-eligible-to-switch-over-to-http}

HTTP/2 を使用するには、以下の要件を満たしている必要があります。

* リッチメディアリクエストにセキュア HTTPS を使用している。
* アドビ製品にバンドルされたコンテンツ配信ネットワーク（CDN）を Dynamic Media ライセンスの一部として使用している。
* 専用ドメイン（company-h.assetsadobe#.com 以外）を使用している。

   既に専用ドメインがある場合、アドビのカスタマーサポート経由でオプトインできます。

   専用ドメインがない場合、アドビは 2018年に HTTP/2 への移行を予定しています。

## Dynamic Media アカウントに対して HTTP/2 を有効にする方法  {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

HTTP/2 への切り替えは、お客様からのリクエストが必要となり、自動的には行われません。

1. HTTP/2 に切り替えるには、アドビのカスタマーサポートにリクエストしてください。詳しくは、[Adobe Experience Manager サポートポータルへのアクセス](https://helpx.adobe.com/jp/experience-manager/kb/accessing-aem-support-portal.html)を参照してください。

   1. サポートリクエストには、以下の情報を記入してください。

      1. 主要連絡先の氏名、電子メールアドレス、電話番号。
      1. HTTP/2 への切り替えが必要なすべてのドメイン。
      1. リッチメディアリクエストについて、セキュリティで保護された HTTPS を使用していることを確認します。
      1. アドビ経由で CDN を利用し、直接の関係で管理していないことを確認します。
      1. 専用ドメインを使用していることを確認します。Dynamic Media を使用している場合は、専用ドメインを使用します。
   1. カスタマーサポートでは、リクエストの送信順に基づいて HTTP/2 の顧客待機リストに追加します。
   1. アドビでリクエストを処理する準備が整うと、移行についての調整や完了予定日の設定のため、カスタマーサポートから連絡が入ります。
   1. 完了すると通知されるので、正常に HTTP2 へ移行されたことを確認できます。

      ブラウザーにはこのことが表示されないので、拡張機能をダウンロードする必要があります。

      Firefox および Chrome では、「HTTP/2 および SPDY インディケーター」という拡張機能があります。ブラウザーは HTTP/2 をセキュア接続でのみサポートするので、確認するには https の付いた URL を呼び出す必要があります。HTTP/2 がサポートされている場合、拡張機能に青色の稲妻記号および「X-Firefox-Spdy: h2」というヘッダーで示されます。


## HTTP/2 への切り替え見込み時期  {#when-can-i-expect-to-be-transitioned-over-to-http}

リクエストは、カスタマーサポートが受信した順番に基づいて処理されます。

>[!NOTE]
>
>HTTP/2 への移行ではキャッシュをクリアするので、リードタイムが長期化する場合があります。そのため、一度に処理できる顧客の移行は数件のみとなります。

## HTTP/2 への切り替えに伴うリスク {#what-are-the-risks-with-moving-to-http}

HTTP/2 への切り替えには、新しい CDN 設定への移行が伴うので、CDN でキャッシュがクリアされます。

キャッシュが再作成されるまで、キャッシュされていないコンテンツはアドビの元のサーバーに直接アクセスして取得されます。このため、元のサーバーからリクエストをプルするときに許容できるパフォーマンスが維持されるように、アドビでは一度に少数の顧客の移行を処理するよう計画します。

## URL または Web サイトが HTTP/2 でアクティベートされていることを確認する方法 {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

ブラウザーにはこのことが表示されないので、拡張機能をダウンロードする必要があります。

Firefox および Chrome では、「HTTP/2 および SPDY インディケーター」という拡張機能があります。ブラウザーは HTTP/2 をセキュア接続でのみサポートするので、確認するには https の付いた URL を呼び出す必要があります。HTTP/2 がサポートされている場合、拡張機能で青色の稲妻記号および `X-Firefox-Spdy` : `h2` というヘッダーで示されます。
