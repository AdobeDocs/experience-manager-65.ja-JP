---
title: コマース統合フレームワークを使用したAEMとAdobeのコマース(Magento)の統合
description: AEMとAdobeコマース(Magento)は、コマース統合フレームワーク(CIF)を使用してシームレスに統合されます。 CIF を使用すると、AEM は Magento インスタンスにアクセスし、GraphQL を介して Magento と通信できます。また、AEM オーサーは、製品とカテゴリの選択機能と製品コンソールを使用して、Magento からオンデマンドで取得した製品とカテゴリデータを参照できます。さらに、CIF には標準搭載のストアフロントが用意されており、コマースプロジェクトの迅速化に役立ちます。
thumbnail: aem-magento-architecture.jpg
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 43%

---

# コマース統合フレームワークを使用したAEMとAdobeのコマース(Magento)の統合{#aem-magento-framework}

Experience ManagerとAdobeコマース(Magento)は、コマース統合フレームワーク(CIF)を使用してシームレスに統合されます。 CIFを使用すると、AEMはAdobeコマースの[GraphQL API](https://devdocs.magento.com/guides/v2.4/graphql/)を使用して、コマースインスタンスに直接アクセスし、通信できます。

## アーキテクチャの概要 {#overview}

全体的なアーキテクチャは次のとおりです。

![CIF アーキテクチャの概要](../assets/AEM_Magento_Architecture.png)

CIF内では、サーバー側とクライアント側の通信パターンがサポートされます。
サーバー側API呼び出しは、組み込みの汎用[GraphQLクライアント](https://github.com/adobe/commerce-cif-graphql-client)と、コマースGraphQLスキーマ用に生成されたデータモデルの[セット](https://github.com/adobe/commerce-cif-magento-graphql)を組み合わせて使用して実装されます。 また、GraphQL クエリや GQL 形式のミューテーションも使用できます。

[React](https://reactjs.org/) を使用して構築されるクライアントサイドコンポーネントの場合は、[Apollo Client](https://www.apollographql.com/docs/react/) が使用されます。

## AEM CIF コアコンポーネントのアーキテクチャ {#cif-core-components}

![AEM CIF コアコンポーネントのアーキテクチャ](../assets/cif-component-architecture.jpg)

[AEM CIFコアコンポー](https://github.com/adobe/aem-core-cif-components) ネントは、 [AEM WCMコアコンポーネント](https://github.com/adobe/aem-core-wcm-components)と同様のデザインパターンとベストプラクティスに従っています。

AEM CIFコアコンポーネントのAdobeコマースとのビジネスロジックおよびバックエンド通信は、Slingモデルに実装されています。 プロジェクト固有の要件を満たすためにこのロジックをカスタマイズする必要がある場合は、Slingモデルの委任パターンを使用できます。

>[!TIP]
>
>[AEM CIF コアコンポーネントのカスタマイズ](../customizing/customize-cif-components.md)ページには、CIF コアコンポーネントのカスタマイズ方法に関する詳細な例とベストプラクティスが記載されています。

プロジェクト内では、AEM CIFコアコンポーネントとカスタムプロジェクトコンポーネントは、Slingのコンテキスト対応設定を使用して、AEMページに関連付けられたAdobeコマースストア用に設定されたクライアントを簡単に取得できます。
