---
title: コンテンツの HTTP/2 配信の
description: HTTP/2 によりブラウザーとサーバーの通信が改善され、必要な処理能力を抑えながら情報をより高速に転送できます。
uuid: d9deb945-bdf5-4d6b-95c8-8bae4442e618
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: c8e145ad-f021-4043-8190-62151775e296
role: Business Practitioner, Administrator
exl-id: 9eb9f309-33e5-4694-84d2-fb2cd3de50a6
feature: 公開，設定
source-git-commit: c9aec973faf4caef741961d92a6f258646aeddb7
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 52%

---

# コンテンツのHTTP/2配信{#http-delivery-of-content}

アドビは、パフォーマンスの向上という全体的な利点をもたらすコンテンツの HTTP/2 配信に対応しました。

>[!NOTE]
>
>この機能を使用するには、Adobe Experience Manager Dynamic Mediaに組み込まれている標準搭載のCDNを使用する必要があります。 その他のカスタムCDNは、この機能ではサポートされません。

## HTTP/2 とは {#what-is-http}

HTTP/2 によりブラウザーとサーバーの通信が改善され、必要な処理能力を抑えながら情報をより高速に転送できます。

HTTP/2 とその利点については、次の Web サイトで簡潔に説明されています。

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## コンテンツ配信を HTTP/2 に移行する主なメリット {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

パフォーマンスの向上は、大きく異なる場合があります。 これは、Webサイトのコード、Dynamic Mediaの使用方法、消費者のデバイス、画面、場所など、様々な要因に基づきます。

アドビ独自のテストでは、以下の結果が出ています。

* 画像の場合、デバイスおよびブラウザーに応じて、応答時間が 7％～28％向上しました。パフォーマンスの向上は、iOS デバイスにおいて最も顕著でした。
* ビューアの場合、読み込み時間のパフォーマンスが 15％向上しました。

以下のデモは、HTTP/1 と HTTP/2 の読み込みの差異を示しています。

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## HTTP/2 に切り替えるには  {#am-i-eligible-to-switch-over-to-http}

HTTP/2 を使用するには、以下の要件を満たしている必要があります。

* リッチメディアリクエストにセキュア HTTPS を使用している。
* アドビ製品にバンドルされたコンテンツ配信ネットワーク（CDN）を Dynamic Media ライセンスの一部として使用している。
* 専用ドメイン（company-h.assetsadobe#.com 以外）を使用している。

   既に専用ドメインがある場合は、テクニカルサポートを通じてオプトインできます。

   専用ドメインがない場合、Adobeでは2018年にHTTP/2への移行をスケジュールする予定です。

## Dynamic Media アカウントに対して HTTP/2 を有効にする方法 {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

HTTP/2に切り替えるためのリクエストを開始します。自動的にはおこなわれません。

1. HTTP/2に切り替えるには、カスタマーケアリクエストをAdobeに送信します。 [AEM サポートポータルへのアクセス](https://helpx.adobe.com/jp/experience-manager/kb/accessing-aem-support-portal.html)を参照してください。

   1. サポートリクエストには、以下の情報を記入してください。

      1. 主要連絡先の氏名、電子メールアドレス、電話番号。
      1. HTTP/2に切り替えるすべてのドメイン。
      1. リッチメディアリクエストにセキュアなHTTPSを使用していることを確認します。
      1. Adobeを通じてCDNを使用し、直接関係で管理されていないことを確認します。
      1. 専用ドメインを使用していることを確認します。 Dynamic Mediaを使用する場合は、専用ドメインを使用します。
   1. カスタマーケアは、リクエストが送信された順序に基づいてHTTP/2顧客待機リストにユーザーを追加します。
   1. Adobeでリクエストを処理する準備が整うと、カスタマーケアから連絡があり、移行の調整と目標日の設定がおこなわれます。
   1. 完了後に通知が届き、HTTP/2への正常な切り替えを確認できます。

      ブラウザーにはこのことが表示されないので、拡張機能をダウンロードする必要があります。

      FirefoxおよびChromeの場合、「HTTP/2 and SPDY Indicator」という拡張機能があります。 ブラウザーは HTTP/2 をセキュア接続でのみサポートするので、確認するには https の付いた URL を呼び出す必要があります。http/2がサポートされている場合、拡張機能は青いFlash記号とヘッダー「X-Firefox-Spdy」で示されます。&quot;h2&quot;です。


## HTTP/2 への切り替え見込み時期 {#when-can-i-expect-to-be-transitioned-over-to-http}

リクエストは、カスタマーケアに届いた順に処理されます。

>[!NOTE]
>
>HTTP/2への切り替えにはキャッシュのクリアが伴うので、リードタイムが長くなる場合があります。 そのため、一度に処理できる顧客の移行は数件のみとなります。

## HTTP/2 への切り替えに伴うリスク  {#what-are-the-risks-with-moving-to-http}

HTTP/2 への切り替えには、新しい CDN 設定への移行が伴うので、CDN でキャッシュがクリアされます。

キャッシュが再作成されるまで、キャッシュされていないコンテンツはアドビの元のサーバーに直接アクセスして取得されます。したがって、Adobeは、接触チャネルからリクエストをプルする際に許容可能なパフォーマンスが維持されるように、一度に少数の顧客の移行を処理する予定です。

## URL または Web サイトが HTTP/2 でアクティベートされていることを確認する方法  {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

ブラウザーにはこのことが表示されないので、拡張機能をダウンロードする必要があります。

FirefoxおよびChromeの場合、「HTTP/2 and SPDY Indicator」という拡張機能があります。 ブラウザーは HTTP/2 をセキュア接続でのみサポートするので、確認するには https の付いた URL を呼び出す必要があります。http/2がサポートされている場合、拡張子は青いFlash記号とヘッダー`X-Firefox-Spdy`で示されます。`h2`.
