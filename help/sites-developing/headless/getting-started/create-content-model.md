---
title: コンテンツフラグメントモデルのヘッドレス作成のクイックスタートガイド
description: コンテンツフラグメントモデルを使用して、Adobe Experience Manager（AEM）のヘッドレス機能を使用して作成および提供するコンテンツの構造を定義します。
exl-id: 653e35c9-7b6a-49ae-b55d-af2ec40e257d
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
source-wordcount: '478'
ht-degree: 100%
---
# コンテンツフラグメントモデルのヘッドレス作成のクイックスタートガイド {#creating-content-fragment-models}

コンテンツフラグメントモデルを使用して、Adobe Experience Manager（AEM）のヘッドレス機能を使用して作成および提供するコンテンツの構造を定義します。

## コンテンツフラグメントモデルとは {#what-are-content-fragment-models}

[設定を作成したので、](create-configuration.md)この設定を使用してコンテンツフラグメントモデルを作成できます。

コンテンツフラグメントモデルは、AEM で作成および管理するデータとコンテンツの構造を定義するもので、 コンテンツの一種の基礎として機能します。 コンテンツの作成を選択すると、作成者はあなたが定義したコンテンツフラグメントモデルから選択します。これが、コンテンツの作成のガイドとなります。

## コンテンツフラグメントモデルの作成方法 {#how-to-create-a-content-fragment-model}

情報アーキテクトは、新しいモデルが必要になると、これらのタスクを断続的に実行します。 この入門ガイドでは、1 つのモデルのみを作成します。

1. AEM にログインし、メインメニューで&#x200B;**ツール／アセット／コンテンツフラグメントモデル**&#x200B;を選択します。
1. 設定の作成で生成されたフォルダーをクリックします。

   ![モデルフォルダー](assets/models-folder.png)
1. 「**作成**」をクリックします。
1. 「**モデルタイトル**」、「**タグ**」、「**説明**」を入力します。 また、「**モデルを有効化**」を選択／選択解除して、モデルを作成時にすぐに有効にするかどうかを指定することもできます。

   ![モデルの作成](assets/models-create.png)
1. 確認ウィンドウで、「**開く**」をクリックしてモデルを設定します。

   ![確認ウィンドウ](assets/models-confirmation.png)
1. **コンテンツフラグメントモデルエディター** を使用して、 **データタイプ** 列からフィールドをドラッグ&amp;ドロップして、コンテンツフラグメントモデルを作成します。

   ![フィールドのドラッグ＆ドロップ](assets/models-drag-and-drop.png)

1. フィールドを配置した後、そのプロパティを設定する必要があります。 エディターは、追加されたフィールドの「**プロパティ**」タブに自動的に切り替わります。このフィールドで、必須フィールドを指定できます。

   ![プロパティの設定](assets/models-configure-properties.png)
1. モデルの構築が完了したら、「**保存**」をクリックします。

1. 新規作成されたモデルのモードは、モデルの作成時に「**モデルを有効化**」を選択したかどうかによって異なります。
   * 選択済み - 新しいモデルは既に&#x200B;**有効**&#x200B;になっています。
   * 未選択 - 新しいモデルは&#x200B;**ドラフト**&#x200B;モードで作成されます。

1. まだ有効にしていない場合、このモデルを使用するにはモデルを&#x200B;**有効**&#x200B;にする必要があります。
   1. 作成したモデルを選択し、「**有効化**」をクリックします。

      ![モデルの有効化](assets/models-enable.png)
   1. 確認ダイアログで「**有効にする**」をタップまたはクリックして、モデルの有効化を確認します。

      ![有効化確認ダイアログ](assets/models-enabling.png)
1. モデルが有効になり、使用できる状態になります。

   ![モデルの有効化](assets/models-enabled.png)

**コンテンツフラグメントモデルエディター**&#x200B;は、単純なテキストフィールド、アセット参照、他のモデルへの参照、JSON データなど、様々なデータタイプをサポートしています。

モデルは複数作成できます。 モデルは他のコンテンツフラグメントを参照できます。 [設定](create-configuration.md)を使用して、モデルを整理します。

## 次の手順 {#next-steps}

モデルを作成してコンテンツフラグメントの構造を定義したので、入門ガイドの第 3 部に進み、[フラグメントを保存するフォルダーを作成](create-assets-folder.md)します。

>[!TIP]
>
>コンテンツフラグメントモデルについて詳しくは、[コンテンツフラグメントモデルのドキュメント](/help/assets/content-fragments/content-fragments-models.md)を参照してください。
