---
title: コンテンツフラグメントとヘッドレスクイック開始ガイドへのアクセスと配信
description: AEM Assets REST API を使用して、コンテンツフラグメントと、コンテンツフラグメントコンテンツのヘッドレス配信用の GraphQL API を管理する方法について説明します。
exl-id: 4664b3a4-4873-4f42-b59d-aadbfaa6072f
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Developer
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 100%

---

# コンテンツフラグメントとヘッドレスクイック開始ガイドへのアクセスと配信 {#accessing-delivering-content-fragments}

AEM Assets REST API を使用して、コンテンツフラグメントと、コンテンツフラグメントコンテンツのヘッドレス配信用の GraphQL API を管理する方法について説明します。

## GraphQL API と Assets REST API とは {#what-are-the-apis}

[コンテンツフラグメントはいくつか作成したので、AEM API](create-content-fragment.md) を使用してそれらをヘッドレスで配信できます。

* [GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) API を使用すると、コンテンツフラグメントにアクセスして配信するリクエストを作成できます。
   * これを使用するには、[AEM で エンドポイントを定義して有効にする必要があり](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint)、必要に応じて [GraphiQL インターフェイスをインストールする必要があります](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#installing-graphiql-interface)。
* [アセット REST API](/help/assets/assets-api-content-fragments.md) を使用すると、コンテンツフラグメント（およびその他のアセット）を作成および変更できます。

このガイドの残りの部分では、GraphQL へのアクセスとコンテンツフラグメントの配信について説明します。

## GraphQL を使用したコンテンツフラグメントの配信方法 {#how-to-deliver-a-content-fragment}

情報アーキテクトは、チャネルエンドポイントがコンテンツを配信するためのクエリを設計します。これらのクエリは、エンドポイントごと、モデルごとに 1 回だけ考慮してください。この入門ガイドでは、1 つだけ作成します。

1. AEM にログインし、[GraphiQL インターフェイス](/help/sites-developing/headless/graphql-api/graphiql-ide.md)にアクセスします。
   * 例：`http://<host>:<port>/aem/graphiql.html`

1. GraphiQL は、GraphQL のブラウザー内のクエリエディターです。クエリーを作成して、コンテンツフラグメントを取得し、それらを JSON としてヘッドレスに配信できます。
   * 左パネルで、クエリを作成できます。
   * 右側のパネルに結果が表示されます。
   * クエリエディターは、コード補完機能とホットキーを備えており、クエリを簡単に実行できます。
     ![GraphiQL エディター](assets/graphiql.png)

1. 作成したモデルが `person` で `firstName`、`lastName`、`position` の各フィールドを持つ場合は、単純なクエリーを構築して、コンテンツフラグメントのコンテンツを取得できます。

   ```text
   query 
   {
     personList {
       items {
         _path
         firstName
         lastName
         position
       }
     }
   }
   ```

1. 左パネルにクエリを入力します。
<!--
   ![GraphiQL query](assets/graphiql-query.png)
-->

1. 「**クエリを実行**」アイコン（右矢印）をクリックするか `Ctrl-Enter` ホットキーを使用すると、結果が JSON として右側のパネルに表示されます。
   ![GraphiQL の結果](assets/graphiql-results.png)

1. 以下をクリックします。
   * ページの右上にある&#x200B;**ドキュメント**&#x200B;をクリックすると、文脈依存ドキュメントが表示され、独自のモデルに適合したクエリを構築するのにに役立ちます。
   * 上部のツールバーにある&#x200B;**履歴**&#x200B;をクリックすると、以前のクエリが表示されます。
   * 「**名前を付けて保存**」と「**保存**」をクリックしてクエリを保存します。保存後は、**永続クエリ**&#x200B;パネルと「**パブリッシュ**」でクエリを一覧表示して取得できます。.
     ![GraphiQL ドキュメント](assets/graphiql-documentation.png)

GraphQL を使用すると、特定のデータセットや個々のデータオブジェクトをターゲットにするだけでなく、オブジェクトの特定の要素、ネストされた結果を配信したり、クエリ変数のサポートを提供したりできる構造化クエリが可能になります。

GraphQLは、繰り返しの API リクエストや過剰な配信を避けることができます。代わりに、単一の API クエリへの応答としてレンダリングに必要なものを正確に一括配信できます。結果の JSON を使用して、他のサイトやアプリにデータを配信できます。

## 次の手順 {#next-steps}

これで作業は完了です。AEM のヘッドレスコンテンツ管理に関する基本的な内容を説明しました。利用可能な機能の包括的な理解を深めるためのリソースは他にもたくさんあります。

* **[設定ブラウザー](create-configuration.md)** - AEM 設定ブラウザーの詳細
* **[コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)** - コンテンツフラグメントの作成と管理に関する詳細
* **[GraphiQL IDE](/help/sites-developing/headless/graphql-api/graphiql-ide.md)** - GraphiQL IDE の使用の詳細
* **[永続クエリ](/help/sites-developing/headless/graphql-api/persisted-queries.md)** - 永続クエリの詳細
* **[AEM Assets HTTP API でサポートされるコンテンツフラグメント](/help/assets/assets-api-content-fragments.md)** - CRUD 操作（作成、読み取り、更新、削除）を介して HTTP API 経由で直接 AEM コンテンツにアクセスする方法の詳細
* **[GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)** - コンテンツフラグメントをヘッドレスで配信する方法の詳細
