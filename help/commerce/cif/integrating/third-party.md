---
title: コマース統合フレームワークを使用した AEM とサードパーティコマースの統合
description: 大規模企業では、ストアフロントを強化するために、追加のサードパーティ製コマースソリューションが必要になる場合があります。I/O Runtime を使用してサードパーティのコマースソリューションを Adobe Experience Manager に接続するような統合シナリオで、コマース統合フレームワーク（CIF）を使用できます。
thumbnail: cif-third-party-architecture.jpg
exl-id: e99899a4-df86-4108-991a-8b30d303a279
source-git-commit: 885d0763fca9ad4eab499081adca9b83875b27e1
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 100%

---

# コマース統合フレームワークを使用した AEM とサードパーティコマースの統合 {#aem-third-party}

Adobe Commerce 以外のソリューションの統合は、CIF の一般的なシナリオです。様々な API やスキーマを持つサードパーティソリューションは、統合レイヤーを介して接続できます。

## アーキテクチャ {#architecture}

全体的なアーキテクチャは次のとおりです。

![AEM と Magento 以外またはサードパーティとの統合のアーキテクチャ概要](../assets//AEM_nonMagento_Architecture.png)

この統合レイヤーの目的は、サードパーティの API とスキーマを、サポートされている Adobe Commerce GraphQL API と Experience Manager 外のスキーマにマッピングすることです。このカプセル化により、統合のロジックとシステムを、Experience Manager 内のコードを変更することなくアップデートできます。

## 統合のソリューション要件

Experience Manager はデータをオンデマンドで取得するため、製品カタログのリアルタイム API が必要です。

>[!TIP]
>
>リアルタイム API を使用できない場合は、API を使用した外部製品キャッシュを統合に使用する必要があります。例：[Magento オープンソース](https://business.adobe.com/jp/products/magento/open-source.html)

完全な GraphQL スキーマを実装する必要はありません。必要なユースケースを有効にするには、スキーマのオブジェクトだけを実装します。

## バックエンドの使用例

CIF は、製品カタログへのリアルタイムのアクセスと製品エクスペリエンス管理ツールで Experience Manager を拡張しています。このシームレスな統合により、作成者は、必要に応じて、コンテンツのコンテキストを離れることなく、組み込み UI を使用してコマースデータにアクセスできます。

これらのユースケースを可能にするには、製品カタログ API の統合が必要です。

## フロントエンドのユースケース

[AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)は、CIF でサポートされている Adobe Commerce API を使用してデータを取得および交換します。コンポーネントを再利用するには、それぞれの API を実装する必要があります。

パフォーマンスが重要なクライアントサイドのコンポーネントでは、サードパーティソリューションと直接通信して遅延を回避することが推奨されます。

## 統合の開発 {#develop-integration}

統合レイヤーには [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime.html) を使用することをお勧めします。これは、サードパーティ用の CIF アドオンに含まれています。マイクロサービスに似たアプローチがとられており、簡単に複数のソリューションを統合するのに適しています。

[参照実装](https://github.com/adobe/commerce-cif-graphql-integration-reference)は、コマースソリューションへの統合を構築するための出発点として最適です。GraphQL がサポートされていますが、REST などの他のタイプの API と統合することもできます。

この統合レイヤーは、サードパーティのレイヤー（Mulesoft など）が使用可能な場合や、統合がサードパーティのソリューションの上に構築される場合には必要ありません。

## 事前定義済みコネクタ {#connectors}

コネクタは、プロジェクトの良い出発点となります。これには、コマースソリューション固有の接続とデフォルトの API マッピングが付属しています。これらのコネクタは、サードパーティによって作成されており、アドビで維持管理されているわけではありません。詳しくは、それぞれのパートナーに問い合わせください。

* [SAP Commerce](https://github.com/diconium/commerce-cif-graphql-integration-hybris)（Diconium が作成）
* [Commercetools](https://github.com/diconium/commerce-cif-graphql-integration-commercetool)（Diconium が作成）

>[!TIP]
>
>コネクタは、プロジェクトでコマース統合を速めるのに役立ちますが、プラグアンドプレイではありません。エンタープライズコマースソリューションは通常、大幅にカスタマイズされており、カスタム統合が必要になります。コマースプラットフォーム、Adobe Commerce GraphQL スキーマおよび Adobe I/O Runtime に関する十分な知識が必要です。
