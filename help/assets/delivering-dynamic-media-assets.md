---
title: Dynamic Media アセットを配信
description: ビデオ、画像などの Dynamic Media アセットを web ページに配信する方法について説明します。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: 274af114-845a-46bd-b091-802cf589687a
feature: Asset Management,Renditions
solution: Experience Manager, Experience Manager Assets
autotag-review: '2026-05-18T18:45:05.823Z'
TQID: 'https://experienceleague.adobe.com/a5ifneRAYCIMHKCGJHGQu9aoQt3EWZu1hiGYItlPZOE'
product_v2:
  - id: e14eb250-3c22-4a07-9061-a78112b2b826
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
source-git-commit: 9c96b6744c7af2f061b4dfbf403560047485f9b5
workflow-type: tm+mt
source-wordcount: 324
ht-degree: 92%

---

# Dynamic Media アセットの配信{#delivering-dynamic-media-assets}

ビデオでも画像でも、Dynamic Media アセットの配信方法は、Web サイトの実装方法によって異なります。

Dynamic Media を使用する場合、次の複数のオプションがあります。

* Web サイトが Adobe Experience Manager 上にホストされている場合は、Dynamic Media アセットを直接ページに追加します。
* Web サイトが Experience Manager 上にない場合は、次のいずれかの方法を選択します。

   * ビデオまたは画像を web サイトに埋め込みます。
   * Web アプリケーションにURLをリンクします。 ビデオプレーヤーをポップアップウィンドウまたはモーダルウィンドウとして配信する場合は、リンクを使用します。
   * レスポンシブサイトの場合は、[最適化された画像を配信](/help/assets/responsive-site.md)できます。

>[!NOTE]
>
>スマートイメージングは、既存の画像プリセットで機能し、配信の直前にインテリジェンスを使用して、ブラウザーまたはネットワークの接続速度に基づいて画像のファイルサイズをさらに低減します。 詳しくは、[スマートイメージング](/help/assets/imaging-faq.md)を参照してください。

詳しくは、次のトピックを参照してください。

* [Web ページへの Dynamic Media アセットの追加](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [ビデオまたは画像ビューアを web ページに埋め込む](/help/assets/embed-code.md)
* [Dynamic Media でホットリンク保護を有効化する](/help/assets/hotlink-protection.md)
* [Web アプリケーションに URL をリンクする](/help/assets/linking-urls-to-yourwebapplication.md)
* [レスポンシブサイト用に最適化された画像の配信](/help/assets/responsive-site.md)
* [コンテンツの HTTP/2 配信](/help/assets/http2.md)
* [Dynamic Media Classic を使用して CDN キャッシュを無効にします](/help/assets/invalidate-cdn-cache-dm-classic.md)
* [ルールセットを使用して URL を変換する](/help/assets/using-rulesets-to-transform-urls.md)


## Dynamic Media アセットの HTTP/2 配信 {#http-delivery-of-dynamic-media-assets}

Experience Manager では、HTTP/2 上でのすべての Dynamic Media コンテンツ（画像とビデオ）の配信をサポートするようになりました。 つまり、画像やビデオの公開済み URL または埋め込みコードを、ホストされているアセットを受け入れる任意のアプリケーションと統合できるようになります。 その公開済みアセットは、HTTP/2 プロトコルを使用して配信されます。 この配信方法を使用すると、ブラウザーとサーバーの通信方法が改善され、すべてのDynamic Mediaアセットの応答時間と読み込み時間が向上します。

詳しくは、[コンテンツの HTTP/2 配信に関するよくある質問](/help/sites-administering/scene7-http2faq.md)を参照してください。
