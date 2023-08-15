---
title: GraphQL のコンテンツフラグメントを使用したヘッドレスコンテンツ配信
description: ヘッドレスコンテンツ配信に AEM コンテンツフラグメントを GraphQL と共に使用する方法を説明します。
feature: Content Fragments
role: User
exl-id: 2debd678-2d73-41f2-b33c-c29d661f6a6b
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 91%

---

# GraphQL のコンテンツフラグメントを使用したヘッドレスコンテンツ配信 {#headless-content-delivery-using-content-fragments-with-graphQL}

Adobe Experience Manager (AEM) を使用すると、AEM GraphQL API（標準 GraphQL に基づいてカスタマイズされた実装）と共にコンテンツフラグメントを使用して、ご利用のアプリケーションで使用する構造化されたコンテンツをヘッドレスで配信できます。単一の API クエリをカスタマイズする機能を使用すると、レンダリングする必要のある特定のコンテンツを（単一の API クエリへの応答として）取得して配信できます。

<!--
>[!NOTE]
>
>See [Headless and AEM](/help/implementing/developing/headless/introduction.md) for an introduction to Headless Development for AEM Sites.
-->

>[!NOTE]
>
>GraphQL は現在 Adobe Experience Manager (AEM) の 2 つの（別々の）シナリオで使用されています。
>
>* [AEM Commerce は、GraphQL 経由でコマースプラットフォームのデータを使用します](/help/commerce/cif/integrating/magento.md)。
>* [AEM コンテンツフラグメントは、AEM GraphQL API（標準の GraphQL に基づいてカスタマイズされた実装）と連携して、アプリケーションで使用する構造化コンテンツを配信します](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)。

## ヘッドレス CMS {#headless-cms}

ヘッドレスコンテンツ管理システム（CMS）とは次のことを意味します。

* 「*ヘッドレスコンテンツ管理システム（ヘッドレス CMS）は、API経由でコンテンツにアクセスし、あらゆるデバイスで表示できるようにするコンテンツリポジトリとして一から構築された、バックエンド専用のコンテンツ管理システム（CMS）です。*」

  [ウィキペディア](https://en.wikipedia.org/wiki/Headless_content_management_system)を参照してください。

AEM のコンテンツフラグメントのオーサリングとは、次のことを意味します。

* コンテンツフラグメントを使用すると、主にフォーマットされたページに直接公開することを目的としていない（1:1）コンテンツを作成できます。

* コンテンツフラグメントのコンテンツは、コンテンツフラグメントモデルに従って、あらかじめ決められた方法で構造化されます。これにより、アプリケーションへのアクセスが簡素化され、コンテンツの処理が促進されます。

## GraphQL - 概要 {#graphql-overview}

GraphQL とは次のことを意味します。

* 「*...API のクエリ言語と、既存のデータを使用してこれらのクエリを満たすランタイムです。*」

  [GraphQL.org](https://graphql.org) を参照

The [AEM GraphQL API](#aem-graphql-api) を使用すると、 [コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)；の場合、各クエリは特定のモデルタイプに従っています。 返されたコンテンツは、アプリケーションで使用できます。

## AEM GraphQL API {#aem-graphql-api}

Adobe Experience では、標準 GraphQL API をカスタマイズした実装を開発しています。詳しくは、「[コンテンツフラグメントと共に使用する AEM GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)」を参照してください。

AEM GraphQL API の実装は、[GraphQL Java ライブラリ](https://graphql.org/code/#java)に基づいています。

## AEM GraphQL API で使用するコンテンツフラグメント {#content-fragments-use-with-aem-graphql-api}

[コンテンツフラグメント](#content-fragments)は、AEM クエリの GraphQL の基盤として次のように使用できます。

* ページに依存しないコンテンツをデザイン、作成、キュレーションおよび公開できます。
* [コンテンツフラグメントモデル](#content-fragments-models)は、定義されたデータタイプを使用して、必要な構造を提供します。
* モデルの定義時に使用できる[フラグメント参照](#fragment-references)を使用して、構造の追加のレイヤーを定義できます。

![GraphQL と共に使用するコンテンツフラグメント](assets/cfm-nested-01.png " GraphQL と共に使用するコンテンツフラグメント")

### コンテンツフラグメント {#content-fragments}

コンテンツフラグメント：

* 構造化コンテンツを含みます。

* 作成されるフラグメントの構造を事前定義する[コンテンツフラグメントモデル](#content-fragments-models)に基づいています。

### コンテンツフラグメントモデル {#content-fragments-models}

[コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)は、

* **有効**&#x200B;にされると、[スキーマ](https://graphql.org/learn/schema/)の生成に使用されます。

* GraphQL に必要なデータタイプとフィールドを提供します。アプリケーションが、可能なことだけを要求して期待するものを受け取るようにします。

* データタイプ&#x200B;**[フラグメント参照](#fragment-references)**&#x200B;は、別のコンテンツフラグメントを参照するためにモデル内で使用できるので、構造レベルを追加します。

### フラグメント参照 {#fragment-references}

**[フラグメント参照](/help/assets/content-fragments/content-fragments-models.md#fragment-reference-nested-fragments)**&#x200B;は、

* GraphQL との関連で特に興味深いものです。

* コンテンツフラグメントモデルの定義時に使用できる特定のデータタイプです。

* 特定のコンテンツフラグメントモデルに依存する別のフラグメントを参照します。

* 構造化データを取得できます。

   * **マルチフィード**&#x200B;として定義した場合、複数のサブフラグメントをプライムフラグメントで参照（取得）できます。

### JSON プレビュー {#json-preview}

コンテンツフラグメントモデルの設計と開発に役立つように、[JSON 出力](/help/assets/content-fragments/content-fragments-json-preview.md)をプレビューできます。

## AEM での GraphQL の使用方法 - サンプルコンテンツとサンプルクエリ {#learn-graphql-with-aem-sample-content-queries}

AEM GraphQL API の使い方の紹介は、「[AEM での GraphQL の使用方法 - コンテンツとクエリの例](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md)」を参照してください。

## チュートリアル - AEM ヘッドレスと GraphQL をはじめる前に

実践的なチュートリアルを探している場合は、AEM の GraphQL API を使用し、外部アプリで使用するコンテンツをヘッドレス CMS シナリオで構築して公開する方法を示す「[AEM ヘッドレスと GraphQL をはじめる前に](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=ja)」のエンドツーエンドのチュートリアルをご覧ください。
