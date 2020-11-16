---
title: ベストプラクティス
seo-title: ベストプラクティス
description: このページでは、サイト開発を担当する経験豊富な AEM 開発者がモバイルアプリテンプレートやコンポーネントを作成する際に役立つベストプラクティスおよびガイドラインについて説明します。
seo-description: このページでは、サイト開発を担当する経験豊富な AEM 開発者がモバイルアプリテンプレートやコンポーネントを作成する際に役立つベストプラクティスおよびガイドラインについて説明します。
uuid: 7733c8b1-a88c-455c-8080-f7add4205b92
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a0647696-72c3-409b-85ba-9275d8f99cff
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 67%

---


# ベストプラクティス {#best-practices}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

AEM Mobile On-demand Servicesアプリの作成は、Cordova（またはPhoneGap）シェルで直接実行するアプリの作成とは異なります。 開発者は、以下の事項に精通している必要があります。

* 標準でサポートされているプラグイン、および AEM Mobile 固有のプラグイン。

>[!NOTE]
>
>プラグインについて詳しくは、以下のリソースを参照してください。
>
>* [AEM Mobile での Cordova プラグインの使用](https://helpx.adobe.com/jp/digital-publishing-solution/help/cordova-api.html)
>* [AEM Mobile 固有の Cordova 対応プラグインの使用](https://helpx.adobe.com/jp/digital-publishing-solution/help/app-runtime-api.html)

>



* プラグイン機能を使用するテンプレートは、プラグインのブリッジなしでもブラウザーでオーサリング可能なように記述する必要があります。

   * For example, make sure to wait for the *deviceready* function before attempting to access a plugin&#39;s API.

## AEM 開発者向けガイドライン {#guidelines-for-aem-developers}

次のガイドラインは、モバイルアプリのテンプレートとコンポーネントを作成するサイト開発経験があるAEM開発者の役に立ちます。

**再利用性と拡張性を向上させるために AEM Sites テンプレートを構造化する**

* 1つのモノリシックファイルよりも複数のコンポーネントスクリプトファイルを優先

   * A number of empty extension points are provided, such as *customheaderlibs.html* and *customfooterlibs.html*, which allow the developer to change the page template while duplicating as little core code as possible
   * Templates can then be extended and customized via Sling&#39;s *sling:resourceSuperType* mechanism

* 使用するテンプレート言語は、JSP よりも Sightly/HTL の方が望ましい

   * この方法を使用すると、XSS保護で構築されたオファーやマークアップからコードを分離することが推奨され、構文がより使い慣れています

**デバイス上でのパフォーマンスを最適化する**

* 記事固有のスクリプトやスタイルシートは、dps-article contentsyncテンプレートを使用して、記事のペイロードに含める必要があります
* 複数の記事で共有されるスクリプトやスタイルシートは、dps-HTMLResources contentsyncテンプレートを使用して、共有リソースに含める必要があります
* レンダリングを妨げる外部スクリプトを参照してはなりません。

>[!NOTE]
>
>レンダリングを妨げる外部スクリプトについて詳しくは、[こちら](https://developers.google.com/speed/docs/insights/BlockingJS)を参照してください。

**Web 向けの汎用的な JS および CSS ライブラリよりも、アプリ固有のクライアント側 JS および CSS ライブラリの方が望ましい**

* jQuery Mobile などのライブラリで多数のデバイスやブラウザーを処理する際のオーバーヘッドを回避するためです。
* テンプレートがアプリの Web ビュー内で実行されるときに、そのアプリがサポートするプラットフォームとバージョンを自身で管理でき、JavaScript がサポートされることをあらかじめ把握できます。例えば、jQuery MobileやOnsen UIよりもイオン性（おそらくCSSのみ）を、Bootstrapよりも優先します。

>[!NOTE]
>
>jQuery Mobile について詳しくは、[こちら](https://jquerymobile.com/browser-support/1.4/)を参照してください。

**フルスタックライブラリよりもマイクロライブラリの方が望ましい**

* 記事が依存するライブラリが増えるほど、デバイスの画面上にコンテンツが表示されるまでの時間が長くなります。記事ごとに新しい Web ビューを使用してレンダリングすると、毎回ライブラリが初期化されてしまうので、さらに時間が長くなります。
* 記事が SPA（シングルページアプリ）として作成されていない場合は、Angular などのフルスタックライブラリを組み込む必要がない可能性があります。
* ページに必要なインタラクティブ機能を追加するには、[Fastclick](https://github.com/ftlabs/fastclick) や [Velocity.js](https://velocityjs.org) などの、より小規模で特定の目的に特化したライブラリを使用することが望ましいといえます。

**記事のペイロードのサイズを最小限に抑える**

* サポートする最大のビューポートを効果的にカバーできる最小のアセットを適切な解像度で使用します。
* *ImageOptim* などのツールを画像に使用して、余分なメタデータを削除します。

## さらに先のステップ {#getting-ahead}

他の 2 つの役割および責任について詳しくは、以下のリソースを参照してください。

* [管理者](/help/mobile/aem-mobile.md)
* [作成者](/help/mobile/aem-mobile-on-demand.md)
