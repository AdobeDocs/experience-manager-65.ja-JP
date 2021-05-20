---
title: コマース統合フレームワーク(CIF)アドオンの主な変更点
description: 古いCIFバージョンと比較した、 Commerce Integration Framework(CIF)アドオンの主な変更点です。
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32,c136763f-56aa-450e-8796-bc84bf6c205d
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 3%

---

# Commerce Integration Framework(CIF)アドオンの主な変更点{#notable-changes}

このドキュメントでは、主にCIF Classic（クイックスタート）とCIFオープンソースと呼ばれる、Commerce Integration Framework(CIF)アドオンと古いCIFバージョンの重要な違いについて説明します。

## インストールと更新

AEM CIFアドオンパッケージがインストールされ、AEM Package Managerで更新されます。

**以前のCIFバージョン**

* CIF Classic:インストールは不要で、CIFはクイックスタートの一部でした。 CIFの更新は、通常のAEMまたはサービスパックの更新に含まれていました
* CIFオープンソース：GitHubを使用したインストール。 更新は、手動更新/メンテナンス作業の一部でした。

## エンドポイントの設定

エンドポイントはOSGiコンソールを介して設定されます。

**以前のCIFバージョン**

* CIF Classic:AEMのOSGi設定を使用
* CIFオープンソース：CIF設定ブラウザーを使用

## CIF Veniaプロジェクトのデプロイメント

プロジェクトは[GitHub AEMガイド — CIF Veniaプロジェクト](https://github.com/adobe/aem-cif-guides-venia)で入手でき、AEMパッケージマネージャーを介してデプロイされます。

**以前のCIFバージョン**

* CIF Classic:AEMパッケージのインストールを使用

## 製品カタログデータ

製品カタログデータは、必要なGraphQL APIをサポートする外部エンドポイントへのリアルタイム呼び出しを通じて、オンデマンドでリクエストされます。 これらのAPIは、任意の日付でのライブデータまたはステージングデータへのアクセスをサポートします。 レプリケーションは不要。

**以前のCIFバージョン**

* CIF Classic:ライブおよびステージングされた製品データは、完全または差分の製品読み込みを通じてAEMオーサー上のJCRに読み込まれ、保持されます。 ライブ製品データがAEMパブリッシュにレプリケートされます。

## AEMレンダリングを使用した製品カタログエクスペリエンス

AEMは、製品やカテゴリに割り当てられたAEMカタログテンプレートを使用して、製品カタログのエクスペリエンスをその場でレンダリングします。 レプリケーションは不要。

**以前のCIFバージョン**

* CIF Classic:AEMオーサーは、カタログのブループリントツールを使用して、各カテゴリ/製品のAEMページを作成します。 これらのページはAEMパブリッシュにレプリケートされます。

>[!NOTE]
>
>AEM Managed ServiceまたはAEM On-PremiseでのCIFの使用方法に関する追加ドキュメントについては、[Commerce Integration Framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)を参照してください。
