---
title: ベストプラクティス
seo-title: Best Practices
description: このページでは、サイト開発を担当する経験豊富な AEM 開発者がモバイルアプリテンプレートやコンポーネントを作成する際に役立つベストプラクティスおよびガイドラインについて説明します。
seo-description: Follow this page to  learn best practices and guidelines that will help experienced AEM developers for sites, who want to build mobile app templates and components.
uuid: 7733c8b1-a88c-455c-8080-f7add4205b92
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a0647696-72c3-409b-85ba-9275d8f99cff
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 65%

---

# ベストプラクティス {#best-practices}

>[!NOTE]
>
>アドビは、シングルページアプリケーションフレームワークをベースにしたクライアント側のレンダリング（React など）を必要とするプロジェクトには SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

AEM Mobile On-demand Servicesアプリの構築は、Cordova（または PhoneGap）シェルで直接実行するアプリの構築とは異なります。 開発者は、以下の事項に精通している必要があります。

* 標準でサポートされているプラグイン、および AEM Mobile 固有のプラグイン。

>[!NOTE]
>
>プラグインについて詳しくは、以下のリソースを参照してください。
>
>* [AEM Mobile での Cordova プラグインの使用](https://helpx.adobe.com/jp/digital-publishing-solution/help/cordova-api.html)
>* [AEM Mobile 固有の Cordova 対応プラグインの使用](https://helpx.adobe.com/jp/digital-publishing-solution/help/app-runtime-api.html)
>


* プラグイン機能を使用するテンプレートは、プラグインのブリッジなしでもブラウザーでオーサリング可能なように記述する必要があります。

   * 例えば、 *deviceready* 関数を使用して、プラグインの API にアクセスしようとします。

## AEM 開発者向けガイドライン {#guidelines-for-aem-developers}

次のガイドラインは、モバイルアプリのテンプレートとコンポーネントを作成する経験豊富なAEM開発者を支援します。

**再利用性と拡張性を向上させるために AEM Sites テンプレートを構造化する**

* 1 つのモノリシックスクリプトよりも複数のコンポーネントスクリプトファイルを優先

   * 次のような空の拡張ポイントが多数提供されます。 *customheaderlibs.html* および *customfooterlibs.html*&#x200B;できるだけコアコードをほとんど複製せずに、開発者がページテンプレートを変更できるようにします。
   * その後、Sling の *sling:resourceSuperType* 機構

* 使用するテンプレート言語は、JSP よりも Sightly/HTL の方が望ましい

   * この方法を使用すると、マークアップからコードを分離し、XSS 保護に組み込まれたオファーを提供し、より身近な構文を持つようになります

**デバイス上でのパフォーマンスを最適化する**

* 記事固有のスクリプトとスタイルシートは、dps-article contentsync テンプレートを使用して、記事のペイロードに含める必要があります
* 複数の記事で共有されるスクリプトやスタイルシートは、 dps-HTMLResources contentsync テンプレートを使用して、共有リソースに含める必要があります
* レンダリングを妨げる外部スクリプトを参照してはなりません。

>[!NOTE]
>
>レンダリングを妨げる外部スクリプトについて詳しくは、[こちら](https://developers.google.com/speed/docs/insights/BlockingJS)を参照してください。

**Web 向けの汎用的な JS および CSS ライブラリよりも、アプリ固有のクライアント側 JS および CSS ライブラリの方が望ましい**

* jQuery Mobile などのライブラリで多数のデバイスやブラウザーを処理する際のオーバーヘッドを回避するためです。
* テンプレートがアプリの Web ビュー内で実行されるときに、そのアプリがサポートするプラットフォームとバージョンを自身で管理でき、JavaScript がサポートされることをあらかじめ把握できます。例えば、jQuery Mobile よりも Ionic （おそらく CSS のみ）、Bootstrapよりも Onsen UI の方が望ましい。

>[!NOTE]
>
>jQuery Mobile について詳しくは、[こちら](https://jquerymobile.com/browser-support/1.4/)を参照してください。

**フルスタックライブラリよりもマイクロライブラリの方が望ましい**

* 記事が依存するライブラリが増えるほど、デバイスの画面上にコンテンツが表示されるまでの時間が長くなります。記事ごとに新しい Web ビューを使用してレンダリングすると、毎回ライブラリが初期化されてしまうので、さらに時間が長くなります。
* 記事が SPA（シングルページアプリ）として作成されていない場合は、Angular などのフルスタックライブラリを組み込む必要がない可能性があります。
* ページに必要なインタラクティブ機能を追加するには、[Fastclick](https://github.com/ftlabs/fastclick) や [Velocity.js](https://velocityjs.org) などの、より小規模で特定の目的に特化したライブラリを使用することが望ましいといえます。

**記事のペイロードのサイズを最小限に抑える**

* サポートする最大のビューポートを効果的にカバーできる最小のアセットを、適切な解像度で使用します。
* *ImageOptim* などのツールを画像に使用して、余分なメタデータを削除します。

## さらに先のステップ {#getting-ahead}

他の 2 つの役割および責任について詳しくは、以下のリソースを参照してください。

* [管理者](/help/mobile/aem-mobile.md)
* [作成者](/help/mobile/aem-mobile-on-demand.md)
