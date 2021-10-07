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
ht-degree: 58%

---

# コンテンツの HTTP/2 配信 {#http-delivery-of-content}

アドビは、パフォーマンスの向上という全体的な利点をもたらすコンテンツの HTTP/2 配信に対応しました。

>[!NOTE]
>
>この機能を使用するには、Adobe Experience Manager Dynamic Media にバンドルされている標準搭載の CDN を使用する必要があります。この機能では、その他のカスタム CDN はサポートされません。

## HTTP/2 とは  {#what-is-http}

HTTP/2 によりブラウザーとサーバーの通信が改善され、必要な処理能力を抑えながら情報をより高速に転送できます。

HTTP/2 とその利点については、次の Web サイトで簡潔に説明されています。

[HTTP/2 について知っておくべきこと](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html)

## コンテンツ配信を HTTP/2 に移行する主なメリット  {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

パフォーマンスの向上は、大きく異なる場合があります。 これは、Web サイトのコード、Dynamic Mediaの使用方法、消費者のデバイス、画面、場所など、様々な要因に基づいています。

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

   既に専用ドメインがある場合は、カスタマーサポートを通じてAdobeをオプトインできます。

   専用ドメインがない場合、Adobeでは 2018 年に HTTP/2 への移行をスケジュールする予定です。

## Dynamic Media アカウントに対して HTTP/2 を有効にする方法  {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

HTTP/2 に切り替えるリクエストを開始します。自動的にはおこなわれません。

1. HTTP/2 に切り替えるには、カスタマーサポートAdobeを開始します。 [Adobe Experience Managerサポートポータルへのアクセス ](https://helpx.adobe.com/jp/experience-manager/kb/accessing-aem-support-portal.html) を参照してください。

   1. サポートリクエストには、以下の情報を記入してください。

      1. 主要連絡先の氏名、電子メールアドレス、電話番号。
      1. HTTP/2 に切り替えるすべてのドメイン。
      1. リッチメディアリクエストにセキュアな HTTPS を使用していることを確認します。
      1. Adobeを通じて CDN を使用し、直接関係で管理されていないことを確認します。
      1. 専用ドメインを使用していることを確認します。 Dynamic Mediaを使用する場合は、専用のドメインを使用します。
   1. カスタマーサポートは、リクエストが送信された順に HTTP/2 顧客待機リストに追加します。
   1. Adobeがリクエストを処理する準備が整うと、カスタマーサポートから連絡があり、移行に関する調整と目標日の設定がおこなわれます。
   1. 完了後に通知が届き、HTTP/2 への正常な切り替えを確認できます。

      ブラウザーにはこのことが表示されないので、拡張機能をダウンロードする必要があります。

      Firefox および Chrome の場合、「HTTP/2 and SPDY Indicator」という拡張機能があります。 ブラウザーは HTTP/2 をセキュア接続でのみサポートするので、確認するには https の付いた URL を呼び出す必要があります。http/2 がサポートされている場合、拡張機能は青色のFlash記号とヘッダー「X-Firefox-Spdy」で示されます。&quot;h2&quot;


## HTTP/2 への切り替え見込み時期  {#when-can-i-expect-to-be-transitioned-over-to-http}

リクエストは、カスタマーサポートに届いた順に処理されます。

>[!NOTE]
>
>HTTP/2 への切り替えにはキャッシュのクリアが伴うので、リードタイムが長くなる場合があります。 そのため、一度に処理できる顧客の移行は数件のみとなります。

## HTTP/2 への切り替えに伴うリスク {#what-are-the-risks-with-moving-to-http}

HTTP/2 への切り替えには、新しい CDN 設定への移行が伴うので、CDN でキャッシュがクリアされます。

キャッシュが再作成されるまで、キャッシュされていないコンテンツはアドビの元のサーバーに直接アクセスして取得されます。このため、元のサーバーからリクエストをプルするときに許容できるパフォーマンスが維持されるように、アドビでは一度に少数の顧客の移行を処理するよう計画します。

## URL または Web サイトが HTTP/2 でアクティベートされていることを確認する方法 {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

ブラウザーにはこのことが表示されないので、拡張機能をダウンロードする必要があります。

Firefox および Chrome の場合、「HTTP/2 and SPDY Indicator」という拡張機能があります。 ブラウザーは HTTP/2 をセキュア接続でのみサポートするので、確認するには https の付いた URL を呼び出す必要があります。http/2 がサポートされている場合、拡張子は青いFlash記号とヘッダー `X-Firefox-Spdy` で示されます。`h2`.
