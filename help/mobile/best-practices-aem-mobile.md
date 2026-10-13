---
title: AEM Mobile On-demand Servicesのベストプラクティス
description: モバイルアプリテンプレートとコンポーネントを構築するサイトを対象とした、Adobe Experience Manager（AEM）の有能な開発者を支援するベストプラクティスとガイドラインについて説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 63ceaba6-b796-4c13-a86d-f0609ec679c9
solution: Experience Manager
feature: Mobile
role: User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%
---
# ベストプラクティス {#best-practices}

{{ue-over-mobile}}

AEM Mobile On-demand Services アプリの構築は、Cordova （またはPhoneGap）シェルで直接実行されるアプリの構築とは異なります。 開発者は、次のことについて把握している必要があります。

* すぐに使えるプラグインと、Adobe Experience Manager（AEM）モバイル固有のプラグインを提供しています。

>[!NOTE]
>
>プラグインについて詳しくは、次のリソースを参照してください。
>
>* [AEM MobileでのCordova プラグインの使用](https://helpx.adobe.com/digital-publishing-solution/help/cordova-api.html)
>* [AEM Mobile固有のCordova対応プラグインの使用](https://helpx.adobe.com/digital-publishing-solution/help/app-runtime-api.html)
>

* プラグイン機能を使用するテンプレートは、プラグインブリッジが存在しない場合でもブラウザーでオーサリング可能な方法で記述する必要があります。

  * 例えば、プラグインのAPIにアクセスする前に、*deviceready*&#x200B;関数を待つようにしてください。

## AEM開発者向けガイドライン {#guidelines-for-aem-developers}

次のガイドラインは、モバイルアプリテンプレートとコンポーネントを構築するサイトを対象とした、AEMの適切な開発者に役立ちます。

**再利用と拡張性を促進するためにAEM Sites テンプレートを構成する**

* 単一のモノリシック形式よりも複数のコンポーネントスクリプトファイルを優先する

  * *customheaderlibs.html*&#x200B;や&#x200B;*customfooterlibs.html*&#x200B;など、空の拡張ポイントがいくつか用意されています。これにより、開発者はコアコードをできるだけ複製せずにページテンプレートを変更できます
  * テンプレートは、Slingの&#x200B;*sling:resourceSuperType* メカニズムを使用して拡張およびカスタマイズできます

* テンプレート言語として、JSPよりもSightly/HTLを優先する

  * これを使用すると、マークアップからのコードの分離が促進され、組み込みのXSS保護が提供され、より使い慣れた構文を使用できます

**オンデバイスパフォーマンスの最適化**

* アーティクル固有のスクリプトとスタイルシートは、dps-article contentsync テンプレートを使用して、アーティクルペイロードに含める必要があります
* 複数の記事で共有されているスクリプトとスタイルシートは、dps-HTMLResources contentsync テンプレートを使用して、共有リソースに含める必要があります
* レンダリングブロッキングされている外部スクリプトは参照しないでください

>[!NOTE]
>
>レンダーブロック外部スクリプト [について詳しくは、こちらを参照してください](https://developers.google.com/speed/docs/insights/BlockingJS)。

**web固有のJSおよびCSS ライブラリよりも、アプリ固有のクライアントサイド JSおよびCSS ライブラリを優先**

* jQuery Mobileのようなライブラリで膨大なデバイスやブラウザーを処理するオーバーヘッドを避ける
* テンプレートがアプリのweb ビューで実行されている場合、アプリがサポートするプラットフォームとバージョン、およびJavaScript サポートが存在するという情報を制御できます。 たとえば、jQuery MobileよりもIonic （CSSのみ）を、BootstrapよりもOnsen UIを好みます。

>[!NOTE]
>
>jQuery mobileについて詳しくは、[こちら](https://jquerymobile.com/browser-support/1.4/)をクリックしてください。

**フルスタックよりもマイクロライブラリを優先**

* コンテンツをデバイスのガラスに取り込むのに要する時間は、記事が依存するすべてのライブラリによって遅くなります。 この遅さは、新しいweb ビューを使用してすべての記事をレンダリングする場合に悪化するため、各ライブラリをゼロから再初期化する必要があります
* 記事がSPA （シングルページアプリ）として構築されていない場合は、Angularのようなフルスタックライブラリを含める必要はないでしょう
* ページに必要なインタラクティブ機能（[Fastclick](https://github.com/ftlabs/fastclick)や[Velocity.js](https://velocityjs.org)など）の追加に役立つ、小さな単一目的のライブラリを好みます

**記事ペイロードのサイズを最小化**

* サポートする最大のビューポートを効果的にカバーできる最小のアセットを、合理的な解像度で使用します
* 画像に&#x200B;*ImageOptim*&#x200B;のようなツールを使用して、余分なメタデータを削除できるようにします

## 一歩先を行く {#getting-ahead}

その他の2つの役割と責任について詳しくは、以下のリソースを参照してください。

* [管理者](/help/mobile/aem-mobile.md)
* [作成者](/help/mobile/aem-mobile-on-demand.md)
