---
title: e コマースの概要
seo-title: e コマースの概要
description: AEM の汎用 e コマースは、標準インストールの一部として提供され、e コマースフレームワークのすべての機能を含みます。
seo-description: AEM の汎用 e コマースは、標準インストールの一部として提供され、e コマースフレームワークのすべての機能を含みます。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: 5d46836a8b7b66daa8f27bc6fad14319ab1f58a7

---


# e コマースの概要{#ecommerce-overview}

AEM の汎用 e コマースは、標準インストールの一部として提供され、e コマースフレームワークのすべての機能を含みます。

アドビでは、2 つのバージョンの Commerce 統合フレームワークを提供しています。

|  | CIF オンプレミス | CIF クラウド |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| サポートされている AEM バージョン | AEM オンプレミスまたは AMS 6.x | AEM AMS 6.4 および 6.5 |
| バックエンド | - AEM、Java <br> — モノリシック統合、ビルド前のマッピング（テンプレート）<br> - JCRリポジトリ | - Magento <br>- javaとJavaScript <br>- JCRリポジトリにコマースデータが保存されていません |
| フロントエンド | AEM サーバー側によってページをレンダリング | 混在型ページアプリケーション（ハイブリッドレンダリング） |
| 製品カタログ |  — 製品インポーター、エディター、AEMでのキャッシュ — AEMま <br>たはプロキシページを含む通常のカタログ |  — 製品のインポートな <br>し — 汎用テンプレ <br>ート — コネクタ経由のオンデマンドデータ |
| スケーラビリティ |  — 最大で数百万個の製品をサポート可能（使用事例に依存） <br> — ディスパッチャーでのキャッシュ |  — ボリューム制限な <br>し — ディスパッチャーまたはCDNでのキャッシュ |
| 標準化されたデータモデル | いいえ | あり。Magento GraphQL スキーマ |
| 利用可能場所 | <br> はい：- SAP Commerce Cloud(AEM 6.4およびHybris 5をサポートするように更新（デフォルト）。Hybris 4 <br>- Salesforce Commerce Cloud（AEM 6.4をサポートするためにオープンソースのコネクタ）との互換性を維持します。 | あり。GitHub 経由のオープンソース。<br>Magento Commerce（Magento 2.3.2（デフォルト）をサポート、Magento 2.3.1 と互換性あり） |
| 用途 | 使用例の制限：小さな静的カタログの読み込みが必要な場合 | ほとんどの使用例で好ましいソリューション |


## その他の実装のデプロイ {#deploying-other-implementations}

For AEM and Magento, please see [AEM and Magento integration](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md) using the [Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html).

>[!NOTE]
>
>e コマースの実装の概念および管理について詳しくは、[e コマースの管理](/help/sites-administering/ecommerce.md)を参照してください。
>
>For information about extending eCommerce capabilities, see [Developing eCommerce](/help/sites-developing/ecommerce.md).

