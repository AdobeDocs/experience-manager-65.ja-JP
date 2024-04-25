---
title: ソーシャルコンポーネントフレームワーク
description: ソーシャルコンポーネントフレームワーク（SCF）を使用すると、Communities コンポーネントの設定、カスタマイズ、拡張のプロセスが簡単になります
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 5ca58bc3-8505-4d91-9cd1-6b2e2671f1be
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1478'
ht-degree: 1%

---

# ソーシャルコンポーネントフレームワーク {#social-component-framework}

ソーシャルコンポーネントフレームワーク（SCF）を使用すると、サーバーサイドとクライアントサイドの両方で Communities コンポーネントを設定、カスタマイズ、拡張するプロセスが簡単になります。

このフレームワークのメリットは次のとおりです。

* **機能**:80% のユースケースに対して、カスタマイズをほとんど、またはまったく行わずに、すぐに統合できる。
* **Skinnable**:CSS スタイル設定のためのHTML属性の一貫した使用。
* **拡張可能**: コンポーネントの実装はオブジェクト指向で、ビジネスロジックが軽い – サーバーでビジネスログインを簡単に増分追加できます。
* **柔軟**：オーバーレイおよびカスタマイズが容易なシンプルなロジックレス JavaScript テンプレート。
* **Accessible**:HTTP API は、モバイルアプリを含む任意のクライアントからの投稿をサポートします。
* **ポータブル**：あらゆるテクノロジーで構築されたあらゆる web ページへの統合/埋め込み。

インタラクティブ機能を使用して、オーサーインスタンスまたはパブリッシュインスタンスを探索します [コミュニティコンポーネントガイド](components-guide.md).

## 概要 {#overview}

SCF では、コンポーネントは、SocialComponent POJO、Handlebars JS テンプレート（コンポーネントをレンダリングする）、および CSS （コンポーネントのスタイルを設定する）で構成されます。

Handlebars JS テンプレートは、モデル/ビュー JS コンポーネントを拡張して、クライアント上のコンポーネントとのユーザー操作を処理できます。

コンポーネントがデータの変更をサポートする必要がある場合、SocialComponent API の実装を書き込んで、従来の web アプリケーションのモデル/データオブジェクトに類似したデータの編集/保存をサポートできます。 さらに、操作（コントローラー）と操作サービスを追加して、操作リクエストの処理、ビジネスロジックの実行、モデル/データオブジェクトの API の呼び出しを行うこともできます。

SocialComponent API は、クライアントがビューレイヤーまたは HTTP クライアントに必要とするデータを提供するように拡張できます。

### クライアント向けのページのレンダリング方法 {#how-pages-are-rendered-for-client}

![scf-page-rendering](assets/scf-overview.png)

### コンポーネントのカスタマイズと拡張 {#component-customization-and-extension}

コンポーネントをカスタマイズまたは拡張するには、/apps ディレクトリにオーバーレイと拡張機能のみを書き込みます。これにより、今後のリリースへのアップグレードプロセスが簡単になります。

