---
title: AEM Mobile On-demand Servicesのベストプラクティス
description: モバイルアプリのテンプレートやコンポーネントを作成するサイトの有能なAdobe Experience Manager（AEM）開発者に役立つ、ベストプラクティスとガイドラインについて説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# ベストプラクティス {#best-practices}

{{ue-over-mobile}}

AEM Mobile On-demand Services アプリの構築は、Cordova （または PhoneGap）シェルで直接実行されるアプリの構築とは異なります。 開発者は、次の点に精通している必要があります。

* 標準でサポートされているプラグインと、Adobe Experience Manager（AEM）モバイル専用のプラグイン。

>[!NOTE]
>
>プラグインについて詳しくは、次のリソースを参照してください。
>
>* [AEM Mobileでの Cordova プラグインの使用 ](https://helpx.adobe.com/jp/digital-publishing-solution/help/cordova-api.html)
>* [AEM Mobile固有の Cordova 対応プラグインの使用 ](https://helpx.adobe.com/jp/digital-publishing-solution/help/app-runtime-api.html)
>

* プラグイン機能を使用するテンプレートは、プラグインブリッジが存在することなく、ブラウザーで引き続きオーサリングできるように記述する必要があります。

   * 例えば、プラグインの API にアクセスする前に、必ず *deviceready* 関数を待ってください。

## AEM開発者向けガイドライン {#guidelines-for-aem-developers}

次のガイドラインは、モバイルアプリのテンプレートとコンポーネントを作成するサイトの有能なAEM開発者に役立ちます。

**再利用と拡張性を促進するためのAEM Sites テンプレートの構造化**

* 単一のモノリシックなスクリプトファイルよりも複数のコンポーネントスクリプトファイルを優先します

   * *customheaderlibs.html* や *customfooterlibs.html* など、いくつかの空の拡張ポイントが提供されており、開発者はできるだけ少ないコアコードを複製しながらページテンプレートを変更できます
   * テンプレートは、Sling の *sling:resourceSuperType* メカニズムを使用して拡張およびカスタマイズできます

* テンプレート言語として JSP よりも Sightly/HTL を優先します

   * これを使用すると、コードをマークアップから分離し、組み込みの XSS 保護を提供し、より使い慣れた構文を使用できます

**オンデバイスでのパフォーマンス用に最適化**

* dps-article contentsync テンプレートを使用して、記事固有のスクリプトとスタイルシートを記事のペイロードに含める必要があります
* 複数の記事で共有されるスクリプトシートとスタイルシートは、dps-HTMLResources contentsync テンプレートを使用して共有リソースに含める必要があります
* レンダリングをブロックする外部スクリプトを参照しないでください

>[!NOTE]
>
>レンダリングをブロックする外部スクリプトについて詳しくは、[ こちら ](https://developers.google.com/speed/docs/insights/BlockingJS) を参照してください。

**web 固有のものよりアプリ固有のクライアントサイド JS および CSS ライブラリを優先します**

* jQuery Mobile のようなライブラリでオーバーヘッドを回避して、幅広いデバイスとブラウザーを処理できるようにします
* アプリの web ビューでテンプレートが実行されている場合、アプリがサポートするプラットフォームとバージョンを制御でき、JavaScriptがサポートする知識を利用できます。 例えば、jQuery Mobile より Ionic （CSS のみ）を優先し、Bootstrapより Onsen UI を優先します。

>[!NOTE]
>
>jQuery モバイルについて詳しくは、[ こちら ](https://jquerymobile.com/browser-support/1.4/) をクリックしてください。

**フルスタックよりマイクロライブラリを優先**

* コンテンツをデバイスに送信するのにかかる時間は、記事が依存するライブラリごとに短縮されます。 この速度低下は、新しい web ビューを使用してすべての記事をレンダリングする場合に悪化するため、各ライブラリを最初から再度初期化する必要があります
* 記事がSPA（シングルページアプリ）としてビルドされていない場合は、Angularのようなフルスタックライブラリを含める必要はありません
* [Fastclick](https://github.com/ftlabs/fastclick) や [Velocity.js など、ページで必要なインタラクティビティを追加するのに役立つ、より小さい単目的ライブラリをお勧め ](https://velocityjs.org) ます。

**記事ペイロードのサイズを最小限に抑える**

* 妥当な解像度で、サポートする最大のビューポートを効果的にカバーできる最小限のアセットを使用します
* 画像に *ImageOptim* などのツールを使用して、余分なメタデータを削除します

## 前に進む {#getting-ahead}

他の 2 つの役割と責務について詳しくは、以下のリソースを参照してください。

* [管理者](/help/mobile/aem-mobile.md)
* [作成者](/help/mobile/aem-mobile-on-demand.md)
