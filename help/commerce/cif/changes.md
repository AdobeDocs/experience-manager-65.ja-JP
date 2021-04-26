---
title: Commerce Integration Framework (CIF)アドオンの注目すべき変更点
description: 古いCIFバージョンと比較したCommerce Integration Framework(CIF)アドオンの顕著な変更。
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32,c136763f-56aa-450e-8796-bc84bf6c205d
translation-type: tm+mt
source-git-commit: a8dba82029168660b84b085ab46d0406b19961ef
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 9%

---

# Commerce Integration Framework (CIF)アドオン{#notable-changes}に対する注目すべき変更

このドキュメントでは、主にCIF Classic(Quickstart)とCIF Open-sourceと呼ばれる、Commerce Integration Framework(CIF)アドオンと古いCIFバージョンとの重要な違いに焦点を当ててます。

## インストールとアップデート

AEM CIFアドオンパッケージがAEM package managerでインストールされ、更新されます。

**以前のCIFバージョン**

* CIF Classic:インストールは必要ありません。CIFはQuickstartの一部でした。 CIFのアップデートは、通常のAEMまたはサービスパックのアップデートの一部でした。
* CIF Open-source:GitHubを介したインストール。 アップデートは、手動アップデート/メンテナンス作業の一部でした。

## エンドポイントの設定

エンドポイントは、OSGiコンソールを介して設定されます。

**以前のCIFバージョン**

* CIF Classic:AEMでのOSGi設定を使用
* CIF Open-source:CIF設定ブラウザを使用

## CIFベニアプロジェクトの導入

プロジェクトは[GitHub AEMガイド — CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia)で利用可能。展開はパッケージAEM managerを介して行われます。

**以前のCIFバージョン**

* CIF Classic:AEMパッケージのインストールを使用

## 商品カタログデータ

必要なGraphQL APIをサポートする外部エンドポイントへのリアルタイム呼び出しを通じて、製品カタログデータがオンデマンドでリクエストされます。 これらのAPIは、任意の日にライブデータまたはステージデータへのアクセスをサポートします。 レプリケーションは必要ありません。

**以前のCIFバージョン**

* CIF Classic:製品のライブデータとステージデータが、完全または差分の製品インポートを通じて、AEM AuthorのJCRにインポートされて保持されます。 ライブ製品のデータがAEM Publishに複製されます。

## AEMレンダリングでの商品カタログのエクスペリエンス

AEMは、製品やカテゴリに割り当てられたAEMカタログテンプレートを使用して、製品カタログのエクスペリエンスをその場でレンダリングします。 レプリケーションは必要ありません。

**以前のCIFバージョン**

* CIF Classic:AEM Authorは、カタログのBluePrintツールを使用して、すべてのカテゴリ/製品のAEMページを作成します。 これらのページはAEM Publishに複製されます。

>[!NOTE]
>
>AEM Managed Service またはオンプレミスの AEM での CIF の使用方法に関する追加ドキュメントについては、[Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html) を参照してください。
