---
title: コマース統合フレームワーク（CIF）アドオンの主な変更点
description: 以前のバージョンと比較した、コマース統合フレームワーク（CIF）アドオンの主な変更点です。
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
source-git-commit: 78359fb8ecbcc0227ab5a3910175aed73d823902
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 100%

---

# コマース統合フレームワーク（CIF）アドオンの主な変更点{#notable-changes}

このドキュメントでは、主に CIF Classic（Quickstart）と CIF Open-source と呼ばれる、コマース統合フレームワーク（CIF）アドオンと古い CIF バージョンの重要な相違点について説明します。

## インストールとアップデート

AEM Package Manager で AEM CIF アドオンパッケージがインストールされ更新されます。

**以前の CIF バージョン**

* CIF Classic：インストールは不要で、CIF は Quickstart の一部でした。CIF のアップデートは、通常の AEM またはサービスパックのアップデートに含まれていました。
* CIF オープンソース：GitHub を介したインストールアップデートは、手動アップデートやメンテナンス作業の一部でした。

## エンドポイントの設定

エンドポイントは OSGi コンソールを介して設定されます。

**以前の CIF バージョン**

* CIF Classic：AEM の OSGi 設定を使用
* CIF Open-source：CIF 設定ブラウザーを使用

## CIF Venia プロジェクトのデプロイメント

プロジェクトは [GitHub AEM Guides - CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia) で入手可能で、デプロイメントは AEM Package Manager で行われます。

**以前の CIF バージョン**

* CIF Classic：AEM パッケージのインストールを使用

## 製品カタログデータ

製品カタログデータは、必要な GraphQL API をサポートする外部エンドポイントへのリアルタイム呼び出しを通じて、オンデマンドでリクエストされます。これらの API は、任意の日付のライブデータまたはステージングデータへのアクセスをサポートします。レプリケーションは不要です。

**以前の CIF バージョン**

* CIF Classic：ライブおよびステージングされた製品データは、完全または差分の製品読み込みを通じて AEM オーサー上の JCR に読み込まれ、保持されます。ライブ製品データが AEM パブリッシュにレプリケートされます。

## AEM レンダリングを使用した製品カタログエクスペリエンス

AEM は、製品やカテゴリに割り当てられた AEM カタログテンプレートを使用して、製品カタログエクスペリエンスをその場でレンダリングします。レプリケーションは不要です。

**以前の CIF バージョン**

* CIF Classic：AEM オーサーは、カタログのブループリントツールを使用して、各カテゴリ／製品の AEM ページを作成します。これらのページは AEM パブリッシュにレプリケートされます。

>[!NOTE]
>
>AEM Managed Service またはオンプレミスの AEM での CIF の使用方法に関する追加ドキュメントについては、[コマース統合フレームワーク](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html) を参照してください。
