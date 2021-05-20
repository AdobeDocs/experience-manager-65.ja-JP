---
title: e コマースの概要
seo-title: e コマースの概要
description: AEM の汎用 e コマースは、標準インストールの一部として提供され、e コマースフレームワークのすべての機能を含みます。
seo-description: AEM の汎用 e コマースは、標準インストールの一部として提供され、e コマースフレームワークのすべての機能を含みます。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
feature: コマース統合フレームワーク
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 57%

---

# e コマースの概要{#ecommerce-overview}

AEM の汎用 e コマースは、標準インストールの一部として提供され、e コマースフレームワークのすべての機能を含みます。

アドビでは、2 つのバージョンの Commerce 統合フレームワークを提供しています。

|  | CIF オンプレミス | CIF クラウド |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| サポートされている AEM バージョン | AEM オンプレミスまたは AMS 6.x | AEM AMS 6.4 および 6.5 |
| バックエンド | - AEM、Java <br> — モノリシック統合、ビルド前マッピング（テンプレート）<br> - JCRリポジトリ | -Magento<br>- JavaおよびJavaScript <br>- JCRリポジトリに保存されたコマースデータはありません |
| フロントエンド | AEM サーバー側によってページをレンダリング | 混在型ページアプリケーション（ハイブリッドレンダリング） |
| 製品カタログ | - AEM <br>の製品インポーター、エディター、キャッシュ — AEMまたはプロキシページを含む通常のカタログ |  — 製品のインポートなし<br> — 汎用テンプレート<br> — コネクタを介したオンデマンドデータ |
| スケーラビリティ |  — 最大で数百万個の製品をサポートできます（使用例によって異なります）。<br> - Dispatcherでのキャッシュ |  — ボリューム制限なし<br> - DispatcherまたはCDNでのキャッシュ |
| 標準化されたデータモデル | 不可 | あり。Magento GraphQL スキーマ |
| 入手方法 | はい：<br> - SAPCommerce Cloud(AEM 6.4とHybris 5をサポートするように更新（デフォルト）、Hybris 4 <br>- SalesforceCommerce Cloud(AEM 6.4をサポートするオープンソースのコネクタ)との互換性を維持) | あり。GitHub 経由のオープンソース。<br>Magento Commerce（Magento 2.3.2（デフォルト）をサポート、Magento 2.3.1 と互換性あり） |
| 用途 | 限定的な使用例：小さな静的カタログの読み込みが必要な場合 | ほとんどの使用例で好ましいソリューション |


## その他の実装のデプロイ  {#deploying-other-implementations}

AEMとMagentoの場合は、[AEMとMagentoの統合](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)を参照してください。[コマース統合フレームワーク](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html)を使用します。

>[!NOTE]
>
>e コマースの実装の概念および管理について詳しくは、[e コマースの管理](/help/commerce/cif-classic/administering/ecommerce.md)を参照してください。
>
>eコマース機能の拡張について詳しくは、[eコマースの開発](/help/commerce/cif-classic/developing/ecommerce.md)を参照してください。

