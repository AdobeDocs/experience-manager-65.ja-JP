---
title: コンテンツフラグメントへのアクセスとヘッドレス配信クイック開始ガイド
description: AEM Assets REST API を使用して、コンテンツフラグメントと、コンテンツフラグメントコンテンツのヘッドレス配信用の GraphQL API を管理する方法について説明します。
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
source-git-commit: 6c75af3957c319c38177cd62c90e781a982ba91b
workflow-type: ht
source-wordcount: '532'
ht-degree: 100%

---

# コンテンツフラグメントへのアクセスとヘッドレス配信クイック開始ガイド {#accessing-delivering-content-fragments}

AEM Assets REST API を使用して、コンテンツフラグメントと、コンテンツフラグメントコンテンツのヘッドレス配信用の GraphQL API を管理する方法について説明します。

## GraphQL API と Assets REST API とは {#what-are-the-apis}

[コンテンツフラグメントはいくつか作成したので、AEM API](create-content-fragment.md) を使用してそれらをヘッドレスで配信できます。

* [GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md) API を使用すると、コンテンツフラグメントにアクセスして配信するリクエストを作成できます。
   * これを使用するには、[AEM でエンドポイントを定義して有効にする必要があり](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint)、必要に応じて [GraphiQL インターフェイスをインストールする必要があります](/help/assets/content-fragments/graphql-api-content-fragments.md#installing-graphiql-interface)。
* [アセット REST API](/help/assets/assets-api-content-fragments.md) を使用すると、コンテンツフラグメント（およびその他のアセット）を作成および変更できます。

このガイドの残りの部分では、GraphQL へのアクセスとコンテンツフラグメントの配信について説明します。

## GraphQL を使用したコンテンツフラグメントの配信方法 {#how-to-deliver-a-content-fragment}

情報アーキテクトは、コンテンツを配信するために、チャネルエンドポイント用のクエリを設計する必要があります。一般に、これらのクエリは、モデルやエンドポイントごとに 1 回だけ作成する必要があります。この「はじめる前に」ガイドの目的上、1 つだけ作成します。

1. AEM にログインし、GraphiQL インターフェイスにアクセスします。
   * 例：`https://<host>:<port>/content/graphiql.html`

1. GraphiQL は、GraphQL のブラウザー内のクエリエディターです。クエリを構築して、コンテンツフラグメントを取得し、それらを JSON としてヘッドレスに配信できます。
   * 左側のパネルでは、クエリを作成できます。
   * 右側のパネルに結果が表示されます。
   * クエリエディターは、コード補完機能とホットキーを備えており、クエリを簡単に実行できます。
      ![GraphiQL エディター](../assets/graphiql.png)

1. 作成したモデルが `person` で `firstName`、`lastName`、`position` の各フィールドを持つ場合は、単純なクエリを構築して、コンテンツフラグメントのコンテンツを取得できます。

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

1. 左側のパネルにクエリを入力します。
   ![GraphiQL クエリ](../assets/graphiql-query.png)

1. 「**クエリを実行**」ボタンをクリックするか `Ctrl-Enter` ホットキーを使用すると、結果が JSON として右側のパネルに表示されます。
   ![GraphiQL の結果](../assets/graphiql-results.png)

1. 以下をクリックします。
   * ページの右上にある&#x200B;**ドキュメント**。文脈依存ドキュメントが表示され、独自のモデルに適合するクエリの構築に役立ちます。
   * 上部のツールバーにある&#x200B;**履歴**。以前のクエリが表示されます。
      ![GraphiQL ドキュメント](../assets/graphiql-documentation.png)

GraphQL を使用すると、特定のデータセットや個々のデータオブジェクトだけでなく、オブジェクトの特定の要素、ネストされた結果、クエリ変数のオファーサポートなどをターゲットできる構造化クエリが可能です。

GraphQL では、反復的な API リクエストと過剰な配信を回避でき、代わりに単一の API クエリに対するレンダリングに必要なものを一括配信できます。結果の JSON を使用して、他のサイトやアプリにデータを配信できます。

## 次の手順 {#next-steps}

これで作業は完了です。AEM のヘッドレスコンテンツ管理に関する基本的な内容を説明しました。もちろん、利用可能な機能の包括的な理解を深めるためのリソースは他にもたくさんあります。 

* **[設定ブラウザー](create-configuration.md)** - AEM 設定ブラウザーの詳細
* **[コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)** - コンテンツフラグメントの作成と管理に関する詳細
* **[AEM Assets HTTP API でサポートされるコンテンツフラグメント](/help/assets/assets-api-content-fragments.md)** - CRUD 操作（作成、読み取り、更新、削除）を介して HTTP API 経由で直接 AEM コンテンツにアクセスする方法の詳細
* **[GraphQL API](/help/assets/content-fragments/graphql-api-content-fragments.md)** - コンテンツフラグメントをヘッドレスで配信する方法の詳細
