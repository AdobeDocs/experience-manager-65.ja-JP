---
title: AEM Livefyre のレシピ
seo-title: AEM Livefyre のレシピ
description: Adobe Experience Manager Livefyre の一般的なユースケースについての手順の説明。
seo-description: Adobe Experience Manager Livefyre の一般的なユースケースについての手順の説明。
uuid: 78695a63-fca6-4990-9755-0aeaae4a7f64
contentOwner: alba
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fdea5ede-d44f-463e-af8a-111ee7469ede
translation-type: tm+mt
source-git-commit: 072898f18d418eac8e9d9e94453db34d62dd3ed9
workflow-type: tm+mt
source-wordcount: '1559'
ht-degree: 73%

---


# AEM Livefyre のレシピ{#aem-livefyre-recipes}

Adobe Experience Manager Livefyre の一般的なユースケースについての手順の説明。

## 標準 Livefyre AEM コンポーネントを使用して UGC をキュレーションし、Livefyre Media Wall を使用して表示する {#curate-ugc-using-the-out-of-the-box-livefyre-aem-components-and-display-using-livefyre-media-wall}

Media Wall は、ソーシャルおよびネイティブの Livefyre コンテンツをリアルタイムのソーシャルウォールにストリーミングします。AEM に Media Wall を実装する方法は、ユースケースと要件に応じて複数あります。

AEM Livefyre パッケージでは初期設定済みの実装が提供されますが、従来の統合ではカスタム Livefyre AEM コンポーネントを作成する機能が提供されます。

### AEM の統合 {#aem-integration}

