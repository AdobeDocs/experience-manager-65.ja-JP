---
title: eコマースの概要
description: AEM の汎用 e コマースは、標準インストールの一部として使用でき、e コマースフレームワークの全機能を提供します。
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
source-git-commit: f349c8fd9c370ba589d217cd3b1d0521ae5c5597
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 92%

---

# e コマースの概要 {#ecommerce-overview}

AEM の汎用 e コマースは、標準インストールの一部として使用でき、e コマースフレームワークの全機能を提供します。

アドビでは、2 つのバージョンの Commerce 統合フレームワークを提供しています。

|                         | CIF オンプレミス | CIF クラウド |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| サポートされている AEM バージョン | AEM オンプレミスまたは AMS 6.x | AEM AMS 6.4 と 6.5 |
| バックエンド | - AEM, Java™ <br>  — モノリシック統合、ビルド前のマッピング（テンプレート）<br> - JCR リポジトリ | - Adobe Commerce <br>- Java と JavaScript <br>- JCR リポジトリには Commerce データは保存されません |
| フロントエンド | AEM サーバーサイドでレンダリングされたページ | 混在型ページアプリケーション（ハイブリッドレンダリング） |
| 製品カタログ | - AEMでの製品インポーター、エディター、キャッシュ <br>- AEM またはプロキシページを含む通常のカタログ | - 製品のインポートなし <br>- 汎用テンプレート <br> - コネクタを介したオンデマンドデータ |
| スケーラビリティ | - 数億個までの製品をサポート可能（ユースケースによって異なる） <br> - Dispatcher でのキャッシュ | - ボリューム制限なし <br>- Dispatcher または CDN でのキャッシュ |
| 標準化されたデータモデル | 不可 | 可、Adobe Commerce GraphQL スキーマ |
| 入手方法 | 可：<br> - SAP Commerce Cloud（AEM 6.4 と Hybris 5（デフォルト）をサポートし、Hybris 4 との互換性を維持するように更新された拡張機能）<br>- Salesforce Commerce Cloud（AEM 6.4 をサポートする オープンソースコネクタ） | GitHub を通じてオープンソースで使用可能。<br> Adobe Commerce（2.3.2（デフォルト）をサポート、2.3.1 と互換性あり） |
| 用途 | 限られた使用例：小さい場合に必要に応じて静的カタログを読み込む | 大部分のユースケースで推奨されるソリューション |


## 他の実装のデプロイ {#deploying-other-implementations}

AEM と Adobe Commerce については、[コマース統合フレームワーク](/help/commerce/cif/introduction.md)を使用した [AEM と Adobe Commerce の統合](/help/commerce/cif/integrating/magento.md)を参照してください。

>[!NOTE]
>
>e コマースの実装の概念および管理について詳しくは、[e コマースの管理](/help/commerce/cif-classic/administering/ecommerce.md)を参照してください。
>
>e コマース機能の拡張について詳しくは、[e コマースの開発](/help/commerce/cif-classic/developing/ecommerce.md)を参照してください。
