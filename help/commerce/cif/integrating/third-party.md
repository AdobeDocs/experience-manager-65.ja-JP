---
title: Commerce Integration Frameworkを使用したAEMとサードパーティCommerceの統合
description: エンタープライズビジネスでは、ストアフロントを強化するために、サードパーティのコマースソリューションを追加する必要がある場合があります。 I/O Runtimeを使用してサードパーティのコマースソリューションをAdobe Experience Managerに接続する場合、Commerce Integration Framework(CIF)をこのような統合シナリオで使用できます。
thumbnail: cif-third-party-architecture.jpg
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 4%

---

# Commerce Integration Frameworkを使用したAEMとサードパーティのコマースの統合{#aem-third-party}

非Adobeコマースソリューションの統合は、CIFの一般的なシナリオです。 様々なAPIとスキーマを持つサードパーティのソリューションは、統合レイヤーを介して接続できます。

## アーキテクチャ {#architecture}

全体的なアーキテクチャは次のとおりです。

![AEM非Magento/サードパーティアーキテクチャの概要](../assets//AEM_nonMagento_Architecture.png)

この統合レイヤーの目的は、サードパーティのAPIとスキーマを、Experience Manager外のサポートされているAdobeコマースGraphQL APIおよびスキーマに対してマッピングすることです。 このカプセル化により、Experience Manager内のコードを変更せずに、統合ロジックとシステムを更新できます。

## 統合のソリューション要件

Experience Managerがオンデマンドでデータを取得する際には、商品カタログのリアルタイムAPIが必要です。

>[!TIP]
>
>リアルタイムAPIが使用できない場合は、APIを使用した外部製品キャッシュを統合に使用する必要があります。 例[Magentoオープンソース](https://magento.com/products/magento-open-source)

完全なGraphQLスキーマを実装する必要はありません。必要なユースケースを有効にするには、スキーマのオブジェクトだけを使用します。

## バックエンドの使用例

CIFは、リアルタイムの商品カタログアクセスおよび商品体験管理ツールでExperience Managerを拡張します。 このシームレスな統合により、作成者は、コンテンツのコンテキストを離れることなく、必要に応じて埋め込みUIを使用してコマースデータにアクセスできます。

これらのユースケースのロックを解除するには、製品カタログAPIの統合が必要です。

## フロントエンドの使用例

[AEM CIFコア](https://github.com/adobe/aem-core-cif-components) コンポーネントは、CIFでサポートされているAdobeコマースAPIを使用してデータを取得し、交換します。コンポーネントを再利用するには、それぞれのAPIを実装する必要があります。

パフォーマンスに重要なクライアント側のコンポーネントは、遅延を回避するために、サードパーティのソリューションと直接通信することをお勧めします。

## 統合の開発{#develop-integration}

統合層には[Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html)を使用することをお勧めします。 サードパーティのCIFアドオンに含まれます。 マイクロサービスに似たアプローチで機能するので、複数のソリューションを容易に統合するのに適しています。

[リファレンス実装](https://github.com/adobe/commerce-cif-graphql-integration-reference)は、コマースソリューションへの統合を構築するための最初のポイントです。 GraphQLをサポートしますが、RESTなど他のタイプのAPIと統合することもできます。

サードパーティのレイヤー（Mulesoftなど）が使用可能な場合や、統合がサードパーティのソリューションの上に構築される場合は、この統合レイヤーは不要です。
