---
title: 'AEM Livefyre のレシピ '
seo-title: AEM Livefyre Recipes
description: Adobe Experience Manager Livefyre の一般的なユースケースについての手順の説明。
seo-description: Step-by-step instructions on common use cases for Adobe Experience Manager Livefyre.
uuid: 78695a63-fca6-4990-9755-0aeaae4a7f64
contentOwner: alba
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fdea5ede-d44f-463e-af8a-111ee7469ede
exl-id: 7ccd67a7-9945-48c1-9986-f4eaf0f2b961
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1545'
ht-degree: 100%

---

# AEM Livefyre のレシピ {#aem-livefyre-recipes}

Adobe Experience Manager Livefyre の一般的なユースケースについての手順の説明。

## 標準 Livefyre AEM コンポーネントを使用して UGC をキュレーションし、Livefyre Media Wall を使用して表示する {#curate-ugc-using-the-out-of-the-box-livefyre-aem-components-and-display-using-livefyre-media-wall}

Media Wall は、ソーシャルおよびネイティブの Livefyre コンテンツをリアルタイムのソーシャルウォールにストリーミングします。AEM に Media Wall を実装する方法は、ユースケースと要件に応じて複数あります。

AEM Livefyre パッケージでは初期設定済みの実装が提供されますが、従来の統合ではカスタム Livefyre AEM コンポーネントを作成する機能が提供されます。

### AEM の統合 {#aem-integration}

