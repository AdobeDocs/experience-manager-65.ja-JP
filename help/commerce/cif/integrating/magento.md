---
title: コマース統合フレームワークを使用した、AEM と Adobe Commerce（Magento）の統合
description: AEM と Adobe Commerce（Magento）は、コマース統合フレームワーク（CIF）を使用してシームレスに統合されます。CIF を使用すると、AEM は Magento インスタンスにアクセスし、GraphQL を介して Magento と通信できます。また、AEM オーサーは、製品とカテゴリの選択機能と製品コンソールを使用して、Magento からオンデマンドで取得した製品とカテゴリデータを参照できます。さらに、CIF には標準搭載のストアフロントが用意されており、コマースプロジェクトの迅速化に役立ちます。
thumbnail: aem-magento-architecture.jpg
exl-id: f843784c-5ff7-41d1-97c5-13facb8459b2
source-git-commit: 4d11b0f87abab5c15e41bd65a4bdc4d98fad6ab1
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 76%

---

# コマース統合フレームワークを使用した、AEM と Adobe Commerce（Magento）の統合 {#aem-magento-framework}

Experience Manager と Adobe Commerce（Magento）は、コマース統合フレームワーク（CIF）を使用してシームレスに統合されます。CIFを使用すると、AEMはAdobeコマースの[GraphQL API](https://devdocs.magento.com/guides/v2.4/graphql/)を使用して、コマースインスタンスに直接アクセスし、通信できます。

>[!NOTE]
>
> サポートされているGraphQL APIの最小バージョンは2.3.5です。一部の機能は、新しいバージョンでのみ、またはAdobeコマースエディションでのみサポートされています。

## アーキテクチャの概要 {#overview}

全体的なアーキテクチャは次のとおりです。

![CIF アーキテクチャの概要](../assets/AEM_Magento_Architecture.png)

CIF内では、サーバー側とクライアント側の通信パターンがサポートされます。
サーバー側API呼び出しは、組み込みの汎用[GraphQLクライアント](https://github.com/adobe/commerce-cif-graphql-client)と、コマースGraphQLスキーマ用に生成されたデータモデルの[セット](https://github.com/adobe/commerce-cif-magento-graphql)を組み合わせて使用して実装されます。さらに、GraphQLクエリやGQL形式のミューテーションも使用できます。

[React](https://reactjs.org/) を使用して構築されるクライアントサイドコンポーネントの場合は、[Apollo Client](https://www.apollographql.com/docs/react/) が使用されます。

## AEM CIF コアコンポーネントのアーキテクチャ {#cif-core-components}

![AEM CIF コアコンポーネントのアーキテクチャ](../assets/cif-component-architecture.jpg)

[AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)は、[AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components)と同様の設計パターンとベストプラクティスに従っています。

AEM CIF コアコンポーネントの Adobe Commerce とのビジネスロジックとバックエンドの通信は、Sling Model で実装されます。プロジェクト固有の要件を満たすために、このロジックをカスタマイズする必要がある場合は、Sling モデルの委任パターンを使用できます。

>[!TIP]
>
>[AEM CIF コアコンポーネントのカスタマイズ](../customizing/customize-cif-components.md)ページには、CIF コアコンポーネントのカスタマイズ方法に関する詳細な例とベストプラクティスが記載されています。

プロジェクト内では、AEM CIF コアコンポーネントとカスタムプロジェクトコンポーネントは、Sling Context-Aware 設定を使用して、AEM ページに関連付けられた Adobe Commerce ストア用に設定されたクライアントを簡単に取得できます。
