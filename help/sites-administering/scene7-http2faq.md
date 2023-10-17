---
title: コンテンツの HTTP/2 配信の FAQ
description: HTTP/2 コンテンツ配信の概要と、HTTP/2 コンテンツ配信で Web コンテンツの全体的なパフォーマンスを向上させる方法について説明します。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 2428914c-5fb0-439e-a1ef-8ee30b890f58
source-git-commit: 06a6d4e0ba2aeaefcfb238233dd98e8bbd6731da
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 83%

---

# コンテンツの HTTP/2 配信の FAQ{#http-delivery-of-content-faq}

コンテンツの HTTP/2 配信が可能になったことをお知らせします。HTTP/2 を使用すると、全体的なパフォーマンスの向上に気が付きます。

## HTTP/2 とは  {#what-is-http}

HTTP/2 によりブラウザーとサーバーの通信が改善され、必要な処理能力を抑えながら情報をより高速に転送できます。

次の Web サイトでは、HTTP/2 とその利点について簡単かつ簡単に説明します。

[HTTP/2 について知っておく必要がある事項です](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html)。

## コンテンツ配信を HTTP/2 に移行する主なメリット  {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

パフォーマンスがどれくらい向上するかは、web サイトのコード、Dynamic Media の使用方法、消費者のデバイス、画面と場所などによって異なります。

アドビ独自のテストでは、以下の結果が出ています。

* 画像の場合、デバイスおよびブラウザーに応じて、応答時間が 7％～28％向上しました。パフォーマンスの最も顕著な向上は、iOSデバイスでした。
* ビューアの場合、読み込み時のパフォーマンスが 15%向上しました。

次のデモは、HTTP/1 と HTTP/2 の読み込みの違いを示しています。

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## HTTP/2 に切り替える資格はありますか？ {#am-i-eligible-to-switch-over-to-http}

HTTP/2 を使用するには、次の要件を満たす必要があります。

* リッチメディアリクエストにセキュア HTTPS を使用している。
* アドビ製品にバンドルされたコンテンツ配信ネットワーク（CDN）を Dynamic Media ライセンスの一部として使用します。
* 汎用の Dynamic Media ドメイン（`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com` のいずれか）ではなく、専用ドメイン（`images.company.com` または `mycompany.scene7.com`）を使用します。

  ドメインを探すには、[Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)を開き、企業アカウントにログインします。**[!UICONTROL 設定]**／**[!UICONTROL アプリケーション設定]**／**[!UICONTROL 一般設定]**&#x200B;に移動します。「**公開先サーバー名**」というラベルの付いたフィールドを見つけます。現在、汎用の Dynamic Media ドメインを使用している場合は、この切り替えの一環として独自のカスタムドメインへの移行をリクエストできます。

## Dynamic Media アカウントに対して HTTP/2 を有効にする方法  {#what-is-the-process-for-enabling-http-for-my-scene-account}

1. [Admin Console を使用してサポートケースを作成](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)し、HTTP/2 に切り替えるように要求します。自動的には切り替わりません。
1. サポートケースには、次の情報を記入してください。

   * 主要連絡先名、メールおよび電話番号。
   * HTTP/2 への切り替えが必要なすべてのドメイン。つまり、`images.company.com` または `mycompany.scene7.com`。

     ドメインを探すには、[Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)を開き、企業アカウントにログインします。**[!UICONTROL 設定]**／**[!UICONTROL アプリケーション設定]**／**[!UICONTROL 一般設定]**&#x200B;に移動します。「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。

   * リッチメディアリクエストにセキュアな HTTPS を使用していることを確認します。
   * 直接の関係で管理されていない、Adobeを通じて CDN を使用していることを確認します。
   * 専用ドメインを使用していることを確認します。つまり、`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com` などの汎用の Dynamic Media ドメインではなく、`images.company.com` または `mycompany.scene7.com` です。

     ドメインを探すには、[Dynamic Media Classic デスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)を開き、企業アカウントにログインします。**[!UICONTROL 設定]**／**[!UICONTROL アプリケーション設定]**／**[!UICONTROL 一般設定]**&#x200B;に移動します。「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。現在、汎用の Dynamic Media ドメインを使用している場合は、この切り替えの一環として独自のカスタムドメインへの移行をリクエストできます。

1. アドビカスタマーサポートによって、リクエストの送信順に基づいて HTTP/2 の顧客待機リストに追加されます。
1. アドビでリクエストを処理する準備が整うと、移行についての調整や完了予定日の設定のため、カスタマーサポートから連絡が入ります。
1. 完了後に通知があり、HTTP/2 への正常な切り替えを確認できます。

## HTTP/2 への切り替えをいつ期待できますか？ {#when-can-i-expect-to-be-transitioned-over-to-http}

リクエストは、カスタマーサポートに届いた順に処理されます。

>[!NOTE]
>
>HTTP/2 への移行ではキャッシュをクリアするので、リードタイムが長くなる場合があります。そのため、一度に処理できる顧客の移行は数件のみとなります。

## HTTP/2 への切り替えに伴うリスク {#what-are-the-risks-with-moving-to-http}

HTTP/2 への切り替えには、新しい CDN 設定への移行が伴うので、CDN でキャッシュがクリアされます。

キャッシュされていないコンテンツは、キャッシュが再構築されるまで、Adobeの元のサーバーに直接ヒットします。 そのため、起点サーバーからの要求のプル時に許容範囲のパフォーマンスを確保できるよう、アドビでは、一度に処理するお客様の移行件数を数件にとどめるつもりです。

## URL または web サイトが HTTP/2 でアクティベートされていることを確認する方法 {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Web ブラウザーで使用できる拡張機能をダウンロードします。Firefox および Chrome の場合は、「**[!UICONTROL HTTP/2 and SPDY Indicator]**」という拡張機能があります。ブラウザーは HTTP/2 をセキュア接続でのみサポートするので、確認するには https の付いた URL を呼び出す必要があります。この拡張では、HTTP/2 がサポートされている場合、青い稲妻マークおよび「X-Firefox-Spdy: h2」というヘッダーによって示されます。
