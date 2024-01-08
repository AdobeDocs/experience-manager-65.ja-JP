---
title: AEM Mobile On-demand Servicesのベストプラクティス
description: モバイルアプリのテンプレートとコンポーネントを作成するサイト向けの、有能なAdobe Experience Manager(AEM) 開発者に役立つベストプラクティスとガイドラインについて説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
source-git-commit: 99808cb38c5d376ccb7fb550c5212138890cec11
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 1%

---

# ベストプラクティス {#best-practices}

>[!NOTE]
>
>Adobeは、単一ページアプリケーションのフレームワークベースのクライアントサイドレンダリング（React など）を必要とするプロジェクトでは、SPA Editor を使用することをお勧めします。 [詳細情報](/help/sites-developing/spa-overview.md)。

AEM Mobile On-demand Servicesアプリの構築は、Cordova（または PhoneGap）シェルで直接実行するアプリの構築とは異なります。 開発者は、以下に関する知識が必要です。

* 標準でサポートされるプラグインとAdobe Experience Manager(AEM)Mobile 固有のプラグイン。

>[!NOTE]
>
>プラグインの詳細については、次のリソースを参照してください。
>
>* [AEM Mobileでの Cordova プラグインの使用](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [AEM Mobile固有の Cordova 対応プラグインの使用](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)
>

* プラグイン機能を使用するテンプレートは、プラグインブリッジが存在しなくても、ブラウザーで引き続きオーサリング可能な形で記述する必要があります。

   * 例えば、 *deviceready* 関数を使用して、プラグインの API にアクセスしようとします。

## AEM Developers 向けガイドライン {#guidelines-for-aem-developers}

次のガイドラインは、モバイルアプリのテンプレートとコンポーネントを作成するサイト向けに、有能なAEM開発者に役立ちます。

**再利用と拡張性を促進するAEMサイトテンプレートを構築する**

* 1 つのモノリシックスクリプトよりも複数のコンポーネントスクリプトファイルを優先

   * 次のような空の拡張ポイントが複数提供されます。 *customheaderlibs.html* および *customfooterlibs.html*&#x200B;できるだけコアコードをほとんど複製せずに、開発者がページテンプレートを変更できるようにします。
   * その後、Sling の *sling:resourceSuperType* 機構

* テンプレート言語として JSP よりも Sightly/HTL を優先

   * この方法を使用すると、マークアップからコードを分離し、組み込みの XSS 保護を提供し、より使い慣れた構文を持つようになります

**デバイス上でのパフォーマンスを最適化**

* dps-article contentsync テンプレートを使用して、記事固有のスクリプトおよびスタイルシートを記事のペイロードに含める必要があります。
* 複数の記事で共有されるスクリプトおよびスタイルシートは、 dps-HTMLResources コンテンツ同期テンプレートを使用して、共有リソースに含める必要があります
* レンダリングブロックの外部スクリプトを参照しない

>[!NOTE]
>
>レンダリングをブロックする外部スクリプトについて詳しくは、こちらを参照してください [ここ](https://developers.google.com/speed/docs/insights/BlockingJS).

**Web 固有のライブラリよりも、アプリ固有のクライアント側 JS および CSS ライブラリの方が好ましい**

* jQuery Mobile などのライブラリで大量のデバイスやブラウザーを処理する際のオーバーヘッドを回避する
* テンプレートをアプリの Web ビューで実行する場合、アプリがサポートするプラットフォームとバージョンを制御し、JavaScript サポートが存在することを把握できます。 例えば、jQuery Mobile よりも Ion（CSS のみ）、Bootstrapよりも Onsen UI の方が望ましいです。

>[!NOTE]
>
>jQuery モバイルについて詳しくは、以下を参照してください： [ここ](https://jquerymobile.com/browser-support/1.4/).

**フルスタックよりもマイクロライブラリの方が望ましい**

* 記事が依存するすべてのライブラリによって、コンテンツをデバイスのグラスに取り込むのにかかる時間が遅くなります。 新しい Web ビューを使用してすべての記事をレンダリングすると、この低速化が伴うので、各ライブラリを最初から再び初期化する必要があります
* 記事がSPA （シングルページアプリ）としてビルドされていない場合、Angularのようなフルスタックライブラリを含める必要がない可能性があります
* ページに必要なインタラクティビティを追加するのに役立つ、より小さく、単一目的のライブラリを好む。例： [Fastclick](https://github.com/ftlabs/fastclick) または [Velocity.js](https://velocityjs.org)

**記事のペイロードのサイズを最小化**

* サポートする最大のビューポートを効果的にカバーできる最小のアセットを、適切な解像度で使用します。
* 次のようなツールを使用 *ImageOptim* 画像上で、余分なメタデータを削除できます。

## 先に進む {#getting-ahead}

その他の 2 つの役割と責務について詳しくは、以下のリソースを参照してください。

* [管理者](/help/mobile/aem-mobile.md)
* [オーサー](/help/mobile/aem-mobile-on-demand.md)
