---
title: コンテンツフラグメントと共に使用する AEM GraphQL API
description: Adobe Experience Manager（AEM） のコンテンツフラグメントを AEM GraphQL API と共に使用してヘッドレスコンテンツ配信を実現する方法を説明します。
feature: Content Fragments,GraphQL API
exl-id: beae1f1f-0a76-4186-9e58-9cab8de4236d
source-git-commit: 42ef4694a3301ae1cd34766ce4c19f4b0e2f2c38
workflow-type: tm+mt
source-wordcount: '3695'
ht-degree: 95%

---

# コンテンツフラグメントと共に使用する AEM GraphQL API {#graphql-api-for-use-with-content-fragments}

Adobe Experience Manager（AEM） のコンテンツフラグメントを AEM GraphQL API と共に使用してヘッドレスコンテンツ配信を実現する方法を説明します。

コンテンツフラグメントと共に使用する AEM GraphQL API は、オープンソースの標準 GraphQL API に大きく依存しています。

AEM の GraphQL API を使用すると、ヘッドレス CMS 実装の JavaScript クライアントにコンテンツフラグメントを効率的に配信できます。

* REST で API リクエストの反復を回避
* 特定の要件に限定された配信を確保
* 1 つの API クエリへの応答としてレンダリングに必要なものだけを一括配信

>[!NOTE]
>
>GraphQL は現在 Adobe Experience Manager (AEM) の 2 つの（別々の）シナリオで使用されています。
>
>* [AEM Commerce が、GraphQL 経由でコマースプラットフォームのデータを使用する](/help/commerce/cif/integrating/magento.md)。
>* AEM コンテンツフラグメントが、AEM GraphQL API（標準の GraphQL に基づくカスタム実装）と連携して、アプリケーションで使用するための構造化コンテンツを配信する。


## GraphQL API {#graphql-api}

GraphQL とは次のことを意味します。