Livefyre Adobe Experience Manager パッケージは、AEM 6.1、6.2Sp1、6.3、6.4、6.4 SP1 で使用できます。AEM 5.x および 6.0 ではサポートされていません。詳しい手順については、[Livefyreとの統合](https://helpx.adobe.com/jp/experience-manager/6-4/sites/administering/using/livefyre.html)を参照してください。

サポートされているLivefyreアプリケーションを確認するには、[AEM Support Matrix for Livefyre Apps](https://helpx.adobe.com/jp/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps)を参照してください。

### 従来の実装(カスタマイズされたAEMコンポーネント用) {#traditional-implementation-for-customized-aem-components}

Livefyre をカスタム AEM コンポーネントまたは WordPress、Sitecore、DemandWare などの他の CMS に実装する方法は 3 つあります。従来の Livefyre 統合は CMS に依存しません。

**方法 1：Designer アプリの実装**

* **説明：** Livefyre アプリを統合するための最も簡単で最速の方法。数分で Media Wall App をページに統合するためのカスタマイズされた JavaScript 埋め込みコードを設計、構成、および生成できます。
* **方法：Media Wallアプリの**  [作成、プレビュー、公開、埋め込み](https://docs.adobe.com/content/help/en/livefyre/using/apps/c-create-an-app.html)

* **例：**[https://codepen.io/dharafyre/pen/bvGrLo](https://codepen.io/dharafyre/pen/bvGrLo)

**方法 2：SDK の実装**

* **説明：**[Livefyre.js](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) はサイトのアプリと認証を強化するコアライブラリです。これはグローバル *window.Livefyre* オブジェクトと単一のパブリックメソッド *Livefyre.require* を定義します。これらは、Livefyre アプリの組み込みやサードパーティのユーザー認証プラットフォームとの統合に役立つ、その他の Livefyre JavaScript ライブラリをロードするために使用されます。

* **方法**：[Livefyre JavaScript SDK の streamhub-wallpackage の使用](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/c-media-wall-integration.html)

* **例**：[https://codepen.io/dharafyre/pen/KZKBNv?editors=1010](https://codepen.io/dharafyre/pen/KZKBNv?editors=1010)

SDK を使用した高度なカスタマイズについては、[StreamHub SDK](https://github.com/Livefyre/streamhub-sdk) を参照してください。

**方法 3：API の実装**

* カスタマイズされたエクスペリエンスとデータの視覚化を作成するために、[ブートストラップとストリーム API](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html) を使用して Livefyre とソーシャルデータを利用することで、一から Livefyre Apps を作成できます。

UGC用UIを作成する際は、[Twitter](https://developer.twitter.com/en/developer-terms/display-requirements.html)、[Facebook](https://ja.facebookbrand.com/#brand-guidelines-assets)、[Instagram](https://en.instagram-brand.com/)の表示ガイドラインに従っていることを確認してください。

### Media Wall 認証の統合 {#media-wall-authentication-integration}

認証を必要とする Media Wall の統合については、以下を参照してください。

* [AEMIdentity Management用のシングルサインオン](https://helpx.adobe.com/jp/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) 統合のカスタマイズ
* サードパーティ製認証プラットフォーム用 [ID 統合](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html)

### ユースケースの概要  {#use-case-overview}

AEM の顧客として、標準 Livefyre AEM コンポーネントを使用して UGC をキュレートし、Livefyre Media Wall を使用して表示したい。

実装手順：

1. [概要](https://helpx.adobe.com/jp/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Livefyre を使用するための AEM の設定](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [AEM Media Wall コンポーネントをページにドラッグアンドドロップ](https://helpx.adobe.com/jp/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMSites)
1. [UGC をキュレートして Media Wall コンポーネントに表示するための、ストリームの設定とルールの追加](https://docs.adobe.com/content/help/en/livefyre/using/streams/c-streams.html)

UGCのストリーミングに関するトレーニングビデオについては、[Livefyreでの自動コンテンツストリームの作成とソーシャルコンテンツの検索](https://helpx.adobe.com/jp/experience-manager/tutorials.html)を参照してください。

### お客様の例 {#customer-examples}

* [CNN Media Wall](https://edition.cnn.com/specials/nepal-earthquake-media-wall)
* [PGA Tour Media Wall](https://www.pgatour.com/social-hub.html)

カスタマイズされたエクスペリエンスとデータの視覚化を作成するために、[ブートストラップとストリーム API](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html) を使用して Livefyre とソーシャルデータを利用することで、一から Livefyre Apps を作成できます。

認証が必要なLivefyreアプリについては、サードパーティの認証プラットフォームの[IDの統合](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html)を参照してください。

* [PGAツアーメディアウォール](https://www.pgatour.com/social-hub.html)
* [TimeOut](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)

## AEM Components または従来の Livefyre 統合を使用して Livefyre コメントを統合する  {#integrate-livefyre-comments-using-aem-components-or-traditional-livefyre-integration}

### AEM の統合 {#aem-integration-1}

Livefyre Adobe Experience Manager パッケージは、AEM 6.1、6.2Sp1、6.3、6.4、6.4 SP1 で使用できます。AEM 5.x および 6.0 ではサポートされていません。詳しい手順については、[Livefyreとの統合](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html)を参照してください。

### 従来の実装(カスタマイズされたAEMコンポーネント用) {#traditional-implementation-for-customized-aem-components-1}

Livefyre コメントアプリケーションをカスタム AEM コンポーネントまたは WordPress、Sitecore、DemandWare などの他の CMS に実装する方法は 3 つあります。従来の Livefyre 統合は CMS に依存しません。

**方法 1：Designer アプリの実装**

* **説明：** Livefyre アプリを統合するための最も簡単で最速の方法。数分で Media Wall App をページに統合するためのカスタマイズされた JavaScript 埋め込みコードを設計、構成、および生成できます。
* **方法：コメントアプリの** [作成、プレビュー、投稿、埋め込み](https://docs.adobe.com/content/help/en/livefyre/using/apps/c-create-an-app.html)

* **例：**[https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

**方法 2：SDK の実装**

* **説明：**[Livefyre.js](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) はサイトのアプリと認証を強化するコアライブラリです。これはグローバル *window.Livefyre* オブジェクトと単一のパブリックメソッド *Livefyre.require* を定義します。これらは、Livefyre アプリの組み込みやサードパーティのユーザー認証プラットフォームとの統合に役立つ、その他の Livefyre JavaScript ライブラリをロードするために使用されます。

* **方法：**

   * [CollectionMeta トークン](https://docs.adobe.com/content/help/en/livefyre/implementation/getting-started/implementation-process/c-collectionmeta-tokent.html)を使ったコレクション／アプリの作成。
   * Livefyre.js 埋め込みコード構造を使った[コメントアプリ](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/comments/c-comments-integration.html)のサイトへの統合。

* **例：**[https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

SDKを使用した高度なカスタマイズについては、[StreamHub SDKs](https://github.com/Livefyre/streamhub-sdk)を参照してください。

**方法 3：API の実装**

* カスタマイズされたエクスペリエンスとデータの視覚化を作成するために、[ブートストラップとストリーム API](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html) を使用して Livefyre とソーシャルデータを利用することで、一から Livefyre Apps を作成できます。

### コメントアプリ認証の統合  {#comments-app-authentication-integration}

* [AEMIdentity Management用のシングルサインオン](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) 統合のカスタマイズ
* サードパーティ製認証プラットフォーム用 [ID 統合](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html)

### お客様の例 {#customer-examples-1}

* [ポイズ語（キンバリークラーク）](https://www.poise.com/en-us/advice-and-support/blog-and-podcast/blog/5-holiday-party-tips-for-managing-lbl)

## Livefyre AEM Assets 統合を使用して AEM Assets に UGC を読み込む {#use-livefyre-aem-assets-integration-to-import-ugc-in-aem-assets}

**Livefyre セットアップ（UGC キュレーションおよび Rights Management 用）：**

1. [Livefyre Asset Library フォルダーに UGC をキュレートするためのストリームの設定とルールの追加](https://docs.adobe.com/content/help/en/livefyre/using/streams/c-streams.html)。

   1. UGCのストリーミングに関するトレーニングビデオについては、[Livefyreでの自動コンテンツストリームの作成とソーシャルコンテンツの検索](https://helpx.adobe.com/experience-manager/tutorials.html)を参照してください。

1. [Livefyre Asset Library フォルダー内のキュレーション済み UGC の収集、整理、管理](https://docs.adobe.com/content/help/en/livefyre/using/library/assets/c-assets.html)。

   1. Livefyre Studioアセットライブラリでのフォルダーの作成と管理に関するトレーニングビデオについては、[Adobe Experience ManagerLivefyreでのアセットの操作](https://helpx.adobe.com/experience-manager/tutorials.html)を参照してください。

1. [Livefyre Studio を使用してキュレーションされた UGC の権限のリクエスト](https://docs.adobe.com/content/help/en/livefyre/using/rights-requests/c-how-requesting-rights-works.html)。

**AEM セットアップ（AEM Assets に UGC を読み込むため）**

1. [概要](https://helpx.adobe.com/jp/experience-manager/6-3/sites/administering/using/livefyre.html#GettingStarted)
1. [Livefyre を使用するための AEM の設定](https://helpx.adobe.com/jp/experience-manager/6-3/sites/administering/using/livefyre.html#ConfigureAEMtouseLivefyre)
1. [Livefyre によってキュレーションされた UGC の AEM Assets への読み込み](https://helpx.adobe.com/jp/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMAssets)

* [Tourism Australia](https://www.australia.com/en-us)

## AEM Components または従来の Livefyre 統合を使用して Livefyre レビューを統合する  {#integrate-livefyre-reviews-using-aem-components-or-traditional-livefyre-integration}

### AEM の統合 {#aem-integration-2}

Livefyre Adobe Experience Manager パッケージは、AEM 6.1、6.2Sp1、6.3、6.4、6.4 SP1 で使用できます。AEM 5.x および 6.0 ではサポートされていません。詳しい手順については、[Livefyreとの統合](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html)を参照してください。

レビューコンポーネントは、AEM 6.1 ではサポートされていないコンポーネントです。[Livefyre アプリの AEM サポート一覧](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps)を確認してください。

### 従来の実装（カスタマイズされた AEM コンポーネント用）  {#traditional-implementation-for-customized-aem-components-2}

Livefyre レビューアプリをカスタム AEM コンポーネントまたは WordPress、Sitecore、DemandWare などの他の CMS に実装する方法は 2 つあります。従来の Livefyre 統合は CMS に依存しません。

**メソッド 1：SDK の実装**

* **説明：**[Livefyre.js](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) はサイトのアプリと認証を強化するコアライブラリです。これはグローバル *window.Livefyre* オブジェクトと単一のパブリックメソッド *Livefyre.require* を定義します。これらは、Livefyre アプリの組み込みやサードパーティのユーザー認証プラットフォームとの統合に役立つ、その他の Livefyre JavaScript ライブラリをロードするために使用されます。

* **方法：**

   * レビューコレクション内に格納するメタデータを指定するためのレビュー [CollectionMeta トークン](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/c-reviews-integration.html)の作成。
   * *Livefyre.js* 埋め込みコード構造を使用した Sites への[レビューアプリ](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/c-reviews-integration.html)の統合

* **例：**[https://codepen.io/dharafyre/pen/GXgvvd](https://codepen.io/dharafyre/pen/GXgvvd)

SDKを使用した高度なカスタマイズについては、[StreamHub SDKs](https://github.com/Livefyre/streamhub-sdk)を参照してください。

**メソッド 2：API の実装**

* カスタマイズされたエクスペリエンスとデータの視覚化を作成するために、ブートストラップとストリーム API を使用して Livefyre とソーシャルデータを利用することで、一から Livefyre Apps を作成できます。

その他の評価およびレビューAPIについては、[こちら](https://api.livefyre.com/docs/apis/by-category/ratings-and-reviews)を参照してください。

### コメントアプリ認証の統合 {#comments-app-authentication-integration-1}

* [AEMIdentity Management用のシングルサインオン](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) 統合のカスタマイズ
* サードパーティ製認証プラットフォーム用 [ID 統合](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html)

### お客様の例 {#customer-examples-2}

* [TimeOut](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)
* [myrecipes](https://www.myrecipes.com/recipe/shrimp-florentine-pasta)

