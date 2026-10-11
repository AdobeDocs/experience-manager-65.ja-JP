---
title: コンテンツの HTTP/2 配信
description: HTTP/2 によりブラウザーとサーバーの通信がどのように改善され、必要な処理能力を抑えながら情報をより高速に転送できるのかを説明します。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
exl-id: 9eb9f309-33e5-4694-84d2-fb2cd3de50a6
feature: Publishing,Configuration
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: da0dfbce-df02-4f8b-b32d-a4e3b1d05085
    internal-label: Configuration
  - id: f59890ff-de81-47d5-9ef8-7ab2dd10c6c3
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: f901afa4-5613-4581-add5-219fa5f03fb5
    internal-label: Publishing
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 97%
---
# コンテンツの HTTP/2 配信 {#http-delivery-of-content}

アドビは、パフォーマンスの向上という全体的な利点をもたらすコンテンツの HTTP/2 配信に対応しました。

>[!NOTE]
>
>この機能を使用するには、Adobe Experience Manager Dynamic Media にバンドルされている標準搭載の CDN を使用する必要があります。 この機能では、その他のカスタム CDN はサポートされません。

## HTTP/2 とは {#what-is-http}

HTTP/2 によりブラウザーとサーバーの通信が改善され、必要な処理能力を抑えながら情報をより高速に転送できます。

HTTP/2 とその利点については、次の web サイトで簡潔に説明されています。

[HTTP/2について知っておくべきこと](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html)

## コンテンツ配信を HTTP/2 に移行する主なメリット {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

パフォーマンスの向上の度合いは大きく異なる場合があります。 これは、web サイトのコード、Dynamic Media の使用方法、消費者のデバイス、画面、場所など、多くの要因に基づきます。

アドビ独自のテストでは、以下の結果が出ています。

* 画像の場合、デバイスおよびブラウザーに応じて、応答時間が 7％～28％向上しました。 最もパフォーマンスが向上したのは iOS デバイスでした。
* ビューアの場合、読み込み時間のパフォーマンスが 15％向上しました。

<!--
The following demonstration illustrates the difference between HTTP/1 versus HTTP/2 loading:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)
-->

## HTTP/2 に切り替えるには {#am-i-eligible-to-switch-over-to-http}

HTTP/2 を使用するには、以下の要件を満たしている必要があります。

* リッチメディアリクエストにセキュア HTTPS を使用している。
* アドビ製品にバンドルされたコンテンツ配信ネットワーク（CDN）を Dynamic Media ライセンスの一部として使用します。
* 専用ドメイン（company-h.assetsadobe#.com 以外）を使用します。

  既に専用ドメインがある場合、アドビのカスタマーサポート経由でオプトインできます。

  専用ドメインがない場合、アドビは 2018年に HTTP/2 への移行を予定しています。

## Dynamic Media アカウントに対して HTTP/2 を有効にする方法 {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

HTTP/2 への切り替えは、お客様からのリクエストが必要となり、自動的には行われません。

1. HTTP/2 に切り替えるには、アドビのカスタマーサポートにリクエストしてください。 詳しくは、[サポートチケットを開く](https://experienceleague.adobe.com/?support-solution=General&lang=ja&support-tab=home#support)を参照してください。

   1. サポートリクエストには、以下の情報を記入してください。

      1. 主要連絡先の氏名、メールアドレス、電話番号。
      1. HTTP/2 への切り替えが必要なすべてのドメイン。
      1. リッチメディアリクエストについて、セキュリティで保護された HTTPS を使用していることを確認します。
      1. アドビ経由で CDN を利用し、直接契約で管理されていないことを確認します。
      1. 専用ドメインを使用していることを確認します。 Dynamic Media を使用している場合は、専用ドメインを使用します。

   1. カスタマーサポートでは、リクエストの送信順に基づいて HTTP/2 の顧客待機リストに追加します。
   1. アドビでリクエストを処理する準備が整うと、移行についての調整や完了予定日の設定のため、カスタマーサポートから連絡が入ります。
   1. 完了すると通知されるので、正常に HTTP/2 へ移行されたことを確認できます。

      ブラウザーにはこのことが表示されないので、拡張機能をダウンロードする必要があります。

      Firefox および Chrome では、「HTTP/2 および SPDY インディケーター」という拡張機能があります。 ブラウザーは HTTP/2 をセキュア接続でのみサポートするので、確認するには https の付いた URL を呼び出す必要があります。 http/2がサポートされている場合、拡張機能はiを示します。 拡張機能は、青色の稲妻シンボルおよび `X-Firefox-Spdy` : `h2` というヘッダーの形式です。

## HTTP/2 への移行のタイミング {#when-can-i-expect-to-be-transitioned-over-to-http}

リクエストは、カスタマーサポートが受信した順に処理されます。

>[!NOTE]
>
>HTTP/2 への移行ではキャッシュをクリアするので、リードタイムが長期化する場合があります。 そのため、一度に処理できる顧客の移行は数件のみとなります。

## HTTP/2 への切り替えに伴うリスク {#what-are-the-risks-with-moving-to-http}

HTTP/2 への切り替えには、新しい CDN 設定への移行が伴うので、CDN でキャッシュがクリアされます。

キャッシュが再作成されるまで、キャッシュされていないコンテンツはアドビの元のサーバーに直接アクセスして取得されます。 このため、元のサーバーからリクエストをプルするときに許容できるパフォーマンスが維持されるように、アドビでは一度に少数の顧客の移行を処理するよう計画します。

## URL または Web サイトが HTTP/2 でアクティベートされていることを確認する方法 {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

ブラウザーにはこのことが表示されないので、拡張機能をダウンロードする必要があります。

Firefox および Chrome では、「HTTP/2 および SPDY インディケーター」という拡張機能があります。 ブラウザーは HTTP/2 をセキュア接続でのみサポートするので、確認するには https の付いた URL を呼び出す必要があります。 HTTP/2 がサポートされている場合は、拡張機能にそのことが示されます。 拡張機能は、青色の稲妻シンボルおよび `X-Firefox-Spdy` : `h2` というヘッダーの形式です。
