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

* **機能性**:80% のユースケースに対して、カスタマイズをほとんど、またはまったく行うことなく、すぐに統合できる標準搭載の機能。
* **Skinnable**:CSS スタイル設定のためのHTML属性の一貫した使用。
* **拡張可能**: コンポーネント実装はオブジェクト指向で、ビジネスロジックをシンプルにします。サーバーでビジネスログインを簡単に増分追加できます。
* **柔軟**：オーバーレイおよびカスタマイズが容易な、シンプルでロジックレスのJavaScript テンプレート。
* **アクセス可能**:HTTP API は、モバイルアプリを含む任意のクライアントからの投稿をサポートしています。
* **ポータブル**：任意のテクノロジーで作成された任意の web ページに統合または埋め込みます。

インタラクティブな [ コミュニティコンポーネントガイド ](components-guide.md) を使用して、オーサーインスタンスまたはパブリッシュインスタンスを探索します。

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
   * 編集が必要なのは [CSS](client-customize.md#skinning-css) のみです。
* ルックアンドフィールに関して：
   * JS テンプレートと CSS を変更します。
* ルック、フィール、UX に関して：
   * JS テンプレート、CSS および [JavaScriptの拡張/上書き ](client-customize.md#extending-javascript) を変更します。
* JS テンプレートまたはGETエンドポイントで使用可能な情報を変更するには：
   * [SocialComponent](server-customize.md#socialcomponent-interface) を拡張します
* 操作中にカスタム処理を追加するには：
   * [OperationExtension](server-customize.md#operationextension-class) を書き込みます。
* カスタム操作を追加するには：
   * [Sling Post操作 ](server-customize.md#postoperation-class) を作成します。
   * 必要に応じて、既存の [OperationServices](server-customize.md#operationservice-class) を使用します。
   * 必要に応じて、JavaScript コードを追加して、クライアント側から操作を呼び出します。

## サーバーサイドフレームワーク {#server-side-framework}

フレームワークは、サーバー上の機能にアクセスし、クライアントとサーバー間のインタラクションをサポートするための API を提供します。

### Java™ API {#java-apis}

Java™ API は、容易に継承またはサブクラス化できる抽象クラスおよびインターフェイスを提供します。

メインクラスについては、[ サーバーサイドのカスタマイズ ](server-customize.md) ページを参照してください。

UGC の操作については、[ ストレージリソースプロバイダーの概要 ](srp.md) を参照してください。

### HTTP API {#http-api}

HTTP API は、PhoneGap アプリ、ネイティブアプリ、その他の統合およびマッシュアップ用のクライアントプラットフォームのカスタマイズと選択を容易にサポートします。 さらに、HTTP API を使用すると、クライアントレスでコミュニティサイトをサービスとして実行できるので、フレームワークコンポーネントを、あらゆるテクノロジーで作成された任意の web ページに統合できます。

### HTTP API - GETリクエスト {#http-api-get-requests}

フレームワークは、すべての SocialComponent に対して、HTTP ベースの API エンドポイントを提供します。 エンドポイントにアクセスするには、「.social.json」セレクター+拡張子を持つGETリクエストをリソースに送信します。 Sling を使用すると、リクエストは `DefaultSocialGetServlet` に渡されます。

**`DefaultSocialGetServlet`**

1. リソース（resourceType）を `SocialComponentFactoryManager` に渡し、リソースを表す `SocialComponent` を選択できる SocialComponentFactory を受け取ります。

1. ファクトリを呼び出し、リソースとリクエストを処理できる `SocialComponent` を受け取ります。
1. `SocialComponent` を呼び出してリクエストを処理し、結果の JSON 表現を返します。
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

[ コミュニティコンテンツストア ](working-with-srp.md) に保存された UGC の処理について詳しくは、以下を参照してください。

* [ ストレージリソースプロバイダーの概要 ](srp.md) – 概要とリポジトリの使用状況の概要。
* [SRP と UGC の初期設定 ](srp-and-ugc.md) - SRP API ユーティリティメソッドと例。
* [SRP による UGC へのアクセス ](accessing-ugc-with-srp.md) - コーディングガイドライン。

### サーバーサイドのカスタマイズ {#server-side-customizations}

サーバーサイドでの Communities コンポーネントのビジネスロジックと動作のカスタマイズについては、[ サーバーサイドのカスタマイズ ](server-customize.md) を参照してください。

## Handlebars JS テンプレート言語 {#handlebars-js-templating-language}

新しいフレームワークでより顕著な変更の 1 つは、サーバークライアントレンダリング用の一般的なオープンソーステクノロジーである `Handlebars JS` （HBS）テンプレート言語の使用です。

HBS スクリプトはシンプルで、ロジックレスで、サーバーとクライアントの両方でコンパイルされ、オーバーレイとカスタマイズが簡単です。HBS はクライアントサイドレンダリングをサポートしているので、当然クライアント UX とバインドされます。

このフレームワークは、SocialComponents を開発するときに役立ついくつかの [Handlebars ヘルパー ](handlebars-helpers.md) を提供します。

サーバーで Sling がGETリクエストを解決すると、リクエストの応答に使用されるスクリプトが特定されます。 スクリプトが HBS テンプレート（.hbs）の場合、Sling はリクエストを Handlebars エンジンに委任します。 次に、Handlebars エンジンは、適切な SocialComponentFactory から SocialComponent を取得し、コンテキストを作成して、HTMLをレンダリングします。

### アクセス制限なし {#no-access-restriction}

Handlebars （HBS）テンプレートファイル（.hbs）は、.jsp および.html テンプレートファイルに似ていますが、クライアントブラウザーとサーバーの両方でレンダリングに使用できる点が異なります。 そのため、クライアント側テンプレートを要求するクライアントブラウザーは、サーバーから.hbs ファイルを受け取ります。

これには、Sling 検索パス内のすべての HBS テンプレート（/libs/または/apps の下のすべての.hbs ファイル）を、オーサーまたはパブリッシュから任意のユーザーが取得できる必要があります。

.hbs ファイルへの HTTP アクセスは禁止されない場合があります。

### コミュニティコンポーネントを追加または含める {#add-or-include-a-communities-component}

ほとんどの Communities コンポーネントは、Sling のアドレス可能なリソースとして *追加* する必要があります。 一部の Communities コンポーネントは、既存のリソース以外としてテンプレートに *含める* ことができます。これにより、ユーザー生成コンテンツ（UGC）を書き込む場所を動的に含めたりカスタマイズしたりできます。

どちらの場合も、コンポーネントの [ 必須のクライアントライブラリ ](clientlibs.md) が存在する必要があります。

**コンポーネントを追加**

コンポーネントの追加とは、リソース（コンポーネント）のインスタンスを追加するプロセスを指します。例えば、オーサー編集モードでコンポーネントブラウザー（サイドキック）からページにドラッグした場合などです。

結果は、par ノードの下の JCR 子ノードになります。このノードは、Sling でアドレス可能です。

**コンポーネントを含める**

コンポーネントの追加とは、スクリプト言語を使用するなど ](srp.md#for-non-existing-resources-ners) テンプレート内に [ 「存在しない」リソース（JCR ノードなし）への参照を追加するプロセスを指します。

Adobe Experience Manager（AEM） 6.1 以降では、コンポーネントを追加するのではなく、動的に含めると、そのコンポーネントのプロパティをオーサー *デザイン* モードで編集できます。

一部のAEM Communities コンポーネントのみ動的に含めることができます。 次のとおりです。

* [コメント](essentials-comments.md)
* [レーティング](rating-basics.md)
* [レビュー](reviews-basics.md)
* [投票](essentials-voting.md)

[ コミュニティコンポーネントガイド ](components-guide.md) を使用すると、含めるコンポーネントを追加から含めるに切り替えることができます。

**Handlebars** テンプレート言語を使用する場合、resourceType を指定することにより、[include ヘルパー ](handlebars-helpers.md#include) を使用して既存のリソースが含まれます。

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**JSP を使用する場合**、リソースはタグ [cq:include](../../help/sites-developing/taglib.md#lt-cq-include) を使用してインクルードされます。

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>コンポーネントをテンプレートに追加したりテンプレートに含めたりせずに、ページに動的に追加するには、[ コンポーネントのサイドローディング ](sideloading.md) を参照してください。

### Handlebars ヘルパー {#handlebars-helpers}

SCF で使用可能なカスタムヘルパーのリストと説明については、[SCF Handlebars ヘルパー ](handlebars-helpers.md) を参照してください。

## クライアントサイドフレームワーク {#client-side-framework}

### モデルビューJavaScriptフレームワーク {#model-view-javascript-framework}

このフレームワークには、機能豊富なインタラクティブコンポーネントの開発を容易にするモデルビューJavaScriptフレームワークである [Backbone.js](https://backbonejs.org/) の拡張機能が含まれています。 オブジェクト指向の特性により、拡張可能で再利用可能なフレームワークがサポートされます。 HTTP API を使用すると、クライアントとサーバー間の通信が簡略化されます。

このフレームワークは、サーバー側の Handlebars テンプレートを使用して、クライアント用のコンポーネントをレンダリングします。 モデルは、HTTP API で生成された JSON 応答に基づいています。 ビューは、Handlebars テンプレートで生成されたHTMLにバインドされ、インタラクティブ機能を提供します。

### CSS 規則 {#css-conventions}

CSS クラスを定義および使用する場合は、次の規則を使用することをお勧めします。

* 名前空間が明確に指定された CSS クラスセレクター名を使用し、「heading」や「image」などの汎用名は避けます。
* CSS スタイルシートがページ上の他の要素やスタイルとうまく連携するように、特定のクラスセレクタースタイルを定義します。 例：`.social-forum .topic-list .li { color: blue; }`
* スタイル設定のための CSS クラスを、JavaScriptが駆動する UX 用の CSS クラスとは別に保持します。

### クライアントサイドのカスタマイズ {#client-side-customizations}

クライアントサイドでの Communities コンポーネントの外観と動作をカスタマイズするには、以下の情報を含む [ クライアントサイドのカスタマイズ ](client-customize.md) を参照してください。

* [オーバーレイ](client-customize.md#overlays)
* [拡張子](client-customize.md#extensions)
* [HTMLのマークアップ](client-customize.md#htmlmarkup)
* [CSS のスキニング](client-customize.md#skinning-css)
* [JavaScriptの拡張](client-customize.md#extending-javascript)
* [SCF の clientlibs](client-customize.md#clientlibs-for-scf)

## 機能とコンポーネントの基本事項 {#feature-and-component-essentials}

開発者にとって不可欠な情報については、[ 機能とコンポーネントの基本事項 ](essentials.md) の節で説明します。

開発者向けの追加情報については、[ コーディングのガイドライン ](code-guide.md) の節を参照してください。

## トラブルシューティング {#troubleshooting}

一般的な問題と既知の問題については、[ トラブルシューティング ](troubleshooting.md) の節を参照してください。