Livefyre Adobe Experience Manager パッケージは、AEM 6.1、6.2 SP1、6.3、6.4、6.4 SP1 で使用できます。AEM 5.x および 6.0 ではサポートされていません。手順について詳しくは、[Livefyre との統合](https://helpx.adobe.com/jp/experience-manager/6-4/sites/administering/using/livefyre.html)を参照してください。

どの Livefyre アプリがサポートされているかを確認するには、[Livefyre アプリの AEM サポート一覧](https://helpx.adobe.com/jp/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps)を参照してください。

### 従来の実装（カスタマイズされた AEM コンポーネント用） {#traditional-implementation-for-customized-aem-components}

Livefyre をカスタム AEM コンポーネントまたは WordPress、Sitecore、DemandWare などの他の CMS に実装する方法は 3 つあります。従来の Livefyre 統合は CMS に依存しません。

**方法 1：Designer アプリの実装**

* **説明：** Livefyre アプリを統合するための最も簡単で最速の方法。数分で Media Wall App をページに統合するためのカスタマイズされた JavaScript 埋め込みコードを設計、構成、および生成できます。
* **方法：** [Media Wall アプリの作成、プレビュー、公開、埋め込み](https://docs.adobe.com/content/help/ja/livefyre/using/home.html)

* **例：**[https://codepen.io/dharafyre/pen/bvGrLo](https://codepen.io/dharafyre/pen/bvGrLo)

**方法 2：SDK の実装**

* **説明：**[Livefyre.js](https://docs.adobe.com/content/help/ja/livefyre/implementation/c-livefyre_js.html) はサイトのアプリと認証を強化するコアライブラリです。これはグローバル *window.Livefyre* オブジェクトと単一のパブリックメソッド *Livefyre.require* を定義します。これらは、Livefyre アプリの組み込みやサードパーティのユーザー認証プラットフォームとの統合に役立つ、その他の Livefyre JavaScript ライブラリをロードするために使用されます。

* **方法**：[Livefyre JavaScript SDK の streamhub-wallpackage の使用](https://docs.adobe.com/content/help/ja/livefyre/implementation/app-integrations/c-media-wall-integration.html)

* **例**：[https://codepen.io/dharafyre/pen/KZKBNv?editors=1010](https://codepen.io/dharafyre/pen/KZKBNv?editors=1010)

SDK を使用した高度なカスタマイズについては、[StreamHub SDK](https://github.com/Livefyre/streamhub-sdk) を参照してください。

**方法 3：API の実装**

* カスタマイズされたエクスペリエンスおよびデータビジュアライゼーションを作成するには、[Bootstrap and Stream API](https://docs.adobe.com/content/help/ja/livefyre/implementation/advanced-topics/bootstrap-stream-api.html) を使用して Livefyre とソーシャルデータを利用することで、いちから Livefyre アプリを作成できます。

UGC の UI を構築する際は、[Twitter](https://developer.twitter.com/en/developer-terms/display-requirements.html)、[Facebook](https://ja.facebookbrand.com/#brand-guidelines-assets)、[Instagram](https://en.instagram-brand.com/) のディスプレイガイドラインに従うようにしてください。

### Media Wall 認証の統合 {#media-wall-authentication-integration}

認証を必要とする Media Wall の統合については、以下を参照してください。

* AEM Identity Management 用の[シングルサインオン統合のカスタマイズ](https://helpx.adobe.com/jp/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration)
* サードパーティ製認証プラットフォーム用 [ID 統合](https://docs.adobe.com/content/help/ja/livefyre/implementation/identity-integration/t-about-identity-integration.html)

### ユースケースの概要 {#use-case-overview}

AEM の顧客として、標準 Livefyre AEM コンポーネントを使用して UGC をキュレートし、Livefyre Media Wall を使用して表示したい。

実装手順：

1. [はじめに](https://helpx.adobe.com/jp/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Livefyre を使用するために AEM を設定](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [AEM Media Wall コンポーネントをページにドラッグ＆ドロップ](https://helpx.adobe.com/jp/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMSites)
1. [UGC をキュレーションして Media Wall コンポーネントに表示するために、ストリームを設定してルールを追加](https://docs.adobe.com/content/help/ja/livefyre/using/home.html)

ストリーミング UGC のトレーニングビデオについては、[Adobe Experience Manager Livefyre での自動コンテンツストリームの作成とソーシャルコンテンツの検索](https://helpx.adobe.com/jp/experience-manager/tutorials.html)を参照してください。

### お客様の例 {#customer-examples}

* [CNN の Media Wall](https://edition.cnn.com/specials/nepal-earthquake-media-wall)
* [PGA Tour の Media Wall](https://www.pgatour.com/social-hub.html)

カスタマイズされたエクスペリエンスおよびデータビジュアライゼーションを作成するには、[Bootstrap and Stream API](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html) を使用して Livefyre とソーシャルデータを利用することで、いちから Livefyre アプリを作成できます。

認証が必要な Livefyre アプリについては、サードパーティ製認証プラットフォーム用 [ID 統合](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html)を参照してください。

* [PGA Tour の Media Wall](https://www.pgatour.com/social-hub.html)
* [TimeOut](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)

## AEM Components または従来の Livefyre 統合を使用して Livefyre コメントを統合する {#integrate-livefyre-comments-using-aem-components-or-traditional-livefyre-integration}

### AEM の統合 {#aem-integration-1}

Livefyre Adobe Experience Manager パッケージは、AEM 6.1、6.2 SP1、6.3、6.4、6.4 SP1 で使用できます。AEM 5.x および 6.0 ではサポートされていません。手順について詳しくは、[Livefyre との統合](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html)を参照してください。

### 従来の実装（カスタマイズされた AEM コンポーネント用） {#traditional-implementation-for-customized-aem-components-1}

Livefyre コメントアプリケーションをカスタム AEM コンポーネントまたは WordPress、Sitecore、DemandWare などの他の CMS に実装する方法は 3 つあります。従来の Livefyre 統合は CMS に依存しません。

**方法 1：Designer アプリの実装**

* **説明：** Livefyre アプリを統合するための最も簡単で最速の方法。数分で Media Wall App をページに統合するためのカスタマイズされた JavaScript 埋め込みコードを設計、構成、および生成できます。
* **方法：** [コメントアプリの作成、プレビュー、公開、埋め込み](https://docs.adobe.com/content/help/en/livefyre/using/apps/c-create-an-app.html)

* **例：**[https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

**方法 2：SDK の実装**

* **説明：**[Livefyre.js](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) はサイトのアプリと認証を強化するコアライブラリです。これはグローバル *window.Livefyre* オブジェクトと単一のパブリックメソッド *Livefyre.require* を定義します。これらは、Livefyre アプリの組み込みやサードパーティのユーザー認証プラットフォームとの統合に役立つ、その他の Livefyre JavaScript ライブラリをロードするために使用されます。

* **方法：**

   * [CollectionMeta トークン](https://docs.adobe.com/content/help/ja/livefyre/implementation/getting-started/implementation-process/c-collectionmeta-tokent.html)を使用したコレクション／アプリの作成。
   * Livefyre.js 埋め込みコード構造を使用したサイトへの[コメントアプリ](https://docs.adobe.com/content/help/ja/livefyre/implementation/app-integrations/comments/c-comments-integration.html)の統合。

* **例：**[https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

SDK を使用した高度なカスタマイズについては、[StreamHub SDK](https://github.com/Livefyre/streamhub-sdk) を参照してください。

**方法 3：API の実装**

* カスタマイズされたエクスペリエンスおよびデータビジュアライゼーションを作成するには、[Bootstrap and Stream API](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html) を使用して Livefyre とソーシャルデータを利用することで、いちから Livefyre アプリを作成できます。

### コメントアプリ認証の統合 {#comments-app-authentication-integration}

* AEM Identity Management 用の[シングルサインオン統合のカスタマイズ](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration)
* サードパーティ製認証プラットフォーム用 [ID 統合](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html)

### お客様の例 {#customer-examples-1}

* [Poise（Kimberly Klark）](https://www.poise.com/en-us/advice-and-support/blog-and-podcast/blog/5-holiday-party-tips-for-managing-lbl)

## Livefyre AEM Assets 統合を使用して AEM Assets に UGC を読み込む {#use-livefyre-aem-assets-integration-to-import-ugc-in-aem-assets}

**Livefyre セットアップ（UGC キュレーションおよび Rights Management 用）：**

1. [Livefyre Asset Library フォルダーに UGC をキュレーションするために、ストリームを設定してルールを追加](https://docs.adobe.com/content/help/en/livefyre/using/streams/c-streams.html)します。

   1. ストリーミング UGC のトレーニングビデオについては、[Adobe Experience Manager Livefyre での自動コンテンツストリームの作成とソーシャルコンテンツの検索](https://helpx.adobe.com/experience-manager/tutorials.html)を参照してください。

1. [Livefyre Asset Library フォルダーにキュレーション済み UGC を収集、整理、管理](https://docs.adobe.com/content/help/ja/livefyre/using/library/assets/c-assets.html)します。

   1. Livefyre Studio Asset Library でのフォルダーの作成および管理に関するトレーニングビデオについては、[Adobe Experience Manager Livefyre でのアセットの操作](https://helpx.adobe.com/experience-manager/tutorials.html)を参照してください。

1. [Livefyre Studio を使用してキュレーションされた UGC の権限のリクエスト](https://docs.adobe.com/content/help/ja/livefyre/using/home.html)。

**AEM セットアップ（AEM Assets に UGC を読み込むため）**

1. [はじめに](https://helpx.adobe.com/jp/experience-manager/6-3/sites/administering/using/livefyre.html#GettingStarted)
1. [Livefyre を使用するために AEM を設定](https://helpx.adobe.com/jp/experience-manager/6-3/sites/administering/using/livefyre.html#ConfigureAEMtouseLivefyre)
1. [Livefyre によってキュレーションされた UGC の AEM Assets への読み込み](https://helpx.adobe.com/jp/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMAssets)

* [Tourism Australia](https://www.australia.com/en-us)

## AEM Components または従来の Livefyre 統合を使用して Livefyre レビューを統合する {#integrate-livefyre-reviews-using-aem-components-or-traditional-livefyre-integration}

### AEM の統合 {#aem-integration-2}

Livefyre Adobe Experience Manager パッケージは、AEM 6.1、6.2 SP1、6.3、6.4、6.4 SP1 で使用できます。AEM 5.x および 6.0 ではサポートされていません。手順について詳しくは、[Livefyre との統合](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html)を参照してください。

レビューコンポーネントは、AEM 6.1 ではサポートされていないコンポーネントです。[Livefyre アプリの AEM サポート一覧](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps)を確認してください。

### 従来の実装（カスタマイズされた AEM コンポーネント用） {#traditional-implementation-for-customized-aem-components-2}

Livefyre レビューアプリをカスタム AEM コンポーネントまたは WordPress、Sitecore、DemandWare などの他の CMS に実装する方法は 2 つあります。従来の Livefyre 統合は CMS に依存しません。

**方法 1：SDK の実装**

* **説明：**[Livefyre.js](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) はサイトのアプリと認証を強化するコアライブラリです。これはグローバル *window.Livefyre* オブジェクトと単一のパブリックメソッド *Livefyre.require* を定義します。これらは、Livefyre アプリの組み込みやサードパーティのユーザー認証プラットフォームとの統合に役立つ、その他の Livefyre JavaScript ライブラリをロードするために使用されます。

* **方法：**

   * レビュー [CollectionMeta トークン](https://docs.adobe.com/content/help/ja/livefyre/implementation/app-integrations/c-reviews-integration.html)を作成して、レビューコレクション内に保存するメタデータを指定します。
   * *Livefyre.js* 埋め込みコード構造を使用したサイトへの[レビューアプリ](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/c-reviews-integration.html)の統合

* **例：**[https://codepen.io/dharafyre/pen/GXgvvd](https://codepen.io/dharafyre/pen/GXgvvd)

SDK を使用した高度なカスタマイズについては、[StreamHub SDK](https://github.com/Livefyre/streamhub-sdk) を参照してください。

**方法 2：API の実装**

* カスタマイズされたエクスペリエンスおよびデータビジュアライゼーションを作成するには、Bootstrap and Stream API を使用して Livefyre とソーシャルデータを利用することで、いちから Livefyre アプリを作成できます。

追加の評価とレビュー API については、[こちら](https://api.livefyre.com/docs/apis/by-category/ratings-and-reviews)を参照してください。

### コメントアプリ認証の統合 {#comments-app-authentication-integration-1}

* AEM Identity Management 用の[シングルサインオン統合のカスタマイズ](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration)
* サードパーティ製認証プラットフォーム用 [ID 統合](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html)

### お客様の例 {#customer-examples-2}

* [TimeOut](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)
* [myrecipes](https://www.myrecipes.com/recipe/shrimp-florentine-pasta)
