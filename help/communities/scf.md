---
title: ソーシャルコンポーネントフレームワーク
seo-title: Social Component Framework
description: ソーシャルコンポーネントフレームワーク（SCF）によって、コミュニティコンポーネントの設定、カスタマイズおよび拡張のプロセスが簡素化されます
seo-description: The social component framework (SCF) simplifies the process of configuring, customizing, and extending Communities components
uuid: 23b4418d-b91c-46fc-bf42-1154ef79fe5a
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d7b5b5e3-2d84-4a6b-bcc2-d490882ff3ed
exl-id: 5ca58bc3-8505-4d91-9cd1-6b2e2671f1be
source-git-commit: 1d5cfff10735ea31dc0289b6909851b8717936eb
workflow-type: tm+mt
source-wordcount: '1483'
ht-degree: 52%

---

# ソーシャルコンポーネントフレームワーク {#social-component-framework}

ソーシャルコンポーネントフレームワーク（SCF）によって、サーバー側とクライアント側の両方で、コミュニティコンポーネントの設定、カスタマイズおよび拡張のプロセスが簡素化されます。

フレームワークの利点：

* **機能**:80%の使用例に対するカスタマイズがほとんどあるいはまったく行われず、すぐに使用できる簡単な統合。
* **スキン可能**:CSS スタイル設定でHTML属性を一貫して使用。
* **拡張可能**:コンポーネントの実装は、オブジェクト指向でビジネスロジックが軽量で、サーバー上に増分的なビジネスログインを簡単に追加できます。
* **柔軟**:簡単にオーバーレイおよびカスタマイズできる、単純なロジックのない JavaScript テンプレートです。
* **アクセス可能**:HTTP API は、モバイルアプリを含む任意のクライアントからの投稿をサポートします。
* **ポータブル**:あらゆるテクノロジーで構築された Web ページに統合/埋め込みます。

インタラクティブな[コミュニティコンポーネントガイド](components-guide.md)を使用して、オーサーまたはパブリッシュインスタンスについて確認してください。

## 概要 {#overview}

SCF では、コンポーネントは SocialComponent POJO、Handlebars JS テンプレート（コンポーネントをレンダリングするため）および CSS（コンポーネントのスタイルを設定するため）で構成されます。

Handlebars JS テンプレートでは、モデル／ビュー JS コンポーネントを拡張して、クライアントでのコンポーネントとのユーザーインタラクションを処理できます。

コンポーネントがデータの変更をサポートする必要がある場合は、従来の Web アプリケーションでのモデル／データオブジェクトと同様のデータの編集／保存をサポートするために、SocialComponent API の実装を記述できます。また、操作リクエストの処理、ビジネスロジックの実行、およびモデル/データオブジェクトでの API の呼び出しを行うために、操作（コントローラー）と操作サービスを追加できます。

クライアントが必要とするデータをビューレイヤーまたは HTTP クライアントに提供するために、SocialComponent API を拡張できます。

### クライアントに対するページのレンダリング方法 {#how-pages-are-rendered-for-client}

![scf-page-rendering](assets/scf-overview.png)

### コンポーネントのカスタマイズおよび拡張 {#component-customization-and-extension}

コンポーネントをカスタマイズまたは拡張するには、今後のリリースへのアップグレードプロセスを簡素化する /apps ディレクトリに対してオーバーレイおよび拡張のみを記述します。

