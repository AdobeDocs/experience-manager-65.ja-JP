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
feature: Commerce統合フレームワーク
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
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
| バックエンド | - AEM, Java <br> — モノリシック統合、ビルド前のマッピング（テンプレート）<br> - JCRリポジトリ | -Magento<br>- JavaとJavaScript <br>- JCRリポジトリにコマースデータが保存されていません。 |
| フロントエンド | AEM サーバー側によってページをレンダリング | 混在型ページアプリケーション（ハイブリッドレンダリング） |
| 製品カタログ |  — 製品インポーター、エディター、AEMでのキャッシュ<br>- AEMまたはプロキシページを含む通常のカタログ |  — 製品のインポートなし<br> — 汎用テンプレート<br> — コネクタ経由のオンデマンドデータ |
| スケーラビリティ |  — 数百万個までの製品をサポート可能（使用事例によって異なります） <br> — ディスパッチャーでのキャッシュ |  — ボリュームに制限がない<br> — ディスパッチャーまたはCDNのキャッシュ |
| 標準化されたデータモデル | いいえ | あり。Magento GraphQL スキーマ |
| 入手方法 | はい：<br> - SAPCommerce Cloud(AEM 6.4とHybris 5 （デフォルト）をサポートするように更新)、Hybris 4 <br>- SalesforceCommerce Cloud(AEM 6.4をサポートするようにオープンソースのコネクタ)との互換性を維持 | あり。GitHub 経由のオープンソース。<br>Magento Commerce（Magento 2.3.2（デフォルト）をサポート、Magento 2.3.1 と互換性あり） |
| 用途 | 限定的な使用例：小さい静的なカタログの読み込みが必要な場合 | ほとんどの使用例で好ましいソリューション |


## その他の実装のデプロイ  {#deploying-other-implementations}

AEMとMagentoについては、[Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html)を使用したAEMとMagentoの統合](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)を参照してください。[

>[!NOTE]
>
>e コマースの実装の概念および管理について詳しくは、[e コマースの管理](/help/sites-administering/ecommerce.md)を参照してください。
>
>eコマース機能の拡張について詳しくは、[eコマースの開発](/help/sites-developing/ecommerce.md)を参照してください。

