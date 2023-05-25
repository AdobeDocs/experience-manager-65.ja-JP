---
title: 最適化された GraphQL フィルタリング用コンテンツフラグメントの更新
description: ヘッドレスコンテンツ配信のために、Adobe Experience Manager で最適化された GraphQL フィルタリング用にコンテンツフラグメントを更新する方法について説明します。
source-git-commit: 1481d613783089046b44d4652d38f7b4b16acc4d
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 42%

---


# 最適化された GraphQL フィルタリング用コンテンツフラグメントの更新 {#updating-content-fragments-for-optimized-graphql-filtering}

GraphQLフィルターのパフォーマンスを最適化するには、コンテンツフラグメントを更新する手順を実行します。

>[!NOTE]
>
>コンテンツフラグメントを更新した後、次の推奨事項に従うことができます。 [GraphQLクエリの最適化](/help/sites-developing/headless/graphql-api/graphql-optimization.md).

## 前提条件 {#prerequisites}

AEMの 6.5.17.0リリース以降が存在することを確認します。

## コンテンツフラグメントの更新 {#updating-content-fragments}

この手順を実行するには、次の手順に従います。

1. [OSGi 設定の指定](/help/sites-deploying/configuring-osgi.md) の **コンテンツフラグメント移行ジョブ設定**:

   ![OSGi コンテンツフラグメント移行ジョブ設定](assets/cfm-graphql-update-01.png "OSGi コンテンツフラグメント移行ジョブ設定")

1. ダイアログで、次の 2 つのパラメータを設定します。

   * **ContentFragmentMigration:Enabled** : `1`
   * **ContentFragmentMigration:Enforce** : `1`

1. **保存** スペシフィケーション：更新手順が開始されます。

1. 手順が完了するまで待ちます。 プロパティが `cfGlobalVersion` 次の日に表示： `/content/dam` に設定されている `1`.

1. OSGi 設定に戻り、手順を非アクティブにします。

   のダイアログで、 **コンテンツフラグメント移行ジョブ設定** 次の 2 つのパラメーターを設定します。

   * **ContentFragmentMigration:Enabled** : `0`
   * **ContentFragmentMigration:Enforce** : `0`

## 制限事項 {#limitations}

次の制限事項に注意してください。

* GraphQL フィルターのパフォーマンスの最適化は、すべてのコンテンツフラグメントを完全に更新した後にのみ可能です（JCR ノード `/content/dam` の `cfGlobalVersion` のプロパティが存在することで示される）

* コンテンツフラグメントをコンテンツパッケージから読み込む場合（`crx/de` を使用）、更新手順を実行してから、更新手順が再実行されるまで、これらのコンテンツフラグメントは GraphQL クエリ結果で考慮されません。