* スキニングの場合：
   * 次の項目のみ [CSS で編集が必要](client-customize.md#skinning-css).
* 外観と操作性：
   * JS テンプレートと CSS を変更します。
* 外観、操作性、UX に関しては、次の点に注意してください。
   * JS テンプレート、CSS およびの変更 [JavaScript の拡張/オーバーライド](client-customize.md#extending-javascript).
* JS テンプレートまたはGETエンドポイントで使用可能な情報を変更するには：
   * の拡張 [SocialComponent](server-customize.md#socialcomponent-interface).
* 操作中にカスタム処理を追加するには：
   * を書く [OperationExtension](server-customize.md#operationextension-class).
* 新しいカスタム操作を追加するには：
   * 新しい [Sling Post 操作](server-customize.md#postoperation-class).
   * 既存を使用 [OperationServices](server-customize.md#operationservice-class) 必要に応じて。
   * 必要に応じてクライアント側から操作を呼び出す JavaScript コードを追加します。

## サーバー側フレームワーク {#server-side-framework}

このフレームワークでは、サーバー上の機能にアクセスし、クライアントとサーバー間のインタラクションをサポートするための API が提供されます。

### Java API {#java-apis}

Java API では、継承またはサブクラス化が容易な抽象クラスおよびインターフェイスが提供されます。

メインクラスについては、[サーバー側のカスタマイズ](server-customize.md)ページで説明します。

訪問 [ストレージリソースプロバイダの概要](srp.md) を参照してください。

### HTTP API {#http-api}

HTTP API によって、PhoneGap アプリ、ネイティブアプリ、その他の統合およびマッシュアップについて、カスタマイズの容易さとクライアントプラットフォームの選択がサポートされます。さらに、HTTP API を使用すると、コミュニティサイトをクライアントなしでサービスとして実行できるので、フレームワークコンポーネントを任意のテクノロジーで構築された任意の Web ページに統合できます。

### HTTP API - GET 要求 {#http-api-get-requests}

すべての SocialComponent に対して、フレームワークによって HTTP ベースの API エンドポイントが提供されます。このエンドポイントにアクセスするには、「.social.json」セレクターと拡張子を使用してGETリクエストをリソースに送信します。 Sling を使用して、要求が `DefaultSocialGetServlet`.

**`DefaultSocialGetServlet`**

1. リソース (resourceType) を `SocialComponentFactoryManager` とは、 `SocialComponent` リソースを表しています。

1. ファクトリを呼び出し、を受け取ります。 `SocialComponent` リソースとリクエストを処理できる
1. を呼び出します。 `SocialComponent`：リクエストを処理し、結果の JSON 表現を返します。
1. JSON 応答をクライアントに返します。

**`GET Request`**

デフォルトの GET Servlet が、SocialComponent がカスタマイズ可能な JSON で応答する .social.json 要求をリスニングします。

![scf-framework](assets/scf-framework.png)

### HTTP API - POST 要求 {#http-api-post-requests}

GET（読み取り）操作に加え、コンポーネントに対するその他の操作（作成、更新、削除など）を可能にするエンドポイントパターンがフレームワークによって定義されます。これらのエンドポイントは、入力を受け入れ、HTTP ステータスコードまたは JSON 応答オブジェクトを使用して応答する HTTP API です。

このフレームワークエンドポイントパターンにより、CUD 操作は拡張、再利用およびテストが可能になります。

**`POST Request`**

SocialComponent 操作ごとに Sling POST :operation があります。各操作のビジネスロジックとメンテナンスコードは、HTTP API を通じて、または OSGi サービスとして他の場所からアクセスできる OperationService にラップされます。 前/後のアクションに対するプラグ可能な操作拡張をサポートするフックが提供されます。

![scf-post-request](assets/scf-post-request.png)

### ストレージリソースプロバイダー（SRP） {#storage-resource-provider-srp}

[コミュニティコンテンツストア](working-with-srp.md)に格納された UGC の処理については、以下を参照してください。：

* [ストレージリソースプロバイダの概要](srp.md)  — の概要とリポジトリの使用の概要。
* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP API ユーティリティのメソッドと例。
* [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md)  — コーディングのガイドライン。

### サーバー側のカスタマイズ {#server-side-customizations}

サーバー側のコミュニティコンポーネントのビジネスロジックおよび動作のカスタマイズについて詳しくは、[サーバー側のカスタマイズ](server-customize.md)を参照してください。

## Handlebars JS テンプレート言語 {#handlebars-js-templating-language}

新しいフレームワークの顕著な変更の 1 つは、 `Handlebars JS` (HBS) テンプレート言語。サーバー — クライアントレンダリング用の一般的なオープンソーステクノロジーです。

HBS スクリプトは、単純で、ロジックがなく、サーバーとクライアントの両方でコンパイルされ、オーバーレイやカスタマイズが容易であり、HBS ではクライアント側のレンダリングがサポートされているのでクライアント UX と自然にバインドします。

このフレームワークでは、SocialComponent の開発に便利な複数の [Handlebars ヘルパー](handlebars-helpers.md)が提供されます。

サーバーで、Sling は GET 要求を解決するときに、要求への応答に使用されるスクリプトを識別します。スクリプトが HBS テンプレート (.hbs) の場合、Sling は要求を Handlebars エンジンに委任します。 次に、Handlebars Engine は、適切な SocialComponentFactory から SocialComponent を取得し、コンテキストを構築し、HTMLをレンダリングします。

### アクセス制限なし {#no-access-restriction}

Handlebars（HBS）テンプレートファイル（.hbs）は、.jsp および .html テンプレートファイルに似ていますが、クライアントブラウザーとサーバーの両方でレンダリングに使用できる点が異なります。そのため、クライアント側テンプレートを要求するクライアントブラウザーは、.hbs ファイルをサーバーから受け取ります。

これには、sling 検索パス内のすべての HBS テンプレート（/libs/ または /apps の下の .hbs ファイル）を、オーサーまたはパブリッシュから任意のユーザーが取得できる必要があります。

.hbs ファイルへの HTTP アクセスは禁止できません。

### コミュニティコンポーネントの追加またはインクルード {#add-or-include-a-communities-component}

ほとんどのコミュニティコンポーネントは、Sling アドレス可能リソースとして追加する必要があります。**&#x200B;一部のコミュニティコンポーネントは、 *含む* を既存のリソース以外としてテンプレートに追加し、ユーザー生成コンテンツ (UGC) を書き込む場所を動的に組み込み、カスタマイズできるようにします。

どちらの場合も、コンポーネントの [必要なクライアントライブラリ](clientlibs.md) は、も存在する必要があります。

**コンポーネントの追加**

コンポーネントの追加は、コンポーネントブラウザー（サイドキック）からページにオーサー編集モードでドラッグされたときなどに、リソース（コンポーネント）のインスタンスを追加するプロセスです。

結果は、同位ノードの下の JCR 子ノードであり、これは Sling アドレス可能です。

**コンポーネントのインクルード**

コンポーネントを含めると、 [「存在しない」リソース](srp.md#for-non-existing-resources-ners) （JCR ノードなし）をテンプレート内に追加します（スクリプト言語の使用など）。

AEM 6.1 以降では、コンポーネントが追加される代わりに動的に含まれる場合、コンポーネントのプロパティをオーサー*デザイン*モードで編集できます。

一部の AEM Communities コンポーネントのみを動的にインクルードできます。次のようになります。

* [コメント](essentials-comments.md)
* [レーティング](rating-basics.md)
* [レビュー](reviews-basics.md)
* [投票](essentials-voting.md)

この [コミュニティコンポーネントガイド](components-guide.md) を使用すると、インクルード可能なコンポーネントを追加からインクルードに切り替えることができます。

**Handlebars を使用する場合** テンプレート言語、存在しないリソースは [ヘルパーを含める](handlebars-helpers.md#include) resourceType を指定する。

`{{include this.id path="comments" resourceType="social/commons/components/hbs/comments"}}`

**JSP** を使用する場合、リソースはタグ [cq:include](../../help/sites-developing/taglib.md#lt-cq-include) を使用してインクルードされます。

```
<cq:include path="votes"
 resourceType="social/tally/components/voting" />
```

>[!NOTE]
>
>コンポーネントを、テンプレートに追加またはインクルードせずに、ページに動的に追加するには、[コンポーネントのサイドローディング](sideloading.md)を参照してください。

### Handlebars ヘルパー {#handlebars-helpers}

SCF で使用できるカスタムヘルパーのリストおよび説明については、[SCF Handlebars ヘルパー](handlebars-helpers.md)を参照してください。

## クライアント側フレームワーク {#client-side-framework}

### モデル - ビュー JavaScript フレームワーク {#model-view-javascript-framework}

このフレームワークには、リッチでインタラクティブなコンポーネントの開発を促進するために、[Backbone.js](https://www.backbonejs.org/)（モデル - ビュー JavaScript フレームワーク）という拡張が含まれています。オブジェクト指向の特性は、拡張可能/再利用可能なフレームワークをサポートします。 クライアントとサーバー間の通信は、HTTP API を使用して簡単になります。

このフレームワークでは、サーバー側の Handlebars テンプレートを利用して、クライアント用にコンポーネントをレンダリングします。 モデルは、HTTP API によって生成された JSON 応答に基づいています。 ビューは、Handlebars テンプレートによって生成されるHTMLに結合され、インタラクティビティを提供します。

### CSS の規則 {#css-conventions}

CSS クラスの定義と使用に推奨される規則を以下に示します。

* 明確に名前空間化された CSS クラスセレクター名を使用し、「heading」、「image」などの汎用名を使用しないでください。
* 特定のクラスセレクタースタイルを定義して、CSS スタイルシートがページ上の他の要素やスタイルとうまく連携するようにします。 例：`.social-forum .topic-list .li { color: blue; }`
* スタイル設定用の CSS クラスを、JavaScript によって駆動される UX 用の CSS クラスとは別に保持します。

### クライアント側のカスタマイズ {#client-side-customizations}

クライアント側でのコミュニティコンポーネントの外観と動作をカスタマイズするには、以下に関する情報が含まれている[クライアント側のカスタマイズ](client-customize.md)を参照してください。

* [オーバーレイ](client-customize.md#overlays)
* [拡張子](client-customize.md#extensions)
* [HTML マークアップ](client-customize.md#htmlmarkup)
* [CSS のスキンの適用](client-customize.md#skinning-css)
* [JavaScript の拡張](client-customize.md#extending-javascript)
* [SCF の clientlib](client-customize.md#clientlibs-for-scf)

## 機能とコンポーネントの基本事項 {#feature-and-component-essentials}

開発者にとっての基本情報が、[機能とコンポーネントの基本事項](essentials.md)の節で説明されています。

開発者向けの追加情報については、[コーディングのガイドライン](code-guide.md)の節を参照してください。

## トラブルシューティング {#troubleshooting}

一般的な課題および既知の問題が、[トラブルシューティング](troubleshooting.md)の節で説明されています。
