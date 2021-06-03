---
title: コンテンツの HTTP/2 配信の FAQ
description: HTTP/2 コンテンツ配信について説明します。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 2428914c-5fb0-439e-a1ef-8ee30b890f58
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 89%

---

# コンテンツの HTTP/2 配信の FAQ{#http-delivery-of-content-faq}

コンテンツの HTTP/2 配信が可能になったことをお知らせします。HTTP/2 を使用すると、パフォーマンスが全体的に向上します。

## HTTP/2 とは {#what-is-http}

HTTP/2 によりブラウザーとサーバーの通信が改善され、必要な処理能力を抑えながら情報をより高速に転送できます。

HTTP/2 とその利点については、次の Web サイトで簡潔に説明されています。

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## コンテンツ配信を HTTP/2 に移行する主なメリット {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

パフォーマンスがどれくらい向上するかは、Web サイトのコード、Dynamic Media の使用方法、消費者のデバイス、画面と場所などに応じて異なります。

アドビ独自のテストでは、以下の結果が出ています。

* 画像の場合、デバイスおよびブラウザーに応じて、応答時間が 7％～28％向上しました。パフォーマンスの向上は、iOS デバイスにおいて最も顕著でした。
* ビューアの場合、読み込み時間のパフォーマンスが 15％向上しました。

以下のデモは、HTTP/1 と HTTP/2 の読み込みの差異を示しています。

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## HTTP/2 に切り替えるには  {#am-i-eligible-to-switch-over-to-http}

HTTP/2 を使用するには、以下の要件を満たしている必要があります。

* リッチメディアリクエストにセキュア HTTPS を使用している。
* アドビ製品にバンドルされたコンテンツ配信ネットワーク（CDN）を Dynamic Media ライセンスの一部として使用している。
* 汎用の Dynamic Media ドメイン（`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com` のいずれか）ではなく、専用ドメイン（`images.company.com` または `mycompany.scene7.com`）を使用している。

   ドメインを見つけるには、[Dynamic Media Classicデスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=ja#getting-started)を開き、会社のアカウントにログインします。 次に、**[!UICONTROL 設定/アプリケーション設定/一般設定]**&#x200B;をタップします。 「**公開先サーバー名**」というラベルの付いたフィールドを見つけます。現在、汎用の Dynamic Media ドメインを使用している場合は、この切り替えの一環として独自のカスタムドメインへの移行をリクエストできます。

## Dynamic Media アカウントに対して HTTP/2 を有効にする方法 {#what-is-the-process-for-enabling-http-for-my-scene-account}

1. [Admin Console を使用してサポートケースを作成](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)し、HTTP/2 に切り替えるように要求する必要があります。自動的には切り替わりません。
1. サポートケースには、次の情報を記入してください。

   * 主要連絡先名、電子メールおよび電話番号。
   * HTTP/2 への切り替えが必要なすべてのドメイン。つまり、`images.company.com` または `mycompany.scene7.com`。

      ドメインを見つけるには、[Dynamic Media Classicデスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、会社のアカウントにログインします。 次に、**[!UICONTROL 設定]** / **[!UICONTROL アプリケーション設定]** / **[!UICONTROL 一般設定]**&#x200B;をタップします。 「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。

   * リッチメディアリクエストについて、セキュリティで保護された HTTPS を使用していることを確認します。
   * 直接的関係で管理するのではなく、アドビを介して CDN を使用していることを確認します。
   * 専用ドメインを使用していることを確認します。つまり、`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com` などの汎用の Dynamic Media ドメインではなく、`images.company.com` または `mycompany.scene7.com` です。

      ドメインを見つけるには、[Dynamic Media Classicデスクトップアプリケーション](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)を開き、会社のアカウントにログインします。 次に、**[!UICONTROL 設定]** / **[!UICONTROL アプリケーション設定]** / **[!UICONTROL 一般設定]**&#x200B;をタップします。 「**[!UICONTROL 公開先サーバー名]**」というラベルの付いたフィールドを見つけます。現在、汎用の Dynamic Media ドメインを使用している場合は、この切り替えの一環として独自のカスタムドメインへの移行をリクエストできます。

1. テクニカルサポートによって、リクエストの送信順に基づいて HTTP/2 の顧客待機リストに追加されます。
1. アドビでリクエストを処理する準備が整うと、サポートから連絡があり、移行についての調整および完了予定日の設定がおこなわれます。
1. 完了後に通知があり、HTTP/2 への正常な切り替えを確認できます。

## HTTP/2 への切り替え見込み時期 {#when-can-i-expect-to-be-transitioned-over-to-http}

リクエストは、テクニカルサポートに届いた順に処理されます。

>[!NOTE]
>
>HTTP/2 への切り替えにはキャッシュのクリアが含まれるので、リードタイムが長くなる場合があります。そのため、一度に処理できる顧客の移行は数件のみとなります。

## HTTP/2 への切り替えに伴うリスク  {#what-are-the-risks-with-moving-to-http}

HTTP/2 への切り替えには、新しい CDN 設定への移行が伴うので、CDN でキャッシュがクリアされます。

キャッシュが再作成されるまで、キャッシュされていないコンテンツはアドビの元のサーバーに直接アクセスして取得されます。このため、元のサーバーからリクエストをプルするときに許容できるパフォーマンスが維持されるように、アドビでは一度に少数の顧客の移行を処理するよう計画します。

## URL または Web サイトが HTTP/2 でアクティベートされていることを確認する方法  {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Web ブラウザーで使用する拡張機能をダウンロードする必要があります。Firefox および Chrome の場合は、「**[!UICONTROL HTTP/2 and SPDY Indicator]**」という拡張機能があります。ブラウザーは HTTP/2 をセキュア接続でのみサポートするので、確認するには https の付いた URL を呼び出す必要があります。この拡張では、HTTP/2 がサポートされている場合、青い稲妻マークおよび「X-Firefox-Spdy: h2」というヘッダーによって示されます。
