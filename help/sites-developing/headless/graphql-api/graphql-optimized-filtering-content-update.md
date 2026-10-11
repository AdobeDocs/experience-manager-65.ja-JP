---
title: 最適化された GraphQL フィルタリング用コンテンツフラグメントの更新
description: ヘッドレスコンテンツ配信に最適化された Adobe Experience Manager の GraphQL フィルタリング用にコンテンツフラグメントを更新する方法について説明します。
exl-id: d78ec052-c091-49ca-9f36-a3d24eb9edd5
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
  - id: d429a63e-ade4-4117-b04e-9b996d1c94ef
    internal-label: Integrations
  - id: c124fa01-25c5-42ec-adf6-21d1c114058b
    internal-label: Developer tools
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
  - id: a02b73a7-bdfc-4225-bdfd-69f7891ab55e
    internal-label: GraphQL
  - id: d781bc8f-52af-43f6-84d0-b73e59a130d5
    internal-label: Persisted queries
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 93%
---
# 最適化された GraphQL フィルタリング用コンテンツフラグメントの更新 {#updating-content-fragments-for-optimized-graphql-filtering}

GraphQL フィルターのパフォーマンスを最適化するには、コンテンツフラグメントを更新する手順を実行する必要があります。

>[!NOTE]
>
>コンテンツフラグメントを更新した後、[GraphQL クエリの最適化](/help/sites-developing/headless/graphql-api/graphql-optimization.md)についての推奨事項に従うことができます。

## 前提条件 {#prerequisites}

AEMの6.5.17.0 リリース以上が必要です。

## コンテンツフラグメントの更新 {#updating-content-fragments}

この手続きを実行するには、次の手順に従います。

1. **コンテンツフラグメント移行ジョブ設定** の [OSGi 設定を指定します](/help/sites-deploying/configuring-osgi.md)。

   ![OSGi コンテンツフラグメント移行ジョブ設定](assets/cfm-graphql-update-01.png "OSGi コンテンツフラグメント移行ジョブ設定")

1. ダイアログで、これら 2 つのパラメーターを次のように設定します。

   * **ContentFragmentMigration:Enabled** : `1`
   * **ContentFragmentMigration:Enforce** : `1`

1. 指定した値を&#x200B;**保存**&#x200B;します。更新手続きが開始されます。

1. 手続きが完了するまで待ちます。 プロパティ `cfGlobalVersion` が `/content/dam` に表示され `1` に設定されたら、手続きは完了です。

1. OSGi 設定に戻って、手続きのアクティベートを解除します。

   **コンテンツフラグメント移行ジョブ設定**&#x200B;のダイアログで、これら 2 つのパラメータを次のように設定します。

   * **ContentFragmentMigration:Enabled** : `0`
   * **ContentFragmentMigration:Enforce** : `0`

## 制限事項 {#limitations}

次の制限事項に注意してください。

* GraphQL フィルターのパフォーマンスの最適化は、すべてのコンテンツフラグメントを完全に更新した後にのみ可能です（JCR ノード `/content/dam` の `cfGlobalVersion` のプロパティが存在することで示される）

* コンテンツフラグメントをコンテンツパッケージから読み込む場合（`crx/de` を使用）、更新手順を実行してから、更新手順が再実行されるまで、これらのコンテンツフラグメントは GraphQL クエリ結果で考慮されません。