* スキニング用：
   * のみ [CSS を編集する必要があります](client-customize.md#skinning-css).
* ルックアンドフィールに関して：
   * JS テンプレートと CSS を変更します。
* ルック、フィール、UX に関して：
   * JS テンプレート、CSS および [javascript の拡張/上書き](client-customize.md#extending-javascript).
* JS テンプレートまたはGETエンドポイントで使用可能な情報を変更するには：
   * を拡張する [SocialComponent](server-customize.md#socialcomponent-interface).
* 操作中にカスタム処理を追加するには：
   * 書き込み [OperationExtension](server-customize.md#operationextension-class).
* カスタム操作を追加するには：
   * を作成 [Sling Post 操作](server-customize.md#postoperation-class).
   * 既存のものを使用 [OperationServices](server-customize.md#operationservice-class) 必要に応じて。
   * 必要に応じて、クライアント側から操作を呼び出す JavaScript コードを追加します。

## サーバーサイドフレームワーク {#server-side-framework}

フレームワークは、サーバー上の機能にアクセスし、クライアントとサーバー間のインタラクションをサポートするための API を提供します。

### Java™ API {#java-apis}

Java™ API は、容易に継承またはサブクラス化できる抽象クラスおよびインターフェイスを提供します。

メインクラスは以下で説明します [サーバーサイドのカスタマイズ](server-customize.md) ページ。

訪問 [ストレージリソースプロバイダーの概要](srp.md) ugc の操作について説明します。

### HTTP API {#http-api}

HTTP API は、PhoneGap アプリ、ネイティブアプリ、その他の統合およびマッシュアップ用のクライアントプラットフォームのカスタマイズと選択を容易にサポートします。 さらに、HTTP API を使用すると、クライアントレスでコミュニティサイトをサービスとして実行できるので、フレームワークコンポーネントを、あらゆるテクノロジーで作成された任意の web ページに統合できます。

### HTTP API - GETリクエスト {#http-api-get-requests}

フレームワークは、すべての SocialComponent に対して、HTTP ベースの API エンドポイントを提供します。 エンドポイントにアクセスするには、「.social.json」セレクター+拡張子を持つGETリクエストをリソースに送信します。 Sling を使用すると、リクエストはに渡されます。 `DefaultSocialGetServlet`.

**`DefaultSocialGetServlet`**

1. リソース（resourceType）をに渡します `SocialComponentFactoryManager` を選択できる SocialComponentFactory を受け取ります `SocialComponent` リソースを表します。

1. ファクトリを呼び出して、 `SocialComponent` リソースとリクエストを処理できます。
1. を呼び出します `SocialComponent`。リクエストを処理し、結果の JSON 表現を返します。
1. クライアントに対する JSON 応答を返します。

**`GET Request`**

デフォルトのGETサーブレットは、SocialComponent がカスタマイズ可能な JSON を使用して応答する.social.json リクエストをリッスンします。

![scf-framework](assets/scf-framework.png)

### HTTP API -POSTリクエスト {#http-api-post-requests}

GET（読み取り）操作に加えて、コンポーネントに対して他の操作（作成、更新、削除など）を有効にするエンドポイントパターンも定義されます。 これらのエンドポイントは、入力を受け入れ、HTTP ステータスコードまたは JSON 応答オブジェクトで応答する HTTP API です。

このフレームワークエンドポイントパターンにより、CUD 操作が拡張可能、再利用可能、テスト可能になります。

**`POST Request`**

すべての SocialComponent 操作に Sling POST:operation があります。 各操作のビジネスロジックとメンテナンスコードは、OperationService にラップされます。このサービスは、HTTP API を介して、または他の場所から OSGi サービスとしてアクセスできます。 前後のアクションに対して、プラグ可能な操作拡張をサポートするフックが提供されます。

![scf-post-request](assets/scf-post-request.png)

### ストレージリソースプロバイダー（SRP） {#storage-resource-provider-srp}

に保存された UGC の処理について [コミュニティコンテンツストア](working-with-srp.md)を参照してください。

* [ストレージリソースプロバイダーの概要](srp.md)  – 概要とリポジトリ使用状況の概要。
* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP API ユーティリティのメソッドと例。
* [SRP による UGC へのアクセス](accessing-ugc-with-srp.md) - コーディングガイドライン

### サーバーサイドのカスタマイズ {#server-side-customizations}

訪問 [サーバーサイドのカスタマイズ](server-customize.md) サーバーサイドでの Communities コンポーネントのビジネスロジックと動作のカスタマイズについて説明します。

## Handlebars JS テンプレート言語 {#handlebars-js-templating-language}

新しいフレームワークで顕著な変更の 1 つは、 `Handlebars JS` （HBS）テンプレート言語。サーバークライアントレンダリング用の一般的なオープンソーステクノロジーです。

HBS スクリプトはシンプルで、ロジックレスで、サーバーとクライアントの両方でコンパイルされ、オーバーレイとカスタマイズが簡単です。HBS はクライアントサイドレンダリングをサポートしているので、当然クライアント UX とバインドされます。

フレームワークには次の機能があります [Handlebars ヘルパー](handlebars-helpers.md) これは、SocialComponents を開発する際に役立ちます。

サーバーで Sling がGETリクエストを解決すると、リクエストの応答に使用されるスクリプトが特定されます。 スクリプトが HBS テンプレート（.hbs）の場合、Sling はリクエストを Handlebars エンジンに委任します。 次に、Handlebars エンジンは、適切な SocialComponentFactory から SocialComponent を取得し、コンテキストを作成して、HTMLをレンダリングします。

### アクセス制限なし {#no-access-restriction}

Handlebars （HBS）テンプレートファイル（.hbs）は、.jsp および.html テンプレートファイルに似ていますが、クライアントブラウザーとサーバーの両方でレンダリングに使用できる点が異なります。 そのため、クライアント側テンプレートを要求するクライアントブラウザーは、サーバーから.hbs ファイルを受け取ります。

これには、Sling 検索パス内のすべての HBS テンプレート（/libs/または/apps の下のすべての.hbs ファイル）を、オーサーまたはパブリッシュから任意のユーザーが取得できる必要があります。

.hbs ファイルへの HTTP アクセスは禁止されない場合があります。

### コミュニティコンポーネントを追加または含める {#add-or-include-a-communities-component}

ほとんどの Communities コンポーネントは、 *追加済み* sling アドレス可能リソースとして。 Communities コンポーネントの一部は次のとおりです *included* ユーザー生成コンテンツ（UGC）を書き込む場所を動的に含めたりカスタマイズしたりできるようにする、既存でないリソースとしてテンプレートに追加する。

どちらの場合も、コンポーネントは [必要なクライアントライブラリ](clientlibs.md) も存在する必要があります。

**コンポーネントを追加**

コンポーネントの追加とは、リソース（コンポーネント）のインスタンスを追加するプロセスを指します。例えば、オーサー編集モードでコンポーネントブラウザー（サイドキック）からページにドラッグした場合などです。

結果は、par ノードの下の JCR 子ノードになります。このノードは、Sling でアドレス可能です。

**コンポーネントを含める**

コンポーネントを含めると、への参照を追加するプロセスになります。 [「存在しない」リソース](srp.md#for-non-existing-resources-ners) （JCR ノードなし）スクリプティング言語の使用など、テンプレート内で使用できます。

Adobe Experience Manager（AEM） 6.1 の時点では、コンポーネントが追加されるのではなく、動的に含まれる場合、オーサー環境でそのコンポーネントのプロパティを編集することができます *デザイン* モード。

一部のAEM Communities コンポーネントのみ動的に含めることができます。 次のとおりです。

* [コメント](essentials-comments.md)
* [レーティング](rating-basics.md)
* [レビュー](reviews-basics.md)
* [投票](essentials-voting.md)

この [コミュニティコンポーネントガイド](components-guide.md) 含めるコンポーネントを追加から含めるに切り替えることができます。

**Handlebars の使用時** テンプレート言語。既存のリソース以外は、 [ヘルパーを含める](handlebars-helpers.md#include) resourceType を指定する場合：

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**JSP を使用する場合**&#x200B;の場合、タグを使用してリソースがインクルードされます [cq:include](../../help/sites-developing/taglib.md#lt-cq-include):

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>コンポーネントをテンプレートに追加したりテンプレートに含めたりせずに、ページに動的に追加するには、を参照してください。 [コンポーネントのサイドローディング](sideloading.md).

### Handlebars ヘルパー {#handlebars-helpers}

参照： [SCF Handlebars ヘルパー](handlebars-helpers.md) SCF で使用できるカスタムヘルパーのリストと説明については、を参照してください。

## クライアントサイドフレームワーク {#client-side-framework}

### モデルビュー JavaScript フレームワーク {#model-view-javascript-framework}

フレームワークには、の拡張機能が含まれています [Backbone.js](https://backbonejs.org/)は、リッチなインタラクティブなコンポーネントの開発を容易にするモデルビュー JavaScript フレームワークです。 オブジェクト指向の特性により、拡張可能で再利用可能なフレームワークがサポートされます。 HTTP API を使用すると、クライアントとサーバー間の通信が簡略化されます。

このフレームワークは、サーバー側の Handlebars テンプレートを使用して、クライアント用のコンポーネントをレンダリングします。 モデルは、HTTP API で生成された JSON 応答に基づいています。 ビューは、Handlebars テンプレートで生成されたHTMLにバインドされ、インタラクティブ機能を提供します。

### CSS 規則 {#css-conventions}

CSS クラスを定義および使用する場合は、次の規則を使用することをお勧めします。

* 名前空間が明確に指定された CSS クラスセレクター名を使用し、「heading」や「image」などの汎用名は避けます。
* CSS スタイルシートがページ上の他の要素やスタイルとうまく連携するように、特定のクラスセレクタースタイルを定義します。 例：`.social-forum .topic-list .li { color: blue; }`
* スタイル設定のための CSS クラスを、JavaScript による UX 用の CSS クラスとは別に保持します。

### クライアントサイドのカスタマイズ {#client-side-customizations}

クライアントサイドでの Communities コンポーネントの外観と動作のカスタマイズについては、を参照してください。 [クライアントサイドのカスタマイズ](client-customize.md)。これには、次に関する情報が含まれます。

* [オーバーレイ](client-customize.md#overlays)
* [拡張子](client-customize.md#extensions)
* [HTMLのマークアップ](client-customize.md#htmlmarkup)
* [CSS のスキニング](client-customize.md#skinning-css)
* [JavaScript の拡張](client-customize.md#extending-javascript)
* [SCF の clientlibs](client-customize.md#clientlibs-for-scf)

## 機能とコンポーネントの基本事項 {#feature-and-component-essentials}

開発者向けの基本的な情報については、を参照してください。 [機能とコンポーネントの基本事項](essentials.md) セクション。

追加の開発者情報については、を参照してください。 [コーディングのガイドライン](code-guide.md) セクション。

## トラブルシューティング {#troubleshooting}

よくある問題と既知の問題については、を参照してください。 [トラブルシューティング](troubleshooting.md) セクション。
