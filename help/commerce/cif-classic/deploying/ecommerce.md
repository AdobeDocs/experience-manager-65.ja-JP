---
title: eコマースの概要
description: AEM の汎用 e コマースは、標準インストールの一部として使用でき、e コマースフレームワークの全機能を提供します。
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
solution: Experience Manager,Commerce
role: Admin, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 97%
---
# e コマースの概要{#ecommerce-overview}

AEM の汎用 e コマースは、標準インストールの一部として使用でき、e コマースフレームワークの全機能を提供します。

アドビでは、2 つのバージョンの Commerce Integration Framework を提供しています。

|                         | CIF オンプレミス | CIF クラウド |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| サポートされている AEM バージョン | AEM オンプレミスまたは AMS 6.x | AEM AMS 6.4 と 6.5 |
| バックエンド | - AEM、Java™ <br> - モノリシック統合、ビルド前のマッピング（テンプレート）<br> - JCR リポジトリ | - Adobe Commerce <br>- Java と JavaScript <br>- JCR リポジトリには Commerce データは保存されません |
| フロントエンド | AEM サーバーサイドでレンダリングされたページ | 混在型ページアプリケーション（ハイブリッドレンダリング） |
| 製品カタログ | - AEMでの製品インポーター、エディター、キャッシュ <br>- AEM またはプロキシページを含む通常のカタログ | - 製品のインポートなし <br>- 汎用テンプレート <br> - コネクタを介したオンデマンドデータ |
| スケーラビリティ | - 数億個までの製品をサポート可能（ユースケースによって異なる） <br> - Dispatcher でのキャッシュ | - ボリューム制限なし <br>- Dispatcher または CDN でのキャッシュ |
| 標準化されたデータモデル | 不可 | 可、Adobe Commerce GraphQL スキーマ |
| 入手方法 | 可：<br> - SAP Commerce Cloud（AEM 6.4 と Hybris 5（デフォルト）をサポートし、Hybris 4 との互換性を維持するように更新された拡張機能）<br>- Salesforce Commerce Cloud（AEM 6.4 をサポートする オープンソースコネクタ） | はい、GitHub経由でオープンソースで行います。<br> Adobe Commerce（2.3.2（デフォルト）をサポート、2.3.1 と互換性あり） |
| 用途 | 限定的なユースケース：小規模なシナリオでは、必要に応じて静的カタログを読み込みます | 大部分のユースケースで推奨されるソリューション |


## 他の実装のデプロイ {#deploying-other-implementations}

AEM と Adobe Commerce については、[Commerce Integration Framework](/help/commerce/cif/introduction.md) を使用した [AEM と Adobe Commerce の統合](/help/commerce/cif/integrating/magento.md)を参照してください。

>[!NOTE]
>
>e コマースの実装の概念および管理について詳しくは、[e コマースの管理](/help/commerce/cif-classic/administering/ecommerce.md)を参照してください。
>
>e コマース機能の拡張について詳しくは、[e コマースの開発](/help/commerce/cif-classic/developing/ecommerce.md)を参照してください。
