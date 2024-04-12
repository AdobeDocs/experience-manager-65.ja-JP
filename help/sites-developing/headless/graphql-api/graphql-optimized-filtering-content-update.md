---
title: 最適化された GraphQL フィルタリング用コンテンツフラグメントの更新
description: ヘッドレスコンテンツ配信のために、Adobe Experience Managerで最適化されたGraphQL フィルタリング用にコンテンツフラグメントを更新する方法について説明します。
exl-id: d78ec052-c091-49ca-9f36-a3d24eb9edd5
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Architect,Data Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 49%

---

# 最適化された GraphQL フィルタリング用コンテンツフラグメントの更新 {#updating-content-fragments-for-optimized-graphql-filtering}

GraphQL フィルターのパフォーマンスを最適化するには、コンテンツフラグメントを更新する手順を実行する必要があります。

>[!NOTE]
>
>コンテンツフラグメントを更新した後、[GraphQL クエリの最適化](/help/sites-developing/headless/graphql-api/graphql-optimization.md)についてのレコメンデーションに従うことができます。

## 前提条件 {#prerequisites}

6.5.17.0 リリース以降のAEMがあることを確認します。

## コンテンツフラグメントの更新 {#updating-content-fragments}

この手順を実行するには、以下の手順を実行します。

1. [OSGi 設定の指定](/help/sites-deploying/configuring-osgi.md) の場合 **コンテンツフラグメント移行ジョブの設定**:

   ![OSGi コンテンツフラグメント移行ジョブの設定](assets/cfm-graphql-update-01.png "OSGi コンテンツフラグメント移行ジョブの設定")

1. ダイアログで、これら 2 つのパラメーターを次のように設定します。

   * **ContentFragmentMigration：有効** : `1`
   * **ContentFragmentMigration：強制** : `1`

1. **保存** 仕様 – 更新手順が開始します。

1. 手順が完了するまで待ちます。 この手順は、プロパティが `cfGlobalVersion` 次に表示 `/content/dam` およびがに設定されています。 `1`.

1. OSGi 設定に戻って手順を非アクティブ化します。

   のダイアログで **コンテンツフラグメント移行ジョブの設定** これら 2 つのパラメーターを次のように設定します。

   * **ContentFragmentMigration：有効** : `0`
   * **ContentFragmentMigration：強制** : `0`

## 制限事項 {#limitations}

次の制限事項に注意してください。

* GraphQL フィルターのパフォーマンスの最適化は、すべてのコンテンツフラグメントを完全に更新した後にのみ可能です（JCR ノード `/content/dam` の `cfGlobalVersion` のプロパティが存在することで示される）

* コンテンツフラグメントをコンテンツパッケージから読み込む場合（`crx/de` を使用）、更新手順を実行してから、更新手順が再実行されるまで、これらのコンテンツフラグメントは GraphQL クエリ結果で考慮されません。
