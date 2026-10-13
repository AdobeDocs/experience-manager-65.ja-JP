---
title: ヘッドレス設定の作成に関するクイックスタートガイド
description: AEM 6.5 でヘッドレス機能を使い始めるための最初の手順として、設定を作成します。
exl-id: f1df97a1-164f-4ed4-bb63-34caf35ae27c
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
source-wordcount: '296'
ht-degree: 91%
---
# ヘッドレス設定の作成に関するクイックスタートガイド {#creating-configuration}

AEM 6.5 でヘッドレス機能を使い始めるには、まず設定を作成する必要があります。

## 設定とは {#what-is-a-configuration}

設定ブラウザーには、AEM の設定用の汎用設定 API、コンテンツ構造、解決メカニズムが用意されています。

AEM のヘッドレスなコンテンツ管理に関しては、AEM 内でコンテンツモデルを作成できるワークプレイスとして設定を考えてみてください。これにより、将来のコンテンツとコンテンツフラグメントの構造を定義できます。 複数の設定を作成して、これらのモデルを分離できます。

>[!NOTE]
>
>コンテンツモデルの管理での設定の使用方法は、[フルスタック AEM の実装ページテンプレート](/help/sites-authoring/templates.md)と似ています。

## 設定の作成方法 {#how-to-create-a-configuration}

管理者は、設定を 1 回だけ作成する必要があります。コンテンツモデルの整理のために新しいワークスペースが必要になることはほとんどありません。 この「はじめる前に」ガイドの目的上、設定を 1 つ作成する必要があります。

1. AEM にログインし、メインメニューで&#x200B;**ツール／一般／設定ブラウザー**&#x200B;を選択します。
1. 設定の&#x200B;**タイトル**&#x200B;を入力します。
   * 名前はタイトルに基づいて自動生成され、[AEMの命名規則](/help/sites-developing/naming-conventions.md)に従って調整されます。リポジトリ内のノード名になります。
1. 次のオプションを確認します。
   * **コンテンツフラグメントモデル**
   * **GraphQL の永続的なクエリ**

   ![設定の作成](assets/create-configuration.png)

1. 「**作成**」をクリックします

必要に応じて、複数の設定を作成できます。 設定は入れ子にすることもできます。

>[!NOTE]
>
>実装要件に応じて、**コンテンツフラグメントモデル**&#x200B;および **GraphQL の永続的なクエリ**&#x200B;に加えて、設定オプションが必要になる場合があります。

## 次の手順 {#next-steps}

この設定を使用して、「はじめる前に」ガイドの第 2 部に進み、[コンテンツフラグメントモデルを作成します。](create-content-model.md)

<!--
>[!TIP]
>
>For complete details about the Configuration Browser, [see the Configuration Browser documentation.](/help/sites-developing/configurations.md)
-->