* 「*...API のクエリ言語と、既存のデータを使用してこれらのクエリを満たすランタイムです。GraphQL は、API のデータの完全で理解可能な説明を提供し、必要なものを正確に要求する力をクライアントに与え、API の長期的な発展を促し、強力な開発ツールの実現を可能にします。*」

   [GraphQL.org](https://graphql.org) を参照

* 「*...柔軟な API レイヤー用のオープンな仕様。GraphQL を既存のバックエンドに重ね合わせて、以前に比べて迅速に製品を構築…。*」

   「[Explore GraphQL](https://www.graphql.com)」を参照

* *「...2012 年に Facebook 社内で開発されたデータクエリ言語および仕様です。その後、2015 年には公式にオープンソースとなりました。開発者の生産性を高め、転送データの量を最小限に抑えるために、REST ベースのアーキテクチャに代わる手段を提供します。GraphQL は、あらゆる規模の数百の組織により実稼働環境で使用されています...」*

   [GraphQL Foundation](https://foundation.graphql.org/) を参照してください。

<!--
"*Explore GraphQL is maintained by the Apollo team. Our goal is to give developers and technical leaders around the world all of the tools they need to understand and adopt GraphQL.*". 
-->

GraphQL API の詳細については、（多くのリソースの中でも特に）以下を参照してください。

* [graphql.org](https://graphql.org)：

   * [GraphQL の概要](https://graphql.org/learn)

   * [GraphQL の仕様](https://spec.graphql.org/)

* [graphql.com](https://graphql.com)：

   * [ガイド](https://www.graphql.com/guides/)

   * [チュートリアル](https://www.graphql.com/tutorials/)

   * [導入事例](https://www.graphql.com/case-studies/)

AEM 用 GraphQL の実装は、標準の GraphQL Java ライブラリをベースにしています。以下を参照してください。

* [graphQL.org - Java](https://graphql.org/code/#java)

* [GitHub の GraphQL Java](https://github.com/graphql-java)

### GraphQL 用語 {#graphql-terminology}

GraphQL では次を使用します。

* **[クエリ](https://graphql.org/learn/queries/)**

* **[スキーマとタイプ](https://graphql.org/learn/schema/)**：

   * スキーマは、コンテンツフラグメントモデルに基づいて AEM で生成されます。
   * GraphQL では、スキーマを使用して、AEM 用 GraphQL の実装で使用可能なタイプと操作を提供します。

* **[フィールド](https://graphql.org/learn/queries/#fields)**

* **[GraphQL エンドポイント](#graphql-aem-endpoint)**
   * GraphQL クエリに応答し、GraphQL スキーマへのアクセスを提供する AEM 内のパス。

   * 詳しくは、[GraphQL エンドポイントの有効化](#enabling-graphql-endpoint)を参照してください。

[ベストプラクティス](https://graphql.org/learn/best-practices/)を含む包括的な詳細については、「[(GraphQL.org) GraphQL の概要](https://graphql.org/learn/)」を参照してください。

### GraphQL クエリタイプ {#graphql-query-types}

GraphQL では、次のいずれかを返すクエリを実行できます。

* **1 つのエントリ**

* **[エントリのリスト](https://graphql.org/learn/schema/#lists-and-non-null)**

AEMは、クエリ（両方のタイプ）をに変換する機能を提供します。 [永続クエリ](/help/assets/content-fragments/persisted-queries.md):Dispatcher および CDN によってキャッシュできます。

### GraphQLクエリのベストプラクティス（Dispatcher と CDN） {#graphql-query-best-practices}

この [永続クエリ](/help/assets/content-fragments/persisted-queries.md) パブリッシュインスタンスでは、次のように使用することをお勧めします。

* キャッシュされます
* これらは、AEMによって一元的に管理されます

>[!NOTE]
>
>通常、オーサー環境には Dispatcher/CDN がないので、そこでの永続化されたクエリの使用に利益はありません。テスト以外に

POST要求を使用するGraphQLクエリはキャッシュされないので、お勧めしません。そのため、デフォルトインスタンスでは、Dispatcher は、このようなクエリをブロックするように設定されています。

GraphQLはGETリクエストもサポートしますが、これらの制限（URL の長さなど）に達して、永続化クエリを使用するのを避けることができます。

>[!NOTE]
>
>直接クエリを実行する機能は、将来、廃止される可能性があります。

## AEM 用 GraphQL のエンドポイント {#graphql-aem-endpoint}

エンドポイントは、AEM 用 GraphQL へのアクセスに使用するパスです。このパスを使用すると、以下が可能になります。

* GraphQL スキーマへのアクセス
* GraphQL クエリの送信
* （GraphQL クエリに対する）応答の受信

AEM には次の 2 種類のエンドポイントがあります。

* グローバル
   * すべてのサイトで使用できます。
   * このエンドポイントは、（[設定ブラウザー](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)で定義された）すべての Sites 設定のすべてのコンテンツフラグメントモデルを使用できます。
   * Sites 設定間で共有する必要があるコンテンツフラグメントモデルがある場合は、それらをグローバル Sites 設定の下に作成する必要があります。
* Sites 設定：
   * [設定ブラウザー](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)で定義されている Sites 設定に対応します。
   * 指定したサイト／プロジェクトに固有です。
   * Sites 設定固有のエンドポイントは、その特定の Sites 設定のコンテンツフラグメントモデルと、グローバル Sites 設定のコンテンツフラグメントモデルを使用します。

>[!CAUTION]
>
>コンテンツフラグメントエディターを使用すると、Sites 設定のコンテンツフラグメントから別の Sites 設定のコンテンツフラグメントを（ポリシーを介して）参照できます。
>
>この場合、Sites 設定固有のエンドポイントを使用してすべてのコンテンツを取得できるわけではありません。
>
>コンテンツ作成者がこのシナリオを制御する必要があります。例えば、共有コンテンツフラグメントモデルをグローバルサイト設定の下に配置すると便利です。

AEM グローバルエンドポイント用 GraphQL のリポジトリーパスは次のとおりです。

`/content/cq:graphql/global/endpoint`

アプリは、リクエスト URL で次のパスを使用できます。

`/content/_cq_graphql/global/endpoint.json`

AEM 用 GraphQL のエンドポイントを有効にするには、次の操作が必要です。

* [GraphQL エンドポイントの有効化](#enabling-graphql-endpoint)
* [GraphQL エンドポイントの公開](#publishing-graphql-endpoint)

### GraphQL エンドポイントの有効化 {#enabling-graphql-endpoint}

GraphQL エンドポイントを有効にするには、まず適切な設定が必要です。「[コンテンツフラグメント - 設定ブラウザー ](/help/assets/content-fragments/content-fragments-configuration-browser.md)」を参照してください。

>[!CAUTION]
>
>[コンテンツフラグメントモデルの使用が有効になっていない](/help/assets/content-fragments/content-fragments-configuration-browser.md)場合、「**作成**」オプションは使用できません。

対応するエンドポイントを有効にするには、以下を行います。

1. **ツール**／**Assets** に移動し、「**GraphQL**」を選択します。
1. 「**作成**」を選択します。
1. **新しい GraphQL エンドポイントを作成**&#x200B;ダイアログが開きます。以下を指定します。
   * **名前**：エンドポイントの名前。任意のテキストを入力できます。
   * **使用する GraphQL スキーマの提供元**： ドロップダウンを使用して、必要なサイト／プロジェクトを選択します。

   >[!NOTE]
   >
   >ダイアログには次の警告が表示されます。
   >
   >* *慎重に管理しない場合、GraphQL エンドポイントによりデータのセキュリティとパフォーマンスで問題が発生する可能性があります。エンドポイントを作成した後で、適切な権限を設定するようにしてください。*


1. 「**作成**」で確定します。
1. 「**次の手順**」ダイアログには、セキュリティコンソールへの直接リンクが表示されるので、新しく作成したエンドポイントに適切な権限が付与されているか確認できます。

   >[!CAUTION]
   >
   >エンドポイントは、すべてのユーザーがアクセスできます。そのため、GraphQL クエリがサーバーに大きな負荷をかける可能性があるので、特にパブリッシュインスタンスでは、セキュリティ上の問題が発生するおそれがあります。
   >
   >使用例に適した ACL をエンドポイントに設定できます。

### GraphQL エンドポイントの公開 {#publishing-graphql-endpoint}

新しいエンドポイントを選択し、「 **公開**」を選択して、すべての環境で完全に使用できるようにします。

>[!CAUTION]
>
>エンドポイントは、すべてのユーザーがアクセスできます。
>
>GraphQL クエリがサーバーに大きな負荷をかける可能性があるので、パブリッシュインスタンスでは、セキュリティ上の問題が発生する恐れがあります。
>
>ユースケースに適した ACL をエンドポイントに設定する必要があります。

## GraphiQL インターフェイス {#graphiql-interface}

標準の [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql) インターフェイスの実装は、AEM GraphQL で使用できます。

>[!NOTE]
>
>GraphiQL は AEM のすべての環境に含まれています（ただし、エンドポイントを設定した場合にのみアクセス可能／表示可能になります）。
>
>以前のリリースでは、GraphiQL IDE をインストールするためにパッケージが必要でした。これをインストール済みの場合は、削除できます。

このインターフェイスを使用すると、クエリを直接入力しテストできます。

次に例を示します。

* `http://localhost:4502/content/graphiql.html`

構文のハイライト表示機能、オートコンプリート、自動候補表示などの機能と共に、履歴およびオンラインドキュメントが提供されています。

![GraphiQL インターフェイス ](assets/cfm-graphiql-interface.png "GraphiQL インターフェイス")

>[!NOTE]
>
>詳しくは、 [GraphiQL IDE の使用](/help/assets/content-fragments/graphiql-ide.md).

## オーサー環境とパブリッシュ環境の使用例 {#use-cases-author-publish-environments}

使用例は、AEM 環境のタイプによって異なる場合があります。

* パブリッシュ環境の使用目的：
   * JS アプリケーションのデータのクエリ（標準の使用例）

* オーサー環境の使用目的：
   * 「コンテンツ管理用」のデータのクエリ：
      * AEM の GraphQL は現在読み取り専用の API です。
      * REST API は、CR(U)D の操作に使用できます。

## 権限 {#permission}

Assets へのアクセスに必要な権限です。

GraphQLクエリは、基になるリクエストのAEMユーザーの権限で実行されます。 一部のフラグメント（Assets として保存）への読み取りアクセス権を持っていない場合、ユーザーは結果セットに含まれません。

また、GraphQLクエリを実行するには、ユーザーがGraphQLエンドポイントにアクセスできる必要があります。

## スキーマ生成 {#schema-generation}

GraphQL は、厳密に型指定された API です。つまり、データは型別に明確に構造化され編成される必要があります。

GraphQL の仕様には、特定のインスタンス上のデータをクエリするための堅牢な API を作成する方法に関する一連のガイドラインが用意されています。そのタスクを行うには、クライアントは[スキーマ](#schema-generation)を取得する必要があります。この中には、クエリに必要なすべての型が定義されています。

コンテンツフラグメントの場合、GraphQL スキーマ（構造とタイプ）は、**有効**&#x200B;な[コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)とそれらのデータタイプに基づいています。

>[!CAUTION]
>
>（**有効**&#x200B;になっているコンテンツフラグメントモデルから派生した）すべての GraphQL スキーマは、GraphQL エンドポイントを通じて読み取り可能です。
>
>つまり、漏洩するおそれがあるので、機密データが使用可能になっていないことを確認する必要があります。例えば、これには、モデル定義のフィールド名として存在する可能性のある情報が含まれます。

例えば、ユーザーが `Article` という名前のコンテンツフラグメントモデルを作成した場合、AEM は `ArticleModel` 型のオブジェクト `article` を生成します。この型に含まれるフィールドは、モデルで定義されているフィールドとデータ型に対応しています。

1. コンテンツフラグメントモデル：

   ![GraphQL で使用するコンテンツフラグメントモデル](assets/cfm-graphqlapi-01.png "GraphQL で使用するコンテンツフラグメントモデル")

1. 対応する GraphQL スキーマ（GraphiQL 自動生成ドキュメントからの出力）:
   ![コンテンツフラグメントモデルに基づく GraphQL スキーマ](assets/cfm-graphqlapi-02.png "コンテンツフラグメントモデルに基づく GraphQL スキーマ")

   この図では、生成された型 `ArticleModel` に複数の[フィールド](#fields)が含まれていることがわかります。

   * そのうちの 3 つ（`author`、`main`、`referencearticle`）は、ユーザーが管理しています。

   * その他のフィールド（この例では `_path`、`_metadata`、`_variations`）は AEM によって自動的に追加されたもので、特定のコンテンツフラグメントに関する情報を提供する便利な手段となっています。これらの[ヘルパーフィールド](#helper-fields)は、ユーザーが定義したものと自動生成されたものを区別するために、先頭に `_` が付いています。

1. ユーザーが Article モデルに基づいてコンテンツフラグメントを作成すると、GraphQL を使用してそれをクエリできます。例については、（[GraphQL で使用するコンテンツフラグメント構造のサンプル](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)に基づいた）[サンプルクエリ](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries)を参照してください。

AEM 用 GraphQL では、スキーマには柔軟性があります。つまり、コンテンツフラグメントモデルを作成、更新、削除するたびに、スキーマが自動生成されます。また、コンテンツフラグメントモデルを更新すると、データスキーマキャッシュも更新されます。

Sites GraphQL サービスは、コンテンツフラグメントモデルに対する変更を（バックグラウンドで）リッスンします。更新が検出されると、スキーマのその部分だけが再生成されます。この最適化により、時間が節約され、安定性も確保されます。

例えば、次のようになります。

1. `Content-Fragment-Model-1` と `Content-Fragment-Model-2` を含んだパッケージをインストールすると、

   1. `Model-1` と `Model-2` の GraphQL 型が生成されます。

1. 次に `Content-Fragment-Model-2` を変更すると、

   1. `Model-2` GraphQL 型だけが更新されます。

   1. 一方、`Model-1` は同じままです。

>[!NOTE]
>
>REST API を使用してコンテンツフラグメントモデルの一括更新を行う場合などには、この点に留意することが大切です。

スキーマは、GraphQL クエリと同じエンドポイントを通じて提供され、クライアントはスキーマが拡張子 `GQLschema` で呼び出されることに対処します。例えば、`/content/cq:graphql/global/endpoint.GQLschema` で単純な `GET` リクエストを実行すると、`text/x-graphql-schema;charset=iso-8859-1` の Content-type を持つスキーマが出力されます。

### スキーマの生成 - 未公開のモデル {#schema-generation-unpublished-models}

コンテンツフラグメントがネストされると、親のコンテンツフラグメントモデルは公開されますが、参照モデルは公開されません。

>[!NOTE]
>
>AEM UI はこのような問題を回避しますが、プログラムを使用して、またはコンテンツパッケージを使用して公開すると、この問題が発生する可能性があります。

この場合、AEM は親コンテンツフラグメントモデルの&#x200B;*不完全な*&#x200B;スキーマを生成します。つまり、非公開のモデルに依存するフラグメント参照がスキーマから削除されます。

## フィールド {#fields}

スキーマ内には、次の 2 つの基本的なカテゴリに属する個々のフィールドがあります。

* ユーザーが生成するフィールド

   選択された[フィールドタイプ](#field-types)を使用して、コンテンツフラグメントモデルの設定方法に基づいてフィールドが作成されます。フィールド名は、**データタイプ**&#x200B;の「**プロパティ名**」フィールドから取得されます。

   * また、**レンダリング時の名前**&#x200B;プロパティも考慮する必要があります。ユーザーが特定のデータ型を、例えば、1 行のテキストか複数フィールドのどちらかとして設定できるからです。

* AEM 用 GraphQL が生成する多数の[ヘルパーフィールド](#helper-fields)

   これらは、コンテンツフラグメントを識別するためや、コンテンツフラグメントに関する詳細を取得するために使用されます。

### フィールドタイプ {#field-types}

AEM 用 GraphQL では一連のタイプをサポートしています。サポートされているすべてのコンテンツフラグメントモデルデータ型と、それに対応する GraphQL 型を以下の表に示します。

| コンテンツフラグメントモデル - データ型 | GraphQL の型 | 説明 |
|--- |--- |--- |
| 1 行のテキスト | String、[String] |  作成者名、場所名などの単純な文字列に使用します。 |
| 複数行テキスト | String |  記事の本文などのテキストを出力するために使用します |
| Number |  Float、[Float] | 浮動小数点数と整数を表示するために使用します |
| Boolean |  Boolean |  チェックボックスを表示するために使用します（単純な真／偽のステートメント） |
| 日時 | Calendar |  日時を ISO 8086 形式で表示するために使用します。選択したタイプに応じて、AEM GraphQL で使用できるフレーバーは、`onlyDate`、`onlyTime`、`dateTime` の 3 つです。 |
| 定義済みリスト |  String |  モデルの作成時に定義されたオプションのリストに含まれるオプションを表示するために使用します |
|  タグ |  [String] |  AEM で使用されているタグを表す文字列のリストを表示するために使用します |
| コンテンツ参照 |  String |  AEM 内の別のアセットへのパスを表示するために使用します |
| フラグメント参照 |  *モデルタイプ* |  特定のモデルタイプの別のコンテンツフラグメントを参照するために使用します（モデルの作成時に定義されます） |

### ヘルパーフィールド {#helper-fields}

ユーザー生成フィールドのデータ型に加えて、AEM 用 GraphQL では、コンテンツフラグメントの識別やコンテンツフラグメントに関する追加情報の提供に役立つ多数の&#x200B;*ヘルパー*&#x200B;フィールドも生成されます。

#### パス {#path}

パスフィールドは、GraphQL で識別子として使用されます。これは、AEM リポジトリ内のコンテンツフラグメントアセットのパスを表します。これをコンテンツフラグメントの識別子として選択した理由は次のとおりです。

* AEM 内で一意である
* 取得しやすい

次のコードでは、コンテンツフラグメントモデル `Person` に基づいて作成されたすべてのコンテンツフラグメントのパスを表示します。

```xml
{
  personList {
    items {
      _path
    }
  }
}
```

特定のタイプのコンテンツフラグメントを 1 つ取得するには、まずそのパスも決定する必要があります。次に例を示します。

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      firstName
      name
    }
  }
}
```

[サンプルクエリ - 1 つの特定の都市フラグメント](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)を参照してください。

#### メタデータ {#metadata}

また、AEM では GraphQL を通じて、コンテンツフラグメントのメタデータも公開します。メタデータは、コンテンツフラグメントのタイトル、サムネールパス、コンテンツフラグメントの説明、作成日など、コンテンツフラグメントを説明する情報です。

メタデータはスキーマエディターで生成され、特定の構造を持たないので、コンテンツフラグメントのメタデータを公開するために GraphQL 型 `TypedMetaData` が実装されました。`TypedMetaData` では、次のスカラー型でグループ化された情報を公開します。

| フィールド |
|--- |
| `stringMetadata:[StringMetadata]!` |
| `stringArrayMetadata:[StringArrayMetadata]!` |
| `intMetadata:[IntMetadata]!` |
| `intArrayMetadata:[IntArrayMetadata]!` |
| `floatMetadata:[FloatMetadata]!` |
| `floatArrayMetadata:[FloatArrayMetadata]!` |
| `booleanMetadata:[BooleanMetadata]!` |
| `booleanArrayMetadata:[booleanArrayMetadata]!` |
| `calendarMetadata:[CalendarMetadata]!` |
| `calendarArrayMetadata:[CalendarArrayMetadata]!` |

各スカラー型は、名前と値の 1 つのペアを表すか、名前と値のペアの配列を表します。このペアの値は、グループ化されたときの型になります。

例えば、コンテンツフラグメントのタイトルを取得する場合は、このプロパティが String 型プロパティであることがわかっているので、すべての String 型メタデータをクエリすることになります。

メタデータをクエリするには、次のようにします。

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _path
      _metadata {
        stringMetadata {
          name
          value
        }
      }
    }
  }
}
```

生成された GraphQL スキーマを表示するには、すべてのメタデータ GraphQL 型を表示します。すべてのモデルタイプは同じ `TypedMetaData` を持ちます。

>[!NOTE]
>
>**標準メタデータと配列メタデータの違い**：
>`StringMetadata` と `StringArrayMetadata` はどちらも、リポジトリに格納されているものについての指定であり、その取得手段についての指定ではありません。
>
>例えば、`stringMetadata` フィールドを呼び出すと、リポジトリに `String` として格納されているすべてのメタデータの配列を受け取ることになります。一方、`stringArrayMetadata` を呼び出すと、リポジトリに `String[]` として格納されているすべてのメタデータの配列を受け取ります。

詳しくは、[メタデータのサンプルクエリ - 「GB」という賞のメタデータのリスト](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)を参照してください。

#### バリエーション {#variations}

コンテンツフラグメントのバリエーションに対するクエリを簡略化するために、`_variations` フィールドが実装されています。次に例を示します。

```xml
{
  personByPath(_path: "/content/dam/path/to/fragment/john-doe") {
    item {
      _variations
    }
  }
}
```

詳しくは、[サンプルクエリ - 名前付きバリエーションを持つすべての都市](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)を参照してください。

>[!NOTE]
>
>指定されたバリエーションがコンテンツフラグメントに対して存在しない場合、マスターバリエーションが（フォールバック）デフォルトとして返されます。

<!--
## Security Considerations {#security-considerations}
-->

## GraphQL 変数 {#graphql-variables}

GraphQL では、クエリに変数を含めることができます。詳しくは、[GraphQL の変数に関するドキュメント](https://graphql.org/learn/queries/#variables)を参照してください。

例えば、特定のバリエーションを持つ `Article` タイプのコンテンツフラグメントをすべて取得するには、次のように、GraphiQL で変数 `variation` を指定します。

![GraphQL 変数](assets/cfm-graphqlapi-03.png "GraphQL 変数")

```xml
### query
query GetArticlesByVariation($variation: String!) {
    articleList(variation: $variation) {
        items {
            _path
            author
            _variations
        }
    }
}
 
### in query variables
{
    "variation": "uk"
}
```

## GraphQL ディレクティブ {#graphql-directives}

GraphQL では、GraphQL ディレクティブと呼ばれる変数に基づいてクエリを変更する可能性があります。

例えば、変数 `includePrice` に基づいて、すべての `AdventureModels` のクエリに `adventurePrice` フィールドを含めることができます。

![GraphQL ディレクティブ](assets/cfm-graphqlapi-04.png "GraphQL ディレクティブ")

```xml
### query
query GetAdventureByType($includePrice: Boolean!) {
  adventureList {
    items {
      adventureTitle
      adventurePrice @include(if: $includePrice)
    }
  }
}
 
### in query variables
{
    "includePrice": true
}
```

## フィルタリング {#filtering}

GraphQL クエリでフィルタリングを使用して、特定のデータを返すこともできます。

フィルタリングでは、論理演算子と論理式に基づいた構文を使用します。

例えば、次の（基本的な）クエリでは、`Jobs` または `Smith` という名前を持つすべての人を抜き出します。

```xml
query {
  personList(filter: {
    name: {
      _logOp: OR
      _expressions: [
        {
          value: "Jobs"
        },
        {
          value: "Smith"
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

その他の例については、以下を参照してください。

* [AEM 用 GraphQL の拡張機能](#graphql-extensions)の詳細

* [このサンプルコンテンツおよび構造を使用したサンプルクエリ](/help/assets/content-fragments/content-fragments-graphql-samples.md#graphql-sample-queries-sample-content-fragment-structure)

   * さらに、サンプルクエリ用に準備されている[サンプルコンテンツおよび構造](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)

* [WKND プロジェクトに基づいたサンプルクエリ](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-queries-using-wknd-project)

## AEM 用の GraphQL - 拡張機能の概要 {#graphql-extensions}

AEM 用の GraphQL でのクエリの基本操作は、標準の GraphQL 仕様に従います。AEM での GraphQL クエリには、次のような拡張機能があります。

* 結果が 1 つだけ必要な場合：
   * モデル名（例：city）を使用します

* 結果のリストを想定している場合：
   * モデル名に `List` を付け加えます（例：`cityList`）
   * [サンプルクエリ - すべての都市に関するすべての情報](#sample-all-information-all-cities)を参照してください

* フィルター `includeVariations` は `List` のクエリタイプに含まれます。クエリ結果でコンテンツフラグメントのバリエーションを取得するには、`includeVariations` フィルターは `true` に設定する必要があります。

   >[!CAUTION]
   >フィルター `includeVariations` は、システム生成フィールド `_variation` と併用できません。

* 論理和（OR）を使用する場合：
   * ` _logOp: OR` を使用します
   * [サンプルクエリ - 「Jobs」または「Smith」という名前を持つすべての人物](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-all-persons-jobs-smith)を参照してください

* 論理積（AND）も存在しますが、（多くの場合）暗黙的です

* コンテンツフラグメントモデル内のフィールドに対応するフィールド名に対してクエリを実行できます
   * [サンプルクエリ - ある会社の CEO と従業員の詳細](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-full-details-company-ceos-employees)を参照してください

* モデルのフィールドに加えて、次のようなシステム生成フィールドがあります（フィールド名の先頭にアンダースコアが付きます）。

   * コンテンツの場合：

      * `_locale`：言語を表示します（言語マネージャーに基づく）
         * [特定ロケールの複数のコンテンツフラグメントのサンプルクエリ](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-multiple-fragments-given-locale)を参照してください
      * `_metadata`：フラグメントのメタデータを表示します
         * [メタデータのサンプルクエリ - 「GB」という賞のメタデータのリスト](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-metadata-awards-gb)を参照してください
      * `_model`：コンテンツフラグメントモデル（パスとタイトル）のクエリを許可します
         * [モデルからのコンテンツフラグメントモデルのサンプルクエリ](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-content-fragment-model-from-model)を参照してください
      * `_path`：リポジトリ内のコンテンツフラグメントへのパス
         * [サンプルクエリ - 1 つの特定の都市フラグメント](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)を参照してください
      * `_reference`：参照（リッチテキストエディターでのインライン参照など）を表示します
         * [プリフェッチされた参照を含んだ複数のコンテンツフラグメントのサンプルクエリ](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-multiple-fragments-prefetched-references)を参照してください
      * `_variation`：コンテンツフラグメント内の特定のバリエーションを表示します

         >[!NOTE]
         >
         >指定されたバリエーションがコンテンツフラグメントに対して存在しない場合、マスターバリエーションが（フォールバック）デフォルトとして返されます。

         >[!CAUTION]
         >システム生成フィールド `_variation` は、フィルター `includeVariations` と併用できません。

         * [サンプルクエリ - 名前付きバリエーションを持つすべての都市](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-cities-named-variation)を参照してください
      * `_tags`：タグを含むコンテンツフラグメントまたはバリエーションの ID を表示する `cq:tags` 識別子の配列です。

         * [サンプルクエリ - 市区町村の区切り文字としてタグ付けされた、すべての都市の名前](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-names-all-cities-tagged-city-breaks)を参照してください。
         * 詳しくは、[特定のタグが添付された、任意のモデルのコンテンツフラグメントバリエーションのサンプルクエリ](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-fragment-variations-given-model-specific-tag)を参照してください。

         >[!NOTE]
         >
         >また、コンテンツフラグメントのメタデータを一覧表示して、タグをクエリできます。
   * 操作の場合：

      * `_operator`：特定の演算子（`EQUALS`、`EQUALS_NOT`、`GREATER_EQUAL`、`LOWER`、`CONTAINS`、`STARTS_WITH`）を適用します
         * [サンプルクエリ - 「Jobs」という名前を持たないすべての人物](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-all-persons-not-jobs)を参照してください
         * [サンプルクエリ - `_path` が特定のプレフィックスで始まるすべてのアドベンチャーを参照してください](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-all-adventures-cycling-path-filter)
      * `_apply`：特定の条件（例：`AT_LEAST_ONCE`）を適用します
         * [サンプルクエリ - 少なくとも 1 回は現れる項目を含んだ配列をフィルタリング](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-array-item-occur-at-least-once)を参照してください
      * `_ignoreCase`：クエリの実行時に大文字と小文字を区別しません
         * [サンプルクエリ - 名前に SAN が含まれるすべての都市（大文字と小文字を区別しない場合）](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-all-cities-san-ignore-case)を参照してください











* GraphQL のユニオン型がサポートされています

   * `... on` を使用します
      * [特定モデルのコンテンツフラグメントのうちコンテンツ参照を含んだものを取得するサンプルクエリ](/help/assets/content-fragments/content-fragments-graphql-samples.md#sample-wknd-fragment-specific-model-content-reference)を参照してください

* ネストされたフラグメントに対するクエリ時のフォールバック：

   * 要求されたバリエーションがネストされたフラグメントに存在しない場合、 **マスター** バリエーションが返されます。

<!--
## Persisted Queries (Caching) {#persisted-queries-caching}

After preparing a query with a POST request, it can be executed with a GET request that can be cached by HTTP caches or a CDN.

This is required as POST queries are usually not cached, and if using GET with the query as a parameter there is a significant risk of the parameter becoming too large for HTTP services and intermediates.

Persisted queries must always use the endpoint related to the [appropriate Sites configuration](#graphql-aem-endpoint); so they can use either, or both:

* The Global configuration and endpoint
  The query has access to all Content Fragment Models.
* Specific Sites configuration(s) and endpoint(s)
  Creating a persisted query for a specific Sites configuration requires a corresponding Sites-configuration-specific endpoint (to provide access to the related Content Fragment Models). 
  For example, to create a persisted query specifically for the WKND Sites configuration, a corresponding WKND-specific Sites configuration, and a WKND-specific endpoint must be created in advance.

>[!NOTE]
>
>See [Enable Content Fragment Functionality in Configuration Browser](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) for more details.
>
>The **GraphQL Persistence Queries** need to be enabled, for the appropriate Sites configuration. 

For example, if there is a particular query called `my-query`, which uses a model `my-model` from the Sites configuration `my-conf`:

* You can create a query using the `my-conf` specific endpoint, and then the query will be saved as following: 
`/conf/my-conf/settings/graphql/persistentQueries/my-query`
* You can create the same query using `global` endpoint, but then the query will be saved as following:
`/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>These are two different queries - saved under different paths. 
>
>They just happen to use the same model - but via different endpoints.


Here are the steps required to persist a given query:

1. Prepare the query by PUTing it to the new endpoint URL `/graphql/persist.json/<config>/<persisted-label>`.

   For example, create a persisted query:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. At this point, check the response.

   For example, check for success:

     ```xml
     {
       "action": "create",
       "configurationName": "wknd",
       "name": "plain-article-query",
       "shortPath": "/wknd/plain-article-query",
       "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
     }
     ```

1. You can then replay the persisted query by GETing the URL `/graphql/execute.json/<shortPath>`.

   For example, use the persisted query:

   ```xml
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Update a persisted query by POSTing to an already existing query path.

   For example, use the persisted query:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. Create a wrapped plain query.

   For example:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Create a wrapped plain query with cache control.

   For example:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. Create a persisted query with parameters:

   For example:

   ```xml
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```

1. Executing a query with parameters.

   For example:

   ```xml
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"

   $ curl -X GET \
       "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters;apath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   ```

1. To execute the query on publish, the related persist tree need to replicated

   * Using a POST for replication:

     ```xml
     $curl -X POST   http://localhost:4502/bin/replicate.json \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -F path=/conf/wknd/settings/graphql/persistentQueries/plain-article-query \
       -F cmd=activate
     ```

   * Using a package:
     1. Create a new package definition.
     1. Include the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).
     1. Build the package.
     1. Replicate the package.

   * Using replication/distribution tool.
     1. Go to the Distribution tool.
     1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

   * Using a workflow (via workflow launcher configuration):
     1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).

1. Once the query configuration is on publish, the same principles apply, just using the publish endpoint.

   >[!NOTE]
   >
   >For anonymous access the system assumes that the ACL allows "everyone" to have access to the query configuration.
   >
   >If that is not the case it will not be able to execute.

   >[!NOTE]
   >
   >Any semicolons (";") in the URLs need to be encoded.
   >
   >For example, as in the request to Execute a persisted query:
   >
   >```xml
   >curl -X GET \ "http://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3bapath=%2fcontent2fdam2fwknd2fen2fmagazine2falaska-adventure2falaskan-adventures;withReference=false"
   >```

## Querying the GraphQL endpoint from an External Website {#query-graphql-endpoint-from-external-website}

To access the GraphQL endpoint from an external website you need to configure the:

* [CORS Filter](#cors-filter)
* [Referrer Filter](#referrer-filter)
-->

### CORS フィルター {#cors-filter}

>[!NOTE]
>
>AEM での CORS リソース共有ポリシーについて詳しくは、[クロスオリジンリソース共有（CORS）について](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=ja#understand-cross-origin-resource-sharing-(cors))を参照してください。

GraphQL エンドポイントにアクセスするには、顧客の Git リポジトリーに CORS ポリシーを設定する必要があります。それには、目的のエンドポイントに適した OSGi CORS 設定ファイルを追加します。

この設定では、アクセスを許可する必要がある信頼できる Web サイトオリジン `alloworigin` または `alloworiginregexp` を指定する必要があります。

例えば、`https://my.domain` の GraphQL エンドポイントと永続クエリのエンドポイントへのアクセスを許可するには、以下を使用します。

```xml
{
  "supportscredentials":true,
  "supportedmethods":[
    "GET",
    "HEAD",
    "POST"
  ],
  "exposedheaders":[
    ""
  ],
  "alloworigin":[
    "https://my.domain"
  ],
  "maxage:Integer":1800,
  "alloworiginregexp":[
    ""
  ],
  "supportedheaders":[
    "Origin",
    "Accept",
    "X-Requested-With",
    "Content-Type",
    "Access-Control-Request-Method",
    "Access-Control-Request-Headers"
  ],
  "allowedpaths":[
    "/content/_cq_graphql/global/endpoint.json",
    "/graphql/execute.json/.*"
  ]
}
```

エンドポイントのバニティーパスを設定した場合は、`allowedpaths` でも使用できます。

### リファラーフィルター {#referrer-filter}

CORS 設定に加えて、サードパーティホストからのアクセスを許可するために、リファラーフィルターを設定する必要があります。

それには、以下を行う適切な OSGi Referrer Filter 設定ファイルを追加します。

* 信頼できる Web サイトのホスト名（`allow.hosts` または `allow.hosts.regexp`）を指定する。
* この名前のホストに対するアクセスを許可する。

例えば、リファラー `my.domain` を持つリクエストにアクセスを許可するには、次の操作を行います。

```xml
{
    "allow.empty":false,
    "allow.hosts":[
      "my.domain"
    ],
    "allow.hosts.regexp":[
      ""
    ],
    "filter.methods":[
      "POST",
      "PUT",
      "DELETE",
      "COPY",
      "MOVE"
    ],
    "exclude.agents.regexp":[
      ""
    ]
}
```

>[!CAUTION]
>
>以下は顧客の責任で行う必要があります。
>
>* 信頼できるドメインにのみアクセスを許可する
>* 機密情報が公開されていないことを確認する
>* ワイルドカードの [*] 構文を使用しない。これを使用すると、GraphQL エンドポイントへの認証済みアクセスが無効になり、エンドポイントが世界中に公開されることになります。


>[!CAUTION]
>
>（**有効**&#x200B;になっているコンテンツフラグメントモデルから派生した）すべての GraphQL [スキーマ](#schema-generation)は、GraphQL エンドポイントを通じて読み取り可能です。
>
>つまり、漏洩するおそれがあるので、機密データが使用可能になっていないことを確認する必要があります。例えば、これには、モデル定義のフィールド名として存在する可能性のある情報が含まれます。

## 認証 {#authentication}

[コンテンツフラグメントに対するリモート AEM GraphQL クエリの認証](/help/assets/content-fragments/graphql-authentication-content-fragments.md)を参照してください。

<!-- to be addressed later -->

<!--
## Sorting {#sorting}
-->

<!-- to be addressed later -->

<!--
## Paging {#paging}
-->

## FAQ {#faqs}

次のような質問が寄せられました。

1. **Q**：「*AEM 用 GraphQL API と Query Builder API の違いは何ですか？*」

   * **A**：「AEM GraphQL API *は JSON 出力の完全な制御が可能であり、コンテンツをクエリするための業界標準になっています。今後、AEM GraphQL API への投資が計画されています。*」

## チュートリアル - AEM ヘッドレスと GraphQL をはじめる前に {#tutorial}

実践的なチュートリアルを探している場合は、AEM の GraphQL API を使用し、外部アプリで使用するコンテンツをヘッドレス CMS シナリオで構築して公開する方法を示す「[AEM ヘッドレスと GraphQL をはじめる前に](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=ja)」のエンドツーエンドのチュートリアルをご覧ください。
